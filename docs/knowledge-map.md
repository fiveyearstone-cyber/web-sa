# Bản đồ kiến thức

Mục đích: liệt kê **đầy đủ** các chủ đề cần học để không để lại lỗ hổng. AI cập nhật trạng thái sau mỗi buổi học.

**Trạng thái:**
- `[ ]` Chưa học
- `[~]` Đã học tổng quan (biết là gì, dùng để làm gì)
- `[x]` Đã thực hành và nắm vững
- `[!]` Đã học nhưng còn yếu, cần ôn lại
- `[-]` Hoãn lại (ghi lý do)

---

## 0. Bức tranh toàn cảnh
- [~] Hệ sinh thái .NET: .NET, ASP.NET Core, EF Core, C# — vai trò từng mảnh
- [~] HTTP: request/response, method, status code, header, body, statelessness — idempotent còn yếu (xem log)
- [ ] REST & thiết kế API: resource, URI, idempotency, versioning (tổng quan) — *đang học (Bài 2): đã học resource/URI/method; idempotent còn yếu; chưa học status code, hành động không phải CRUD, versioning, phân trang, ProblemDetails*
- [~] Một request đi qua hệ thống backend thế nào (từ client → Kestrel → middleware → endpoint → database → response) — đã nắm mô hình củ hành và short-circuit
- [ ] Tổng quan kiến trúc phần mềm & vì sao cần kiến trúc — *đang học (Bài 2 Phần B): đã giảng, chờ kiểm tra*
- [ ] Phân tích nghiệp vụ e-commerce: các module, actor, use case chính

## 1. Nền tảng .NET
- [ ] .NET là gì: runtime, SDK, BCL; .NET Framework vs .NET (Core) — lịch sử
- [ ] Chính sách phát hành: LTS vs STS, target framework (TFM)
- [ ] Quá trình biên dịch: C# → IL → JIT → mã máy; AOT (tổng quan)
- [ ] CLR: quản lý bộ nhớ, Garbage Collector (generations, LOH)
- [ ] Assembly, namespace
- [ ] Solution (`.sln`/`.slnx`), project (`.csproj`), project reference
- [ ] MSBuild & SDK-style project: properties, items, build/publish
- [ ] NuGet: package, version, dependency graph, restore, lock file
- [ ] `dotnet` CLI: new, build, run, watch, test, publish, add, sln
- [ ] Debug trong VS Code

## 2. C# nâng cao
- [ ] Value type vs reference type, stack vs heap, boxing/unboxing
- [ ] class, struct, record, record struct — khi nào dùng cái nào
- [ ] OOP: encapsulation, inheritance, polymorphism, abstract, interface (default interface members)
- [ ] Access modifiers, `sealed`, `static`, `partial`
- [ ] Properties: auto-property, `init`, `required`, `field` keyword
- [ ] Equality: `==`, `Equals`, `GetHashCode`, value equality của record
- [ ] Immutability
- [ ] Generics: generic class/method, constraints, covariance/contravariance
- [ ] Delegate, `Func`/`Action`/`Predicate`, lambda, closure
- [ ] Event & event pattern
- [ ] Extension methods & extension members (C# 14+)
- [ ] Collections: List, Dictionary, HashSet, Queue, IEnumerable/ICollection/IList, IReadOnly*
- [ ] `yield return` & iterator
- [ ] LINQ: method syntax vs query syntax, deferred execution, các toán tử chính
- [ ] `IEnumerable` vs `IQueryable`, expression trees
- [ ] Nullable reference types & null-handling operators
- [ ] Pattern matching (type, property, relational, list patterns), switch expression
- [ ] Exceptions: throw/catch/finally, custom exception, khi nào KHÔNG dùng exception
- [ ] `IDisposable`, `using`, `IAsyncDisposable`
- [ ] async/await: Task, ValueTask, state machine, SynchronizationContext, deadlock, `ConfigureAwait`
- [ ] CancellationToken
- [ ] Đa luồng & thread-safety: Thread, ThreadPool, race condition, `lock`, `Interlocked`, `SemaphoreSlim`, concurrent collections, `Lazy<T>`
- [ ] Attributes & reflection
- [ ] Span/Memory (tổng quan)
- [ ] String, StringBuilder, interpolation, culture
- [ ] DateTime, DateTimeOffset, DateOnly/TimeOnly, TimeProvider
- [ ] Source generators (tổng quan)
- [ ] Tính năng mới của C# 15

## 3. ASP.NET Core cơ bản
- [ ] Host, `WebApplicationBuilder`, `WebApplication`, `Program.cs`
- [ ] Kestrel & vòng đời request
- [ ] Middleware pipeline: thứ tự, short-circuit, viết middleware tự tạo
- [ ] Routing: route template, constraint, endpoint routing
- [ ] Minimal API vs Controllers — so sánh & lựa chọn
- [ ] Model binding: route, query, body, header, form
- [ ] Validation (built-in validation, DataAnnotations, tự viết, thư viện)
- [ ] Dependency Injection: IoC, DI container, lifetimes (Singleton/Scoped/Transient), captive dependency, tự viết DI container đơn giản
- [ ] Configuration: providers, thứ tự ưu tiên, environment, user secrets
- [ ] Options pattern: IOptions, IOptionsSnapshot, IOptionsMonitor, validation
- [ ] Logging: ILogger, log level, structured logging, provider
- [ ] Error handling: exception handler, `IExceptionHandler`, ProblemDetails
- [ ] JSON serialization với System.Text.Json
- [ ] Filters (endpoint filters, action filters)
- [ ] OpenAPI & tài liệu API
- [ ] HttpContext, request/response
- [ ] CORS
- [ ] Phân trang, lọc, sắp xếp
- [ ] HttpClient & IHttpClientFactory
- [ ] Background service: IHostedService, BackgroundService
- [ ] Health checks
- [ ] Rate limiting

## 4. Data access
- [ ] Thiết kế CSDL quan hệ: khoá chính/ngoại, chuẩn hoá, quan hệ 1-1, 1-n, n-n
- [ ] SQL căn bản & nâng cao trên PostgreSQL: JOIN, GROUP BY, subquery, CTE, window function
- [ ] Index, execution plan (EXPLAIN)
- [ ] Transaction, ACID, isolation level, locking
- [ ] PostgreSQL: cài đặt, psql, kiểu dữ liệu đặc thù (jsonb, uuid, ...)
- [ ] ADO.NET với Npgsql (viết chay): connection, command, parameter, data reader, SQL injection
- [ ] Connection pooling
- [ ] Dapper: micro ORM là gì, mapping
- [ ] ORM là gì, ưu nhược điểm
- [ ] EF Core: DbContext, DbSet, vòng đời DbContext
- [ ] EF Core: convention, data annotations, Fluent API
- [ ] EF Core: relationships, owned types, value conversion
- [ ] EF Core: migrations
- [ ] EF Core: change tracking, entity state, AsNoTracking
- [ ] EF Core: loading related data (eager, explicit, lazy), N+1
- [ ] EF Core: LINQ → SQL translation, client vs server evaluation
- [ ] EF Core: raw SQL, projection
- [ ] EF Core: concurrency (optimistic concurrency, xmin của PostgreSQL)
- [ ] EF Core: transaction, SaveChanges
- [ ] EF Core: interceptors, global query filter (soft delete, multi-tenant)
- [ ] EF Core: performance (split query, compiled query, bulk operations)
- [ ] Repository & Unit of Work: khi nào cần, khi nào thừa với EF Core

## 5. Nguyên lý thiết kế & testing
- [ ] Clean Code: đặt tên, hàm, comment, xử lý lỗi
- [ ] DRY, KISS, YAGNI
- [ ] SOLID (từng nguyên lý + vi phạm thường gặp)
- [ ] Coupling & cohesion
- [ ] Composition over inheritance
- [ ] Design Patterns — Creational: Factory Method, Abstract Factory, Builder, Singleton, Prototype
- [ ] Design Patterns — Structural: Adapter, Decorator, Facade, Proxy, Composite, Bridge, Flyweight
- [ ] Design Patterns — Behavioral: Strategy, Observer, Command, Template Method, Chain of Responsibility, State, Mediator, Iterator, Visitor, Memento
- [ ] Enterprise patterns: Repository, Unit of Work, Specification, Result pattern, Null Object, Options
- [ ] Anti-patterns & code smells
> Testing được học **từ con số 0** (người học chưa viết test bao giờ) và **bắt đầu sớm từ GĐ 2**, không đợi tới GĐ 5. GĐ 5 là phần đào sâu. Xem thêm mục "Kỹ năng xuyên suốt".
- [ ] Vì sao cần test; các loại test (unit, integration, end-to-end); test pyramid và testing trophy
- [ ] Unit test đầu tiên: project test, `dotnet test`, Arrange-Act-Assert, đặt tên test (GĐ 2)
- [ ] Framework test: xUnit / NUnit / MSTest, so sánh và lựa chọn
- [ ] Assertion; thư viện assertion và license (FluentAssertions chuyển sang license thương mại từ v8)
- [ ] Data-driven test (Theory, InlineData, MemberData)
- [ ] Testability: phụ thuộc ẩn, `DateTime.Now` → `TimeProvider`, DI giúp code dễ test thế nào
- [ ] Test doubles: dummy, stub, fake, mock, spy. Viết fake bằng tay trước, sau đó mới dùng thư viện mocking. Khi nào mock là quá đà
- [ ] Integration test: WebApplicationFactory, test database PostgreSQL local, cô lập dữ liệu giữa các test
- [ ] Test với EF Core: vì sao không nên dùng InMemory provider để test
- [ ] TDD; code coverage (ý nghĩa và giới hạn); mutation testing (tổng quan)

## 6. Kiến trúc ứng dụng
- [ ] Layered architecture (N-tier)
- [ ] Dependency Inversion ở mức kiến trúc
- [ ] Clean Architecture / Onion / Hexagonal (Ports & Adapters)
- [ ] Vertical Slice Architecture
- [ ] So sánh các kiến trúc & lựa chọn
- [ ] DDD tactical: Entity, Value Object, Aggregate, Aggregate Root, invariant
- [ ] DDD tactical: Domain Service, Application Service, Repository, Factory
- [ ] DDD tactical: Domain Event
- [ ] Anemic vs Rich domain model
- [ ] CQRS (mức ứng dụng)
- [ ] Mediator pattern: tự viết vs dùng thư viện
- [ ] Pipeline behavior (cross-cutting trong mediator)
- [ ] DTO, mapping (tự viết vs thư viện)

## 7. Cross-cutting concerns
- [~] Cookie & bộ nhớ trình duyệt: Set-Cookie/Cookie, thuộc tính (HttpOnly, Secure, SameSite, Expires, Domain/Path), cookie/localStorage/sessionStorage/IndexedDB, lưu token ở đâu
- [ ] XSS & CSRF: cơ chế tấn công, phòng chống (HttpOnly, SameSite, anti-forgery token)
- [ ] Authentication: cookie, JWT, refresh token
- [ ] ASP.NET Core Identity
- [ ] Authorization: role, claim, policy, resource-based
- [ ] Bảo mật: OWASP API Security Top 10, hash mật khẩu, quản lý secret, HTTPS
- [ ] Caching: in-memory, distributed, HybridCache, output caching, cache invalidation
- [ ] Resilience: retry, timeout, circuit breaker
- [ ] Observability: structured logging, metrics, tracing, OpenTelemetry
- [ ] API versioning
- [~] Idempotency (thanh toán, tạo đơn hàng): idempotency key, khử trùng lặp bằng unique constraint
- [ ] HTTP conditional requests: ETag, If-Match / If-None-Match, 412 Precondition Failed
- [ ] Phân biệt các bài toán: request trùng lặp (idempotency) và nhiều người sửa đồng thời (concurrency control)
- [ ] Upload file
- [ ] Gửi email/thông báo
- [ ] Background jobs & scheduling
- [ ] Internationalization (tổng quan)

## 8. Kiến trúc hệ thống
- [ ] DDD strategic: Ubiquitous Language, Subdomain, Bounded Context, Context Map
- [ ] Modular Monolith
- [ ] Giao tiếp giữa module: đồng bộ vs bất đồng bộ
- [ ] Event-driven architecture, message broker (tổng quan)
- [ ] Outbox / Inbox pattern
- [ ] Saga (choreography vs orchestration)
- [ ] Eventual consistency
- [ ] Microservices: lợi ích, chi phí, khi nào KHÔNG nên dùng
- [ ] API Gateway, service discovery (tổng quan)
- [ ] Distributed data: database per service

## 9. Solution Architect
- [ ] Yêu cầu chức năng vs phi chức năng (quality attributes)
- [ ] C4 model
- [ ] Architecture Decision Records (ADR)
- [ ] Phân tích trade-off
- [ ] Scalability: vertical/horizontal, stateless
- [ ] CAP theorem, consistency models
- [ ] Performance & capacity planning
- [ ] Chi phí & vận hành

## Kỹ năng xuyên suốt (áp dụng ở mọi giai đoạn)
> Thêm ngày 2026-11-16 theo định hướng của người học: tự code được, trọng tâm là luồng code, kiến trúc, design pattern và lý do; biết review và sửa code do AI sinh ra.
- [ ] Đọc và lần theo luồng code: debugger trong VS Code (breakpoint, step into/over, call stack, watch); đọc source code của framework
- [ ] Debugging có phương pháp: tái hiện lỗi → đọc stack trace/log → khoanh vùng → đặt giả thuyết → kiểm chứng → viết test chặn lỗi tái phát
- [ ] Testing xuyên suốt: bắt đầu từ GĐ 2 (logic thuần), mở rộng theo từng giai đoạn (API ở GĐ 3, database ở GĐ 4)
- [ ] Review và sửa code do AI sinh ra: checklist (đúng nghiệp vụ, edge case, concurrency, N+1, DI lifetime, async, bảo mật, license); viết test chứng minh lỗi trước khi sửa
- [ ] Giao việc cho AI: mô tả yêu cầu rõ ràng (spec, acceptance criteria), chia nhỏ việc, kiểm chứng kết quả
- [ ] Lý giải quyết định thiết kế: sau mỗi bài thực hành, giải thích bằng lời "vì sao viết thế này, có phương án nào khác, đánh đổi gì" (dạng mini-ADR)

## Ngoài phạm vi khoá học
- Docker / container (khoá riêng)
- Frontend
