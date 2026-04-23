# MIST-4610-Group-Project-2

# Team Members:
Group Leader:Meghan Thota
SQL Writer:Ori Cohen-Aka 
Data Wrangler/Database Designer:Luke Van Putten
Conceptual Modeler:Rahul Pullolickal

# Project Goal
Northline Outfitters is a small but growing online retailer selling student friendly lifestyle and tech accessories including hoodies, water bottles, desk lamps, phone cases, keyboards, mouse pads, and backpacks directly to consumers in the United States and Canada. The company sources its merchandise from external vendors and currently manages most of its operational records in Excel rather than a structured database.
The project begins with two raw spreadsheet exports that reflect the informal, day-to-day record keeping of a small business. These files contain a number of data quality issues common to small enterprises operating without a formal database such as inconsistent formatting, unstructured text fields, mixed unit systems, and duplicate or variant records. The goal of this project is to assess those issues, clean and normalize the data, design a relational database that can be analyzed using SQL to support business decision-making.

# Data Model

# Data Quality Assesment
The source dataset reveals contains significant data quality issues that may negatively impact analysis, reporting accuracy, and overall data reliability. The primary issues are listed below:

**1. Inconsistent Data Formats**

-Several fields use inconsistent formats, making the data difficult to process and analyze. Examples include: 

-Dates appear in multiple formats (numeric, abbreviated text, full text).

-Currency values are formatted differently between the unit_price column and line_total column. One uses ("USD 14.99") format while the other uses symbols to format (ex: "$14.99"). They are measuring the same type of value but are recorded differently.

-Discounts and tax values are inconsistently represented (ex: “10%”, “5”, "student 10%", “promo5”).

-Payment methods vary in capitalization (ex: “VISA” vs “visa”).

Impact: These inconsistencies prevent accurate calculations, sorting, and time based analysis without prior data cleaning.

**2. Missing Values**

-Several attributes contain missing or null values, including fields such as tax, line totals, size/weight, and return indicators.

Impact: Missing data leaves an incomplete dataset, introduces potential bias, and may lead to errors in analysis or reporting.

**3. Inconsistent Key Fields**

-Key identifiers like SKUs are not consistently formatted, and relationships between alternative SKUs or parent SKUs are unclear.

Impact: This compromises data integrity and makes it difficult to accurately join or relate datasets.

**4. Unstructured and Combined Fields**

-Some fields contain multiple pieces of information combined into a single column:

-Customer information includes names, status, and location in one field.

-Shipping information is inconsistently recorded (e.g., “Same as billing” vs full address).

-Size or weight column includes information on both size and weight in one field but record different values in different units. (ex:, inches vs centimeters, grams vs pounds).

Impact: This makes querying and analysis more difficult and prevents direct comparison/aggregation without unit standardization

**5. Data Type Issues**

-Some numeric fields are stored as text in Excel, including prices and percentages. Some columns also have mzied datatypes.

Impact: Limits the ability to perform calculations and statistical analysis.

**6. Uncontrolled Free-Text Fields**

-Fields such as notes contain unstructured, inconsistent text entries.

Impact: These fields are difficult to analyze systematically and may introduce ambiguity.

**7. Duplicate Values**

-The dataset contains product rows that are duplicated or represent variants, but are not clearly distinguished. This includes inconsistencies such as SKU case sensitivity (ex:, uppercase vs lowercase) and minor differences in product names.

Impact:
These inconsistencies can lead to duplicate records being treated as separate products and double counting during analysis, resulting in inaccurate aggregations and innacurate analysis (ex: overstated sales totals).

**Conclusion**

Overall, the dataset contains multiple data quality issues, including inconsistencies in formatting, missing values, duplicate records, and lack of standardization. These issues must be addressed through data cleaning processes before the dataset can be used for reliable analysis or decision-making.

---

#Database information:
Name of the database: mb_B6

Additional information: Each query listed above is marked in the database using stored procedures which can be called using the following format: CALL GP_Q1();
