CLEN Architecture

Application Core
  
  The Application Core holds the business model, which includes entities, services, and interfaces. 
- Entities (business model classes that are persisted
- Aggregates (groups of entities)
- Interfaces
- Domain Services
- Specifications
- Custom Exceptions and Guard Clauses
- Domain Events and Handlers


Infrastructure

- The Infrastructure project typically includes data access implementations
- These implementations include the Entity Framework (EF) DbContext, any EF Core Migration objects that have been defined, and data access implementation classes.
- In addition to data access implementations, the Infrastructure project should contain implementations of services that must interact with infrastructure concerns. 
- These services should implement interfaces defined in the Application Core, and so Infrastructure should have a reference to the Application Core project.

Infrastructure types
- EF Core types (DbContext, Migration)
- Data access implementation types (Repositories)
- Infrastructure-specific services (for example, FileLogger or SmtpNotifier)



UI Layer
-  This project should reference the Application Core project, and its types should interact with infrastructure strictly through interfaces defined in Application Core.
-  No direct instantiation of or static calls to the Infrastructure layer types should be allowed in the UI layer.
UI Layer types
- Controllers
- Custom Filters
- Custom Middleware
- Views
- ViewModels
- Startup
