# Fifinya

Dapper extension for .Net projects

## Modules

- [ ] Fifinya.Oracle
- [ ] Fifinya.PostgreSql
- [ ] Fifinya.MySql
- [ ] Fifinya.MsSql

## Usage

```cs
using (var conn = new OracleConnection("{connection string}"))
{
	conn.Open();
	// Create the transaction
	// You could use `var` instead of `SqlTransaction`
	using (OracleTransaction tran = conn.BeginTransaction())
	{
		try
		{
			var sql = "update Widget set Quantity = @quantity where WidgetId = @id";
			var parameters = new { id = widgetId, quantity };
			// pass the transaction along to the Query, Execute, or the related Async methods.
			conn.Execute(sql, parameters, tran);
			// if it was successful, commit the transaction
			tran.Commit();
		}
		catch (Exception ex)
		{
			// Roll the transaction back
			tran.Rollback();
			// Handle the error however you need to.
			throw;
		}
	}
}
```