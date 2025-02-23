# SQL-Explainer
SQL explainer with visual chart creation
*️⃣  Sql Explainer

*️⃣ HOME


Idea > Spec

https://poe.com/s/UlLDSQbIUdSZf3mDgO1j


Ask me one question at a time so we can develop a thorough, step-by-step spec for this idea. Each question should build on my previous answers, and our end goal is to have a detailed specification I can hand off to a developer. Let’s do this iteratively and dig into every relevant detail. Remember, only one question at a time.

Here’s the idea:

Build a Python project that will read in a SQL script and provide an explanation of the tables, columns, relationships, aggregations, and descriptions of columns based on a data dictionary. The purpose is to provide documentation of the SQL script to future developers that will be responsible for improving the script. Another important feature of the program is to generate mermaid entity relationship diagrams to aid in understanding the relationships between source and destination tables and the columns which propagate through the transformation. 

The SQL scripts are mostly very complex ETL processes that will use complex JOIN, SELECT, WHERE and SUB-SELECT statements to create multiple new TABLES, VIEW and aggregate COLUMNS.

Prioritize the explicit relationships between tables highest, then the aggregated interrelated columns that might be generated by a COALESCE statement, and then finally the implicit relationships as lowest priority.


Spec - 1

https://poe.com/s/UbVn9IgFVC15t42KEKyu
