# Lab: SQL injection attack, listing the database contents on Oracle

## Objective
The goal is to exploit a SQL injection vulnerability to retrieve the list of tables, column names, and finally the usernames and passwords from an Oracle database.

## Methodology
1. **Identify Column Count:** Determining the number of columns returned by the original query using `ORDER BY`.
2. **Find Table Names:** Querying `all_tables` to find the user table.
   - Payload: `' UNION SELECT table_name, NULL FROM all_tables WHERE table_name LIKE '%USER%'--`
3. **List Columns:** Finding column names for the identified user table.
   - Payload: `' UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name = 'USERS_TABLE_NAME'--`
4. **Data Extraction:** Retrieving credentials.
