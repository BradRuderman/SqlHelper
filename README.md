SqlHelper
=========

SQL Helper Class for .Net 4.0

-----------------------------------

Description: This class makes it easy to execute stored procedures/plain txt queries and map the result into objects.
It also allows for quick and safe insert/update queries that don't expect a return. 

Requires: .Net 3.5 and Higher

How To Use:

1) Add the class into your project. Build the project to make sure all the assemblies are correctly referenced.
2) Create your table, for example:
    CREATE TABLE [dbo].[users](
      [id] [int] IDENTITY(1,1) NOT NULL,
    	[FirstName] [nvarchar](100) NULL,
    	[LastName][nvarchar](100) NULL,
    	[Age] [int] NULL
    )
3) Define your models for example:
    public class User
    {
        public string First_Name { get; set; }
        public string Last_Name { get; set; }
        public int Age { get; set; }
    }
3) Write your query, make sure to name your result columns = to the property names of the model, in the exact 
   order it is specified in the model:
    var query = "SELECT FirstName as First_Name, LastName as Last_Name, Age FROM users";

4) Execute the query and return the result:
    List<User> result = SqlHelper.ReadQuery<User>(query);


  OR you can also use a predefined stored procedure
    using (SqlCommand cmd = new SqlCommand())
    {
        cmd.CommandType = System.Data.CommandType.StoredProcedure;
        cmd.CommandText = "[dbo].[get_users]";
        result = Helpers.SqlHelper.ReadQuery<User>(cmd);
    }

Another avaliable method is executequery which accepts a SqlCommand and returns true/false if the query executed 
successfully.
-----------------------------------
