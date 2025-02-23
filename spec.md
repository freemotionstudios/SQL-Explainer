
**Project Specification: SQL Script Documentation & ER Diagram Generator**  
**Objective**: Create a Python tool to parse complex ETL SQL scripts (Oracle/PostgreSQL/MS SQL) and generate a data dictionary + Mermaid ER diagrams for documentation.
* * *

### **1. Core Requirements**

- **Input**: SQL scripts with `CREATE TABLE`, `CREATE VIEW`, `INSERT...SELECT`, and complex `JOIN`/subquery logic.
- **Output**: 
    - **Data Dictionary**: Column-level lineage, descriptions, data types, source tables, transformations.
    - **Mermaid ER Diagrams**: Table relationships (prioritized: explicit > aggregated > implicit).
* * *

### **2. Key Features**

#### **Parsing & Analysis**

- **SQL Dialects**: Oracle, PostgreSQL, Microsoft SQL Server.
- **Statements Processed**: 
    - `CREATE TABLE`/`VIEW` (extract columns, constraints, comments).
    - `INSERT...SELECT`/`SELECT` (trace column lineage, aggregations, `JOIN`/`WHERE` logic).
- **Column Lineage**: 
    - Resolve aliases/subqueries to original source columns.
    - Document calculated columns (e.g., `total = [col_a, col_b]`).
- **Relationships**: 
    - **Explicit**: `FOREIGN KEY` constraints.
    - **Aggregated**: Columns derived from functions (e.g., `COALESCE`, `CASE`).
    - **Implicit**: Inferred from `JOIN` conditions.

#### **Documentation**

- **Data Dictionary**: 
    - Column name, data type, source table/column, transformation logic (hybrid format).
    - Flag undocumented columns with `⚠️ Missing Description`.
- **Mermaid Diagrams**: 
    - Tables as nodes, relationships as edges (explicit = solid, aggregated = dashed, implicit = dotted).
    - Directional arrows showing source-to-destination flow.

#### **Error Handling**

- **Warnings**: Log unparseable statements (continue processing).
- **Validation**: 
    - Check for unresolved foreign keys.
    - Validate comment syntax (e.g., Oracle `COMMENT ON` vs. SQL Server `sp_addextendedproperty`).
* * *

### **3. Architecture**
    
    
    ├── sql_parser/           # SQL dialect-aware parsing
    │   ├── ddl_analyzer.py   # Extract tables/columns from CREATE statements
    │   ├── dml_analyzer.py   # Trace SELECT/JOIN lineage
    │   └── comment_parser.py # Extract column/table descriptions
    ├── lineage_tracker/      # Column-to-source mapping
    │   ├── alias_resolver.py # Resolve subquery/CTE aliases
    │   └── transformation.py # Document COALESCE/CASE/arithmetic logic
    ├── diagram_generator/    # Mermaid ER diagram builder
    ├── outputs/  
    │   ├── data_dictionary.md # Markdown/JSON documentation  
    │   └── er_diagram.mmd    # Mermaid diagram  
    ├── tests/           # Pytest Function Unit Tests
    └── main.py               # CLI entrypoint
    

* * *

### **4. Data Handling**

- **Intermediate Representation**: 
    
        TableSchema = {
        "name": "orders",
        "columns": [
            {
                "name": "order_id",
                "type": "INT",
                "source": {"table": "raw_orders", "column": "id"},
                "transformation": None,
                "description": "Primary key for orders"
            }
        ],
        "relationships": [
            {"type": "explicit", "target_table": "customers", "via": "customer_id"}
        ]
    }
    

* * *

### **5. Dependencies**

- **SQL Parsing**: [`sqlglot`](https://github.com/tobymao/sqlglot) (multi-dialect support).
- **Output**: `markdown` (for data dictionary), `mermaid` (CLI or inline).
- **Logging**: `logging` module for warnings/errors.
- **Unit Tests**: `pytest` functional unit tests.
* * *

### **6. Testing Plan**

1. **Unit Tests**: 
    - Verify alias resolution in nested subqueries.
    - Check detection of implicit relationships in `JOIN` clauses.
2. **Integration Tests**: 
    - Sample SQL scripts (Oracle/PostgreSQL/MS SQL) with mixed DDL/DML.
    - Validate data dictionary accuracy and diagram relationships.
3. **Edge Cases**: 
    - Columns with identical aliases across subqueries.
    - Undocumented columns in source scripts.
4. **Performance**: 
    - Benchmark parsing time for 10k+ line scripts.
* * *

### **7. Deliverables**

- CLI command: 
    
        python main.py \
      --input ./sql_scripts/ \
      --output ./docs/ \
      --format markdown
    

- Sample output:  
[Mermaid Diagram](https://mermaid.ink/img/eyJjb2RlIjoiZXJEaWFncmFtXG4gIENVU1RPTUVSIHx8LS1veyBPUkRFUiA6IFwiT25lLXRvLU1hbnlcIlxuICBPRkZFUiAgfHwtLW97IE9SREVSIDogXCJBZ2dyZWdhdGVkIHZpYSBDT0FMRVNDRSgvLiopXCJcbiAgUFJPRFVDVCAgfHwtLW97IE9SREVSIDogXCJKb2luIG9uIGlkID0gcHJvZHVjdF9pZFwiIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)

* * *

**Next Steps**:

1. Finalize SQL dialect-specific comment parsing rules.
2. Define Mermaid styling conventions (colors/line styles).
3. Implement recursive subquery traversal for alias resolution.

Let me know if you need adjustments to this spec!