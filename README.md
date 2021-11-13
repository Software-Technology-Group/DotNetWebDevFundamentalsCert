# Introduction 

In this certificaton you will be creating a full stack .NET solution that includes both front end, middle tier and back end components.  You will be integrating unit testing into your solution as well as some integration testing.  All technologies used in this solution will be based on Microsoft technologies and there will be plenty of descriptions throughout on how to put things together.

# Certification Rules
In order to make sure that we are able to verify your .NET skill throughout the certificaton, you will need to make sure you follow these steps:

1.  Fork this repository into your own repository that you will do all of your work from.
2.  Create a new branch for each section.
3.  Make sure that you commit and push your work to your branch each day you work on it.
4.  Once you are done with a section of the certification, you will need to create a pull request to merge your code into the main branch.  You will need to assign the PR to your certification proctor so they can look at it and make sure you are ready to move onto the next section.  Make sure you do not delete the branch from your repository.  This will allow the proctor to go back and see the work you have done for each section.
5.  Make sure you include copious comments in your code.  As you build the different pieces of the solution, it will be important that your proctor will be able to see what you have done and why you did it that way.

There are many resources online to help you get through the requirements of this certification.  Check here for a non exhaustive list.  As you go through, if you find some resources that are particularly helpful, feel free to let us know and we will include it in this list.

# Section 1 - Getting Started

## Objectives
- Make sure you can use git
- Get a brand new project up and running
  
## Get the necessary files

1.  Fork this repository
2.  Clone your forked repository to your local machine
   
## Setup your Database

This certification uses the DotNetCertification SQL Server Database.  You will need to install that database somewhere.  If you have an instance of SQL server available, you can restore it there.  If not, you can install the Developer edition of SQL Server for free.  If you don't want to install anything on your machine, you can get the docker version of SQL Server for free also.  If you want to use your own, simply restore the DotNetCertification.bak file into your server.  The Docker container already contains both an install of SQL Server and the database already setup.

### Option 1 - Use your own install of SQL Server

- Restore the DotNetCertification.bacpac into your own SQL Server

### Option 2 - Use the docker container

1.  Make sure you have Docker Desktop installed on your machine
2.  Get the prebuilt image from `tfillerup/dotnetcertsqldb:latest`
3.  Run the container `docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=@ReallyStr0ngP@ssw0rd" -p 1433:1433 --name dotnetcertsql -h dotnetcertsql -d tfillerup/dotnetcertsqldb`

# Section 2 - Build out your solution
## Objectives
- Scaffold an existing SQL Database and ready get it ready to use through EF Core

## 1. Create a new branch called Section_2_Solution

## Create your web project

1.  Create a Blazor WebAssembly App called DotNetCert.Web.  Use .NET 6 with no authentication and HTTPS turned on
       - We will set up authentication later using an Azure AD Tenant

## Scaffold the database
1.  Add a new class library project to your solution called DotNetCert.Data
2.  Scaffold the database into the DotNetCert.Data project
       - You can find more information on this at https://docs.microsoft.com/en-us/ef/core/managing-schemas/scaffolding?tabs=vs

## Create Other necessary projects

1.  You will need the following project types for this solution
    1.  ASP.Net Core Web Api
    3.  Common Class Library
    4.  Services Class Library
    5.  Test Project for each actual project

## At this point, you should have 10 projects in your solution.  5 normal projects and 5 test projects.
## Create a pull request for this branch and merge it into main once it has been reviewed.  Make sure to keep this branch in the repo.

# Section 3 - Build API for retreiving data

## Objectives
- Setup at least one custom route for an API endpoint
- Learn how to use Dependency Injection using the built in .NET Core IOC Container
- Make sure to put connection strings in env variables
- Setup logging using Serilog
- Create multiple versions of an API using Versioning
- Implement OpenAPI
  
## 1. Create a new branch called Section_3_WebApi
## 2. Add OpenApi to the app using .NET middleware if is isn't already there
## 3. Add logging using Serilog using .NET middleware

## 4. Build Customer functionality

- Create a Customer service with interface and create Get, Add, Update and Delete methods
  - Setup DI in the WebApi for the Customer service

## 5. Build Order functionality
- Create an Order service with interface and create Get, Add, Update and Delete methods
  - Setup DI in the WebApi for the Order service
- Add a new data model for OrderItem and Product and do a migration and apply the migration.  Make sure you setup the relationships between Order, OrderItem and Product.
  - Use the Fluent API to set primary key and maximum string length on fields.
## 6. Build Invoice functionality
- Create an Invoice service with interface and create Get method
  - Setup DI in the WebApi for the Invoice service

## 7. Add a couple more data models
- Add anouther data model for Employee and CustomerContact.  CustomerContact is a table that contains a link to an employee and a customer and has a free form data entry field for notes and a date field.  Create and apply this migration
  - Use data annotations to set the primary key and max string length on fields

## 8. Wire up the API to the Services
- Create a controller for each service and build an endpoint for each method in each service.

## At this point, your database should look similar to the diagram provided in DatabaseDiagram.png.  Make a diagram of your database in SSMS, take a screenshot of it and put it in your data project and commit it to the repo.

# Section 4 - Build UI

## Objectives
- Use field validation in the UI
- Learn about Blazor Components
  - You can use third party components such as Radzen or Syncfusion where it makes sense
- Use the code behind method on at least one of the pages and the inline method on at least one of the pages

## Create a new branch called Section_4_UI

### Build customer pages to provide the following functionality
- Search for Customer(s) and display results in a list
- Display Customer Details
- Edit details and save back to database
- Add new Customer

### Build Order Functionality
- Search for orders and display results in a list
- Edit Order and save back to database
- Add new Order 
- Cancel an Order

### Build Invoice Functionality
- Display invoice for a specific order

# Section 5 - Add Authentication

## Objectives
- Learn how to use Azure AD Authentication in a web app
- Learn how to limit access to different pieces of an app

## Create a new branch called Section_5_Authentication

### Create Azure AD Tenant (AD tenants are free in Azure but you can get reimbursed up to $35/month for the pay as you go features)
### Wire up app and api to Ad Tenant
### Limit editing/adding to authorized users only

# Section 6 - Unit Tests for web project and API project

## Objectives
- Setup Unit Testing
  
## Create a new branch called Section_6_Unit_Testing
 - Put in unit tests to provide for 60%+ coverage on your code
  - There are several ways to check code coverage.  Find one that you like and use that to calcuate the code coverage percentage.
  - One option would be to download the evauluation version of Visual Studio Enterprise and use the built in tools with that.

# Resources
Setup AD Identity - https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-blazor-server

Setup your api for identity - https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-protected-web-api-overview

Directory Creation Experience - https://portal.azure.com/#create/Microsoft.AzureActiveDirectory

Add OpenAPI to your project - https://docs.microsoft.com/en-us/aspnet/core/tutorials/web-api-help-pages-using-swagger?view=aspnetcore-6.0

