---
customer:
user:
tags:
  - Issue
type: Issue
subject:
archived: false
date created: 2024-08-06
date modified: 2024-08-06
---

# XML Serialization

XML serialization allows you to convert objects into their XML representations and vice versa. This is useful for storing data persistently, transmitting it over a network, or integrating with systems that expect XML input. 

Here are some examples demonstrating how to perform XML serialization in C#:

**1. Serializing an Object:**
Let's say we have a `Person` class:

```csharp
[Serializable] // Mark the class as serializable
public class Person {
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int Age { get; set; }

} 
```

We can serialize an instance of this class into XML like so:

```csharp
Person person = new Person() { FirstName = "John", LastName = "Doe", Age = 30 };

XmlSerializer serializer = new XmlSerializer(typeof(Person)); // Create a serializer for the 'Person' type

using (StreamWriter writer = new StreamWriter("person.xml")) {
    serializer.Serialize(writer, person); // Serialize the object to the XML file
}
```

This code will create an XML file named "person.xml" containing:

```xml
<Person>
  <FirstName>John</FirstName>
  <LastName>Doe</LastName>
  <Age>30</Age>
</Person> 
```

**2. Deserializing from XML:**

To deserialize the `Person` object back from the XML file, use:

```csharp

XmlSerializer serializer = new XmlSerializer(typeof(Person));

using (StreamReader reader = new StreamReader("person.xml")) {
    Person deserializedPerson = (Person)serializer.Deserialize(reader); 
}

Console.WriteLine($"Name: {deserializedPerson.FirstName} {deserializedPerson.LastName}, Age: {deserializedPerson.Age}"); 
```

This code will read the XML file "person.xml", deserialize it back into a `Person` object, and then print the deserialized person's information to the console.

**Important Notes:**

* The `[Serializable]` attribute is required on classes you want to serialize.
* Use the `XmlSerializer` class for basic serialization of objects with public fields or properties. For more complex scenarios, consider using attributes like `[XmlElement]`, `[XmlAttribute]`, and others provided by the .NET Framework for finer control over XML generation.
* Remember to handle potential exceptions during serialization/deserialization (e.g., file not found).
