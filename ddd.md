# DDD

![47817ADD-A553-4D24-9496-283DBB52E683](https://user-images.githubusercontent.com/2544489/126871807-557941bc-990c-4e23-8648-bbd56c0e63d7.jpeg)

![5AE4DAE6-8883-40D7-AA84-A6FD53663C0A](https://user-images.githubusercontent.com/2544489/126891650-282b4cca-a5a4-4543-958e-4c1da66aa0c3.jpeg)


- https://www.infoq.cn/minibook/domain-driven-design-quickly


## 概念

- 实体：标志符经历各种软件状态后能够保持一致
- 值对象
  - 考虑 immutable
- 服务
  - 不属于实体/值对象的行为，比如从一个账户向另一个账户转账
- 聚合：针对数据变化可以考虑成一个单元的一组相关的对象
- Repository
  - 避免对 Infrasture 的感知泄漏到各层
  - 资源库的实现可能会非常类似于基础设施，但资源库的接口是纯粹的领域模型

## 分层

- User Interface
- Application
- Domain
- Infrasture

## Notes

- 通用语言 - Ubiquitous Language
- 挑战通常不是完整 而是简单和容易理解
- 高内聚 低耦合

## The Clean Architecture

![D3523BEA-5E5C-4E0F-A0A9-F685F3F2D75B](https://user-images.githubusercontent.com/2544489/126890387-529bdbe9-6258-435c-b0a0-d9579e14bd4e.jpeg)

> The overriding rule that makes this architecture work is The Dependency Rule. This rule says that source code dependencies can only point inwards. Nothing in an inner circle can know anything at all about something in an outer circle.

> - Testable. The business rules can be tested without the UI, Database, Web Server, or any other external element.
> - Independent of Database. You can swap out Oracle or SQL Server, for Mongo, BigTable, CouchDB, or something else. Your business rules are not bound to the database.

- https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
- https://khalilstemmler.com/articles/software-design-architecture/domain-driven-design-vs-clean-architecture/
- https://khalilstemmler.com/articles/typescript-domain-driven-design/repository-dto-mapper/
