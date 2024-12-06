---
date created: 2024-12-04
date modified: 2024-12-04
---
## Guidelines for Writing DTOs

Let me explain the guidelines for writing DTOs and compare different approaches.

## DTO Guidelines

### 1. Basic Principles

- Keep DTOs simple and flat
- Include only necessary data
- Use meaningful names
- Consider serialization requirements
- Follow consistent naming conventions

### 2. Common Patterns

```csharp
// 1. Basic POCO DTO
public class CustomerDto
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}

// 2. Request/Response Pattern
public class CreateCustomerRequest
{
    public string Name { get; set; }
    public string Email { get; set; }
}

public class CreateCustomerResponse
{
    public int Id { get; set; }
    public string Status { get; set; }
}

// 3. Nested DTOs
public class OrderDto
{
    public int Id { get; set; }
    public CustomerDto Customer { get; set; }
    public List<OrderItemDto> Items { get; set; }
}
```

## Approaches to Creating DTOs

### 1. POCO Approach (Manual)

Pros:
- Full control
- Simple and clear
- No dependencies

Cons:
- Repetitive code
- Manual mapping required

```csharp
public class ProductDto
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

### 2. Using AutoMapper

Pros:
- Reduces boilerplate
- Automatic mapping
- Convention-based

Cons:
- Additional dependency
- Can be "magic" (hidden behavior)

```csharp
// Configuration
public class MappingProfile : Profile
{
    public MappingProfile()
    {
        CreateMap<Product, ProductDto>();
        CreateMap<CreateProductDto, Product>();
    }
}

// Usage
public class ProductService
{
    private readonly IMapper _mapper;

    public ProductDto GetProduct(Product product)
    {
        return _mapper.Map<ProductDto>(product);
    }
}
```

### 3. Using Source Generators (like Mapster)

Pros:
- Compile-time mapping
- Better performance than reflection
- Type-safe

Cons:
- Requires setup
- Build-time dependency

```csharp
// Using Mapster
[GenerateMapper]
public class ProductDto
{
    public int Id { get; set; }
    public string Name { get; set; }
    
    // Custom mapping
    [AdaptIgnore]
    public string CalculatedField { get; set; }
}
```

## Best Practices

### 1. Versioning

```csharp
namespace MyApi.V1.Dtos
{
    public class CustomerDto { }
}

namespace MyApi.V2.Dtos
{
    public class CustomerDto { }
}
```

### 2. Validation

```csharp
public class CreateCustomerDto
{
    [Required]
    [StringLength(100)]
    public string Name { get; set; }

    [Required]
    [EmailAddress]
    public string Email { get; set; }
}
```

### 3. Inheritance (when needed)

```csharp
public abstract class BaseDto
{
    public int Id { get; set; }
    public DateTime CreatedAt { get; set; }
}

public class CustomerDto : BaseDto
{
    public string Name { get; set; }
}
```

## Recommendation

I recommend a hybrid approach:

1. **For Simple Projects**:
   - Use POCO DTOs
   - Manual mapping for simple cases

```csharp
public class SimpleProductDto
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

2. **For Medium/Large Projects**:
   - Use AutoMapper or Mapster
   - Define clear mapping profiles
   - Consider source generators for performance

```csharp
// Using AutoMapper with clear conventions
public class AutoMapperProfile : Profile
{
    public AutoMapperProfile()
    {
        CreateMap<Product, ProductDto>()
            .ForMember(dest => dest.CategoryName, 
                      opt => opt.MapFrom(src => src.Category.Name));
    }
}
```

3. **For Complex Enterprise Projects**:
   - Consider custom mapping solutions
   - Use specialized DTOs for different use cases

```csharp
// Different DTOs for different use cases
public class ProductListDto
{
    public int Id { get; set; }
    public string Name { get; set; }
}

public class ProductDetailsDto : ProductListDto
{
    public string Description { get; set; }
    public decimal Price { get; set; }
    public List<ReviewDto> Reviews { get; set; }
}
```

## Final Tips

1. Keep DTOs in a separate project/namespace
2. Use consistent naming (e.g., suffix with Dto)
3. Document DTOs when they're part of a public API
4. Consider using records for immutable DTOs in C# 9+
5. Include only the data needed for the specific use case

The choice between POCO and library-assisted approaches should be based on:
- Project size and complexity
- Performance requirements
- Team experience
- Maintenance considerations
