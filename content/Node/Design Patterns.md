---
date created: 2024-03-15
date modified: 2024-03-26
tags: DesignPattern
---

# Design Patterns

- https://refactoringguru.cn/design-patterns
- https://empvalley.com/2021/09/11/dive-into-design-patterns/
- http://www.lug.or.kr/files/cheat_sheet/design_pattern_cheatsheet_v1.pdf

- [[FactoryMethod]]
- [[AbstractFactory]]
- [[Builder]]
- [[Prototype]]
- [[Singleton]]

![](../../attachment/Pasted%20image%2020240315153015.png)

## 关系

### 继承

![](../../attachment/Pasted%20image%2020240315145411.png)

### 实现

![](../../attachment/Pasted%20image%2020240315150154.png)

### 抽象

![](../../attachment/Pasted%20image%2020240315151155.png)

### 依赖

![](../../attachment/Pasted%20image%2020240315151637.png)

### 关联

![](../../attachment/Pasted%20image%2020240315151734.png)

### 聚合

![](../../attachment/Pasted%20image%2020240315152843.png)

### 组合

![](../../attachment/Pasted%20image%2020240315152907.png)

### 总结

![](../../attachment/Pasted%20image%2020240315153015.png)

- 依赖： 对类 B 进行修改会影响到类 A 。
- 关联： 对象 A 知道对象 B。 类 A 依赖于类 B。
- 聚合： 对象 A 知道对象 B 且由 B 构成。 类 A 依赖于类 B。
- 组合： 对象 A 知道对象 B、 由 B 构成而且管理着 B 的生命周期。 类 A 依赖于类 B。 
- 实现： 类 A 定义的方法由接口 B 声明 。 对象 A 可被视为对象 B。 类 A 依赖于类 B。
- 继承： 类 A 继承类 B 的接口和实现 ， 但是可以对其进行扩 展。 对象 A 可被视为对象 B。 类 A 依赖于类 B。

六种箭头：

- 继承：三角实线箭头
- 实现：三角虚线箭头
- 关联：普通实线箭头
- 依赖：普通虚线箭头
- 组合：实心菱形箭头
- 聚合：虚心菱形箭头

## Creational patterns

![FactoryMethodUml](FactoryMethodUml.md)

![AbstractFactoryUml](AbstractFactoryUml.md)

![BuilderUml](BuilderUml.md)

![PrototypeUml](PrototypeUml.md)

## Structural patterns

![AdapterUml](AdapterUml.md)

![[BridgeUml]]

![[CompositeUml]]

![[DecoratorUml]]

![[FacadeUml]]

![[FlyweightUml]]

![[ProxyUml]]

## Behavioral patterns

Chain of Responsibility

Command

Iterator

Mediator

Memento

Observer

State

Strategy

Template Method

Visitor
