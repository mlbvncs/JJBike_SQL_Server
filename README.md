# JJBike SQL Server - Business Intelligence Analysis

A comprehensive Business Intelligence project that combines SQL Server and Power BI to analyze and visualize business data from the fictional company JJBike.

---

## 📋 Table of Contents

- [Project Description](#project-description)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the Project](#running-the-project)
- [Project Structure](#project-structure)
- [Project Objectives](#project-objectives)
- [Analysis Highlights](#analysis-highlights)
- [Learning Outcomes](#learning-outcomes)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

## 📝 Project Description

This project demonstrates the complete development of a Business Intelligence solution using SQL Server as the enterprise-grade database management system and Power BI as the visualization and reporting tool.

**Key Focus Areas:**
- Data organization and management using SQL Server
- T-SQL-based data extraction and transformation
- Advanced data modeling and standardization (including Brazilian Portuguese translations)
- Business metrics and KPI development
- Interactive dashboard creation with Power BI
- Data-driven decision-making support
- Enterprise-level database administration

The project includes comprehensive analysis of business metrics such as sales performance, revenue trends, product analysis, customer behavior, and profitability indicators.

---

## 🛠 Technologies Used

| Technology | Purpose |
|-----------|---------|
| **SQL Server** | Enterprise relational database management system |
| **T-SQL** | Data querying, extraction, transformation, and stored procedures |
| **Power BI** | Data visualization and interactive dashboard creation |
| **Git** | Version control |
| **GitHub** | Repository hosting and collaboration |

---

## 📦 Prerequisites

Before getting started, ensure you have the following installed on your system:

- **SQL Server** (SQL Server 2019 or higher)
  - Download: https://www.microsoft.com/en-us/sql-server/sql-server-downloads
  - Editions: Express (free), Developer, Standard, or Enterprise
  
- **SQL Server Management Studio (SSMS)** (latest version)
  - Download: https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms
  
- **Power BI Desktop** (latest version)
  - Download: https://powerbi.microsoft.com/en-us/desktop/
  
- **Git** (for cloning the repository)
  - Download: https://git-scm.com/

### System Requirements
- **OS:** Windows Server 2016+ (or Windows 10/11 for development)
- **RAM:** Minimum 4GB (8GB recommended for SQL Server)
- **Disk Space:** At least 1GB free space
- **Processor:** 1.4 GHz 64-bit processor compatible with x64 instruction set

---

## 💻 Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/mlbvncs/JJBike_SQL_Server.git
cd JJBike_SQL_Server
```

### Step 2: Install SQL Server

#### Option A: SQL Server Express (Free Edition)

1. Download SQL Server Express from the official Microsoft website
2. Run the installer
3. Choose "Basic" installation for quick setup
4. Accept the default configuration or customize as needed
5. Complete the installation wizard

#### Option B: SQL Server Developer Edition

1. Download SQL Server Developer Edition (free for development)
2. Run the installer with custom configuration
3. Select Database Engine Services
4. Choose "Mixed Mode" authentication for development flexibility
5. Set SA (System Administrator) password
6. Complete the installation

### Step 3: Set Up the Database

#### Using SQL Server Management Studio (SSMS)

1. **Open SQL Server Management Studio**
   - Launch SSMS from the Start Menu
   - Connect to your SQL Server instance
   - Authentication: Use Windows Authentication or SQL Authentication

2. **Create a New Database**
   ```sql
   CREATE DATABASE [JJBike_DB]
   ON 
   (
       NAME = JJBike_data,
       FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\JJBike_data.mdf'
   )
   LOG ON 
   (
       NAME = JJBike_log,
       FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\JJBike_log.ldf'
   );
   GO
   ```

3. **Create Database User (Optional)**
   ```sql
   USE [JJBike_DB];
   GO
   CREATE LOGIN jjbike_user WITH PASSWORD = 'YourStrongPassword123!';
   CREATE USER jjbike_user FOR LOGIN jjbike_user;
   ALTER ROLE db_owner ADD MEMBER jjbike_user;
   GO
   ```

4. **Set Database Properties**
   ```sql
   USE [JJBike_DB];
   ALTER DATABASE [JJBike_DB] SET COMPATIBILITY_LEVEL = 150;
   ALTER DATABASE [JJBike_DB] SET RECOVERY FULL;
   GO
   ```

### Step 4: Import Database Scripts

1. Navigate to the **2. Artifacts** folder to locate the T-SQL scripts
2. Open the scripts in SSMS and execute them in the correct order:

```sql
-- Connect to the JJBike_DB database
USE [JJBike_DB];
GO

-- Execute the schema creation script
-- Execute the data import script
-- Execute views and stored procedures script
-- Execute analysis queries
```

Or execute from command line using sqlcmd:

```bash
sqlcmd -S localhost\MSSQLSERVER -U sa -P YourPassword -d JJBike_DB -i "2. Artifacts\01_schema_creation.sql"
sqlcmd -S localhost\MSSQLSERVER -U sa -P YourPassword -d JJBike_DB -i "2. Artifacts\02_data_import.sql"
sqlcmd -S localhost\MSSQLSERVER -U sa -P YourPassword -d JJBike_DB -i "2. Artifacts\03_views_stored_procedures.sql"
```

### Step 5: Configure Backup and Recovery

1. Set up database backups in SSMS
2. Configure maintenance plans for regular backups
3. Test recovery procedures

### Step 6: Configure Power BI Connection

1. Create a DSN (Data Source Name) for ODBC connection (optional)
   - Windows Control Panel → Administrative Tools → ODBC Data Source Administrator
   - Create a System DSN pointing to your SQL Server instance

---

## 🚀 Running the Project

### 1. Verify SQL Server Installation

```bash
sqlcmd -S localhost\MSSQLSERVER -U sa -P YourPassword -Q "SELECT @@VERSION;"
```

Or use SSMS to connect and verify the instance is running.

### 2. Verify Database Creation

```sql
USE master;
GO
SELECT name, database_id, create_date FROM sys.databases WHERE name = 'JJBike_DB';
GO
```

### 3. Execute Analysis Queries

Open SSMS and connect to the JJBike_DB database:

```sql
USE [JJBike_DB];
GO

-- Run analysis queries from the 2. Artifacts folder
-- Example: Sales analysis
SELECT * FROM vw_SalesAnalysis;

-- Example: Product performance
SELECT * FROM vw_ProductPerformance;

-- Example: Customer behavior
SELECT * FROM vw_CustomerBehavior;
GO
```

### 4. Create Stored Procedures (if included)

Execute the stored procedure scripts:

```sql
USE [JJBike_DB];
GO
-- Execute stored procedures creation script
EXEC sp_AnalyzeSalesPerformance;
EXEC sp_GenerateKPIs;
EXEC sp_CustomerSegmentation;
GO
```

### 5. Connect to Power BI

1. **Open Power BI Desktop**
2. Click **Get Data** → **SQL Server**
3. Enter connection details:
   - **Server:** localhost\MSSQLSERVER (or your server name)
   - **Database:** JJBike_DB
   - **Data Connectivity Mode:** Import or DirectQuery (choose based on data size)
4. Select tables and views:
   - Select your fact tables
   - Select dimension tables
   - Select views (vw_*)
5. Click **Load** to import the data
6. Configure data transformations in Power Query if needed
7. Create relationships between tables in the data model
8. Build your dashboards and reports

### 6. Create Power BI Dashboards

Create visualizations for:
- Sales Performance Dashboard
- Revenue Analytics Dashboard
- Product Performance Dashboard
- Customer Insights Dashboard
- Executive Summary Dashboard

### 7. Explore the Analysis

- Review the **Analysis.pdf** file for detailed findings and methodology
- Check the dashboards created in Power BI
- Examine T-SQL queries in the **2. Artifacts** folder
- Review stored procedures and their execution plans

### 8. Performance Tuning (Optional)

Create indexes for optimal query performance:

```sql
USE [JJBike_DB];
GO

-- Create indexes on frequently queried columns
CREATE NONCLUSTERED INDEX IX_Sales_Date 
ON dbo.Sales(SaleDate) INCLUDE (Amount, Quantity);

CREATE NONCLUSTERED INDEX IX_Products_Category
ON dbo.Products(CategoryID) INCLUDE (ProductName, Price);
GO
```

---

## 📂 Project Structure

```
JJBike_SQL_Server/
│
├── 1. Environments/
│   ├── Configuration files
│   ├── Connection strings
│   ├── Environment variables
│   └── SQL Server instance settings
│
├── 2. Artifacts/
│   ├── 01_schema_creation.sql (database schema and tables)
│   ├── 02_data_import.sql (data loading and ETL)
│   ├── 03_views_stored_procedures.sql (views and procedures)
│   ├── 04_analysis_queries.sql (analytical queries)
│   ├── 05_kpi_calculations.sql (KPI definitions)
│   ├── Indexes and optimization scripts
│   ├── Backup and recovery scripts
│   └── Power BI resources
│
├── 3. Translations/
│   ├── Brazilian Portuguese translations
│   ├── Data standardization mappings
│   ├── Localization files
│   └── Column and table naming conventions
│
├── Analysis.pdf
│   └── Comprehensive analysis report and findings
│
├── LICENSE
│   └── MIT License
│
├── .gitignore
│   └── Git ignore configuration
│
└── README.md
    └── This file
```

### Key Folders Explained

**1. Environments/**
- Contains environment configuration files for different deployment stages
- Connection strings for development, staging, and production
- SQL Server instance settings and specifications
- Database backup and recovery configurations

**2. Artifacts/**
- T-SQL scripts for database schema creation
- Data import and ETL (Extract, Transform, Load) procedures
- Views for data aggregation and reporting
- Stored procedures for analysis and calculations
- Index optimization scripts
- Performance tuning configurations
- Power BI connection files and resources

**3. Translations/**
- Brazilian Portuguese translations for data and metadata
- Data standardization mappings and business rules
- Localization files for multilingual support
- Column and table naming conventions documentation

---

## 🎯 Project Objectives

- ✅ Build and manage enterprise database structures using SQL Server
- ✅ Develop complex T-SQL queries for data extraction and transformation
- ✅ Create and optimize stored procedures for business logic
- ✅ Implement views for simplified data access and reporting
- ✅ Build Key Performance Indicators (KPIs) using advanced SQL functions
- ✅ Create interactive and intuitive dashboards with Power BI
- ✅ Generate actionable insights to support business decisions
- ✅ Demonstrate enterprise-level BI solution best practices
- ✅ Provide a reproducible BI solution template for SQL Server

---

## 📊 Analysis Highlights

The project includes comprehensive analyses of:

- **Sales Performance:** Total sales, sales trends, growth rates, and performance metrics
- **Revenue Analysis:** Revenue by period, product, region, and customer segment
- **Product Analysis:** Best-selling products, product performance, profitability, and inventory insights
- **Category Performance:** Sales and revenue breakdown by product category
- **Customer Behavior:** Purchasing patterns, customer segmentation, lifetime value, and retention rates
- **Profitability Indicators:** Profit margins, cost analysis, ROI metrics, and contribution margins
- **Operational Metrics:** Efficiency indicators, performance benchmarks, SLA compliance, and KPIs
- **Time-Series Analysis:** Trends, seasonality, and forecasting

---

## 📚 Learning Outcomes

This project strengthens skills in:

- **SQL Server Administration:** Database creation, management, and maintenance
- **T-SQL Development:** Writing complex queries, stored procedures, functions, and views
- **Database Design:** Designing efficient schemas, normalization, and optimization
- **Data Analysis:** Analyzing data to extract meaningful insights and patterns
- **Business Intelligence:** Building end-to-end BI solutions with enterprise tools
- **Performance Tuning:** Index optimization, query optimization, and execution plan analysis
- **Power BI Development:** Creating dashboards, reports, and data models
- **Data Visualization:** Presenting data effectively and intuitively
- **ETL Processes:** Extracting, transforming, and loading data efficiently

---

## 🔧 Troubleshooting

### Connection Issues

**Problem:** Cannot connect to SQL Server
```bash
# Verify SQL Server is running
sqlcmd -S localhost\MSSQLSERVER -E -Q "SELECT @@VERSION;"

# Check SQL Server services
Get-Service | Where-Object {$_.Name -like "*SQL*"}
```

**Solution:** Ensure SQL Server service is running and TCP/IP protocol is enabled in SQL Server Configuration Manager.

### Permission Issues

```sql
-- Grant necessary permissions to user
USE [JJBike_DB];
GO
ALTER ROLE db_owner ADD MEMBER jjbike_user;
GO
```

### Query Performance Issues

```sql
-- Analyze query execution plan
SET STATISTICS IO ON;
SET STATISTICS TIME ON;

-- Your query here

SET STATISTICS IO OFF;
SET STATISTICS TIME OFF;
```

---

## 🤝 Contributing

Contributions, suggestions, and improvements are welcome!

To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Contribution Guidelines
- Follow T-SQL naming conventions
- Add comments to complex queries
- Include sample execution results
- Update documentation accordingly

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

This project is available for educational and portfolio purposes.

---

## 👤 Author

**Malba Vinicius Lopes Santos**

- GitHub: [@mlbvncs](https://github.com/mlbvncs)
- Portfolio: Business Intelligence & Data Analysis
- Specialization: SQL Server, T-SQL, and Power BI

---

## 🌟 Acknowledgments

This project was developed to demonstrate comprehensive BI skills using enterprise-grade SQL Server and provide a practical example of SQL Server and Power BI integration for business intelligence.

If you found this project useful, please consider giving it a star ⭐ and sharing it with others interested in business intelligence and SQL Server!

---

## 📞 Support

For questions or issues:
- Open an issue on GitHub
- Check the Analysis.pdf for detailed documentation
- Review the SQL Server documentation: https://docs.microsoft.com/en-us/sql/

---

**Last Updated:** May 31, 2026  
**Status:** Active Development  
**SQL Server Version:** 2019 and higher  
**Power BI Version:** Latest Desktop Edition
