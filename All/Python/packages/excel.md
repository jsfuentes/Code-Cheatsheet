# Excel

Read with pandas

## Throw Pandas DF into Excel File

`pip install XlsxWriter`

```python

# Specify a writer
writer = pd.ExcelWriter('example.xlsx', engine='xlsxwriter')

# Write your DataFrame to a file     
yourData.to_excel(writer, 'Sheet1')

# Save the result 
writer.save()
```

