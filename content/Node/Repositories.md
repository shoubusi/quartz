---
tags:
  - review
  - ABP
  - knowledge
date created: 2023-11-16
date modified: 2023-11-16
sr-due: 2025-12-01
sr-interval: 467
sr-ease: 235
archived: false
---

# Repositories

https://docs.abp.io/en/abp/latest/Repositories

"_Mediates between the domain and data mapping layers using a collection-like interface for accessing domain objects_" (Martin Fowler).

Repositories, in practice, are used to perform database operations for domain objects (see [Entities](https://docs.abp.io/en/abp/latest/Entities)). Generally, a separated repository is used for each **aggregate root** or entity.

to review
- [Entities & Aggregate Roots](Entities%20&%20Aggregate%20Roots.md#^30m218)

## What is repository pattern for data access

The Repository Pattern is a design pattern commonly used in software development to abstract and encapsulate the logic required to access data sources. It acts as a mediator between the data access layer and the business layers of an application. The primary goal of the Repository Pattern is to decouple the application from the specific data access implementation, making the application more flexible, testable, and maintainable.

### Key Components of the Repository Pattern

1. **Repository Interface**: Defines the methods for data access operations, such as CRUD (Create, Read, Update, Delete) operations.
2. **Repository Implementation**: Implements the repository interface and contains the actual data access logic. This could involve interacting with a database, an API, or any other data source.
3. **Domain Model**: Represents the entities or objects that the repository will manage.

### Benefits of the Repository Pattern

- **Abstraction**: The application code interacts with the repository interface rather than the data source directly, providing a clean separation of concerns.
- **Testability**: Repositories can be easily mocked or stubbed for unit testing, allowing you to test business logic without needing a real database.
- **Flexibility**: Changing the underlying data source (e.g., switching from a SQL database to a NoSQL database) is easier because the repository interface remains the same.
- **Maintainability**: Centralizing data access logic in repositories makes the codebase easier to maintain and understand.

### Example in Csharp

Here's a simple example of the Repository Pattern in C#:

```csharp
// Domain Model
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}

// Repository Interface
public interface IProductRepository
{
    IEnumerable<Product> GetAll();
    Product GetById(int id);
    void Add(Product product);
    void Update(Product product);
    void Delete(int id);
}

// Repository Implementation
public class ProductRepository : IProductRepository
{
    private readonly List<Product> _products = new List<Product>();

    public IEnumerable<Product> GetAll()
    {
        return _products;
    }

    public Product GetById(int id)
    {
        return _products.FirstOrDefault(p => p.Id == id);
    }

    public void Add(Product product)
    {
        _products.Add(product);
    }

    public void Update(Product product)
    {
        var existingProduct = GetById(product.Id);
        if (existingProduct != null)
        {
            existingProduct.Name = product.Name;
            existingProduct.Price = product.Price;
        }
    }

    public void Delete(int id)
    {
        var product = GetById(id);
        if (product != null)
        {
            _products.Remove(product);
        }
    }
}

// Usage in a Service or Controller
public class ProductService
{
    private readonly IProductRepository _productRepository;

    public ProductService(IProductRepository productRepository)
    {
        _productRepository = productRepository;
    }

    public void AddProduct(Product product)
    {
        _productRepository.Add(product);
    }

    public IEnumerable<Product> GetAllProducts()
    {
        return _productRepository.GetAll();
    }
}
```

### Conclusion

The Repository Pattern is a powerful tool for managing data access in a clean and maintainable way. By abstracting the data access logic behind an interface, it promotes better separation of concerns, improves testability, and makes the application more adaptable to changes in the data layer.