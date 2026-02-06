# 📊 SME Loan Portfolio Analytics Platform

**End-to-end SAP Analytics Cloud solution for loan portfolio management and strategic forecasting**

![SAP Analytics Cloud](https://img.shields.io/badge/SAP-Analytics_Cloud-0FAAFF?style=flat-square)
![SAP Datasphere](https://img.shields.io/badge/SAP-Datasphere-0FAAFF?style=flat-square)
![Planning](https://img.shields.io/badge/Feature-Planning_Enabled-success?style=flat-square)

---

## 🎯 Project Overview

Professional analytics platform built for a financial institution managing **2,000+ SME loans** worth **$477.8M**. This portfolio project demonstrates end-to-end SAP Analytics Cloud capabilities from data modeling through interactive planning and forecasting.

### Business Challenge
- Real-time monitoring of $477.8M loan portfolio across 9 regions
- Risk assessment with 33.1% default rate requiring immediate action
- Strategic forecasting for 2022 with scenario planning
- Interactive "what-if" analysis for executive decision-making

### Solution Delivered
Complete analytics solution spanning data modeling (SAP Datasphere), planning model configuration (SAC Planning), and interactive dashboards with real-time calculation capabilities.

---

## 🏗️ Architecture

[![Architecture Overview](./screenshots/12-_ARCHITECTURE_OVERVIEW_.png)

**4-Layer Architecture:**
```
Layer 1: Raw Data (CSV) 
    ↓
Layer 2: SAP Datasphere (Star Schema + Semantic Layer)
    ↓
Layer 3: SAC Planning Model (Scenarios + Calculations)
    ↓
Layer 4: Interactive Dashboards (Reporting + Planning)
```

[View Detailed Architecture](./documentation/Architecture_Diagram.md)

---

## 📊 Data Model

### Star Schema in SAP Datasphere

![Data Model ER Diagram](./screenshots/6-_Data_Model.png)

**Fact Table:** SME_Loan_Portfolio_Analytical
- **2,000 loan records**, 27 columns
- **11 calculated fields**: Risk metrics, delinquency buckets, exposure calculations
- **Measures**: Principal Amount, Interest Income, Days Overdue, Risk Weights

![Fact Table Structure](./screenshots/5-_Loans_Fact.png)

**Dimension Tables:**

<table>
<tr>
<td width="33%">

**Time Dimension**
![Time Dimension](./screenshots/2-_data_dim.png)
- Year → Quarter → Month hierarchy
- Date attributes for filtering

</td>
<td width="33%">

**Geography Dimension**
![Geography Dimension](./screenshots/4-_Geo_Dim.png)
- 9 regions
- Branch locations
- Geo-coordinates for mapping

</td>
<td width="33%">

**Industry Dimension**
![Industry Dimension](./screenshots/3-_industry_dim.png)
- 15 industry sectors
- Risk classification
- Concentration analysis

</td>
</tr>
</table>

**Data Source:**
![Raw Data](./screenshots/1-_SME_Raw_Data.png)

---

## 📈 Dashboard 1: Portfolio Health Monitor

![Portfolio Health Dashboard](./screenshots/7-_SME_Loan_Portfolio_Story.png)

### Key Features:
- **7 KPI Tiles**: Total Principal ($477.8M), Total Loans (2,000), Default Rate (33.1%), Risk Rate (14.7%), Avg Days Overdue (35), Interest Income ($57.3M)
- **Geographic Bubble Map**: Regional exposure visualization (Denver & Phoenix highest concentration)
- **Portfolio Growth Trend**: Principal Amount vs Exposure at Risk over time
- **Delinquency Analysis**: Current (66.95%) vs 1-30 Days (13.25%) vs 31-90 Days vs 90+ Days (19.80%)
- **Industry Concentration**: Top sectors - Construction (18%), Real Estate (15%), Retail (12%)
- **Interactive Filters**: Risk Rating, Region, Year

### Business Insights:
- ⚠️ **33.1% Default Rate** - Requires immediate remediation strategy
- 📍 **Geographic Risk**: Denver and Phoenix show highest portfolio concentration
- 🏗️ **Industry Risk**: Construction and Real Estate represent 33% of portfolio
- 💰 **Exposure at Risk**: $70.2M (14.7%) of portfolio at risk

---

## 📊 Dashboard 2: Planning & Forecast Cockpit

![Planning Dashboard](./screenshots/11-_SME_Planning___Forecast_Story.png)

### Key Features:
- **5 Strategic KPIs**: Actual YTD 2021 ($346.17M ↑19.85%), Planned Forecast 2022 ($429.50M ↑24.07%), Growth vs 2021 (+24.07%), Confidence Level (92%), Risk Level (Medium)
- **Portfolio Growth Trend**: Historical actuals (2018-2021) vs 2022 forecast
- **Scenario Comparison**: Conservative ($385M) vs Forecast ($429.5M) vs Optimistic ($520M)
- **⭐ Interactive Planning Table** - Yellow cells are editable, white cells auto-calculate
- **Default Rate Forecast**: Trending analysis with confidence intervals

### Planning Model Structure

![Planning Model](./screenshots/8-_Planning_Model_Structure.png)

**Dimensions (3):**
- **Time**: Quarterly granularity (2018-2022)
- **Version**: Actual, Forecast, Conservative, Optimistic
- **Scenario**: Annotations and comments

**Measures:**
- **Input (3)**: New_Loans_Count, Avg_Loan_Principal, Expected_Defaults (yellow cells)
- **Calculated (5)**: Total_Principal, Interest_Income, Default_Rate, NPL_Ratio, Growth (white cells)

### Formula Logic

![Calculations](./screenshots/9-_Planning_Model_Calculations.png)

**Key Formulas:**

**Total Principal:**
```javascript
[New_Loans_Count] × [Avg_Loan_Principal]
Example: 520 loans × $45,000 = $23,400,000
```

**Interest Income** (12% annual rate):
```javascript
[Total_Principal] × 0.12 / 4
Example: $23,400,000 × 0.12 / 4 = $702,000/quarter
```

**Default Rate:**
```javascript
IF([New_Loans_Count] = 0, 0,
   ([Expected_Defaults] / [New_Loans_Count]) × 100)
Example: 22 / 520 × 100 = 4.23%
```

**Portfolio Growth** (QoQ %):
```javascript
IF(LOOKUP([Total_Principal], PREVIOUS("Quarter")) = 0, 0,
   ([Total_Principal] - LOOKUP([Total_Principal], PREVIOUS("Quarter"))) / 
   LOOKUP([Total_Principal], PREVIOUS("Quarter")))
Example: ($25.6M - $23.4M) / $23.4M = 9.4%
```

### Data Management

![Data Import](./screenshots/10-_Planning_Model_Data_Management.png)

**Scenario Data:**
- **Actual**: Historical data (2018-2021) - 16 quarters imported
- **Forecast**: Base case projection (2022) - 4 quarters
- **Conservative**: Cautious growth scenario - 5% growth assumption
- **Optimistic**: Aggressive growth scenario - 15% growth assumption

---

## 🎓 Skills Demonstrated

| Category | Capabilities |
|----------|-------------|
| **Data Modeling** | Star schema design, calculated fields, associations, semantic layer, data transformations |
| **SAC Planning** | Multi-dimensional modeling, input/calculated measures, formula logic (IF, LOOKUP, PREVIOUS), scenario management, version control |
| **Data Visualization** | KPI design, geographic bubble maps, trend analysis, professional theming, consistent color palette |
| **Business Analytics** | Financial metrics (NPL ratio, default rate, portfolio growth), risk assessment, concentration analysis |
| **Formula Development** | Conditional logic, time-based lookups, variance calculations, percentage formulas |
| **Dashboard Design** | Interactive filters, drill-down capabilities, mobile-responsive layouts, user experience optimization |

---

## 💼 Business Value

### Operational Insights (Dashboard 1)
✅ **Real-time Monitoring**: Track $477.8M portfolio across 2,000 loans  
✅ **Risk Identification**: Pinpoint 14.7% ($70.2M) exposure at risk  
✅ **Geographic Analysis**: Denver & Phoenix concentration requires diversification  
✅ **Default Management**: 33.1% default rate flagged for immediate action  
✅ **Industry Exposure**: Construction (18%) + Real Estate (15%) = 33% concentration risk

### Strategic Planning (Dashboard 2)
✅ **2022 Forecast**: $429.5M portfolio (+24% growth over 2021)  
✅ **Scenario Planning**: Model conservative ($385M) to optimistic ($520M) outcomes  
✅ **Quarterly Targets**: Q1-Q4 breakdown with default assumptions (4.2%)  
✅ **What-If Analysis**: Change inputs → immediate recalculation of all metrics  
✅ **Decision Support**: 92% forecast confidence for executive planning

---

## 🚀 Technical Highlights

### What Makes This Project Stand Out

1. **Complete Analytics Lifecycle**
   - Not just dashboards - demonstrates full pipeline from CSV to interactive planning
   - Shows understanding of data flow, transformations, and business logic

2. **Planning Capabilities** ⭐
   - Interactive editable tables (not read-only reports)
   - Real-time calculation engine with complex formulas
   - **Key differentiator for SAP Planning Consultant roles**

3. **Production-Ready Quality**
   - Professional design with consistent theming (#1F3B5C navy palette)
   - Comprehensive data model with 11 calculated fields
   - Formula complexity (LAG/PREVIOUS, conditional logic, lookups)

4. **Business Relevance**
   - Real-world financial use case
   - Actual metrics (NPL ratio, default rate, interest income)
   - Decision-support focused (scenario planning, forecasting)

---

## 📁 Project Structure

```
SME_Portfolio_Analytics/
├── README.md                          # This file
├── screenshots/                       # All dashboard and model images
│   ├── 1-_SME_Raw_Data.png
│   ├── 2-_data_dim.png
│   ├── 3-_industry_dim.png
│   ├── 4-_Geo_Dim.png
│   ├── 5-_Loans_Fact.png
│   ├── 6-_Data_Model.png
│   ├── 7-_SME_Loan_Portfolio_Story.png
│   ├── 8-_Planning_Model_Structure.png
│   ├── 9-_Planning_Model_Calculations.png
│   ├── 10-_Planning_Model_Data_Management.png
│   ├── 11-_SME_Planning___Forecast_Story.png
│   └── 12-_ARCHITECTURE_OVERVIEW_.png
├── data/                              # Source data and scenario files
│   ├── SBAcase.csv                    # Raw loan data (2,000 records)
│   ├── Actual_Data_Historical.xlsx    # 2018-2021 actuals
│   ├── forecast_Data_Historical.xlsx  # 2022 forecast
│   ├── Conservative_Data_Historical.xlsx
│   └── Optimistic_Data_Historical.xlsx
└── documentation/                     # Detailed guides
    ├── Architecture_Diagram.md        # Technical architecture
    └── Formula_Reference.md           # All calculations documented
```

---

## 🛠️ Technologies & Tools

- **SAP Analytics Cloud (SAC)** - Dashboard creation, planning models, interactive forecasting
- **SAP Datasphere** - Data modeling, star schema, semantic layer, calculated fields
- **Data Sources** - CSV import, Excel scenario data
- **Design** - Custom theming, professional color palette, responsive layouts

---

## 📊 Key Metrics

| Metric | Value |
|--------|-------|
| **Portfolio Size** | $477.8M |
| **Total Loans** | 2,000 |
| **Regions** | 9 |
| **Industries** | 15 sectors |
| **Dashboards** | 2 (Health + Planning) |
| **Planning Scenarios** | 4 (Actual, Forecast, Conservative, Optimistic) |
| **Calculated Fields** | 11 (Datasphere) + 5 (Planning Model) |
| **Formulas** | 8 complex formulas |
| **Visualizations** | 12 charts and maps |
| **Data Volume** | 2,000 rows × 27 columns |

---

## 🎯 Future Enhancements

**If Expanded to Production:**
- 🔗 **Live Integration**: Connect to SAP ERP or core banking system APIs
- ⏰ **Automated Refresh**: Schedule daily/weekly data updates
- 🔐 **Security**: Row-level security (RLS) by region and role
- 🤖 **Predictive Analytics**: Machine learning for default prediction
- 📱 **Mobile**: Responsive design for tablets and phones
- 📊 **Additional Dashboards**: Collections management, aging analysis, customer profitability
- 🔔 **Alerts**: Automated notifications for threshold breaches
- 🌊 **Workflow**: Approval processes for forecast publishing

---

## 👨‍💼 About This Project

This is a **portfolio demonstration project** built to showcase:
- End-to-end SAP Analytics Cloud implementation skills
- Planning and forecasting capabilities
- Professional dashboard design and data visualization
- Business analytics and financial metrics expertise

**Built by:** Amgad - SAP Analytics Consultant  
**Purpose:** Career development and technical skills demonstration  
**Data Source:** Sample SBA loan dataset (publicly available)

---

## 📞 Contact

**Amgad**  
SAP Analytics Consultant

📧 **Email**: amgadabdelghfar3@gmail.com  
💼 **LinkedIn**: [linkedin.com/in/amgadabdelghfar](https://www.linkedin.com/in/amgadabdelghfar/)  
🌐 **Portfolio**: [View More Projects](#)

---

## 📝 License

This project is for educational and portfolio purposes. Data source is a publicly available sample dataset.

---

## 🙏 Acknowledgments

- SAP Community for Planning Model best practices
- SAP Learning Hub for formula syntax references
- Open-source SBA dataset for realistic business scenario

---

**⭐ If you find this project interesting, please star the repository!**

**Built with SAP Analytics Cloud and Datasphere to demonstrate production-ready analytics and planning skills**

---

### 📈 Project Statistics

- 📅 **Development Time**: 3 weeks
- 🔢 **Lines of Code**: 500+ (formulas, calculations, transformations)
- 📊 **Data Points**: 54,000+ (2,000 loans × 27 attributes)
- 🎨 **Design Hours**: 15+ hours on dashboard UX
- 📐 **Formulas Created**: 16 total calculations
- ✅ **Completion**: 100%
