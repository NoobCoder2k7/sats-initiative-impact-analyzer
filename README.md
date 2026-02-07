# sats-initiative-impact-analyzer

> Causal impact measurement platform for optimizing aviation catering operations 
> across a 225-station global network

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Latest-yellow.svg)](https://powerbi.microsoft.com/)
[![Azure SQL](https://img.shields.io/badge/Azure-SQL%20Database-blue.svg)](https://azure.microsoft.com/en-us/services/sql-database/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

**Built by:** Trang Nguyen | Double Degree in Computer Science & Business (Business Analytics) - NTU Singapore

**Project Type:** Capstone Analytics Platform  
**Industry:** Aviation Operations & Food Service

---

## 🎯 Overview

This platform demonstrates causal inference methodology for measuring operational 
initiative impact in aviation catering operations, addressing SATS Ltd.'s strategic 
needs around revenue mix optimization, network-wide knowledge transfer, and ROI-based 
investment decisions.

**Key Features:**
- 📊 Difference-in-differences causal analysis
- 💰 Financial impact quantification ($52K monthly savings demonstrated)
- 🌐 225-station scalability framework
- 📈 5-page interactive Power BI dashboard
- ✅ Governance-ready data pipeline (98.7% quality score)
- ☁️ Azure SQL cloud integration

[View Documentation](#) | [See Dashboard Screenshots](#) | [Read Methodology](#)
```

---

## **⚠️ IMPORTANT: .gitignore FILE**

**File:** `.gitignore`
```
# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
env/
venv/
*.egg-info/
dist/
build/

# Data (if contains sensitive info)
data/*.csv
!data/data_dictionary.csv  # Keep dictionary
*.xlsx
*.db
*.sqlite

# Azure credentials
*.json
config.py
secrets.py

# Power BI
*.pbix.tmp
~$*.pbix

# OS
.DS_Store
Thumbs.db
desktop.ini

# IDEs
.vscode/
.idea/
*.swp
*.swo

# Logs
*.log
