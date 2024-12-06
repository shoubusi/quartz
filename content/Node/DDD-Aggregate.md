---
date created: 2023-10-13
date modified: 2023-11-19
tags:
  - review
  - ABP
  - knowledge
archived: true
sr-due: 2024-10-01
sr-interval: 33
sr-ease: 290
---
DDD-Aggregate

https://martinfowler.com/bliki/DDD_Aggregate.html

Aggregate is a pattern in Domain-Driven Design. A DDD aggregate is a ==cluster== of domain objects that can be treated as a single unit. An example may be an order and its line-items, these will be separate objects, but it's useful to treat the order (together with its line items) as a single aggregate.

An aggregate will have one of its component objects be the ==aggregate root==. Any ==references from outside== the aggregate should ==only go to the aggregate root==. The root can thus ensure the integrity of the aggregate as a whole.

Aggregates are the basic element of transfer of data storage - you request to ==load or save whole aggregates==. Transactions should not cross aggregate boundaries.

DDD Aggregates are sometimes confused with collection classes (lists, maps, etc). DDD aggregates are domain concepts (order, clinic visit, playlist), while collections are generic. An aggregate will often contain mutliple collections, together with simple fields. 

The term "aggregate" is a common one, and is used in various different contexts (e.g. UML), in which case it does not refer to the same concept as a DDD aggregate.

Aggregate

Aggregate root

 
