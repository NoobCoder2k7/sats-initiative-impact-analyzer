# SATS Initiative Impact Analyzer
## Business Problem Statement

### SATS' Strategic Context (2025)

Following the 2023 acquisition of Worldwide Flight Services (WFS), SATS now operates 
across 225+ stations globally, providing aviation catering and cargo handling services 
covering trade routes responsible for over 50% of global air cargo volume.

However, SATS faces several operational and financial challenges:

**1. Margin Pressure from Revenue Mix Shifts**

SATS' FY2025 annual report highlights "margin pressures in cargo handling business 
due to a less favorable revenue mix and reduced high-margin e-commerce volumes." 
With trade tensions impacting air cargo demand (tariffs on imports from China, Mexico, 
Canada; 25% tariff on steel imports), optimizing resource allocation toward high-margin 
opportunities is critical.

**2. Network Integration & Operational Consistency**

Having "successfully integrated WFS," SATS is "optimistic about leveraging its 
extensive network for more commercial wins." However, with 225 stations across diverse 
regions, regulatory environments, and operational contexts, ensuring consistent 
performance measurement and knowledge transfer is challenging.

**3. Demand Volatility & Forecasting Under Uncertainty**

External factors (trade policies, shipping disruptions, geopolitical situations) 
create unpredictable demand patterns. SATS needs to adapt operations quickly while 
avoiding costly waste from overproduction or service failures from underproduction.

**4. Investment Prioritization Amid Cost Pressures**

With margin pressure, every operational investment (new technology, process changes, 
training programs) must demonstrate clear ROI. Without rigorous measurement, it's 
difficult to know which initiatives deliver value and should be scaled vs. discontinued.

---

### The Measurement Gap

SATS faces a fundamental question when implementing operational improvements:

> **"When we launch an initiative (new forecasting algorithm, premium menu expansion, 
> process standardization), how do we know if observed improvements are due to the 
> initiative itself, or just seasonal patterns, market shifts, or random variation?"**

**Current Challenge:**
- **Correlation ≠ Causation**: Waste decreased after implementing new process, but 
  was it the process or just a slow travel season?
- **Attribution Ambiguity**: Revenue improved, but was it our premium catering or 
  the airline's route expansion?
- **Inconsistent Measurement**: Different stations measure success differently, 
  making cross-station comparison unreliable
- **ROI Uncertainty**: Without causal measurement, business cases for scaling 
  initiatives lack data-driven justification

**Business Impact:**
- Wasted investment in ineffective programs
- Missed opportunities to scale high-ROI initiatives
- Inability to optimize revenue mix systematically
- Reduced confidence in leveraging 225-station network advantages

---

### Proposed Solution

Build a **causal impact measurement platform** that enables SATS to:

**1. Optimize Revenue Mix** 💰
- Test premium service offerings on select routes
- Measure incremental revenue vs. incremental cost
- Calculate ROI to prioritize high-margin opportunities
- Scale winning strategies across 225-station network

**Example Question Answered:**
> "Should we invest in premium meal service on Singapore-London route to attract 
> higher-margin airline contracts?"
>
> → Run controlled experiment: Premium vs. Standard service  
> → Measure: Incremental revenue, customer satisfaction, cost increase  
> → Decision: ROI = 8.5x → Recommend scale to similar long-haul routes

---

**2. Enable Network-Wide Knowledge Transfer** 🌐
- Measure initiative impact at pilot stations using causal methods
- Account for local factors (seasonality, airline mix, station size)
- Project scalability across remaining stations
- Identify which stations are ready for rollout

**Example Question Answered:**
> "Station A reduced waste by 15% with new process. Should we roll out to 224 other 
> stations?"
>
> → Compare Station A (treatment) vs. similar stations (control)  
> → Use difference-in-differences to isolate process effect  
> → Calculate: Network-wide savings potential = $6.2M annually  
> → Recommendation: Phased rollout to high-volume stations first

---

**3. Adapt to Demand Volatility** 📊
- Measure historical relationships between external factors and operational metrics
- Run scenario analysis for different demand environments
- Provide confidence intervals for forecasts under uncertainty
- Enable rapid response to market shifts

**Example Question Answered:**
> "E-commerce volumes dropped 20% due to tariffs. How do we adjust meal forecasts 
> without creating waste?"
>
> → Analyze historical correlation: Cargo volume ↔ Meal demand  
> → Model shows: 20% cargo drop → 12-15% meal demand drop (95% CI)  
> → Adjust forecasts accordingly to minimize waste

---

**4. Rigorously Measure Initiative ROI** 🎯
- Use controlled experiments (A/B tests, difference-in-differences)
- Isolate initiative effects from confounding factors
- Quantify financial impact in SGD
- Support data-driven investment decisions

**Example Question Answered:**
> "Is $500K investment in automated meal planning software worth it?"
>
> → Pilot at 10 stations for 90 days  
> → Measure incremental waste reduction vs. control stations  
> → Result: $85K monthly savings, 12-month payback  
> → Decision: ✅ Proceed with network-wide rollout

---

### Platform Capabilities

**Causal Inference Methodology:**
- Difference-in-differences (DiD) for before/after comparisons
- Control group selection to account for external factors
- Statistical significance testing (95% confidence intervals)
- Adjustment for seasonality, trends, and regional differences

**Business Translation:**
- Operational metrics → Financial impact (SGD)
- Cost-benefit analysis and ROI calculations
- Scenario planning with interactive parameters
- Scalability projections (1 station → 225 stations)

**Governance & Scalability:**
- Automated data quality monitoring (98%+ target)
- Data dictionary (50+ fields documented)
- Lineage tracking (source to dashboard)
- Azure SQL cloud integration for enterprise deployment

**Executive Dashboards (Power BI):**
- Page 1: Executive KPIs (ROI, savings, statistical significance)
- Page 2: Experiment Results (treatment vs. control, DiD visualization)
- Page 3: Financial Impact (cost bridge, payback period, what-if scenarios)
- Page 4: Network Scalability (225-station rollout planning)
- Page 5: Data Governance (quality monitoring, field catalog)

---

### Pilot Use Case: Meal Planning Algorithm

**Business Context:**
With margin pressures from "less favorable revenue mix," SATS needs to optimize 
operations to protect profitability. Meal waste represents direct cost leakage that 
erodes margins.

**Experiment Design:**

**Treatment Group:**
- Routes: SIN-SYD, SIN-BKK (AI-powered forecasting algorithm)
- Period: 60 days post-implementation
- Hypothesis: Algorithm reduces waste 8-12% while maintaining 95%+ service level

**Control Group:**
- Routes: SIN-HKG, SIN-NRT (existing manual forecasting)
- Period: Same 60 days
- Purpose: Account for seasonal trends and external factors

**Key Metrics:**
- Incremental waste reduction (%)
- Cost savings (SGD per month)
- Forecast accuracy improvement
- Service level maintained (no meal shortages)
- ROI calculation

**Expected Demonstration:**
- $52K monthly waste reduction (Singapore hub)
- 94% forecast accuracy (up from 88%)
- 12.3x ROI over 12 months
- Scalability framework: $6.2M annual savings if rolled out network-wide

---

### Strategic Value for SATS

This platform directly supports SATS' stated priorities:

**1. Margin Optimization** ✅
Systematically identify and scale high-margin initiatives across 225 stations

**2. Network Leverage** ✅
Turn WFS acquisition into competitive advantage through consistent measurement and 
knowledge transfer

**3. Operational Agility** ✅
Adapt quickly to demand volatility (tariffs, trade shifts) with data-driven forecasts

**4. Investment Confidence** ✅
Make resource allocation decisions with rigorous ROI measurement, critical during 
margin pressure

---

### Success Criteria

**Analytical Rigor:**
- Isolate causal effects using statistically valid methodology
- Achieve 95%+ confidence in impact estimates
- Account for seasonality, trends, and control group differences

**Business Impact:**
- Quantify improvements in SGD (savings, revenue, ROI)
- Project scalability across 225-station network
- Support executive decision-making with clear financial cases

**Technical Quality:**
- Achieve 98%+ data quality score
- Document full data lineage and governance
- Demonstrate cloud-ready architecture (Azure SQL)

---

### Stakeholders

**Primary Users:** SATS TDX (Technology, Data & Excellence) Department  
**Business Owners:** Regional operations managers, catering leads  
**Executive Sponsors:** CFO (margin optimization), COO (operational efficiency)  
**Data Consumers:** Finance team, station managers, network planning

---

### Project Scope

**What This Delivers:**
- Proof-of-concept causal impact measurement platform
- 5-page Power BI dashboard with interactive scenario planning
- Governance-ready data pipeline (quality monitoring, lineage, documentation)
- Methodology demonstration using simulated aviation catering data

**What Production Would Add:**
- Integration with SATS' actual data systems
- Real-time data pipelines
- Multi-region deployment across 225 stations
- Role-based access control with Azure AD

---

**Note:** This is a student capstone project demonstrating enterprise analytics 
capabilities relevant to SATS' documented strategic challenges. Business impact 
figures are illustrative examples to show methodology, not actual SATS performance 
metrics. However, the analytical approach, governance framework, and technical 
implementation are production-ready and directly applicable to SATS' stated needs 
around revenue optimization, network leverage, and investment prioritization.
