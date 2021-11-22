---
layout: home
---

Various performance improvements, no idea why:

```
private SqlConnection GetOpenConnection(string connectionStringKey)
{
    SqlConnection conn = new(_config.GetConnectionString(connectionStringKey));
    conn.Open();
    conn.Execute("SET ARITHABORT ON;");
    return conn;
}
```