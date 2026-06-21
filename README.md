# ✈️ US Flight Delay Performance Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-Data%20Visualization-F2C811?logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-Data%20Transformation-217346)
![DAX](https://img.shields.io/badge/DAX-Analytics-0078D4)
![Data Model](https://img.shields.io/badge/Data%20Model-Star%20Schema-6A5ACD)
![Status](https://img.shields.io/badge/Status-Completed-success)

An interactive **Power BI dashboard** developed to analyse US flight operations, airline performance, airport congestion, seasonal delay patterns, cancellation rates and the major causes of flight delays.

The project demonstrates an end-to-end business intelligence workflow, including data cleaning, Power Query transformation, dimensional modelling, DAX measure development, interactive dashboard design and analytical insight generation.

---

## 📊 Dashboard Preview

![US Flight Delay Performance Dashboard](assets/dashboard-preview.png)

---

## 🎯 Project Objective

The objective of this project was to transform raw US flight operational data into a structured and interactive analytical dashboard.

The dashboard helps answer key operational questions such as:

- Which airlines demonstrate the strongest arrival performance?
- Which airports experience the highest number of delays?
- How does flight performance change throughout the year?
- What are the main causes of flight delays?
- How does route distance affect on-time performance?
- Which airports may be affected by congestion-related inefficiencies?

---

## 📌 Key Performance Indicators

| KPI | Result |
|---|---:|
| Total Flights | 5M |
| On-Time Rate | 68.9% |
| Average Arrival Delay | -2.06 minutes |
| Cancellation Rate | 1.71% |

A negative average arrival delay indicates that flights arrived slightly earlier than their scheduled arrival time on average.

---

## 🗂️ Dataset Overview

The dataset contains operational records for US domestic flights, including:

- Airline identifier
- Origin and destination airports
- Flight date
- Scheduled departure and arrival times
- Actual departure and arrival times
- Arrival and departure delays
- Flight distance
- Air time
- Cancellation and diversion indicators
- Weather delay
- Airline delay
- Air system delay
- Security delay
- Late aircraft delay

---

## 🧹 Data Preparation and Transformation

The dataset was cleaned and transformed using **Power Query** before being loaded into the Power BI data model.

### Data Cleaning

- Replaced missing delay-cause values with zero
- Standardised column data types
- Removed invalid or inconsistent records
- Prepared numerical fields for accurate aggregation
- Checked key columns for missing and incorrect values

### Time Standardisation

- Converted numeric HHMM values into proper time format
- Created a complete flight date using year, month and day fields
- Derived month name, month number, quarter and day-of-week attributes
- Created a dedicated date dimension for time-based analysis

### Delay Classification

Flights were grouped into the following delay categories:

| Delay Category | Definition |
|---|---|
| On Time | Delay of 0 minutes or less |
| Minor Delay | Delay between 1 and 15 minutes |
| Major Delay | Delay greater than 15 minutes |

An **On-Time Flag** was also created to support the calculation of on-time performance.

### Distance Segmentation

Flights were classified into distance bands:

| Distance Band | Definition |
|---|---|
| Short Haul | 500 miles or less |
| Medium Haul | 501 to 1,500 miles |
| Long Haul | More than 1,500 miles |

This segmentation enables performance comparison across different route types.

---

## 🏗️ Data Modelling

A **star schema** was implemented to improve model clarity, filtering behaviour and analytical performance.

### Fact Table

The central flight table contains transactional flight records and measures such as:

- Arrival delay
- Departure delay
- Distance
- Air time
- Cancellation indicator
- Delay-cause values

### Dimension Tables

- **DimDate:** Date, month, quarter and day-of-week attributes
- **Airlines:** Airline codes and airline names
- **Airports:** Airport codes, cities, states and geographic details

### Model Structure

```text
                    DimDate
                       |
                       |
Airlines -------- Fact_Flights -------- Airports
                       |
                       |
             Destination Airport
```

The fact table stores operational flight data, while the dimension tables provide descriptive attributes for filtering and analysis.

---

## 📐 Key DAX Measures

```DAX
Total Flights =
COUNTROWS(flights)
```

```DAX
Average Arrival Delay =
AVERAGE(flights[ARRIVAL_DELAY])
```

```DAX
Cancelled Flights =
CALCULATE(
    COUNTROWS(flights),
    flights[CANCELLED] = 1
)
```

```DAX
Cancellation Rate =
DIVIDE(
    [Cancelled Flights],
    [Total Flights],
    0
)
```

```DAX
On-Time Rate =
DIVIDE(
    CALCULATE(
        COUNTROWS(flights),
        flights[ARRIVAL_DELAY] <= 0
    ),
    [Total Flights],
    0
)
```

---

## 📈 Dashboard Visualisations

### KPI Cards

The KPI cards provide a high-level overview of:

- Total flights
- On-time rate
- Average arrival delay
- Cancellation rate

### Monthly Delay Trend

A line chart displays the average arrival delay by month, helping identify seasonal patterns and periods of operational disruption.

### Airline Performance Comparison

A bar chart compares the average arrival delay across airlines, helping identify stronger-performing carriers and performance outliers.

### Delay Cause Analysis

A pie chart displays the contribution of major delay causes, including:

- Airline delays
- Air system delays
- Weather delays
- Security delays
- Late aircraft delays

### Airport Performance Matrix

A conditional-formatting matrix compares:

- Major delays
- Minor delays
- On-time flights
- Unknown delay classifications
- Total flight volume

### Geographic Flight Map

The geographic map visualises flight activity by city and highlights major airport hubs and areas with high traffic concentration.

### Interactive Filtering

A distance-band slicer allows users to compare:

- Short-haul flights
- Medium-haul flights
- Long-haul flights

---

## 🔍 Key Insights

- Overall on-time performance was approximately **68.9%**.
- Arrival-delay performance fluctuated across different months.
- September and October demonstrated stronger negative arrival-delay averages than several earlier months.
- Several airlines recorded near-zero or negative average arrival delays, indicating stronger schedule reliability.
- Major delays were concentrated among a smaller number of high-traffic airports.
- Airports such as **ATL, ORD, DFW and DEN** contributed high total delay volumes.
- High flight volumes were associated with larger delay counts, suggesting possible congestion-related inefficiencies.
- Minor delays occurred more frequently than major delays across most airports.
- Short-haul flights demonstrated slightly stronger on-time performance than medium and long-haul flights.
- Airline-related and air-system delays were among the major contributors to overall delay duration.

---

## 🛠️ Tools and Technologies

| Tool | Purpose |
|---|---|
| Power BI Desktop | Dashboard development and visual analytics |
| Power Query | Data cleaning and transformation |
| DAX | KPI and analytical measure development |
| Star Schema | Dimensional data modelling |
| Bing Maps | Geographic flight analysis |
| GitHub | Version control and project documentation |
| Git LFS | Storage of the large Power BI file |

---

## 📁 Repository Structure

```text
us-flight-delay-performance-dashboard/
│
├── README.md
├── US Flight Delays.pbix
├── team14-data visualization (1).pdf
│
└── assets/
    └── dashboard-preview.png
```

---

## 🚀 How to Use the Dashboard

1. Clone the repository:

```bash
git clone https://github.com/Muhammad-Siraj-Bilal/us-flight-delay-performance-dashboard.git
```

2. Open the project folder:

```bash
cd us-flight-delay-performance-dashboard
```

3. Install Git LFS and download the Power BI file:

```bash
git lfs install
git lfs pull
```

4. Open the `.pbix` file using **Microsoft Power BI Desktop**.

5. Use the distance-band slicer and interactive visuals to explore flight performance.

> Power BI Desktop is required to open and interact with the PBIX file.

---

## 💡 Skills Demonstrated

- Business intelligence development
- Data cleaning and preparation
- Power Query transformation
- Dimensional data modelling
- Star-schema implementation
- DAX measure development
- KPI design
- Interactive dashboard development
- Time-series analysis
- Geographic data visualisation
- Operational performance analysis
- Data storytelling

---

## 🔮 Future Improvements

Potential future extensions include:

- Integration of live weather data
- Airport congestion forecasting
- Machine-learning-based delay prediction
- Route-level performance analysis
- Drill-through pages for individual airlines and airports
- Dynamic tooltip pages
- Year-over-year performance comparison
- Financial impact estimation for flight delays
- Deployment through Power BI Service

---

## 👥 Academic Project

This dashboard was developed as part of a **Team 14 academic project** for:

**CST4245 – Data Visualisation, Computer Vision and Imaging**

The project focused on applying dimensional modelling, visual analytics and business intelligence techniques to a large operational flight dataset.

---

## 👤 Author

**Muhammad Siraj Bilal**

- GitHub: [Muhammad-Siraj-Bilal](https://github.com/Muhammad-Siraj-Bilal)
- Repository: [US Flight Delay Performance Dashboard](https://github.com/Muhammad-Siraj-Bilal/us-flight-delay-performance-dashboard)

---

## ⭐ Support

If you found this project useful or interesting, please consider giving the repository a **star**.
