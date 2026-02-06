# Project Architecture
**SME Loan Portfolio Analytics Platform**

##  System Overview

End-to-end SAP Analytics Cloud solution for loan portfolio management with real-time monitoring and strategic forecasting.

**Data Flow:** Raw CSV → Datasphere → Planning Model → SAC Dashboards

---

## 🔄 Architecture Layers

### **Layer 1: Raw Data**
```
📁 SBAcase.csv
├─ 2,000 loan records
├─ 27 columns (Loan ID, Principal, Risk Rating, Industry, etc.)
```

### **Layer 2: SAP Datasphere (Semantic Layer)**
```
 Star Schema Model
├─ FACT: SME_Loan_Portfolio_Analytical
│   ├─ Grain: One row per loan
│   ├─ Measures: Principal Amount, Interest Income, Days Overdue
│   └─ 11 Calculated Fields (Risk metrics, delinquency buckets, flags)
│
└─ DIMENSIONS (3)
    ├─ Time: Year → Quarter → Month hierarchy
    ├─ Geography: Branch, Region  
    └─ Industry: Sector classification

Associations: Fact → Dimensions (many-to-one)
```

### **Layer 3: SAC Planning Model**
```
📐 SME_Portfolio_Planning_Model

DIMENSIONS (3):
├─ Time: Quarterly (2018-2022)
├─ Version: Actual, Forecast, Conservative, Optimistic
└─ Scenario: Annotations/comments

INPUT MEASURES (3 - Editable):
├─ New_Loans_Count
├─ Avg_Loan_Principal  
└─ Expected_Defaults

CALCULATED MEASURES (5 - Formula-Driven):
├─ Total_Principal = Count × Avg_Principal
├─ Interest_Income = Total × 0.12 / 4
├─ Default_Rate = Defaults / Count × 100
├─ NPL_Ratio = (Defaults × Avg) / Total × 100
└─ Growth = (Current - Prior) / Prior × 100

DATA VOLUMES:
├─ Historical Actual: 16 quarters (2018-2021)
├─ Forecast: 4 quarters (2022 base case)
├─ Conservative: 4 quarters (5% growth)
└─ Optimistic: 4 quarters (15% growth)
```

### **Layer 4: SAC Dashboards (Presentation)**
```
📊 Dashboard 1: Portfolio Health Monitor
├─ 7 KPI tiles (Principal, Loans, Default Rate, etc.)
├─ Geographic bubble map (regional exposure)
├─ Portfolio growth trend chart
├─ Delinquency bucket analysis
└─ Interactive filters (Risk Rating, Region, Year)

📈 Dashboard 2: Planning & Forecast Cockpit
├─ 5 Strategic KPIs with variance indicators
├─ Historical vs Forecast trend (2018-2022)
├─ Scenario comparison chart
├─ ⭐ Interactive planning table (editable cells)
├─ Default rate forecast with confidence intervals
└─ Real-time calculation engine
```

---

## 🔄 Data Transformations

### **Raw → Datasphere**
1. Data quality validation (nulls, duplicates)
2. Geocoding: Branch → Latitude/Longitude
3. Date parsing: Disbursement Date → Quarter, Month, Year
4. Risk calculation: Days Overdue → Delinquency_Bucket
5. Binary flags: Is_Default, Is_Delinquent
6. Weighted metrics: Risk_Weight × Principal

### **Datasphere → Planning Model**
1. Aggregation from loan-level to quarterly
2. Historical data import (2018-2021 Actuals)
3. Forecast scenario creation (2022)
4. Dimension mapping (Time, Version, Scenario)
5. Measure configuration (Input vs Calculated)

### **Planning Model → Dashboards**
1. Real-time formula calculations
2. Scenario filtering (Version selector)
3. Time-based slicing (Year, Quarter)
4. Chart data binding
5. Interactive table updates

---



## 🛠️ Technologies

- **SAP Datasphere**: Data modeling, semantic layer, transformations
- **SAP Analytics Cloud**: Dashboards, planning models, forecasting
- **Data Formats**: CSV (source), XLSX (planning imports)
- **Design**: Custom theming (#1F3B5C navy palette)

---

## 📊 Data Flow Diagram

```
┌─────────────┐
│ SBAcase.csv │  Raw Data Layer
│ 2,000 loans │  (CSV file)
└──────┬──────┘
       │ Upload
       ↓
┌─────────────────────┐
│  SAP Datasphere     │  Semantic Layer
│  • Star Schema      │  (Data modeling)
│  • 3 Dimensions     │
│  • Calculated Fields│
└──────┬──────────────┘
       │ Expose
       ↓
┌──────────────────────┐
│ SAC Planning Model   │  Business Logic
│ • 3 Input Measures   │  (Formulas & scenarios)
│ • 5 Calculated       │
│ • 4 Scenarios        │
└──────┬───────────────┘
       │ Power
       ↓
┌───────────────────────┐
│  SAC Dashboards       │  Presentation Layer
│  • Portfolio Health   │  (Interactive reports)
│  • Planning Cockpit   │
└───────────────────────┘
