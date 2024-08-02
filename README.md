# Employee Data Processing and Integration with Snowflake
### Project Overview
This project focuses on processing employee data in JSON format using Azure and Snowflake. The workflow involves data transformation, integration, notification setup, data sharing, and security enhancements.

### Steps and Implementation
#### 1. Data Dumping and Initial Setup
Data Dumping: Employee data in JSON format is dumped into an Azure bucket.

Storage Integration: A storage integration object is created to build a connection between Snowflake and Azure for data access.

Snowflake Setup: In Snowflake, a warehouse, database, schema, and file format are created. An external stage is set up to store the data from Azure.

Table Creation: A table is created to import the data from the external stage. The nested data and arrays are flattened to transform the data into a structured table format.

Additional Table Creation: Another table is created with additional information, such as a tax payer status based on salary and converting null values in the prev_company column to zero experience.
#### 2. Automating Data Ingestion
Snowpipe Creation: A Snowpipe is created to listen for S3 notifications, enabling automatic data ingestion when new files are added to the Azure bucket.

Data Transformation: The recently added data is automatically converted into a table format in Snowflake.
#### 3. Data Sharing with Non-Snowflake Users
Share Creation: A share is created to allow non-Snowflake users to access the employee table.

Reader Account: A reader account is set up and granted all privileges to the share. The shared data is accessed by creating a database and a warehouse in the reader account.
#### 4. Data Transformation and Synchronization
Table Creation: Three tables are created:

employee_json: Contains the raw JSON data.

employee_structured: Contains the formatted JSON data in CSV format.

updated_employee_structured: Contains the updated structured data with applied transformations.
Streams and Tasks: Streams are created to track changes in the source table (employee_structured). Tasks are scheduled to run every minute to update the 
destination table (updated_employee_structured) with any inserts, deletes, or updates from the source table.
#### 5. Materialized Views
Materialized View Creation: A materialized view is created to frequently query the maximum salary in each department.
#### 6. Dynamic Data Masking
Data Masking: Dynamic data masking is implemented to hide confidential data from specific roles. Masking policies are set on the columns that need to be hidden.
### Conclusion
This project demonstrates the integration of Azure and Snowflake for efficient data processing and transformation. It includes automated data ingestion, data sharing, real-time synchronization, and enhanced security measures through dynamic data masking. The setup ensures that the employee data is accessible, up-to-date, and secure across different user roles and platforms.
