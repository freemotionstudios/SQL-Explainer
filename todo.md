## TODO: SQL Script Documentation & ER Diagram Generator

### Phase 1: Project Setup and Core Parsing

- [ ] **Step 1: Project Initialization**
    - [ ] Create the project directory structure as defined in the architecture.
    - [ ] Initialize a `git` repository.
    - [ ] Set up a virtual environment and install the core dependencies (`sqlglot`, `markdown`, `mermaid-py`, `pydantic`, `pandas`, `pytest`, `ruff`).
    - [ ] Create initial `main.py`, and empty files for the modules in `sql_parser`, `lineage_tracker`, `diagram_generator`, `outputs`, and `tests`.
    - [ ] Create a basic `pytest` configuration.
- [ ] **Step 2: Basic SQL Parsing with `sqlglot`**
    - [ ] Implement basic SQL parsing functionality using `sqlglot` in `sql_parser/ddl_analyzer.py`.
    - [ ] Focus on parsing `CREATE TABLE` statements to extract table names and column definitions (name, data type).
    - [ ] Create a `TableSchema` Pydantic model to represent the extracted table schema.
    - [ ] Write unit tests to verify the correct parsing of `CREATE TABLE` statements.
- [ ] **Step 3: Data Dictionary Generation**
    - [ ] Implement a basic data dictionary generation function in `outputs/data_dictionary.py`.
    - [ ] Take the parsed `TableSchema` as input and generate a Markdown representation of the data dictionary.
    - [ ] Update `main.py` to parse a sample SQL file and generate a data dictionary.
    - [ ] Write unit tests to verify the correct generation of the data dictionary.
- [ ] **Step 4: Basic Error Handling and Logging**
    - [ ] Implement basic error handling using `logging` module.
    - [ ] Log unparseable statements as warnings and continue processing.
    - [ ] Add logging to the parsing and data dictionary generation functions.
    - [ ] Write unit tests to verify the correct error handling and logging.

### Phase 2: Advanced Parsing and Lineage Tracking

- [ ] **Step 5: Advanced SQL Parsing**
    - [ ] Extend the SQL parsing functionality in `sql_parser/ddl_analyzer.py` to handle `CREATE VIEW` statements, constraints, and comments.
    - [ ] Update the `TableSchema` model to include constraints and comments.
    - [ ] Write unit tests to verify the correct parsing of `CREATE VIEW` statements, constraints, and comments.
- [ ] **Step 6: Column Lineage Tracking**
    - [ ] Implement basic column lineage tracking in `lineage_tracker/dml_analyzer.py`.
    - [ ] Focus on tracing column lineage in `INSERT...SELECT` statements.
    - [ ] Resolve aliases and subqueries to original source columns.
    - [ ] Update the `TableSchema` model to include column lineage information.
    - [ ] Write unit tests to verify the correct column lineage tracking.
- [ ] **Step 7: Transformation Logic Documentation**
    - [ ] Implement transformation logic documentation in `lineage_tracker/transformation.py`.
    - [ ] Document calculated columns (e.g., `total = [col_a, col_b]`).
    - [ ] Update the `TableSchema` model to include transformation logic information.
    - [ ] Write unit tests to verify the correct transformation logic documentation.

### Phase 3: ER Diagram Generation and Refinement

- [ ] **Step 8: Basic ER Diagram Generation**
    - [ ] Implement basic ER diagram generation in `diagram_generator/er_diagram.py`.
    - [ ] Generate a Mermaid ER diagram based on the `TableSchema` and relationships.
    - [ ] Represent tables as nodes and relationships as edges (explicit = solid, aggregated = dashed, implicit = dotted).
    - [ ] Update `main.py` to generate an ER diagram.
    - [ ] Write unit tests to verify the correct generation of the ER diagram.
- [ ] **Step 9: Relationship Inference**
    - [ ] Implement relationship inference in `sql_parser/dml_analyzer.py`.
    - [ ] Infer implicit relationships from `JOIN` conditions.
    - [ ] Infer aggregated relationships from columns derived from functions (e.g., `COALESCE`, `CASE`).
    - [ ] Update the `TableSchema` model to include inferred relationships.
    - [ ] Write unit tests to verify the correct relationship inference.
- [ ] **Step 10: Diagram Styling and Finalization**
    - [ ] Finalize Mermaid styling conventions (colors/line styles).
    - [ ] Implement directional arrows showing source-to-destination flow.
    - [ ] Update the ER diagram generation function to apply the styling conventions.
    - [ ] Write unit tests to verify the correct styling of the ER diagram.

### Phase 4: Testing, Validation, and Deliverables

- [ ] **Step 11: Validation and Error Handling**
    - [ ] Implement validation checks for unresolved foreign keys and comment syntax.
    - [ ] Add warnings for unparseable statements and undocumented columns.
    - [ ] Write unit tests to verify the correct validation and error handling.
- [ ] **Step 12: Integration Tests**
    - [ ] Create integration tests with sample SQL scripts (Oracle/PostgreSQL/MS SQL) with mixed DDL/DML.
    - [ ] Validate data dictionary accuracy and diagram relationships.
- [ ] **Step 13: CLI and Deliverables**
    - [ ] Implement the CLI entrypoint using `argparse`.
    - [ ] Generate sample output (data dictionary and ER diagram).
    - [ ] Finalize the documentation and testing.

### Step 1: Project Initialization

- [ ] **Step 1.1: Create Project Structure**
    - [ ] Create the base directory `SQL-Explainer` (already exists).
    - [ ] Create subdirectories: `sql_parser`, `lineage_tracker`, `diagram_generator`, `outputs`, `tests`.
    - [ ] Create empty `__init__.py` files in each subdirectory to make them Python packages.
    - [ ] **Prompt 1:**
        - [ ] Create the following directory structure in the current working directory:
            ```
            sql_parser/
            lineage_tracker/
            diagram_generator/
            outputs/
            tests/
            ```
        - [ ] Create an empty `__init__.py` file in each of these directories.
- [ ] **Step 1.2: Initialize Git Repository**
    - [ ] Initialize a `git` repository in the project root.
    - [ ] Create a basic `.gitignore` file (e.g., ignoring `__pycache__`, `.venv`).
    - [ ] **Prompt 2:**
        - [ ] Initialize a git repository in the current working directory.
        - [ ] Create a `.gitignore` file with the following contents:
            ```
            __pycache__/
            .venv/
            *.pyc
            *.log
            ```
- [ ] **Step 1.3: Set Up Virtual Environment and Install Dependencies**
    - [ ] Create a virtual environment using `venv`.
    - [ ] Activate the virtual environment.
    - [ ] Install the core dependencies: `sqlglot`, `markdown`, `mermaid-py`, `pydantic`, `pandas`, `pytest`, `ruff`.
    - [ ] **Prompt 3:**
        - [ ] Create a virtual environment named `.venv` in the current working directory.
        - [ ] Activate the virtual environment.
        - [ ] Install the following packages using pip:
            ```
            sqlglot
            markdown
            mermaid-py
            pydantic
            pandas
            pytest
            ruff
            ```
- [ ] **Step 1.4: Create Initial Files**
    - [ ] Create `main.py` in the project root.
    - [ ] Create empty files: `sql_parser/ddl_analyzer.py`, `sql_parser/dml_analyzer.py`, `sql_parser/comment_parser.py`, `lineage_tracker/alias_resolver.py`, `lineage_tracker/transformation.py`, `diagram_generator/er_diagram.py`, `outputs/data_dictionary.py`, `outputs/er_diagram.mmd`, `tests/test_sql_parser.py`.
    - [ ] **Prompt 4:**
        - [ ] Create the following files in the current working directory:
            ```
            main.py
            sql_parser/ddl_analyzer.py
            sql_parser/dml_analyzer.py
            sql_parser/comment_parser.py
            lineage_tracker/alias_resolver.py
            lineage_tracker/transformation.py
            diagram_generator/er_diagram.py
            outputs/data_dictionary.py
            outputs/er_diagram.mmd
            tests/test_sql_parser.py
            ```
        - [ ] All files should be empty.
- [ ] **Step 1.5: Create Basic Pytest Configuration**
    - [ ] Create a `pytest.ini` file in the project root with basic configuration.
    - [ ] **Prompt 5:**
        - [ ] Create a `pytest.ini` file in the current working directory with the following contents:
            ```
            [pytest]
            testpaths = tests
            ```

### Step 2: Basic SQL Parsing with `sqlglot`

- [ ] **Step 2.1: Define `TableSchema` Pydantic Model**
    - [ ] Define a `TableSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to represent the extracted table schema. The model should include fields for `name` (table name) and `columns` (list of column definitions). Each column definition should include `name` and `type`.
    - [ ] **Prompt 6:**
        - [ ] In the file `sql_parser/ddl_analyzer.py`, define a Pydantic model named `TableSchema` with the following structure:
            ```python
            from pydantic import BaseModel
            from typing import List, Dict

            class ColumnSchema(BaseModel):
                name: str
                type: str

            class TableSchema(BaseModel):
                name: str
                columns: List[ColumnSchema]
            ```
- [ ] **Step 2.2: Implement Basic `CREATE TABLE` Parsing**
    - [ ] Implement a function `parse_create_table` in `sql_parser/ddl_analyzer.py` that takes a `CREATE TABLE` SQL statement as input and returns a `TableSchema` object.
    - [ ] Use `sqlglot` to parse the SQL statement and extract the table name and column definitions.
    - [ ] **Prompt 7:**
        - [ ] In the file `sql_parser/ddl_analyzer.py`, implement a function named `parse_create_table` that takes a `CREATE TABLE` SQL statement as input and returns a `TableSchema` object. Use `sqlglot` to parse the SQL statement and extract the table name and column definitions.
            ```python
            from sqlglot import parse_one, exp

            def parse_create_table(sql: str) -> TableSchema:
                statement = parse_one(sql)
                table_name = statement.args['this'].this
                columns = []
                for column_def in statement.args['expressions']:
                    column_name = column_def.args['this']
                    column_type = column_def.args['kind'].this
                    columns.append(ColumnSchema(name=column_name, type=column_type))
                return TableSchema(name=table_name, columns=columns)
            ```
- [ ] **Step 2.3: Create Basic Unit Tests for `CREATE TABLE` Parsing**
    - [ ] Create a basic unit test in `tests/test_sql_parser.py` to verify the correct parsing of `CREATE TABLE` statements.
    - [ ] Use `pytest` to write the unit test.
    - [ ] **Prompt 8:**
        - [ ] In the file `tests/test_sql_parser.py`, create a unit test to verify the correct parsing of `CREATE TABLE` statements using the `parse_create_table` function.
            ```python
            import pytest
            from sql_parser.ddl_analyzer import parse_create_table, TableSchema

            def test_parse_create_table():
                sql = "CREATE TABLE users (id INT, name VARCHAR(255))"
                table_schema = parse_create_table(sql)
                assert table_schema.name == "users"
                assert len(table_schema.columns) == 2
                assert table_schema.columns[0].name == "id"
                assert table_schema.columns[0].type == "INT"
                assert table_schema.columns[1].name == "name"
                assert table_schema.columns[1].type == "VARCHAR"
            ```
- [ ] **Step 2.4: Run Unit Tests**
    - [ ] Run the unit tests using `pytest` to ensure that the `parse_create_table` function is working correctly.
    - [ ] **Prompt 9:**
        - [ ] Run the unit tests using pytest to ensure that the `parse_create_table` function is working correctly.

### Step 3: Data Dictionary Generation

- [ ] **Step 3.1: Implement Basic Data Dictionary Generation Function**
    - [ ] Implement a function `generate_data_dictionary` in `outputs/data_dictionary.py` that takes a `TableSchema` object as input and returns a Markdown representation of the data dictionary.
    - [ ] The Markdown representation should include the table name and a list of columns with their names and types.
    - [ ] **Prompt 10:**
        - [ ] In the file `outputs/data_dictionary.py`, implement a function named `generate_data_dictionary` that takes a `TableSchema` object as input and returns a Markdown representation of the data dictionary.
            ```python
            from sql_parser.ddl_analyzer import TableSchema

            def generate_data_dictionary(table_schema: TableSchema) -> str:
                markdown = f"# Data Dictionary for {table_schema.name}\\n\\n"
                markdown += "| Column Name | Data Type |\\n"
                markdown += "|---|---|\\n"
                for column in table_schema.columns:
                    markdown += f"| {column.name} | {column.type} |\\n"
                return markdown
            ```
- [ ] **Step 3.2: Update `main.py` to Parse SQL and Generate Data Dictionary**
    - [ ] Update `main.py` to read a sample SQL file (e.g., `sample.sql`) and parse it using the `parse_create_table` function.
    - [ ] Then, generate a data dictionary using the `generate_data_dictionary` function and write it to a file (e.g., `data_dictionary.md`).
    - [ ] **Prompt 11:**
        - [ ] Update `main.py` to read a sample SQL file named `sample.sql` (create this file with a simple CREATE TABLE statement) and parse it using the `parse_create_table` function. Then, generate a data dictionary using the `generate_data_dictionary` function and write it to a file named `data_dictionary.md`.
            ```python
            from sql_parser.ddl_analyzer import parse_create_table
            from outputs.data_dictionary import generate_data_dictionary

            def main():
                with open("sample.sql", "r") as f:
                    sql = f.read()
                table_schema = parse_create_table(sql)
                markdown = generate_data_dictionary(table_schema)
                with open("data_dictionary.md", "w") as f:
                    f.write(markdown)

            if __name__ == "__main__":
                main()
            ```
- [ ] **Step 3.3: Create Sample SQL File**
    - [ ] Create a `sample.sql` file with a simple `CREATE TABLE` statement for testing purposes.
    - [ ] **Prompt 12:**
        - [ ] Create a file named `sample.sql` with the following contents:
            ```sql
            CREATE TABLE users (
                id INT,
                name VARCHAR(255)
            );
            ```
- [ ] **Step 3.4: Create Unit Tests for Data Dictionary Generation**
    - [ ] Create a unit test in `tests/test_sql_parser.py` to verify the correct generation of the data dictionary.
    - [ ] Use `pytest` to write the unit test.
    - [ ] **Prompt 13:**
        - [ ] In the file `tests/test_sql_parser.py`, create a unit test to verify the correct generation of the data dictionary using the `generate_data_dictionary` function.
            ```python
            from outputs.data_dictionary import generate_data_dictionary

            def test_generate_data_dictionary():
                from sql_parser.ddl_analyzer import TableSchema, ColumnSchema
                table_schema = TableSchema(
                    name="users",
                    columns=[
                        ColumnSchema(name="id", type="INT"),
                        ColumnSchema(name="name", type="VARCHAR"),
                    ],
                )
                markdown = generate_data_dictionary(table_schema)
                assert "# Data Dictionary for users" in markdown
                assert "| Column Name | Data Type |" in markdown
                assert "| id | INT |" in markdown
                assert "| name | VARCHAR |" in markdown
            ```
- [ ] **Step 3.5: Run `main.py` and Verify Output**
    - [ ] Run `main.py` to generate the data dictionary.
    - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary.
    - [ ] **Prompt 14:**
        - [ ] Run `main.py` to generate the data dictionary.
        - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary.
- [ ] **Step 3.6: Run Unit Tests**
    - [ ] Run the unit tests using `pytest` to ensure that the `generate_data_dictionary` function is working correctly.
    - [ ] **Prompt 15:**
        - [ ] Run the unit tests using pytest to ensure that the `generate_data_dictionary` function is working correctly.

### Step 4: Basic Error Handling and Logging

- [ ] **Step 4.1: Implement Basic Logging Configuration**
    - [ ] Configure basic logging in `main.py` to log warnings and errors to a file (e.g., `app.log`).
    - [ ] Set the logging level to `WARNING`.
    - [ ] **Prompt 16:**
        - [ ] Configure basic logging in `main.py` to log warnings and errors to a file named `app.log`. Set the logging level to `WARNING`.
            ```python
            import logging

            logging.basicConfig(filename="app.log", level=logging.WARNING)

            from sql_parser.ddl_analyzer import parse_create_table
            from outputs.data_dictionary import generate_data_dictionary

            def main():
                try:
                    with open("sample.sql", "r") as f:
                        sql = f.read()
                    table_schema = parse_create_table(sql)
                    markdown = generate_data_dictionary(table_schema)
                    with open("data_dictionary.md", "w") as f:
                        f.write(markdown)
                except Exception as e:
                    logging.error(f"An error occurred: {e}")

            if __name__ == "__main__":
                main()
            ```
- [ ] **Step 4.2: Add Error Handling to `parse_create_table`**
    - [ ] Add error handling to the `parse_create_table` function in `sql_parser/ddl_analyzer.py` to log unparseable statements as warnings and continue processing.
    - [ ] **Prompt 17:**
        - [ ] Add error handling to the `parse_create_table` function in `sql_parser/ddl_analyzer.py` to log unparseable statements as warnings and continue processing.
            ```python
            import logging
            from sqlglot import parse_one, exp
            from sql_parser.ddl_analyzer import TableSchema, ColumnSchema

            def parse_create_table(sql: str) -> TableSchema:
                try:
                    statement = parse_one(sql)
                    table_name = statement.args['this'].this
                    columns = []
                    for column_def in statement.args['expressions']:
                        column_name = column_def.args['this']
                        column_type = column_def.args['kind'].this
                        columns.append(ColumnSchema(name=column_name, type=column_type))
                    return TableSchema(name=table_name, columns=columns)
                except Exception as e:
                    logging.warning(f"Could not parse CREATE TABLE statement: {sql}. Error: {e}")
                    # Return an empty TableSchema to allow processing to continue
                    return TableSchema(name="unknown", columns=[])
            ```
- [ ] **Step 4.3: Add Error Handling to `generate_data_dictionary`**
    - [ ] Add error handling to the `generate_data_dictionary` function in `outputs/data_dictionary.py` to log errors and continue processing.
    - [ ] **Prompt 18:**
        - [ ] Add error handling to the `generate_data_dictionary` function in `outputs/data_dictionary.py` to log errors and continue processing.
            ```python
            import logging
            from sql_parser.ddl_analyzer import TableSchema

            def generate_data_dictionary(table_schema: TableSchema) -> str:
                try:
                    markdown = f"# Data Dictionary for {table_schema.name}\\n\\n"
                    markdown += "| Column Name | Data Type |\\n"
                    markdown += "|---|---|\\n"
                    for column in table_schema.columns:
                        markdown += f"| {column.name} | {column.type} |\\n"
                    return markdown
                except Exception as e:
                    logging.error(f"Could not generate data dictionary for {table_schema.name}. Error: {e}")
                    return ""
            ```
- [ ] **Step 4.4: Create Unit Tests for Error Handling**
    - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct error handling in `parse_create_table` and `generate_data_dictionary`.
    - [ ] **Prompt 19:**
        - [ ] In the file `tests/test_sql_parser.py`, create unit tests to verify the correct error handling in `parse_create_table` and `generate_data_dictionary`.
            ```python
            import pytest
            import logging
            from sql_parser.ddl_analyzer import parse_create_table
            from outputs.data_dictionary import generate_data_dictionary

            def test_parse_create_table_error_handling(caplog):
                sql = "CREATE TABLE users (id INT, name VARCHAR(255"  # Missing closing parenthesis
                with caplog.at_level(logging.WARNING):
                    table_schema = parse_create_table(sql)
                    assert "Could not parse CREATE TABLE statement" in caplog.text
                    assert table_schema.name == "unknown"

            def test_generate_data_dictionary_error_handling(caplog):
                from sql_parser.ddl_analyzer import TableSchema, ColumnSchema
                table_schema = TableSchema(name="users", columns=[ColumnSchema(name="id", type=123)]) # Incorrect type
                with caplog.at_level(logging.ERROR):
                    markdown = generate_data_dictionary(table_schema)
                    assert "Could not generate data dictionary for users" in caplog.text
                    assert markdown == ""
            ```
- [ ] **Step 4.5: Run `main.py` with Invalid SQL and Verify Logging**
    - [ ] Update the `sample.sql` file with an invalid SQL statement.
    - [ ] Run `main.py` and verify that the error is logged to `app.log`.
    - [ ] **Prompt 20:**
        - [ ] Update the `sample.sql` file with an invalid SQL statement (e.g., missing closing parenthesis).
        - [ ] Run `main.py` and verify that the error is logged to `app.log`.
- [ ] **Step 4.6: Run Unit Tests**
    - [ ] Run the unit tests using `pytest` to ensure that the error handling is working correctly.
    - [ ] **Prompt 21:**
        - [ ] Run the unit tests using pytest to ensure that the error handling is working correctly.

### Phase 2: Advanced Parsing and Lineage Tracking

- [ ] **Step 5: Advanced SQL Parsing**
    - [ ] **Step 5.1: Extend `TableSchema` to Include Constraints and Comments**
        - [ ] Update the `TableSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to include fields for `constraints` (list of constraint definitions) and `comment` (table comment). Each constraint definition should include `type` and `columns`.
        - [ ] **Prompt 22:**
            - [ ] Update the `TableSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to include fields for `constraints` (list of constraint definitions) and `comment` (table comment). Each constraint definition should include `type` and `columns`.
                ```python
                from pydantic import BaseModel
                from typing import List, Dict, Optional

                class ColumnSchema(BaseModel):
                    name: str
                    type: str

                class ConstraintSchema(BaseModel):
                    type: str
                    columns: List[str]

                class TableSchema(BaseModel):
                    name: str
                    columns: List[ColumnSchema]
                    constraints: Optional[List[ConstraintSchema]] = None
                    comment: Optional[str] = None
                ```
    - [ ] **Step 5.2: Implement Parsing for `CREATE VIEW` Statements**
        - [ ] Extend the `parse_create_table` function in `sql_parser/ddl_analyzer.py` to handle `CREATE VIEW` statements. Extract the view name and column definitions.
        - [ ] **Prompt 23:**
            - [ ] Extend the `parse_create_table` function in `sql_parser/ddl_analyzer.py` to handle `CREATE VIEW` statements. Extract the view name and column definitions. Rename the function to `parse_create_statement` and handle both CREATE TABLE and CREATE VIEW.
                ```python
                import logging
                from sqlglot import parse_one, exp
                from sql_parser.ddl_analyzer import TableSchema, ColumnSchema, ConstraintSchema
                from typing import Union

                def parse_create_statement(sql: str) -> TableSchema:
                    try:
                        statement = parse_one(sql)
                        if isinstance(statement, exp.Create):
                            table_name = statement.args['this'].this
                            columns = []
                            for column_def in statement.args['expressions']:
                                column_name = column_def.args['this']
                                column_type = column_def.args['kind'].this
                                columns.append(ColumnSchema(name=column_name, type=column_type))
                            return TableSchema(name=table_name, columns=columns)
                        elif isinstance(statement, exp.CreateView):
                            table_name = statement.this
                            columns = []
                            # Views don't explicitly define columns, so we'll leave it empty for now
                            return TableSchema(name=table_name, columns=columns)
                        else:
                            logging.warning(f"Unsupported statement type: {type(statement)}")
                            return TableSchema(name="unknown", columns=[])
                    except Exception as e:
                        logging.warning(f"Could not parse CREATE statement: {sql}. Error: {e}")
                        # Return an empty TableSchema to allow processing to continue
                        return TableSchema(name="unknown", columns=[])
                ```
    - [ ] **Step 5.3: Implement Parsing for Constraints**
        - [ ] Extend the `parse_create_statement` function in `sql_parser/ddl_analyzer.py` to extract constraints (e.g., `PRIMARY KEY`, `FOREIGN KEY`) from `CREATE TABLE` statements.
        - [ ] **Prompt 24:**
            - [ ] Extend the `parse_create_statement` function in `sql_parser/ddl_analyzer.py` to extract constraints (e.g., `PRIMARY KEY`, `FOREIGN KEY`) from `CREATE TABLE` statements.
                ```python
                import logging
                from sqlglot import parse_one, exp
                from sql_parser.ddl_analyzer import TableSchema, ColumnSchema, ConstraintSchema
                from typing import Union

                def parse_create_statement(sql: str) -> TableSchema:
                    try:
                        statement = parse_one(sql)
                        if isinstance(statement, exp.Create):
                            table_name = statement.args['this'].this
                            columns = []
                            constraints = []
                            for column_def in statement.args['expressions']:
                                column_name = column_def.args['this']
                                column_type = column_def.args['kind'].this
                                columns.append(ColumnSchema(name=column_name, type=column_type))
                                if column_def.args.get('constraints'):
                                    for constraint in column_def.args['constraints']:
                                        if isinstance(constraint, exp.PrimaryKey):
                                            constraints.append(ConstraintSchema(type="primary_key", columns=[column_name]))
                                        elif isinstance(constraint, exp.ForeignKey):
                                            target_table = constraint.args['table'].this
                                            constraints.append(ConstraintSchema(type="foreign_key", columns=[column_name], target_table=target_table))

                        return TableSchema(name=table_name, columns=columns, constraints=constraints)
                    elif isinstance(statement, exp.CreateView):
                        table_name = statement.this
                        columns = []
                        # Views don't explicitly define columns, so we'll leave it empty for now
                        return TableSchema(name=table_name, columns=columns)
                    else:
                        logging.warning(f"Unsupported statement type: {type(statement)}")
                        return TableSchema(name="unknown", columns=[])
                except Exception as e:
                    logging.warning(f"Could not parse CREATE statement: {sql}. Error: {e}")
                    # Return an empty TableSchema to allow processing to continue
                    return TableSchema(name="unknown", columns=[])
                ```
    - [ ] **Step 5.4: Implement Parsing for Comments**
        - [ ] Implement comment parsing in `sql_parser/comment_parser.py` to extract table and column descriptions from SQL scripts. Handle different comment syntaxes (e.g., Oracle `COMMENT ON` vs. SQL Server `sp_addextendedproperty`).
        - [ ] Update the `parse_create_statement` function to use the comment parser and extract table and column comments.
        - [ ] **Prompt 25:**
            - [ ] Implement comment parsing in `sql_parser/comment_parser.py` to extract table and column descriptions from SQL scripts. Handle Oracle's `COMMENT ON` syntax. Then, update the `parse_create_statement` function to use the comment parser and extract table and column comments.
                ```python
                # sql_parser/comment_parser.py
                import logging
                from sqlglot import parse_one, exp

                def parse_comment(sql: str, table_name: str) -> str:
                    try:
                        statement = parse_one(sql)
                        if isinstance(statement, exp.Comment):
                            if statement.args['this'].args['table'].this == table_name:
                                return statement.args['this'].args['expression'].this
                        return None
                    except Exception as e:
                        logging.warning(f"Could not parse COMMENT ON statement: {sql}. Error: {e}")
                        return None

                # sql_parser/ddl_analyzer.py
                import logging
                from sqlglot import parse_one, exp
                from sql_parser.ddl_analyzer import TableSchema, ColumnSchema, ConstraintSchema
                from sql_parser.comment_parser import parse_comment
                from typing import Union

                def parse_create_statement(sql: str, comment_sql: str = None) -> TableSchema:
                    try:
                        statement = parse_one(sql)
                        if isinstance(statement, exp.Create):
                            table_name = statement.args['this'].this
                            columns = []
                            constraints = []
                            for column_def in statement.args['expressions']:
                                column_name = column_def.args['this']
                                column_type = column_def.args['kind'].this
                                columns.append(ColumnSchema(name=column_name, type=column_type))
                                if column_def.args.get('constraints'):
                                    for constraint in column_def.args['constraints']:
                                        if isinstance(constraint, exp.constraints.append(ConstraintSchema(type="primary_key", columns=[column_name]))
                                    elif isinstance(constraint, exp.ForeignKey):
                                        target_table = constraint.args['table'].this
                                        constraints.append(ConstraintSchema(type="foreign_key", columns=[column_name], target_table=target_table))

                        table_comment = parse_comment(comment_sql, table_name) if comment_sql else None

                        return TableSchema(name=table_name, columns=columns, constraints=constraints, comment=table_comment)
                    elif isinstance(statement, exp.CreateView):
                        table_name = statement.this
                        columns = []
                        # Views don't explicitly define columns, so we'll leave it empty for now
                        return TableSchema(name=table_name, columns=columns)
                    else:
                        logging.warning(f"Unsupported statement type: {type(statement)}")
                        return TableSchema(name="unknown", columns=[])
                except Exception as e:
                    logging.warning(f"Could not parse CREATE statement: {sql}. Error: {e}")
                    # Return an empty TableSchema to allow processing to continue
                    return TableSchema(name="unknown", columns=[])
                ```
    - [ ] **Step 5.5: Update `main.py` to Include Comment Parsing**
        - [ ] Update `main.py` to pass the comment SQL to the `parse_create_statement` function.
        - [ ] **Prompt 26:**
            - [ ] Update `main.py` to pass the comment SQL to the `parse_create_statement` function. Assume that the comment immediately follows the CREATE statement.
                ```python
                # main.py
                import logging

                logging.basicConfig(filename="app.log", level=logging.WARNING)

                from sql_parser.ddl_analyzer import parse_create_statement
                from outputs.data_dictionary import generate_data_dictionary

                def main():
                    try:
                        with open("sample.sql", "r") as f:
                            sql_content = f.read()
                        # Split the content into CREATE statement and COMMENT statement (crude approach)
                        statements = sql_content.split(";")
                        create_sql = statements[0].strip() + ";" # Add back the semicolon
                        comment_sql = statements[1].strip() + ";" if len(statements) > 1 else None # Add back the semicolon

                        table_schema = parse_create_statement(create_sql, comment_sql)
                        markdown = generate_data_dictionary(table_schema)
                        with open("data_dictionary.md", "w") as f:
                            f.write(markdown)
                    except Exception as e:
                        logging.error(f"An error occurred: {e}")

                if __name__ == "__main__":
                    main()
                ```
    - [ ] **Step 5.6: Create Unit Tests for Advanced Parsing**
        - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct parsing of `CREATE VIEW` statements, constraints, and comments.
        - [ ] **Prompt 27:**
            - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct parsing of `CREATE VIEW` statements, constraints, and comments.
                ```python
                import pytest
                import logging
                from sql_parser.ddl_analyzer import parse_create_statement, TableSchema, ConstraintSchema, ColumnSchema
                from outputs.data_dictionary import generate_data_dictionary

                def test_parse_create_view():
                    sql = "CREATE VIEW view_users AS SELECT id, name FROM users"
                    table_schema = parse_create_statement(sql)
                    assert table_schema.name == "view_users"
                    assert len(table_schema.columns) == 0

                def test_parse_create_table_constraints():
                    sql = "CREATE TABLE orders (order_id INT PRIMARY KEY, customer_id INT, FOREIGN KEY (customer_id) REFERENCES customers(customer_id))"
                    table_schema = parse_create_statement(sql)
                    assert table_schema.name == "orders"
                    assert len(table_schema.constraints) == 2
                    assert table_schema.constraints[0].type == "primary_key"
                    assert table_schema.constraints[0].columns == ["order_id"]
                    assert table_schema.constraints[1].type == "foreign_key"
                    assert table_schema.constraints[1].columns == ["customer_id"]
                    assert table_schema.constraints[1].target_table == "customers"

                def test_parse_create_table_comments():
                    sql = "CREATE TABLE products (product_id INT, product_name VARCHAR(255))"
                    comment_sql = "COMMENT ON TABLE products IS 'This table stores product information';"
                    table_schema = parse_create_statement(sql, comment_sql)
                    assert table_schema.name == "products"
                    assert table_schema.comment == "'This table stores product information'"
                ```
    - [ ] **Step 5.7: Update `sample.sql` with Advanced SQL**
        - [ ] Update the `sample.sql` file with `CREATE VIEW` statements, constraints, and comments.
        - [ ] **Prompt 28:**
            - [ ] Update the `sample.sql` file with `CREATE VIEW` statements, constraints, and comments.
                ```sql
                CREATE TABLE users (
                    id INT PRIMARY KEY,
                    name VARCHAR(255)
                );

                COMMENT ON TABLE users IS 'This table stores user information';

                CREATE VIEW view_users AS
                SELECT id, name
                FROM users;
                ```
    - [ ] **Step 5.8: Run `main.py` and Verify Output**
        - [ ] Run `main.py` to generate the data dictionary.
        - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary, including the view, constraints, and comments.
        - [ ] **Prompt 29:**
            - [ ] Run `main.py` to generate the data dictionary.
            - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary, including the view, constraints, and comments.
    - [ ] **Step 5.9: Run Unit Tests**
        - [ ] Run the unit tests using `pytest` to ensure that the advanced parsing is working correctly.
        - [ ] **Prompt 30:**
            - [ ] Run the unit tests using pytest to ensure that the advanced parsing is working correctly.

### Step 6: Column Lineage Tracking

- [ ] **Step 6.1: Implement Basic Column Lineage Tracking in `dml_analyzer.py`**
    - [ ] Implement a function `track_column_lineage` in `lineage_tracker/dml_analyzer.py` that takes an `INSERT...SELECT` SQL statement as input and returns a dictionary representing the column lineage.
    - [ ] The dictionary should map each target column in the `INSERT` statement to its source column(s) in the `SELECT` statement.
    - [ ] For now, focus on simple cases where the source column is a direct reference to a column in a table (e.g., `INSERT INTO table1 (col1) SELECT col2 FROM table2`).
    - [ ] **Prompt 31:**
        - [ ] Implement a function `track_column_lineage` in `lineage_tracker/dml_analyzer.py` that takes an `INSERT...SELECT` SQL statement as input and returns a dictionary representing the column lineage.
            ```python
            from sqlglot import parse_one, exp
            from typing import Dict, List

            def track_column_lineage(sql: str) -> Dict[str, List[str]]:
                statement = parse_one(sql)
                if not isinstance(statement, exp.Insert):
                    raise ValueError("Expected INSERT statement")

                target_columns = [t.this for t in statement.args['this'].args['columns']]
                select_statement = statement.args['expression']

                if not isinstance(select_statement, exp.Select):
                    raise ValueError("Expected SELECT statement in INSERT")

                source_columns = []
                for e in select_statement.args['expressions']:
                    if isinstance(e, exp.Identifier):
                        source_columns.append(e.this)
                    else:
                        source_columns.append(str(e)) # Handle expressions

                if len(target_columns) != len(source_columns):
                    raise ValueError("Target and source column counts do not match")

                lineage = {}
                for i, target_column in enumerate(target_columns):
                    lineage[target_column] = [source_columns[i]]

                return lineage
            ```
- [ ] **Step 6.2: Update `TableSchema` to Include Column Lineage**
    - [ ] Update the `ColumnSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to include a field for `source` (a dictionary containing the source table and column).
    - [ ] **Prompt 32:**
        - [ ] Update the `ColumnSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to include a field for `source` (a dictionary containing the source table and column).
            ```python
            from pydantic import BaseModel
            from typing import List, Dict, Optional

            class ColumnSchema(BaseModel):
                name: str
                type: str
                source: Optional[Dict[str, str]] = None

            class ConstraintSchema(BaseModel):
                type: str
                columns: List[str]

            class TableSchema(BaseModel):
                name: str
                columns: List[ColumnSchema]
                constraints: Optional[List[ConstraintSchema]] = None
                comment: Optional[str] = None
            ```
- [ ] **Step 6.3: Update `parse_create_statement` to Incorporate Lineage**
    - [ ] Modify the `parse_create_statement` function in `sql_parser/ddl_analyzer.py` to call `track_column_lineage` when an `INSERT...SELECT` statement is encountered after a `CREATE TABLE` statement.
    - [ ] Update the `ColumnSchema` objects with the lineage information.
    - [ ] **Prompt 33:**
        - [ ] Modify the `parse_create_statement` function in `sql_parser/ddl_analyzer.py` to call `track_column_lineage` when an `INSERT...SELECT` statement is encountered after a `CREATE TABLE` statement. Assume the insert statement comes right after the create table statement. Update the `ColumnSchema` objects with the lineage information.
            ```python
            import logging
            from sqlglot import parse_one, exp
            from sql_parser.ddl_analyzer import TableSchema, ColumnSchema, ConstraintSchema
            from sql_parser.comment_parser import parse_comment
            from lineage_tracker.dml_analyzer import track_column_lineage
            from typing import Union

            def parse_create_statement(sql: str, insert_sql: str = None) -> TableSchema:
                try:
                    statement = parse_one(sql)
                    if isinstance(statement, exp.Create):
                        table_name = statement.args['this'].this
                        columns = []
                        constraints = []
                        for column_def in statement.args['expressions']:
                            column_name = column_def.args['this']
                            column_type = column_def.args['kind'].this
                            columns.append(ColumnSchema(name=column_name, type=column_type))
                            if column_def.args.get('constraints'):
                                for constraint in column_def.args['constraints']:
                                    if isinstance(constraint, exp.PrimaryKey):
                                        constraints.append(ConstraintSchema(type="primary_key", columns=[column_name]))
                                    elif isinstance(constraint, exp.ForeignKey):
                                        target_table = constraint.args['table'].this
                                        constraints.append(ConstraintSchema(type="foreign_key", columns=[column_name], target_table=target_table))

                    table_comment = None #parse_comment(comment_sql, table_name) if comment_sql else None

                    table_schema = TableSchema(name=table_name, columns=columns, constraints=constraints, comment=table_comment)

                    if insert_sql:
                        try:
                            lineage = track_column_lineage(insert_sql)
                            for column in table_schema.columns:
                                if column.name in lineage:
                                    source_column = lineage[column.name][0]
                                    table_schema.columns[table_schema.columns.index(column)].source = {"table": "unknown", "column": source_column} #Need to resolve table
                        except Exception as e:
                            logging.warning(f"Could not track column lineage: {e}")

                    return table_schema

                elif isinstance(statement, exp.CreateView):
                    table_name = statement.this
                    columns = []
                    # Views don't explicitly define columns, so we'll leave it empty for now
                    return TableSchema(name=table_name, columns=columns)
                else:
                    logging.warning(f"Unsupported statement type: {type(statement)}")
                    return TableSchema(name="unknown", columns=[])
            except Exception as e:
                logging.warning(f"Could not parse CREATE statement: {sql}. Error: {e}")
                # Return an empty TableSchema to allow processing to continue
                return TableSchema(name="unknown", columns=[])
            ```
- [ ] **Step 6.4: Create Unit Tests for Column Lineage Tracking**
    - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct column lineage tracking.
    - [ ] **Prompt 34:**
        - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct column lineage tracking.
            ```python
            import pytest
            import logging
            from sql_parser.ddl_analyzer import parse_create_statement, TableSchema, ColumnSchema, ConstraintSchema
            from lineage_tracker.dml_analyzer import track_column_lineage

            def test_track_column_lineage():
                sql = "INSERT INTO table1 (col1) SELECT col2 FROM table2"
                lineage = track_column_lineage(sql)
                assert lineage == {"col1": ["col2"]}

            def test_parse_create_table_lineage():
                create_sql = "CREATE TABLE table1 (col1 INT)"
                insert_sql = "INSERT INTO table1 (col1) SELECT col2 FROM table2"
                table_schema = parse_create_statement(create_sql, insert_sql)
                assert table_schema.name == "table1"
                assert table_schema.columns[0].source == {"table": "unknown", "column": "col2"}
            ```
- [ ] **Step 6.5: Update `sample.sql` with `INSERT...SELECT` Statement**
    - [ ] Update the `sample.sql` file to include an `INSERT...SELECT` statement after the `CREATE TABLE` statement.
    - [ ] **Prompt 35:**
        - [ ] Update the `sample.sql` file to include an `INSERT...SELECT` statement after the `CREATE TABLE` statement.
            ```sql
            CREATE TABLE users (
                id INT PRIMARY KEY,
                name VARCHAR(255)
            );

            INSERT INTO users (id) SELECT user_id FROM raw_users;

            CREATE VIEW view_users AS
            SELECT id, name
            FROM users;
            ```
- [ ] **Step 6.6: Update `main.py` to Pass `INSERT` SQL**
    - [ ] Update `main.py` to pass the `INSERT` SQL to the `parse_create_statement` function.
    - [ ] **Prompt 36:**
        - [ ] Update `main.py` to pass the `INSERT` SQL to the `parse_create_statement` function.
            ```python
            import logging

            logging.basicConfig(filename="app.log", level=logging.WARNING)

            from sql_parser.ddl_analyzer import parse_create_statement
            from outputs.data_dictionary import generate_data_dictionary

            def main():
                try:
                    with open("sample.sql", "r") as f:
                        sql_content = f.read()
                    # Split the content into CREATE statement and INSERT statement (crude approach)
                    statements = sql_content.split(";")
                    create_sql = statements[0].strip() + ";" # Add back the semicolon
                    insert_sql = statements[1].strip() + ";" if len(statements) > 1 else None # Add back the semicolon

                    table_schema = parse_create_statement(create_sql, insert_sql)
                    markdown = generate_data_dictionary(table_schema)
                    with open("data_dictionary.md", "w") as f:
                        f.write(markdown)
                except Exception as e:
                    logging.error(f"An error occurred: {e}")

            if __name__ == "__main__":
                main()
            ```
- [ ] **Step 6.7: Run `main.py` and Verify Output**
    - [ ] Run `main.py` to generate the data dictionary.
    - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary, including the column lineage information.
    - [ ] **Prompt 37:**
        - [ ] Run `main.py` to generate the data dictionary.
        - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary, including the column lineage information.
- [ ] **Step 6.8: Run Unit Tests**
    - [ ] Run the unit tests using `pytest` to ensure that the column lineage tracking is working correctly.
    - [ ] **Prompt 38:**
        - [ ] Run the unit tests using pytest to ensure that the column lineage tracking is working correctly.

### Step 7: Transformation Logic Documentation

- [ ] **Step 7.1: Update `ColumnSchema` to Include Transformation Logic**
    - [ ] Update the `ColumnSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to include a field for `transformation` (a string containing the transformation logic).
    - [ ] **Prompt 39:**
        - [ ] Update the `ColumnSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to include a field for `transformation` (a string containing the transformation logic).
            ```python
            from pydantic import BaseModel
            from typing import List, Dict, Optional

            class ColumnSchema(BaseModel):
                name: str
                type: str
                source: Optional[Dict[str, str]] = None
                transformation: Optional[str] = None

            class ConstraintSchema(BaseModel):
                type: str
                columns: List[str]

            class TableSchema(BaseModel):
                name: str
                columns: List[ColumnSchema]
                constraints: Optional[List[ConstraintSchema]] = None
                comment: Optional[str] = None
            ```
- [ ] **Step 7.2: Implement Transformation Logic Documentation in `transformation.py`**
    - [ ] Implement a function `document_transformation` in `lineage_tracker/transformation.py` that takes a `sqlglot.Expression` object as input and returns a string representation of the transformation logic.
    - [ ] Focus on documenting calculated columns (e.g., `total = col_a + col_b`, `CASE WHEN condition THEN value ELSE value END`).
    - [ ] **Prompt 40:**
        - [ ] Implement a function `document_transformation` in `lineage_tracker/transformation.py` that takes a `sqlglot.Expression` object as input and returns a string representation of the transformation logic.
            ```python
            from sqlglot import exp

            def document_transformation(expression: exp.Expression) -> str:
                """
                Documents the transformation logic of a calculated column.
                """
                return expression.sql()
            ```
- [ ] **Step 7.3: Update `track_column_lineage` to Document Transformations**
    - [ ] Update the `track_column_lineage` function in `lineage_tracker/dml_analyzer.py` to call `document_transformation` for calculated columns and store the transformation logic in the `lineage` dictionary.
    - [ ] **Prompt 41:**
        - [ ] Update the `track_column_lineage` function in `lineage_tracker/dml_analyzer.py` to call `document_transformation` for calculated columns and store the transformation logic in the `lineage` dictionary.
            ```python
            from sqlglot import parse_one, exp
            from typing import Dict, List
            from lineage_tracker.transformation import document_transformation

            def track_column_lineage(sql: str) -> Dict[str, List[str]]:
                statement = parse_one(sql)
                if not isinstance(statement, exp.Insert):
                    raise ValueError("Expected INSERT statement")

                target_columns = [t.this for t in statement.args['this'].args['columns']]
                select_statement = statement.args['expression']

                if not isinstance(select_statement, exp.Select):
                    raise ValueError("Expected SELECT statement in INSERT")

                source_columns = []
                transformations = {}
                for e in select_statement.args['expressions']:
                    if isinstance(e, exp.Identifier):
                        source_columns.append(e.this)
                    else:
                        source_columns.append(str(e)) # Handle expressions
                        transformations[str(e)] = document_transformation(e)

                if len(target_columns) != len(source_columns):
                    raise ValueError("Target and source column counts do not match")

                lineage = {}
                for i, target_column in enumerate(target_columns):
                    lineage[target_column] = {"source": [source_columns[i]]}
                    if source_columns[i] in transformations:
                        lineage[target_column]["transformation"] = transformations[source_columns[i]]

                return lineage
            ```
- [ ] **Step 7.4: Update `parse_create_statement` to Incorporate Transformation Logic**
    - [ ] Modify the `parse_create_statement` function in `sql_parser/ddl_analyzer.py` to update the `ColumnSchema` objects with the transformation logic.
    - [ ] **Prompt 42:**
        - [ ] Modify the `parse_create_statement` function in `sql_parser/ddl_analyzer.py` to update the `ColumnSchema` objects with the transformation logic.
            ```python
            import logging
            from sqlglot import parse_one, exp
            from sql_parser.ddl_analyzer import TableSchema, ColumnSchema, ConstraintSchema
            from sql_parser.comment_parser import parse_comment
            from lineage_tracker.dml_analyzer import track_column_lineage
            from typing import Union

            def parse_create_statement(sql: str, insert_sql: str = None) -> TableSchema:
                try:
                    statement = parse_one(sql)
                    if isinstance(statement, exp.Create):
                        table_name = statement.args['this'].this
                        columns = []
                        constraints = []
                        for column_def in statement.args['expressions']:
                            column_name = column_def.args['this']
                            column_type = column_def.args['kind'].this
                            columns.append(ColumnSchema(name=column_name, type=column_type))
                            if column_def.args.get('constraints'):
                                for constraint in column_def.args['constraints']:
                                    if isinstance(constraint, exp.PrimaryKey):
                                        constraints.append(ConstraintSchema(type="primary_key", columns=[column_name]))
                                    elif isinstance(constraint, exp.ForeignKey):
                                        target_table = constraint.args['table'].this
                                        constraints.append(ConstraintSchema(type="foreign_key", columns=[column_name], target_table=target_table))

                    table_comment = None #parse_comment(comment_sql, table_name) if comment_sql else None

                    table_schema = TableSchema(name=table_name, columns=columns, constraints=constraints, comment=table_comment)

                    if insert_sql:
                        try:
                            lineage = track_column_lineage(insert_sql)
                            for column in table_schema.columns:
                                if column.name in lineage:
                                    column_lineage = lineage[column.name]
                                    table_schema.columns[table_schema.columns.index(column)].source = {"table": "unknown", "column": column_lineage['source'][0]} #Need to resolve table
                                    if "transformation" in column_lineage:
                                        table_schema.columns[table_schema.columns.index(column)].transformation = column_lineage["transformation"]
                        except Exception as e:
                            logging.warning(f"Could not track column lineage: {e}")

                    return table_schema

                elif isinstance(statement, exp.CreateView):
                    table_name = statement.this
                    columns = []
                    # Views don't explicitly define columns, so we'll leave it empty for now
                    return TableSchema(name=table_name, columns=columns)
                else:
                    logging.warning(f"Unsupported statement type: {type(statement)}")
                    return TableSchema(name="unknown", columns=[])
            except Exception as e:
                logging.warning(f"Could not parse CREATE statement: {sql}. Error: {e}")
                # Return an empty TableSchema to allow processing to continue
                return TableSchema(name="unknown", columns=[])
            ```
- [ ] **Step 7.5: Create Unit Tests for Transformation Logic Documentation**
    - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct transformation logic documentation.
    - [ ] **Prompt 43:**
        - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct transformation logic documentation.
            ```python
            import pytest
            import logging
            from sql_parser.ddl_analyzer import parse_create_statement, TableSchema, ColumnSchema, ConstraintSchema
            from lineage_tracker.dml_analyzer import track_column_lineage

            def test_track_column_lineage_transformation():
                sql = "INSERT INTO table1 (col1) SELECT col2 + col3 FROM table2"
                lineage = track_column_lineage(sql)
                assert lineage["col1"]["transformation"] == "(col2 + col3)"

            def test_parse_create_table_transformation():
                create_sql = "CREATE TABLE table1 (col1 INT)"
                insert_sql = "INSERT INTO table1 (col1) SELECT col2 + col3 FROM table2"
                table_schema = parse_create_statement(create_sql, insert_sql)
                assert table_schema.name == "table1"
                assert table_schema.columns[0].transformation == "(col2 + col3)"
            ```
- [ ] **Step 7.6: Update `sample.sql` with Calculated Column**
    - [ ] Update the `sample.sql` file to include an `INSERT...SELECT` statement with a calculated column.
    - [ ] **Prompt 44:**
        - [ ] Update the `sample.sql` file to include an `INSERT...SELECT` statement with a calculated column.
            ```sql
            CREATE TABLE users (
                id INT PRIMARY KEY,
                name VARCHAR(255),
                full_name VARCHAR(255)
            );

            INSERT INTO users (id, full_name) SELECT user_id, first_name || ' ' || last_name FROM raw_users;

            CREATE VIEW view_users AS
            SELECT id, name
            FROM users;
            ```
- [ ] **Step 7.7: Run `main.py` and Verify Output**
    - [ ] Run `main.py` to generate the data dictionary.
    - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary, including the transformation logic for the calculated column.
    - [ ] **Prompt 45:**
        - [ ] Run `main.py` to generate the data dictionary.
        - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary, including the transformation logic for the calculated column.
- [ ] **Step 7.8: Run Unit Tests**
    - [ ] Run the unit tests using `pytest` to ensure that the transformation logic documentation is working correctly.
    - [ ] **Prompt 46:**
        - [ ] Run the unit tests using pytest to ensure that the transformation logic documentation is working correctly.

### Phase 3: ER Diagram Generation and Refinement

- [ ] **Step 8: Basic ER Diagram Generation**
    - [ ] **Step 8.1: Implement Basic ER Diagram Generation Function**
        - [ ] Implement a function `generate_er_diagram` in `diagram_generator/er_diagram.py` that takes a list of `TableSchema` objects as input and returns a Mermaid ER diagram representation.
        - [ ] Represent tables as nodes and relationships as edges (explicit = solid).
        - [ ] For now, only handle explicit relationships (i.e., `FOREIGN KEY` constraints).
        - [ ] **Prompt 47:**
            - [ ] Implement a function `generate_er_diagram` in `diagram_generator/er_diagram.py` that takes a list of `TableSchema` objects as input and returns a Mermaid ER diagram representation.
                ```python
                from sql_parser.ddl_analyzer import TableSchema

                def generate_er_diagram(table_schemas: List[TableSchema]) -> str:
                    """
                    Generates a Mermaid ER diagram representation from a list of TableSchema objects.
                    """
                    diagram = "erDiagram\n"
                    for table_schema in table_schemas:
                        diagram += f"    {table_schema.name} {{\n"
                        for column in table_schema.columns:
                            diagram += f"        {column.type} {column.name}\n"
                        diagram += "    }\n"

                    for table_schema in table_schemas:
                        if table_schema.constraints:
                            for constraint in table_schema.constraints:
                                if constraint.type == "foreign_key":
                                    diagram += f"    {table_schema.name} ||--|| {constraint.target_table} : {constraint.columns[0]}\n"
                    return diagram
                ```
    - [ ] **Step 8.2: Update `main.py` to Generate ER Diagram**
        - [ ] Update `main.py` to call `generate_er_diagram` after parsing the SQL and write the diagram to a file (e.g., `er_diagram.mmd`).
        - [ ] **Prompt 48:**
            - [ ] Update `main.py` to call `generate_er_diagram` after parsing the SQL and write the diagram to a file (e.g., `er_diagram.mmd`).
                ```python
                import logging

                logging.basicConfig(filename="app.log", level=logging.WARNING)

                from sql_parser.ddl_analyzer import parse_create_statement
                from outputs.data_dictionary import generate_data_dictionary
                from diagram_generator.er_diagram import generate_er_diagram

                def main():
                    try:
                        with open("sample.sql", "r") as f:
                            sql_content = f.read()
                        # Split the content into CREATE statement and INSERT statement (crude approach)
                        statements = sql_content.split(";")
                        create_sql = statements[0].strip() + ";" # Add back the semicolon
                        insert_sql = statements[1].strip() + ";" if len(statements) > 1 else None # Add back the semicolon

                        table_schema = parse_create_statement(create_sql, insert_sql)
                        markdown = generate_data_dictionary(table_schema)
                        with open("data_dictionary.md", "w") as f:
                            f.write(markdown)

                        er_diagram = generate_er_diagram([table_schema])
                    with open("er_diagram.mmd", "w") as f:
                        f.write(er_diagram)

                except Exception as e:
                    logging.error(f"An error occurred: {e}")

            if __name__ == "__main__":
                main()
            ```
    - [ ] **Step 8.3: Create Unit Tests for ER Diagram Generation**
        - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct generation of the ER diagram.
        - [ ] **Prompt 49:**
            - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct generation of the ER diagram.
                ```python
                import pytest
                import logging
                from sql_parser.ddl_analyzer import parse_create_statement, TableSchema, ColumnSchema, ConstraintSchema
                from diagram_generator.er_diagram import generate_er_diagram

                def test_generate_er_diagram():
                    create_sql = "CREATE TABLE orders (order_id INT PRIMARY KEY, customer_id INT, FOREIGN KEY (customer_id) REFERENCES customers(customer_id))"
                    table_schema = parse_create_statement(create_sql)
                    er_diagram = generate_er_diagram([table_schema])
                    assert "erDiagram" in er_diagram
                    assert "orders {" in er_diagram
                    assert "customers {" not in er_diagram #Customers table not explicitly defined
                    assert "orders ||--|| customers : customer_id" in er_diagram
                ```
    - [ ] **Step 8.4: Run `main.py` and Verify Output**
        - [ ] Run `main.py` to generate the ER diagram.
        - [ ] Verify that the `er_diagram.mmd` file is created and contains the correct Mermaid ER diagram representation.
        - [ ] **Prompt 50:**
            - [ ] Run `main.py` to generate the ER diagram.
            - [ ] Verify that the `er_diagram.mmd` file is created and contains the correct Mermaid ER diagram representation.
    - [ ] **Step 8.5: Run Unit Tests**
        - [ ] Run the unit tests using `pytest` to ensure that the ER diagram generation is working correctly.
        - [ ] **Prompt 51:**
            - [ ] Run the unit tests using pytest to ensure that the ER diagram generation is working correctly.

### Step 9: Relationship Inference

- [ ] **Step 9.1: Implement Implicit Relationship Inference**
    - [ ] Implement logic in `sql_parser/dml_analyzer.py` to infer implicit relationships from `JOIN` conditions in `SELECT` statements.
    - [ ] For example, if a `SELECT` statement joins `table1` and `table2` on `table1.col1 = table2.col2`, infer an implicit relationship between `table1` and `table2`.
    - [ ] **Prompt 52:**
        - [ ] Implement logic in `sql_parser/dml_analyzer.py` to infer implicit relationships from `JOIN` conditions in `SELECT` statements.
            ```python
            from sqlglot import parse_one, exp
            from typing import Dict, List, Tuple

            def infer_implicit_relationships(sql: str) -> List[Tuple[str, str, str]]:
                """
                Infers implicit relationships from JOIN conditions in a SELECT statement.
                Returns a list of tuples: (table1, table2, join_condition)
                """
                statement = parse_one(sql)
                relationships = []

                if isinstance(statement, exp.Select):
                    for join in statement.args.get('joins', []):
                        if isinstance(join, exp.Join):
                            left = join.args['this'].args['this'].this #table name
                            right = join.args['expression'].args['this'].this #table name
                            condition = join.args['on'].sql()
                            relationships.append((left, right, condition))
                return relationships
            ```
- [ ] **Step 9.2: Implement Aggregated Relationship Inference**
    - [ ] Implement logic in `sql_parser/dml_analyzer.py` to infer aggregated relationships from columns derived from functions (e.g., `COALESCE`, `CASE`).
    - [ ] For example, if a column is derived from `COALESCE(table1.col1, table2.col2)`, infer an aggregated relationship between `table1` and `table2`.
    - [ ] **Prompt 53:**
        - [ ] Implement logic in `sql_parser/dml_analyzer.py` to infer aggregated relationships from columns derived from functions (e.g., `COALESCE`, `CASE`).
            ```python
            from sqlglot import parse_one, exp
            from typing import Dict, List, Tuple

            def infer_aggregated_relationships(sql: str) -> List[Tuple[str, str, str]]:
                """
                Infers aggregated relationships from columns derived from functions.
                Returns a list of tuples: (table1, table2, function)
                """
                statement = parse_one(sql)
                relationships = []

                if isinstance(statement, exp.Select):
                    for e in statement.args['expressions']:
                        if isinstance(e, exp.Coalesce):
                            tables = []
                            for arg in e.args['this']:
                                if isinstance(arg, exp.Column):
                                    table = arg.args['table'].this
                                    tables.append(table)
                            if len(tables) == 2:
                                relationships.append((tables[0], tables[1], "COALESCE"))
                return relationships
            ```
- [ ] **Step 9.3: Update `TableSchema` to Include Inferred Relationships**
    - [ ] Update the `TableSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to include a list of inferred relationships. Each inferred relationship should include the target table, the type of relationship (implicit or aggregated), and the join condition or function.
    - [ ] **Prompt 54:**
        - [ ] Update the `TableSchema` Pydantic model in `sql_parser/ddl_analyzer.py` to include a list of inferred relationships. Each inferred relationship should include the target table, the type of relationship (implicit or aggregated), and the join condition or function.
            ```python
            from pydantic import BaseModel
            from typing import List, Dict, Optional

            class ColumnSchema(BaseModel):
                name: str
                type: str
                source: Optional[Dict[str, str]] = None
                transformation: Optional[str] = None

            class ConstraintSchema(BaseModel):
                type: str
                columns: List[str]

            class InferredRelationshipSchema(BaseModel):
                target_table: str
                type: str #implicit or aggregated
                condition: Optional[str] = None
                function: Optional[str] = None

            class TableSchema(BaseModel):
                name: str
                columns: List[ColumnSchema]
                constraints: Optional[List[ConstraintSchema]] = None
                comment: Optional[str] = None
                inferred_relationships: Optional[List[InferredRelationshipSchema]] = None
            ```
- [ ] **Step 9.4: Update `track_column_lineage` to Incorporate Relationship Inference**
    - [ ] Modify the `track_column_lineage` function in `lineage_tracker/dml_analyzer.py` to call `infer_implicit_relationships` and `infer_aggregated_relationships` and update the `TableSchema` objects with the inferred relationships.
    - [ ] **Prompt 55:**
        - [ ] Modify the `track_column_lineage` function in `lineage_tracker/dml_analyzer.py` to call `infer_implicit_relationships` and `infer_aggregated_relationships` and update the `TableSchema` objects with the inferred relationships.
            ```python
            from sqlglot import parse_one, exp
            from typing import Dict, List
            from lineage_tracker.transformation import document_transformation
            from sql_parser.dml_analyzer import infer_implicit_relationships, infer_aggregated_relationships
            from sql_parser.ddl_analyzer import InferredRelationshipSchema

            def track_column_lineage(sql: str) -> Dict[str, List[str]]:
                statement = parse_one(sql)
                if not isinstance(statement, exp.Insert):
                    raise ValueError("Expected INSERT statement")

                target_columns = [t.this for t in statement.args['this'].args['columns']]
                select_statement = statement.args['expression']

                if not isinstance(select_statement, exp.Select):
                    raise ValueError("Expected SELECT statement in INSERT")

                source_columns = []
                transformations = {}
                for e in select_statement.args['expressions']:
                    if isinstance(e, exp.Identifier):
                        source_columns.append(e.this)
                    else:
                        source_columns.append(str(e)) # Handle expressions
                        transformations[str(e)] = document_transformation(e)

                if len(target_columns) != len(source_columns):
                    raise ValueError("Target and source column counts do not match")

                lineage = {}
                for i, target_column in enumerate(target_columns):
                    lineage[target_column] = {"source": [source_columns[i]]}
                    if source_columns[i] in transformations:
                        lineage[target_column]["transformation"] = transformations[source_columns[i]]

                implicit_relationships = infer_implicit_relationships(select_statement.sql())
                aggregated_relationships = infer_aggregated_relationships(select_statement.sql())

                return lineage, implicit_relationships, aggregated_relationships
            ```
- [ ] **Step 9.5: Update `parse_create_statement` to Incorporate Relationship Inference**
    - [ ] Modify the `parse_create_statement` function in `sql_parser/ddl_analyzer.py` to update the `TableSchema` objects with the inferred relationships.
    - [ ] **Prompt 56:**
        - [ ] Modify the `parse_create_statement` function in `sql_parser/ddl_analyzer.py` to update the `TableSchema` objects with the inferred relationships.
            ```python
            import logging
            from sqlglot import parse_one, exp
            from sql_parser.ddl_analyzer import TableSchema, ColumnSchema, ConstraintSchema, InferredRelationshipSchema
            from sql_parser.comment_parser import parse_comment
            from lineage_tracker.dml_analyzer import track_column_lineage
            from typing import Union

            def parse_create_statement(sql: str, insert_sql: str = None) -> TableSchema:
                try:
                    statement = parse_one(sql)
                    if isinstance(statement, exp.Create):
                        table_name = statement.args['this'].this
                        columns = []
                        constraints = []
                        for column_def in statement.args['expressions']:
                            column_name = column_def.args['this']
                            column_type = column_def.args['kind'].this
                            columns.append(ColumnSchema(name=column_name, type=column_type))
                            if column_def.args.get('constraints'):
                                for constraint in column_def.args['constraints']:
                                    if isinstance(constraint, exp.PrimaryKey):
                                        constraints.append(ConstraintSchema(type="primary_key", columns=[column_name]))
                                    elif isinstance(constraint, exp.ForeignKey):
                                        target_table = constraint.args['table'].this
                                        constraints.append(ConstraintSchema(type="foreign_key", columns=[column_name], target_table=target_table))

                    table_comment = None #parse_comment(comment_sql, table_name) if comment_sql else None

                    table_schema = TableSchema(name=table_name, columns=columns, constraints=constraints, comment=table_comment)

                    if insert_sql:
                        try:
                            lineage, implicit_relationships, aggregated_relationships = track_column_lineage(insert_sql)
                            for column in table_schema.columns:
                                if column.name in lineage:
                                    column_lineage = lineage[column.name]
                                    table_schema.columns[table_schema.columns.index(column)].source = {"table": "unknown", "column": column_lineage['source'][0]} #Need to resolve table
                                    if "transformation" in column_lineage:
                                        table_schema.columns[table_schema.columns.index(column)].transformation = column_lineage["transformation"]

                            inferred_relationships = []
                            for rel in implicit_relationships:
                                inferred_relationships.append(InferredRelationshipSchema(target_table=rel[1], type="implicit", condition=rel[2]))

                            for rel in aggregated_relationships:
                                inferred_relationships.append(InferredRelationshipSchema(target_table=rel[1], type="aggregated", function=rel[2]))

                            table_schema.inferred_relationships = inferred_relationships


                        except Exception as e:
                            logging.warning(f"Could not track column lineage: {e}")

                    return table_schema

                elif isinstance(statement, exp.CreateView):
                    table_name = statement.this
                    columns = []
                    # Views don't explicitly define columns, so we'll leave it empty for now
                    return TableSchema(name=table_name, columns=columns)
                else:
                    logging.warning(f"Unsupported statement type: {type(statement)}")
                    return TableSchema(name="unknown", columns=[])
            except Exception as e:
                logging.warning(f"Could not parse CREATE statement: {sql}. Error: {e}")
                # Return an empty TableSchema to allow processing to continue
                return TableSchema(name="unknown", columns=[])
            ```
- [ ] **Step 9.6: Create Unit Tests for Relationship Inference**
    - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct inference of implicit and aggregated relationships.
    - [ ] **Prompt 57:**
        - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct inference of implicit and aggregated relationships.
            ```python
            import pytest
            import logging
            from sql_parser.ddl_analyzer import parse_create_statement, TableSchema, ColumnSchema, ConstraintSchema, InferredRelationshipSchema
            from lineage_tracker.dml_analyzer import track_column_lineage

            def test_infer_implicit_relationships():
                from sql_parser.dml_analyzer import infer_implicit_relationships
                sql = "SELECT * FROM table1 JOIN table2 ON table1.col1 = table2.col2"
                relationships = infer_implicit_relationships(sql)
                assert len(relationships) == 1
                assert relationships[0] == ("table1", "table2", "table1.col1 = table2.col2")

            def test_infer_aggregated_relationships():
                from sql_parser.dml_analyzer import infer_aggregated_relationships
                sql = "SELECT COALESCE(table1.col1, table2.col2) FROM table1"
                relationships = infer_aggregated_relationships(sql)
                assert len(relationships) == 0 # Should be zero, since we are only looking at the select statement, not the insert

            def test_parse_create_table_inferred_relationships():
                create_sql = "CREATE TABLE table1 (col1 INT)"
                insert_sql = "INSERT INTO table1 (col1) SELECT table2.col2 FROM table2 JOIN table3 ON table2.id = table3.id"
                table_schema = parse_create_statement(create_sql, insert_sql)
                assert table_schema.name == "table1"
                assert len(table_schema.inferred_relationships) == 1
                assert table_schema.inferred_relationships[0].target_table == "table3"
                assert table_schema.inferred_relationships[0].type == "implicit"
                assert table_schema.inferred_relationships[0].condition == "table2.id = table3.id"
            ```
- [ ] **Step 9.7: Update `sample.sql` with `JOIN` and `COALESCE`**
    - [ ] Update the `sample.sql` file to include `JOIN` conditions and `COALESCE` functions in the `INSERT...SELECT` statement.
    - [ ] **Prompt 58:**
        - [ ] Update the `sample.sql` file to include `JOIN` conditions and `COALESCE` functions in the `INSERT...SELECT` statement.
            ```sql
            CREATE TABLE users (
                id INT PRIMARY KEY,
                name VARCHAR(255),
                full_name VARCHAR(255),
                email VARCHAR(255)
            );

            CREATE TABLE user_emails (
                user_id INT PRIMARY KEY,
                email VARCHAR(255)
            );

            INSERT INTO users (id, full_name, email)
            SELECT raw_users.user_id, raw_users.first_name || ' ' || raw_users.last_name, COALESCE(user_emails.email, raw_users.email)
            FROM raw_users
            LEFT JOIN user_emails ON raw_users.user_id = user_emails.user_id;

            CREATE VIEW view_users AS
            SELECT id, name
            FROM users;
            ```
- [ ] **Step 9.8: Run `main.py` and Verify Output**
    - [ ] Run `main.py` to generate the data dictionary.
    - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary, including the inferred relationships.
    - [ ] **Prompt 59:**
        - [ ] Run `main.py` to generate the data dictionary.
        - [ ] Verify that the `data_dictionary.md` file is created and contains the correct Markdown representation of the data dictionary, including the inferred relationships.
- [ ] **Step 9.9: Run Unit Tests**
    - [ ] Run the unit tests using `pytest` to ensure that the relationship inference is working correctly.
    - [ ] **Prompt 60:**
        - [ ] Run the unit tests using pytest to ensure that the relationship inference is working correctly.

### Step 10: Diagram Styling and Finalization

- [ ] **Step 10.1: Implement Styling Conventions**
    - [ ] Define Mermaid styling conventions (colors/line styles) in `diagram_generator/er_diagram.py`.
    - [ ] Use different line styles for explicit, aggregated, and implicit relationships (explicit = solid, aggregated = dashed, implicit = dotted).
    - [ ] **Prompt 61:**
        - [ ] Define Mermaid styling conventions (colors/line styles) in `diagram_generator/er_diagram.py`.
            ```python
            from sql_parser.ddl_analyzer import TableSchema, InferredRelationshipSchema

            def generate_er_diagram(table_schemas: List[TableSchema]) -> str:
                """
                Generates a Mermaid ER diagram representation from a list of TableSchema objects.
                """
                diagram = "erDiagram\n"
                for table_schema in table_schemas:
                    diagram += f"    {table_schema.name} {{\n"
                    for column in table_schema.columns:
                        diagram += f"        {column.type} {column.name}\n"
                    diagram += "    }\n"

                for table_schema in table_schemas:
                    if table_schema.constraints:
                        for constraint in table_schema.constraints:
                            if constraint.type == "foreign_key":
                                diagram += f"    {table_schema.name} ||--|| {constraint.target_table} : {constraint.columns[0]}\n"

                    if table_schema.inferred_relationships:
                        for rel in table_schema.inferred_relationships:
                            if rel.type == "implicit":
                                diagram += f"    {table_schema.name} ..--.. {rel.target_table} : {rel.condition}\n"
                            elif rel.type == "aggregated":
                                diagram += f"    {table_schema.name} .-- {rel.target_table} : {rel.function}\n"

                return diagram
            ```
- [ ] **Step 10.2: Implement Directional Arrows**
    - [ ] Implement directional arrows showing source-to-destination flow in `diagram_generator/er_diagram.py`.
    - [ ] **Prompt 62:**
        - [ ] Implement directional arrows showing source-to-destination flow in `diagram_generator/er_diagram.py`.
            ```python
            from sql_parser.ddl_analyzer import TableSchema, InferredRelationshipSchema

            def generate_er_diagram(table_schemas: List[TableSchema]) -> str:
                """
                Generates a Mermaid ER diagram representation from a list of TableSchema objects.
                """
                diagram = "erDiagram\n"
                for table_schema in table_schemas:
                    diagram += f"    {table_schema.name} {{\n"
                    for column in table_schema.columns:
                        diagram += f"        {column.type} {column.name}\n"
                    diagram += "    }\n"

                for table_schema in table_schemas:
                    if table_schema.constraints:
                        for constraint in table_schema.constraints:
                            if constraint.type == "foreign_key":
                                diagram += f"    {table_schema.name} ||--o{constraint.target_table} : {constraint.columns[0]}\n"

                    if table_schema.inferred_relationships:
                        for rel in table_schema.inferred_relationships:
                            if rel.type == "implicit":
                                diagram += f"    {table_schema.name} ..o{rel.target_table} : {rel.condition}\n"
                            elif rel.type == "aggregated":
                                diagram += f"    {table_schema.name} .o {rel.target_table} : {rel.function}\n"

                return diagram
            ```
- [ ] **Step 10.3: Update `main.py` to Generate Final ER Diagram**
    - [ ] Update `main.py` to call `generate_er_diagram` and generate the final ER diagram with styling conventions and directional arrows.
    - [ ] **Prompt 63:**
        - [ ] Update `main.py` to call `generate_er_diagram` and generate the final ER diagram with styling conventions and directional arrows.
            ```python
            import logging

            logging.basicConfig(filename="app.log", level=logging.WARNING)

            from sql_parser.ddl_analyzer import parse_create_statement
            from outputs.data_dictionary import generate_data_dictionary
            from diagram_generator.er_diagram import generate_er_diagram

            def main():
                try:
                    with open("sample.sql", "r") as f:
                        sql_content = f.read()
                    # Split the content into CREATE statement and INSERT statement (crude approach)
                    statements = sql_content.split(";")
                    create_sql = statements[0].strip() + ";" # Add back the semicolon
                    insert_sql = statements[1].strip() + ";" if len(statements) > 1 else None # Add back the semicolon

                    table_schema = parse_create_statement(create_sql, insert_sql)
                    markdown = generate_data_dictionary(table_schema)
                    with open("data_dictionary.md", "w") as f:
                        f.write(markdown)

                    er_diagram = generate_er_diagram([table_schema])
                    with open("er_diagram.mmd", "w") as f:
                        f.write(er_diagram)

                except Exception as e:
                    logging.error(f"An error occurred: {e}")

            if __name__ == "__main__":
                main()
            ```
- [ ] **Step 10.4: Create Unit Tests for Diagram Styling**
    - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct styling of the ER diagram.
    - [ ] **Prompt 64:**
        - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct styling of the ER diagram.
            ```python
            import pytest
            import logging
            from sql_parser.ddl_analyzer import parse_create_statement, TableSchema, ColumnSchema, ConstraintSchema, InferredRelationshipSchema
            from diagram_generator.er_diagram import generate_er_diagram

            def test_generate_er_diagram_styling():
                create_sql = "CREATE TABLE orders (order_id INT PRIMARY KEY, customer_id INT, FOREIGN KEY (customer_id) REFERENCES customers(customer_id))"
                insert_sql = "INSERT INTO orders (customer_id) SELECT id from customers JOIN addresses ON customers.address_id = addresses.id"
                table_schema = parse_create_statement(create_sql, insert_sql)
                er_diagram = generate_er_diagram([table_schema])
                assert "orders ||--o customers : customer_id" in er_diagram
                assert "orders ..o addresses : customers.address_id = addresses.id" in er_diagram
            ```
- [ ] **Step 10.5: Run `main.py` and Verify Output**
    - [ ] Run `main.py` to generate the ER diagram.
    - [ ] Verify that the `er_diagram.mmd` file is created and contains the final ER diagram with styling conventions and directional arrows.
    - [ ] **Prompt 65:**
        - [ ] Run `main.py` to generate the ER diagram.
        - [ ] Verify that the `er_diagram.mmd` file is created and contains the final ER diagram with styling conventions and directional arrows.
- [ ] **Step 10.6: Run Unit Tests**
    - [ ] Run the unit tests using `pytest` to ensure that the diagram styling is working correctly.
    - [ ] **Prompt 66:**
        - [ ] Run the unit tests using pytest to ensure that the diagram styling is working correctly.

### Phase 4: Testing, Validation, and Deliverables

- [ ] **Step 11: Validation and Error Handling**
    - [ ] **Step 11.1: Implement Validation Checks**
        - [ ] Implement validation checks for unresolved foreign keys in `sql_parser/ddl_analyzer.py`.
        - [ ] Implement validation checks for comment syntax (e.g., Oracle `COMMENT ON` vs. SQL Server `sp_addextendedproperty`) in `sql_parser/comment_parser.py`.
        - [ ] **Prompt 67:**
            - [ ] Implement validation checks for unresolved foreign keys in `sql_parser/ddl_analyzer.py`.
                ```python
                from sqlglot import parse_one, exp
                from typing import List, Dict, Optional

                def validate_foreign_keys(table_schemas: List[TableSchema]) -> List[str]:
                    """
                    Validates that all foreign keys reference existing tables.
                    Returns a list of error messages for unresolved foreign keys.
                    """
                    errors = []
                    table_names = [schema.name for schema in table_schemas]
                    for schema in table_schemas:
                        if schema.constraints:
                            for constraint in schema.constraints:
                                if constraint.type == "foreign_key":
                                    if constraint.target_table not in table_names:
                                        errors.append(f"Unresolved foreign key: {schema.name}.{constraint.columns[0]} references {constraint.target_table}")
                return errors
                ```
    - [ ] **Step 11.2: Implement Comment Syntax Validation**
        - [ ] Implement validation checks for comment syntax (e.g., Oracle `COMMENT ON` vs. SQL Server `sp_addextendedproperty`) in `sql_parser/comment_parser.py`.
        - [ ] **Prompt 68:**
            - [ ] Implement validation checks for comment syntax (e.g., Oracle `COMMENT ON` vs. SQL Server `sp_addextendedproperty`) in `sql_parser/comment_parser.py`. Since we are only supporting Oracle, check that the comment syntax is valid for Oracle.
                ```python
                from sqlglot import parse_one, exp
                from typing import List, Dict, Optional

                def validate_comment_syntax(sql: str) -> Optional[str]:
                    """
                    Validates that the comment syntax is valid for Oracle.
                    Returns an error message if the syntax is invalid, otherwise returns None.
                    """
                    try:
                        statement = parse_one(sql)
                        if isinstance(statement, exp.Comment):
                            if not isinstance(statement.args['this'], exp.Comment):
                                return None
                        return "Invalid comment syntax"
                    except:
                        return "Invalid comment syntax"
                ```
    - [ ] **Step 11.3: Add Warnings for Unparseable Statements and Undocumented Columns**
        - [ ] Add warnings for unparseable statements and undocumented columns in `sql_parser/ddl_analyzer.py` and `outputs/data_dictionary.py`.
        - [ ] **Prompt 69:**
            - [ ] Add warnings for unparseable statements and undocumented columns in `sql_parser/ddl_analyzer.py` and `outputs/data_dictionary.py`.
                ```python
                # sql_parser/ddl_analyzer.py
                import logging
                from sqlglot import parse_one, exp
                from sql_parser.ddl_analyzer import TableSchema, ColumnSchema, ConstraintSchema, InferredRelationshipSchema
                from sql_parser.comment_parser import parse_comment
                from lineage_tracker.dml_analyzer import track_column_lineage
                from typing import Union

                def parse_create_statement(sql: str, insert_sql: str = None) -> TableSchema:
                    try:
                        statement = parse_one(sql)
                        if isinstance(statement, exp.Create):
                            table_name = statement.args['this'].this
                            columns = []
                            constraints = []
                            for column_def in statement.args['expressions']:
                                column_name = column_def.args['this']
                                column_type = column_def.args['kind'].this
                                columns.append(ColumnSchema(name=column_name, type=column_type))
                                if column_def.args.get('constraints'):
                                    for constraint in column_def.args['constraints']:
                                        if isinstance(constraint, exp.PrimaryKey):
                                            constraints.append(ConstraintSchema(type="primary_key", columns=[column_name]))
                                        elif isinstance(constraint, exp.ForeignKey):
                                            target_table = constraint.args['table'].this
                                            constraints.append(ConstraintSchema(type="foreign_key", columns=[column_name], target_table=target_table))

                    table_comment = None #parse_comment(comment_sql, table_name) if comment_sql else None

                    table_schema = TableSchema(name=table_name, columns=columns, constraints=constraints, comment=table_comment)

                    if insert_sql:
                        try:
                            lineage, implicit_relationships, aggregated_relationships = track_column_lineage(insert_sql)
                            for column in table_schema.columns:
                                if column.name in lineage:
                                    column_lineage = lineage[column.name]
                                    table_schema.columns[table_schema.columns.index(column)].source = {"table": "unknown", "column": column_lineage['source'][0]} #Need to resolve table
                                    if "transformation" in column_lineage:
                                        table_schema.columns[table_schema.columns.index(column)].transformation = column_lineage["transformation"]
                                else:
                                    logging.warning(f"Undocumented column: {table_schema.name}.{column.name}")

                            inferred_relationships = []
                            for rel in implicit_relationships:
                                inferred_relationships.append(InferredRelationshipSchema(target_table=rel[1], type="implicit", condition=rel[2]))

                            for rel in aggregated_relationships:
                                inferred_relationships.append(InferredRelationshipSchema(target_table=rel[1], type="aggregated", function=rel[2]))

                            table_schema.inferred_relationships = inferred_relationships

                        except Exception as e:
                            logging.warning(f"Could not track column lineage: {e}")

                    return table_schema

                elif isinstance(statement, exp.CreateView):
                    table_name = statement.this
                    columns = []
                    # Views don't explicitly define columns, so we'll leave it empty for now
                    return TableSchema(name=table_name, columns=columns)
                else:
                    logging.warning(f"Unsupported statement type: {type(statement)}")
                    return TableSchema(name="unknown", columns=[])
            except Exception as e:
                logging.warning(f"Could not parse CREATE statement: {sql}. Error: {e}")
            # Return an empty TableSchema to allow processing to continue
            return TableSchema(name="unknown", columns=[])
                ```
    - [ ] **Step 11.4: Update `main.py` to Perform Validation Checks**
        - [ ] Update `main.py` to call the validation functions and log any errors or warnings.
        - [ ] **Prompt 70:**
            - [ ] Update `main.py  to Perform Validation Checks**
        - [ ] Update `main.py` to call the validation functions and log any errors or warnings.
        - [ ] **Prompt 70:**
            - [ ] Update `main.py` to call the validation functions and log any errors or warnings.
                ```python
                import logging

                logging.basicConfig(filename="app.log", level=logging.WARNING)

                from sql_parser.ddl_analyzer import parse_create_statement, validate_foreign_keys
                from sql_parser.comment_parser import validate_comment_syntax
                from outputs.data_dictionary import generate_data_dictionary
                from diagram_generator.er_diagram import generate_er_diagram

                def main():
                    try:
                        with open("sample.sql", "r") as f:
                            sql_content = f.read()
                        # Split the content into CREATE statement and INSERT statement (crude approach)
                        statements = sql_content.split(";")
                        create_sql = statements[0].strip() + ";" # Add back the semicolon
                        insert_sql = statements[1].strip() + ";" if len(statements) > 1 else None # Add back the semicolon
                        comment_sql = statements[2].strip() + ";" if len(statements) > 2 else None # Add back the semicolon

                        table_schema = parse_create_statement(create_sql, insert_sql)
                        markdown = generate_data_dictionary(table_schema)
                        with open("data_dictionary.md", "w") as f:
                            f.write(markdown)

                        er_diagram = generate_er_diagram([table_schema])
                        with open("er_diagram.mmd", "w") as f:
                            f.write(er_diagram)

                        # Perform validation checks
                        errors = validate_foreign_keys([table_schema])
                        for error in errors:
                            logging.error(error)

                        if comment_sql:
                            comment_error = validate_comment_syntax(comment_sql)
                            if comment_error:
                                logging.error(comment_error)

                    except Exception as e:
                        logging.error(f"An error occurred: {e}")

                if __name__ == "__main__":
                    main()
                ```
    - [ ] **Step 11.5: Create Unit Tests for Validation and Error Handling**
        - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct validation and error handling.
        - [ ] **Prompt 71:**
            - [ ] Create unit tests in `tests/test_sql_parser.py` to verify the correct validation and error handling.
                ```python
                import pytest
                import logging
                from sql_parser.ddl_analyzer import parse_create_statement, TableSchema, ColumnSchema, ConstraintSchema, InferredRelationshipSchema, validate_foreign_keys
                from sql_parser.comment_parser import validate_comment_syntax
                from diagram_generator.er_diagram import generate_er_diagram

                def test_validate_foreign_keys():
                    create_sql1 = "CREATE TABLE orders (order_id INT PRIMARY KEY, customer_id INT, FOREIGN KEY (customer_id) REFERENCES customers(customer_id))"
                    create_sql2 = "CREATE TABLE products (product_id INT PRIMARY KEY)"
                    table_schema1 = parse_create_statement(create_sql1)
                    table_schema2 = parse_create_statement(create_sql2)
                    errors = validate_foreign_keys([table_schema1, table_schema2])
                    assert len(errors) == 1
                    assert "Unresolved foreign key: orders.customer_id references customers" in errors[0]

                def test_validate_comment_syntax():
                    comment_sql = "COMMENT ON TABLE products IS 'This table stores product information'"
                    comment_error = validate_comment_syntax(comment_sql)
                    assert comment_error is None

                    comment_sql = "COMMENT TABLE products IS 'This table stores product information'"
                    comment_error = validate_comment_syntax(comment_sql)
                    assert comment_error == "Invalid comment syntax"
                ```
    - [ ] **Step 11.6: Update `sample.sql` with Validation Errors**
        - [ ] Update the `sample.sql` file to include validation errors (e.g., unresolved foreign keys, invalid comment syntax).
        - [ ] **Prompt 72:**
            - [ ] Update the `sample.sql` file to include validation errors (e.g., unresolved foreign keys, invalid comment syntax).
                ```sql
                CREATE TABLE users (
                    id INT PRIMARY KEY,
                    name VARCHAR(255),
                    full_name VARCHAR(255),
                    email VARCHAR(255)
                );

                CREATE TABLE user_emails (
                    user_id INT PRIMARY KEY,
                    email VARCHAR(255)
                );

                INSERT INTO users (id, full_name, email)
                SELECT raw_users.user_id, raw_users.first_name || ' ' || raw_users.last_name, COALESCE(user_emails.email, raw_users.email)
                FROM raw_users
                LEFT JOIN user_emails ON raw_users.user_id = user_emails.user_id;

                CREATE VIEW view_users AS
                SELECT id, name
                FROM users;

                COMMENT TABLE users IS 'This table stores user information';
                ```
    - [ ] **Step 11.7: Run `main.py` and Verify Output**
        - [ ] Run `main.py` to generate the data dictionary and ER diagram.
        - [ ] Verify that the validation errors and warnings are logged to `app.log`.
        - [ ] **Prompt 73:**
            - [ ] Run `main.py` to generate the data dictionary and ER diagram.
            - [ ] Verify that the validation errors and warnings are logged to `app.log`.
    - [ ] **Step 11.8: Run Unit Tests**
        - [ ] Run the unit tests using `pytest` to ensure that the validation and error handling are working correctly.
        - [ ] **Prompt 74:**
            - [ ] Run the unit tests using pytest to ensure that the validation and error handling are working correctly.

### Step 12: Integration Tests

- [ ] **Step 12.1: Create Sample SQL Scripts**
    - [ ] Create sample SQL scripts (Oracle/PostgreSQL/MS SQL) with mixed DDL/DML in a new directory `integration_tests/`.
    - [ ] Include `CREATE TABLE`, `CREATE VIEW`, `INSERT...SELECT`, `JOIN`, `COALESCE`, and comments.
    - [ ] **Prompt 75:**
        - [ ] Create sample SQL scripts (Oracle/PostgreSQL/MS SQL) with mixed DDL/DML in a new directory `integration_tests/`.
        - [ ] Include `CREATE TABLE`, `CREATE VIEW`, `INSERT...SELECT`, `JOIN`, `COALESCE`, and comments.
        - [ ] Create three files: `integration_tests/oracle.sql`, `integration_tests/postgres.sql`, and `integration_tests/mssql.sql`.
        - [ ] Each file should contain a mix of DDL and DML statements, including CREATE TABLE, CREATE VIEW, INSERT...SELECT, JOIN, COALESCE, and comments.
- [ ] **Step 12.2: Implement Integration Test Function**
    - [ ] Implement an integration test function in `tests/test_sql_parser.py` that reads the sample SQL scripts, parses them, generates the data dictionary and ER diagram, and validates the accuracy of the output.
    - [ ] **Prompt 76:**
        - [ ] Implement an integration test function in `tests/test_sql_parser.py` that reads the sample SQL scripts, parses them, generates the data dictionary and ER diagram, and validates the accuracy of the output.
            ```python
            import pytest
            import logging
            from sql_parser.ddl_analyzer import parse_create_statement, validate_foreign_keys
            from outputs.data_dictionary import generate_data_dictionary
            from diagram_generator.er_diagram import generate_er_diagram
            import os

            def test_integration():
                test_dir = "integration_tests"
                for filename in os.listdir(test_dir):
                    if filename.endswith(".sql"):
                        filepath = os.path.join(test_dir, filename)
                        with open(filepath, "r") as f:
                            sql_content = f.read()

                        # Split the content into CREATE statement and INSERT statement (crude approach)
                        statements = sql_content.split(";")
                        create_sql = statements[0].strip() + ";" # Add back the semicolon
                        insert_sql = statements[1].strip() + ";" if len(statements) > 1 else None # Add back the semicolon

                        table_schema = parse_create_statement(create_sql, insert_sql)
                        markdown = generate_data_dictionary(table_schema)
                        er_diagram = generate_er_diagram([table_schema])

                        # Add assertions to validate the output
                        assert table_schema.name is not None
                        assert len(table_schema.columns) > 0
                        assert "erDiagram" in er_diagram
            ```
- [ ] **Step 12.3: Run Integration Tests**
    - [ ] Run the integration tests using `pytest` to validate the data dictionary accuracy and diagram relationships.
    - [ ] **Prompt 77:**
        - [ ] Run the integration tests using pytest to validate the data dictionary accuracy and diagram relationships.

### Step 13: CLI and Deliverables

- [ ] **Step 13.1: Implement CLI Entrypoint**
    - [ ] Implement the CLI entrypoint using `argparse` in `main.py`.
    - [ ] The CLI should accept the following arguments:
        - [ ] `--input`: Path to the input SQL scripts directory.
        - [ ] `--output`: Path to the output directory.
        - [ ] `--format`: Output format (e.g., `markdown`, `json`).
    - [ ] **Prompt 78:**
        - [ ] Implement the CLI entrypoint using `argparse` in `main.py`.
            ```python
            import logging
            import argparse
            import os

            logging.basicConfig(filename="app.log", level=logging.WARNING)

            from sql_parser.ddl_analyzer import parse_create_statement, validate_foreign_keys
            from outputs.data_dictionary import generate_data_dictionary
            from diagram_generator.er_diagram import generate_er_diagram

            def main():
                parser = argparse.ArgumentParser(description="Generate data dictionary and ER diagram from SQL scripts.")
                parser.add_argument("--input", required=True, help="Path to the input SQL scripts directory.")
                parser.add_argument("--output", required=True, help="Path to the output directory.")
                parser.add_argument("--format", default="markdown", help="Output format (e.g., markdown, json).")
                args = parser.parse_args()

                for filename in os.listdir(args.input):
                    if filename.endswith(".sql"):
                        filepath = os.path.join(args.input, filename)
                        with open(filepath, "r") as f:
                            sql_content = f.read()

                        # Split the content into CREATE statement and INSERT statement (crude approach)
                        statements = sql_content.split(";")
                        create_sql = statements[0].strip() + ";" # Add back the semicolon
                        insert_sql = statements[1].strip() + ";" if len(statements) > 1 else None # Add back the semicolon

                        table_schema = parse_create_statement(create_sql, insert_sql)
                        markdown = generate_data_dictionary(table_schema)

                        output_path = os.path.join(args.output, filename.replace(".sql", ".md"))
                        with open(output_path, "w") as f:
                            f.write(markdown)

                        er_diagram = generate_er_diagram([table_schema])
                        er_diagram_path = os.path.join(args.output, filename.replace(".sql", ".mmd"))
                        with open(er_diagram_path, "w") as f:
                            f.write(er_diagram)

            if __name__ == "__main__":
                main()
            ```
- [ ] **Step 13.2: Generate Sample Output**
    - [ ] Create a sample output directory and generate sample data dictionary and ER diagram files.
    - [ ] **Prompt 79:**
        - [ ] Create a sample output directory named `output` and generate sample data dictionary and ER diagram files by running `main.py` with the `--input` argument pointing to the `integration_tests` directory and the `--output` argument pointing to the `output` directory.
- [ ] **Step 13.3: Finalize Documentation and Testing**
    - [ ] Finalize the documentation and testing.
    - [ ] **Prompt 80:**
        - [ ] Finalize the documentation and testing.



