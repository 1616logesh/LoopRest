1. Set Up Your Environment
Choose a Python framework such as Flask or FastAPI for building the API.
Set up a PostgreSQL or MySQL database to store the CSV data.
Use SQLAlchemy for ORM (Object Relational Mapping) to interact with the database.
2. Data Ingestion
Create scripts to read the CSV files and store the data into relevant database tables.
Tables to create:
store_status: store_id, timestamp_utc, status
business_hours: store_id, dayOfWeek, start_time_local, end_time_local
store_timezones: store_id, timezone_str
3. Time Conversion
Convert timestamp_utc to the store's local time using the timezone_str from the store_timezones table.
Ensure that business hours and status timestamps are aligned in the same timezone.
4. Data Processing Logic
Uptime/Downtime Calculation:
For each store, identify the business hours for the past hour, day, and week.
Calculate the uptime and downtime by comparing the active/inactive status during these intervals.
Implement interpolation logic to estimate uptime/downtime between the polled statuses.
5. API Implementation
/trigger_report:
Start the report generation process.
Store the report status and a unique report_id in a database.
Return the report_id.
/get_report:
Check if the report is complete.
If complete, return the CSV report; otherwise, return "Running".
6. Optimizations
Use indexing in the database to speed up queries.
Implement batching if processing large amounts of data.
7. Testing and Documentation
Write unit tests for each component.
Document your code to explain the logic and assumptions
Considerations
Handle edge cases, such as missing data or stores with varying business hours.
Ensure the solution is scalable to handle frequent updates to the data.
