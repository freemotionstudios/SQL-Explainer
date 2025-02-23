# Project Name: PYTHON-SQL-MAP

Python project that will read in a SQL script and provide an explanation of the tables, columns, 
relationships, aggregations, and descriptions of columns based on a data dictionary. The purpose 
is to provide documentation of the SQL script to future developers that will be responsible for 
improving the script. Another important feature of the program is to generate mermaid entity 
relationship diagrams to aid in understanding the relationships between source and destination 
tables and the columns which propagate through the transformation.

## Software Packages to use

sqlglot
mermaid-py
pytest
pydantic
pandas

## Development standards

Always create clear and concise code
Use PYTEST for creating test cases
Ensure that error handling is implemented
Use the logging module to log errors and debug information
Always take steps to improve the code in small increments and test the results before moving on to the next step
