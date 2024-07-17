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

## specification pattern 

# The specification pattern to the rescue

- Describes a query in an object
- Return an IQueryable<T>
- Generic list method takes specificitation as parameter
- Specification can have meaningful name e.g ProductsWithTypesAndBrandSpecification

### Definindo a interface Specification que todas as especificações devem seguir
public interface ISpecification<T>
{
    bool IsSatisfiedBy(T entity);
}

### Criando uma classe Specification para verificar se um número é par
public class IsEvenSpecification : ISpecification<int>
{
    public bool IsSatisfiedBy(int number)
    {
        return number % 2 == 0;
    }
}

### Exemplo de uso do padrão Specification
public class Program
{
    public static void Main()
    {
        ## Criando uma instância da classe Specification para verificar se um número é par
        var isEvenSpec = new IsEvenSpecification();

        ## Verificando se um número é par utilizando a classe Specification criada
        int numberToCheck = 4;
        if (isEvenSpec.IsSatisfiedBy(numberToCheck))
        {
            Console.WriteLine($"{numberToCheck} é um número par");
        }
        else
        {
            Console.WriteLine($"{numberToCheck} não é um número par");
        }
    }
}

Q: Isn't AutoMapper going to affect perfomance
A: Possibly. Every app is different test!

Q: How do I use theInclude? the spec pattern only allows us to go one level deep
A: Not needed for this app. Plaease see attached PDF how to do this


## API Error Handling 

 - Error handling and exceptions 
 - Develop exception page
 - Validation errors
 - Http response errors
 - Customising the error handling 
 - Middleware
 - Swagger


 ## API Pagination Filtering Sorting Searching

 # Pagination
    - perfomance
    - parameters passed by query string
    - Page size should be limited
    - We should always page results

    - Query commands are stored in a variable
    - Execution of the query is deferred
    - IQueryable<T> creates an expression tree
    - Execution:
        .ToList(), ToArray(), ToDictionary(), Count() or others singleton queries 