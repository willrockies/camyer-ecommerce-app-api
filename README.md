# camyer-ecommerce-app-api


# api-archicteture 

# topics
- Application archicteture
- the repository pattern
- extending the product entity
- related data
- seeding data
- Migration and startup

# Infrasctructure layer
Responsible for dealing with Data store

- Repository 
- DbContext
- Services


the repository pattern - Goals

- Decouple business code from data access
- Separation of concern 
- minimise duplicate query logic
- Testability

the repository pattern - Consequences

- Increased level of abstraction
- Increased maintability, flexibility, testability
- more classes/interfaces - less duplicate code
- Business logic further away from the data
- Harder to optimise certain operations against the data source


EF Migrations commands

dotnet ef database drop -p Infrastructure -s API

dotnet ef migrations remove -p Infrastructure -s API

dotnet ef migrations add InitialCreate -p Infrastructure -s API -o Data/Migrations

## Api Generic repository

- Help avoid duplicate code
- Type safety
- Mostly use generics rather than create them
