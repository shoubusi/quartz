---
date created: 2024-10-15
date modified: 2024-10-15
---
# Relationships Between Entities

One-to-Many (Non-Aggregated)[^3]

One-to-Many (Aggregated)[^4]

Many-to-Many

One-to-One

One-to-Many Behavior on Delete[^5]

This line configures the delete behavior for one-to-many relationships in your Entity Framework Core model. Let's break it down:

```csharp
modelBuilder.SetOneToManyAssociationDeleteBehavior(DeleteBehavior.SetNull, DeleteBehavior.Cascade);
```

1. `SetOneToManyAssociationDeleteBehavior` is a custom extension method provided by DevExpress for XAF applications. It's not a standard Entity Framework Core method.

2. It takes two parameters, both of type `DeleteBehavior`:
   - The first parameter (`DeleteBehavior.SetNull`) is for non-aggregated relationships.
   - The second parameter (`DeleteBehavior.Cascade`) is for aggregated relationships.

3. `DeleteBehavior.SetNull`: For non-aggregated one-to-many relationships, when the principal entity (the "one" side) is deleted, the foreign key in the dependent entities (the "many" side) will be set to null. This prevents the dependent entities from being deleted along with the principal entity.

4. `DeleteBehavior.Cascade`: For aggregated one-to-many relationships, when the principal entity is deleted, all its dependent entities will also be deleted. This is useful for scenarios where the dependent entities shouldn't exist without their principal entity.

This configuration helps to maintain data integrity and defines how the database should handle deletions in related tables. It's particularly useful in XAF applications to ensure that deleting objects behaves consistently with the business logic and data model design.

For example:
- If you delete a Department (non-aggregated), the Employees in that department will have their Department reference set to null rather than being deleted.
- If you delete an Employee (aggregated relationship with Notes), all associated Notes for that Employee will be deleted as well.

This approach provides a balance between maintaining data integrity and avoiding unintended cascading deletions.

Cascade Deletion for Aggregated Entities[^6]

[^3]: https://docs.devexpress.com/eXpressAppFramework/402958/business-model-design-orm/business-model-design-with-entity-framework-core/relationships-between-entities-in-code-and-ui#one-to-many-non-aggregated
[^4]: https://docs.devexpress.com/eXpressAppFramework/402958/business-model-design-orm/business-model-design-with-entity-framework-core/relationships-between-entities-in-code-and-ui#one-to-many-aggregated
[^5]: https://docs.devexpress.com/eXpressAppFramework/402958/business-model-design-orm/business-model-design-with-entity-framework-core/relationships-between-entities-in-code-and-ui#one-to-many-behavior-on-delete
[^6]: https://docs.devexpress.com/eXpressAppFramework/402958/business-model-design-orm/business-model-design-with-entity-framework-core/relationships-between-entities-in-code-and-ui#cascade-deletion-for-aggregated-entities