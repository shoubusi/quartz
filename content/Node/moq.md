---
date created: 2024-11-11
date modified: 2024-11-18
---

# Moq

https://github.com/devlooped/moq

https://github.com/devlooped/moq/wiki/Quickstart

Moq is a mocking library for .NET developed from scratch to take full advantage of .NET Linq expression trees and lambda expressions.

Give examples to explain the basic usage of moq library in .NET

I'll explain the basic usage of Moq, one of the most popular mocking frameworks for .NET, with some practical examples.

### 1. Basic Setup

First, you need to install Moq via NuGet:
```bash
Install-Package Moq
```

### 2. Basic Interface Mocking

Let's start with a simple example. Assume we have this interface:

```csharp
public interface IUserRepository
{
    User GetById(int id);
    bool Save(User user);
}
```

Here's how to create and use a basic mock:

```csharp
[Fact]
public void BasicMockExample()
{
    // Arrange
    var mockRepo = new Mock<IUserRepository>();
    
    // Setup the mock behavior
    mockRepo.Setup(repo => repo.GetById(1))
           .Returns(new User { Id = 1, Name = "John Doe" });
    
    // Get the mock object
    var repository = mockRepo.Object;
    
    // Act
    var user = repository.GetById(1);
    
    // Assert
    Assert.Equal("John Doe", user.Name);
}
```

### 3. Verifying Method Calls

You can verify if methods were called:

```csharp
[Fact]
public void VerifyMethodCalls()
{
    // Arrange
    var mockRepo = new Mock<IUserRepository>();
    var user = new User { Id = 1, Name = "John Doe" };
    
    mockRepo.Setup(repo => repo.Save(It.IsAny<User>()))
           .Returns(true);
    
    var repository = mockRepo.Object;
    
    // Act
    repository.Save(user);
    
    // Assert
    mockRepo.Verify(repo => repo.Save(It.IsAny<User>()), Times.Once);
}
```

### 4. Matching Arguments

Moq provides various ways to match arguments:

```csharp
[Fact]
public void ArgumentMatching()
{
    var mockRepo = new Mock<IUserRepository>();
    
    // Match any integer
    mockRepo.Setup(repo => repo.GetById(It.IsAny<int>()))
           .Returns(new User());
    
    // Match specific value
    mockRepo.Setup(repo => repo.GetById(1))
           .Returns(new User { Id = 1, Name = "John" });
    
    // Match range
    mockRepo.Setup(repo => repo.GetById(It.IsInRange<int>(1, 10, Range.Inclusive)))
           .Returns(new User());
    
    // Match predicate
    mockRepo.Setup(repo => repo.GetById(It.Is<int>(id => id % 2 == 0)))
           .Returns(new User());
}
```

### 5. Throwing Exceptions

You can setup mocks to throw exceptions:

```csharp
[Fact]
public void ThrowingExceptions()
{
    var mockRepo = new Mock<IUserRepository>();
    
    mockRepo.Setup(repo => repo.GetById(-1))
           .Throws<ArgumentException>();
    
    var repository = mockRepo.Object;
    
    Assert.Throws<ArgumentException>(() => repository.GetById(-1));
}
```

### 6. Sequential Returns

You can setup a sequence of return values:

```csharp
[Fact]
public void SequentialReturns()
{
    var mockRepo = new Mock<IUserRepository>();
    
    mockRepo.SetupSequence(repo => repo.GetById(1))
           .Returns(new User { Name = "First Call" })
           .Returns(new User { Name = "Second Call" })
           .Throws<Exception>();
    
    var repository = mockRepo.Object;
    
    var firstCall = repository.GetById(1);
    var secondCall = repository.GetById(1);
    
    Assert.Equal("First Call", firstCall.Name);
    Assert.Equal("Second Call", secondCall.Name);
    Assert.Throws<Exception>(() => repository.GetById(1));
}
```

### 7. Callback

You can execute custom code when a method is called:

```csharp
[Fact]
public void CallbackExample()
{
    var mockRepo = new Mock<IUserRepository>();
    var callCount = 0;
    
    mockRepo.Setup(repo => repo.Save(It.IsAny<User>()))
           .Callback<User>(user => callCount++)
           .Returns(true);
    
    var repository = mockRepo.Object;
    repository.Save(new User());
    
    Assert.Equal(1, callCount);
}
```

These examples cover the most common use cases of Moq. Some key points to remember:

- Use `Mock<T>` to create a mock of interface or class
- Use `Setup()` to define behavior
- Use `Object` property to get the mocked instance
- Use `Verify()` to check if methods were called
- Use `It` class for argument matching
- Use `Times` class to verify number of calls

Moq is very powerful and has many more features, but these examples should help you get started with mocking in your unit tests.