# How to connect to SQL Server?
Step 1:

Get the connection string.

Step 2:

Instantiate `System.Data.SqlClient.SqlConnection` instance with the connection string.

Step 3: 

Check the connection success.

Step 4:

If it is success,

then perform some operations (such as access data from database) with the connection.

Step 5:

Close the connection (if it is not closed).

## examples
### example 1

```
using ConnectionDatabaseProject1.Test;
using ConnectionDatabaseProject1.Utilities.enums;
using System;
using System.Data;
using System.Data.SqlClient;
using System.Text;
using System.Text.RegularExpressions;

namespace ConnectionDatabaseProject1
{
    class Program
    {
        static void Main(string[] args)
        {

          		// an instance that stores query result from Table or Views in SQL Server.
    			DataTable data_dt = new DataTable();

    			#region create an connection and fetch data from database.

    			// your connection string
    			String connectionString = "Data Source=<IpAddress>;Initial Catalog=<DatabaseName>;Persist Security Info=True;User ID=<UserId>;Password=<Password>";

			using (SqlConnection conn = new SqlConnection(connectionString))
			{
				try
				{
					#region fetch data from database.

						// check the connection is opened.
						if (conn.State != ConnectionState.Open)
						{
							conn.Open();
						}
	
						SqlCommand sqlCmd = new SqlCommand();
						SqlDataAdapter sda = new SqlDataAdapter();
	
						// your sql command string.
	          				string sql_tmp = "SELECT　* FROM Table1";
						
						sqlCmd.CommandText = sql_tmp;
	
	          				// assign the Connection of sql command instance.
						sqlCmd.Connection = conn;
	
	          				// determine what query result of command (a `SqlCommand` instance) will be stored at. 
						sda.SelectCommand = sqlCmd;
	
	          				// fill the query result from sda into `data_dt` (a DataTable instance).
						sda.Fill(data_dt);

					#endregion

  					#region read data from query result.

						for (int a = 0; a < data_dt.Rows.Count; a++)
	  					{
	  
	  					}

  					#endregion

					// 清除資料物件
					sqlCmd.Parameters.Clear();

					// 執行完畢,關閉連線
					conn.Close();

					Console.ReadLine();

				}
				catch (Exception ex)
				{
					// check the connection is closed.
					if (conn.State != ConnectionState.Closed)
					{
						conn.Close();
					}
					throw ex;
				}

			}

			#endregion
		}
	}
}
```
