# MIST-4610-Group-Project-2

# Team Members:
Group Leader:Meghan Thota
SQL Writer:Ori Cohen-Aka 
Data Wrangler/Database Designer:Luke Van Putten
Conceptual Modeler:Rahul Pullolickal

# Case Summary
Northline Outfitters is a small but growing online retailer selling student friendly lifestyle and tech accessories including hoodies, water bottles, desk lamps, phone cases, keyboards, mouse pads, and backpacks directly to consumers in the United States and Canada. The company sources its merchandise from external vendors and currently manages most of its operational records in Excel rather than a structured database.
The project begins with two raw spreadsheet exports that reflect the informal, day-to-day record keeping of a small business. These files contain a number of data quality issues common to small enterprises operating without a formal database such as inconsistent formatting, unstructured text fields, mixed unit systems, and duplicate or variant records. The goal of this project is to assess those issues, clean and normalize the data, design a relational database that can be analyzed using SQL to support business decision-making.

# Conceptual Model

Our model is built to represent the real-world workflow of a retail order and inventory system for Northline Outfitters. The **Sales_Order** entity acts as the center of the system, containing key details about each transaction such as the order date, customer, employee handling the order, location, and payment method. Each order is linked to a **Customer** through a one-to-many (1:M) relationship, where one customer can place many orders, but each order belongs to one customer. This allows the business to track purchasing behavior along with attributes like loyalty status and student status.

To represent what is actually being purchased, the **Order_Line** entity breaks each order into individual items. This table connects orders to specific **Products**, while also storing important transaction details like quantity, unit price, discounts, tax, and return status.  This allows the system to capture detailed sales activity at an item level. This creates a (1:M) relationship between **Sales_Order** and **Order_Line**, since one order can contain multiple line items. 

The relationship from **Product** to **Order_Line** forms a (1:M) relationship, as many order lines can reference the same product. Products are organized through the **Category** and **Vendor entities**. Each product is assigned a **primary category** and may also have an **alternative category**, allowing for more flexible classification of items such as apparel, accessories, and tech products. Vendors supply the products, and each product is tied to a specific vendor, making it possible to track supplier relationships and inventory sources.

On the operational side,** Employees** are responsible for processing orders, and the model includes a recursive relationship to represent management structure (employees reporting to managers). **Orders **are also tied to a Location, which stores shipping details such as city, state, and country, since Northline Outfitters’ operations run across the United States and Canada.

In addition to the core system, we included features that improve tracking:

Product Details: The **Product** entity includes attributes such as cost, price, size, weight, and discontinuation status. It also contains a parent SKU field, which can be used to represent relationships between related products.

Transaction Details: Within the **Order_Line** entity, fields for discounts, taxes, and return flags allow the system to capture more detailed information about each sale.

This structure allows Northline Outfitters to move from basic Excel-based tracking to a more structured system that can keep track of both high level order activity and detailed transaction data, supporting more efficient operations and future data analysis.

<img width="405" height="449" alt="Screenshot 2026-04-24 at 8 49 03 AM" src="https://github.com/user-attachments/assets/ee50599e-5758-4ac6-8843-05def74a4b4e" />


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

# Data Cleaning Process
The dataset was cleaned and standardized using a combination of Excel tools and an AI add-in. The process is outlined below in clear steps:

**Step 1: Initial Data Cleanup**

We used Excel’s built-in Find and Replace function to correct inconsistencies in the data, standardize values, and remove obvious errors across the dataset. This was useful for quick bulk updates to improve overall data consistency for differences in capitalization and formatting.

**Step 2: AI-Assisted Cleaning**

Instead of using manual cleaning, we used the Numerous.ai Excel add-in to help identify patterns, automate repetitive fixes, and help with overall with data standardization. This improved efficiency during the cleaning process, while maintaining accuracy of the data.

**Step 3: Column Separation**

The customer_info column contained multiple pieces of information in a single field. We split this into three separate columns:

customer_name
loyalty_status
A partial student_status field

This step improved data structure and made the dataset easier to analyze.

**Step 4: Resolving Student Status Inconsistencies**

Student status information was incomplete and spread across multiple columns. To address this we combined relevant columns using concatenation and prioritized “Yes” values when conflicting information appeared. Therefore the consolidated column called student_final was created. This ensured a single, reliable indicating column of student status for each row.

**Step 5: Manual Review and Validation**

Although automation tools were helpful, some inconsistencies required manual inspection. Working directly in Excel allowed us to scroll through the dataset and identify obvious issues in the data and manually change errors that were missed by automation. Some cells had to be edited individually.
This step ensured the final dataset was accurate and ready for analysis.

# Queries


---

# Database information:
Name of the database: mb_B6

Additional information: Each query listed above is marked in the database using stored procedures which can be called using the following format: CALL GP_Q1();
