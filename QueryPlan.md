# Query Plan in Power Query

## Overview
The query plan feature in Power Query provides a detailed view of your query's evaluation process. It helps identify why a particular query might not fold at a specific step, offering insights into optimizing your data transformations.

## Steps to Use Query Plan

### 1. Review the Query Folding Indicators
Before diving into the query plan, review the query folding indicators to understand which steps are folded and which are not.

### 2. Select the Query Step to Review Its Query Plan
In Power Query Editor, select the step you want to review. The query plan will show detailed information about the evaluation of that step.

### 3. Implement Changes to Your Query
Based on the insights from the query plan, you can make necessary adjustments to improve query folding and overall performance.

## Practical Example
Here's a practical example using the AdventureWorksLT sample database for Azure SQL Server:

```m
let
    Source = Sql.Database("servername", "database"),
    Navigation = Source{[Schema = "Sales", Item = "SalesOrderHeader"]}[Data],
    #"Removed other columns" = Table.SelectColumns(Navigation, {"SalesOrderID", "OrderDate", "SalesOrderNumber", "PurchaseOrderNumber", "AccountNumber", "CustomerID", "TotalDue"}),
    #"Filtered rows" = Table.SelectRows(#"Removed other columns", each [TotalDue] > 1000),
    #"Kept bottom rows" = Table.LastN(#"Filtered rows", 5)
in
    #"Kept bottom rows"
```

This query connects to the `SalesOrderHeader` table, selects specific columns, filters rows where `TotalDue` is greater than 1000, and keeps the last 5 rows.

## Viewing the Query Plan
To view the query plan:
1. Open Power Query Editor.
2. Select the step you want to analyze.
3. Click on the "Query Plan" option to view detailed information.



## Benefits of Using Query Plan
- **Detailed Evaluation**: Provides a comprehensive view of each step's evaluation.
- **Optimization Insights**: Helps identify steps that prevent query folding.
- **Performance Improvement**: Guides you in making changes to enhance query performance.

## Conclusion
The query plan feature is a valuable tool for optimizing your Power Query transformations. By understanding and utilizing this feature, you can ensure your queries are efficient and performant.

---

Feel free to add more details or images as needed! If you have any specific questions or need further assistance, let me know.
