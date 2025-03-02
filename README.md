1. Overview
   
This project involves using Python and Snowflake to extract, transform, and load data from various formats, including CSV, XML, PostgreSQL, and Snowflake Marketplace (weather data). The goal is to analyze the relationship between purchase order amounts and supplier invoice amounts, with the added dimension of analyzing the potential impact of weather conditions on any discrepancies.

2.Data Sources

Purchase Orders: 41 monthly CSV files containing line-item-level data.
Supplier Invoices: XML file with supplier invoice details.
Supplier Information: PostgreSQL database containing supplier information.
Weather Data: NOAA weather data from Cybersyn on Snowflake Marketplace.
Mapping Table: TXT file containing zip codes, latitudes, and longitudes to map weather stations to supplier locations.

3.Project Steps

3.1 Data Extraction and Loading

Load 41 CSV files into a single Snowflake table using Python automation with glob and Snowflake's PUT and COPY INTO commands.
Load the supplier invoice XML data by shredding it into a table.
Use Python and psycopg2 to extract supplier information from PostgreSQL, save it locally, and load it into Snowflake.

3.2 Data Transformation

Calculate total purchase order amounts (POAmount) by summing line item amounts.
Join the purchase order and supplier invoice data, calculating the difference between quoted and invoiced amounts, storing the result in a materialized view or table (purchase_orders_and_invoices).
Extract weather data using latitude and longitude to map weather stations to zip codes from the supplier data.

3.3 Weather Data Integration

Connect to the NOAA Weather & Environment data in Snowflake Marketplace.
Create a materialized view (supplier_zip_code_weather) that links supplier zip codes with daily high temperatures.

3.4 Final Data Join
Join purchase_orders_and_invoices, supplier_case, and supplier_zip_code_weather on zip codes and transaction dates to include weather information in the final analysis.

4. Tools & Technologies
   
Python: Used for data extraction, automation, and transformations.
Snowflake: Database for storing and querying data, performing transformations.
PostgreSQL: Used for storing supplier information.
Power BI: (Optional) Could be used for visualizing the results, though not specifically mentioned.

5.Specific Python Libraries

psycopg2: For PostgreSQL interaction.
glob: For file handling and automation of PUT operations.
pandas: For data manipulation and transformation (if used).


6.Expected Outcomes

A single table containing purchase order and invoice data, joined with supplier and weather data.
A materialized view showing discrepancies between invoice and purchase order amounts, along with corresponding weather conditions, for analysis.
Insights on whether weather affects discrepancies between supplier invoices and purchase order amounts.
