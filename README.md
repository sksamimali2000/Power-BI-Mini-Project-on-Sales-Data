# 📊 Power BI Sales Dashboard – Mini Project  

![Dashboard Preview](Fourth%20Sales%20Mini%20Project%20Dashboard%20pic.jpg)

## 🚀 Project Overview  
This Power BI project analyzes **sales data across multiple countries**, with a focus on creating interactive and dynamic insights using **DAX measures**.  

The dashboard provides:  
✔️ **Total Sales % for United States**  
✔️ **Switch button toggle between Numbers & Percentages**  
✔️ **Dynamic country ordering**  
✔️ **Dynamic text box based on user selection**  

---

## 🎯 Goals & Features  

### 1️⃣ United States Sales %  
- KPI card displaying the **percentage of total sales contributed by the United States**.  
- Implemented using DAX to dynamically calculate share.  

### 2️⃣ Switch Button Between Values  
- Toggle between **Total Sales (Number)** and **% of Total Sales (Percentage)**.  
- Created using a **Switch Table** with parameterized DAX.  

### 3️⃣ Country Order Change  
- Countries in the bar chart can be dynamically **reordered**.  
- Enables custom sorting based on business needs.  

### 4️⃣ Dynamic Text Box  
- Displays selected country in real-time.  
- Example: *“Selected Country is Canada”*.  

---

## 🧮 DAX Measures Used  

```DAX
-- % of Sales Amount from United States
%SalesAmountUnitedStates =
DIVIDE(
    [SalesAmountUnitedStates],
    CALCULATE(
        SUM(fact_InternetSales[SalesAmount]),
        ALL(dim_SalesTeritory[SalesTerritoryCountry])
    )
) * 100




--% of Total Sales Amount
%TotalSalesAmount =
DIVIDE(
    [TotalSalesAmount],
    CALCULATE(
        SUM(fact_InternetSales[SalesAmount]),
        ALL(dim_SalesTeritory[SalesTerritoryCountry]),
        ALL(dim_SalesTeritory[CountryOrder])
    )
) * 100




-- Switch between Number and Percentage
NumberVSPercentage =
IF(
    SELECTEDVALUE(SwitchTable[Datatype]) = "Number",
        [TotalSalesAmount],
    IF(
        SELECTEDVALUE(SwitchTable[Datatype]) = "Percentage",
            [%TotalSalesAmount],
        BLANK()
    )
)



-- United States Sales Amount
SalesAmountUnitedStates =
CALCULATE(
    SUM(fact_InternetSales[SalesAmount]),
    dim_SalesTeritory[SalesTerritoryCountry] = "United States"
)



-- Dynamic Selected Country
SelectedCountry =
VAR CountrySelected = ISFILTERED(dim_SalesTeritory[SalesTerritoryCountry])
RETURN
IF(
    CountrySelected,
    "Selected Country is " & SELECTEDVALUE(dim_SalesTeritory[SalesTerritoryCountry]),
    "Please Choose a Country"
)



-- Total Sales Amount
TotalSalesAmount = SUM(fact_InternetSales[SalesAmount])






📂 Dataset

The dataset used is Fourth Data Extract.xlsx, which contains:

Sales facts (amount, orders, etc.)

Dimension tables: Customer, Product, Sales Territory, Currency.

🖼️ **Dashboard Highlights**

KPI Cards for Sales Amounts & % Shares.

Bar Chart: Number vs Percentage by Sales Territory Country.

Dynamic text box updates based on user-selected country.

Interactive switch toggle between metrics.

🛠️ Tools & Tech

Power BI Desktop

DAX (Data Analysis Expressions)

Excel Data Source

📌 Key Insights

United States contributes ~32% of total sales.

Australia follows closely with ~31% share.

The switch feature allows easy comparison between absolute values and relative percentages.

Dynamic selections make the dashboard highly interactive and user-friendly.

📷 Dashboard Screenshot

(Already included above – you can add more views if needed)

📖 How to Use

Clone/download this repo.

Open the .pbix file in Power BI Desktop.

Load the dataset Fourth Data Extract.xlsx.

Explore dashboard interactions 🚀.

✨ Author

👤 SK Samim Ali

