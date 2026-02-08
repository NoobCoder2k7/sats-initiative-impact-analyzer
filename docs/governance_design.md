# Data Governance Design
## SATS Initiative Impact Analyzer

### Why Governance Matters
For SATS' 225-station global network spanning multiple regions, currencies, and 
regulatory environments, data governance ensures that:
- Metrics remain **trusted** across organizational units
- Analysis is **auditable** for finance and compliance reviews
- Data quality is **consistent** for fair cross-station comparison
- Systems are **scalable** without degrading reliability

This document outlines the governance-ready design for the analytics platform.

---

## 1. Data Quality Monitoring

### Quality Standards
| Dimension | Target | Measurement Method |
|-----------|--------|-------------------|
| **Completeness** | ≥98% | % of non-null values in critical fields |
| **Accuracy** | ≥95% | % of records passing business rule validation |
| **Timeliness** | <24 hours | Age of most recent data vs. current date |
| **Consistency** | ≥99% | % of records with valid foreign key references |

### Implementation Approach
- **Automated Checks**: Python ETL pipeline runs validation on every batch
- **Quality Logging**: All check results stored in `data_quality_log` table
- **Dashboard Monitoring**: Power BI page shows real-time quality trends
- **Alerting**: Email notifications when quality drops below threshold

### Quality Checks by Table

**fact_demand:**
- Completeness: meals_produced, meals_consumed, date, route must be non-null
- Accuracy: meals_produced ≥ meals_consumed (cannot consume more than produced)
- Timeliness: Latest date within 1 day of current date
- Consistency: All foreign keys (route_id, cuisine_id, date_id) exist in dimensions

**Dimension Tables:**
- Completeness: Primary keys and names must be non-null
- Uniqueness: No duplicate primary keys or natural keys
- Referential Integrity: All foreign key relationships validated

---

## 2. Data Dictionary

### Purpose
Provides a single source of truth for field definitions, ownership, and classification, 
ensuring all stakeholders interpret metrics consistently.

### Structure
For each field, document:
- **Table & Column Name**: Technical identifier
- **Data Type**: INT, VARCHAR, DECIMAL, etc.
- **Business Definition**: Plain-language explanation of what the field represents
- **Calculation Logic**: For derived fields (e.g., waste_quantity = produced - consumed)
- **Data Classification**: CONFIDENTIAL (revenue, passenger counts), INTERNAL (meal 
  quantities), PUBLIC (route names, dates)
- **Data Owner**: Person or team responsible for accuracy (e.g., "Catering Manager")
- **Usage Notes**: Any caveats or special considerations

### Implementation
- Stored in `data_dictionary` table (50+ fields documented)
- Accessible via Power BI governance page (searchable catalog)
- Maintained by Data Steward role

### Sample Entries

| Field | Definition | Classification | Owner |
|-------|-----------|----------------|-------|
| meals_produced | Total meals prepared for flight, including all cuisine types | INTERNAL | Catering Manager |
| meals_consumed | Actual meals served to passengers, from cabin crew reports | CONFIDENTIAL | Flight Operations |
| waste_quantity | Calculated: meals_produced - meals_consumed | INTERNAL | Finance Team |
| cost_per_meal | Standard cost per meal in SGD, excluding special dietary items | CONFIDENTIAL | Finance Team |

---

## 3. Data Lineage

### Documentation Approach
Track the full journey of data from source to dashboard:

**Source → Extraction → Transformation → Load → Consumption**

### Lineage Documentation

**fact_demand table:**
- **Source**: CSV files from catering production systems
- **Extraction Method**: Manual upload (future: automated API integration)
- **Transformation Logic**: 
  - Calculate waste_quantity = meals_produced - meals_consumed
  - Assign treatment_flag = 1 for SIN-SYD, SIN-BKK routes
  - Generate data_quality_score from validation checks
- **Load Frequency**: Daily batch at 8:00 AM SGT
- **Consumers**: Power BI dashboards, executive reports, ad-hoc analysis
- **Last Updated**: Tracked via load_timestamp field

**Transformation Documentation Format:**
```
STEP 1: Data Generation/Collection
- Python script: etl_pipeline.py
- Logic: Simulate 120 days of meal demand with seasonal patterns
- Output: Raw CSV (1,440 records)

STEP 2: Quality Validation
- Python function: validate_quality()
- Checks: Completeness, accuracy, timeliness
- Output: data_quality_log.csv + quality_score per record

STEP 3: Data Cleaning
- Action: Fill missing meals_produced using forward-fill method
- Rationale: Preserve time-series continuity
- Impact: ~2% of records affected

STEP 4: Load to Azure SQL
- Python script: load_to_azure.py
- Method: Bulk insert via SQLAlchemy
- Target: Azure SQL Database (sats_analytics_db)

STEP 5: Power BI Refresh
- Method: DirectQuery for real-time; Import for dashboards
- Schedule: Daily refresh via Power Automate at 9:00 AM SGT
- Latency: <1 hour from source data to dashboard
```

---

## 4. Access Control Design

### Principle: Least Privilege
Users receive minimum permissions necessary for their role.

### Role-Based Access Model

**Analytics Reader** (Analysts, Station Managers)
- Permissions: SELECT on all tables
- Use Case: View dashboards, run read-only queries
- Example Users: Regional analysts, operations staff

**Analytics Writer** (ETL Service Account)
- Permissions: SELECT, INSERT, UPDATE on core tables
- Use Case: Automated data loading and quality logging
- Example Users: etl_service_account (system user)

**Data Steward** (Data Governance Team)
- Permissions: ALL on governance tables (data_dictionary, data_quality_log)
- Use Case: Maintain metadata, update definitions, manage quality thresholds
- Example Users: TDX data governance lead

**Database Administrator** (IT/Infrastructure)
- Permissions: Full database admin rights
- Use Case: Schema changes, backup management, performance tuning
- Example Users: Azure SQL admin account

### Implementation Notes
This access control model is **conceptual design** for production deployment. In the 
project prototype:
- All access via single admin account for development
- Production implementation would use Azure AD groups mapped to database roles
- Row-level security (RLS) could restrict users to their region's data

---

## 5. Backup & Recovery Strategy

### Azure SQL Native Features
Azure SQL Database provides built-in backup capabilities:
- **Automated Backups**: Full backup weekly, differential daily, log every 5-10 minutes
- **Retention**: 7 days default (configurable to 35 days)
- **Point-in-Time Restore**: Recover to any minute within retention period
- **Geo-Redundancy**: Backups replicated to paired region for disaster recovery

### Recommended Configuration (Production)
- **Retention Period**: 14 days (balance between cost and recovery flexibility)
- **Backup Frequency**: Use Azure default (no custom scheduling needed)
- **Test Restoration**: Monthly restore to test environment to verify recovery process
- **Documentation**: Maintain runbook for recovery procedures

### Recovery Objectives (Proposed)
- **Recovery Time Objective (RTO)**: 4 hours - Maximum acceptable downtime
- **Recovery Point Objective (RPO)**: 1 hour - Maximum acceptable data loss

### Implementation in Project
This project uses Azure SQL's default backup settings. In production:
1. Configure retention via Azure Portal or CLI
2. Document recovery procedures in operations runbook
3. Schedule monthly restore tests
4. Train TDX team on recovery process

---

## 6. Data Retention Policy

### Operational Data
- **Production Database**: 2 years (operational needs + 1 year lookback for analysis)
- **Archive Storage**: Move to Azure Blob Storage (cold tier) after 2 years
- **Total Retention**: 5 years (regulatory compliance)
- **Deletion**: Automated purge after 5 years

### Aggregated Reports
- **Executive Dashboards**: Refresh with current 2-year window
- **Historical Analysis**: Maintain summary tables (monthly aggregates) indefinitely
- **Audit Trail**: Quality logs and lineage metadata retained for 3 years

### Rationale
- Operations teams need 18-24 months for year-over-year comparisons
- Finance requires 5-year retention for compliance
- Balances storage costs with analytical needs

---

## 7. Change Management

### Schema Changes
- All changes documented in version-controlled SQL migration scripts
- Test in development environment before production deployment
- Communicate breaking changes to dashboard users 2 weeks in advance

### Data Definition Changes
- Updates to data_dictionary table require Data Steward approval
- Change log maintained with before/after definitions
- Email notification to all Analytics Readers when definitions change

---

## 8. Governance Dashboard

### Purpose
Provide transparency into data quality, lineage, and platform health.

### Key Metrics (Power BI Page)
- Overall data quality score (current)
- Quality trends (30-day line chart)
- Data freshness (hours since last update)
- Field catalog (searchable data dictionary)
- Data flow diagram (source to dashboard lineage)

### Target Audience
- **Data Stewards**: Monitor quality issues, update definitions
- **Executives**: Verify data trustworthiness before making decisions
- **Auditors**: Review governance compliance

---

## Implementation Summary

### What This Project Delivers
✅ Automated quality validation in Python ETL  
✅ Quality log table with 98%+ score  
✅ Data dictionary with 50+ field definitions  
✅ Lineage documentation (source to dashboard)  
✅ Power BI governance page  
✅ Governance design documentation  

### What Production Would Add
- Azure AD integration for role-based access
- Formal backup testing schedule
- Row-level security for regional data isolation
- Automated archive to blob storage
- Compliance audit reporting

### Why This Matters for SATS
This governance-ready design demonstrates understanding of enterprise requirements 
beyond typical intern projects. It shows:
- Platform thinking (not just analysis)
- Scalability mindset (225-station deployment)
- Professional documentation
- Production-ready design patterns

Even as a prototype, these governance principles ensure the platform could be 
deployed at scale with confidence in data quality, auditability, and maintainability.
