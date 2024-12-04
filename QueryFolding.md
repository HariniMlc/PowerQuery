# Query Folding in Power Query

## Overview
Query folding is a process where the steps of data transformation applied in Power Query are translated into native query language and executed directly in the data source. This optimizes performance by reducing the amount of data transferred and leveraging the processing power of the data source.

## Why Query Folding is Important
- **Performance**: Reduces the amount of data transferred between the data source and Power Query.
- **Efficiency**: Leverages the data source's processing power for transformations.
- **Scalability**: Handles large datasets more effectively.

## How Query Folding Works
When you apply transformations in Power Query, it attempts to push these transformations back to the data source. If successful, the data source executes the transformations, and only the necessary data is returned to Power Query.

## Checking Query Folding
To check if query folding is occurring:
1. Open Power Query Editor.
2. Right-click on a step in the "Applied Steps" pane.
3. Select "View Native Query". If this option is enabled, query folding is happening.



## Common Transformations that Support Query Folding
- Filtering rows
- Removing columns
- Sorting rows
- Grouping data
- Merging queries

## Transformations that May Prevent Query Folding
- Adding custom columns with complex logic
- Using certain M functions that are not supported by the data source
- Performing operations that require all data to be loaded into memory

## Examples of Query Folding
### Full Query Folding
A transformation that can be fully translated into a native query.

```sql
SELECT * FROM Sales WHERE Date > '2023-01-01'
```

### Partial Query Folding
A transformation where only part of the query can be folded.

```sql
SELECT * FROM Sales
```
Followed by a transformation in Power Query that cannot be folded.

### No Query Folding
A transformation that cannot be translated into a native query at all.

```m
let
    Source = Csv.Document(File.Contents("C:\SalesData.csv"))
in
    Source
```

## Query folding indicators
Query folding indicators help you understand the steps that fold or don't fold.

![image](https://github.com/user-attachments/assets/f871d79d-73fb-46b1-8a5a-4d364cb1f7e0)



## Best Practices
- **Minimize steps that prevent folding**: Try to keep transformations simple and supported by the data source.
- **Check query folding regularly**: Use the "View Native Query" option to ensure transformations are being folded.
- **Optimize data sources**: Ensure your data source is capable of handling the transformations efficiently.

## Conclusion
Query folding is a powerful feature in Power Query that can significantly improve the performance and efficiency of your data transformations. By understanding and leveraging query folding, you can create more scalable and efficient data solutions.



