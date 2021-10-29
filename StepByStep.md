# SQL Server Option 1
1.  Start SQL Server Management Studio
2.  Connect to your server
3.  Open the server node and right click on 'Databases'
4.  Select 'Restore Database'
5.  Select 'Device' and then click on the 3 dot button.
6.  Click 'Add' and then find the .bak file for the WideWorldImporters database
7.  Click 'OK', make sure everything looks good and then click 'OK' again

# Database Option 2

1.  Make sure you have Docker Desktop installed
2.  Download the container.  `docker pull tfillerup/stgdotnetcertification:latest`
3.  `docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=$TGNETDevCert1' -p 1433:1433 -d tfillerup/stgdotnetcertification:latest`
4.  Connect to the database using SSMS

# Create Solution

1.  Create a new project of type 'Blazor Server App'. Call it DotNetCert.Web.  Call the Solution DotNetCert.  Make sure to put it into the same folder that you cloned the repo to.
2.  Set your Target Framework to .NET 5.0 and the authentication type to 'None'.  We will add authentication in a later step of the certification.  Make sure that 'Configure for HTTPS' is checked.

# Database Scaffold

2.  Go to https://docs.microsoft.com/en-us/ef/core/managing-schemas/scaffolding?tabs=vs to learn how to scaffold the database into code first classes.
    1.  Open up a powershell window and navigate to your solution folder
    2.  Install the entity framework CLI tools `dotnet tool install --global dotnet-ef`
    3.  Install the nuget package Microsoft.EntityFrameworkCore.Design
    4.  Install the nuget package Microsoft.EntityFrameworkCore.SqlServer
    5.  Scaffold the database into code first classes `dotnet ef dbcontext scaffold "Data Source={ServerName};Initial Catalog=WideWorld Importers;User ID={UserName};Password={Password};Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False" Microsoft.EntityFrameworkCore.SqlServer --context ApplicationDbContext --context-dir Context --output-dir Models --force`
3.  Add an environment variable in your web project called Database_Connection to store the connection string for the database
4.  Remove the connection string from the OnConfiguring method of the context.
5.  Add the Entity Framework middleware into the DotNetCert.Web app

# Unit Testing
1. Tools that can be used to calculate code coverage
    - Azure Devops Pipelines using results from coverlet
    - Fine Code Coverage VS extension (Amonng other VS extensions)
    - Visual Studio Enterprise (Kindof expensive if you don't have it)