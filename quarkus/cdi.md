https://quarkus.io/guides/cdi

 ## Contexts and Dependency Injection
manages the lifecycle and dependencies of classes, without manually instantiating or wiring them
##  What CDI Does Here

```java
@ApplicationScoped
public class BookService {
```

### `@ApplicationScoped`
- **This makes `BookService` a CDI-managed [[bean]].**
- It tells Quarkus to create **one instance** of `BookService` for the entire application (singleton scope).
- Quarkus manages it v. superbly— no need to call `new BookService()` manually anywhere.

If another class like a resource/controller (e.g. `BookResource`) needs this service, Quarkus will inject it:

```java
@Inject
BookService bookService;
```

Look other [[scopes]]

---


## Why Use CDI

### 1. **Thread-Safe Singleton with Managed Lifecycle**

```java
private final Map<Long, Book> books = new ConcurrentHashMap<>();
```
and
```java
private final AtomicLong idGenerator = new AtomicLong(1);
```
This is a thread-safe, memory-resident store that’s **safe to share globally**. CDI guarantees that only **one instance** exists when `@ApplicationScoped` is used.
### 2. **No Manual Construction or Global Static Mess**
In old Java code, you’d use:
```java
BookService service = new BookService();
```
Or make everything static (bad design). With CDI:
```java
@Inject
BookService service;
```
Quarkus does it cleanly and testably.
### 3. **Easy Testing**
You can write unit tests using `@InjectMock` or just inject mocks/stubs without worrying about wiring dependencies manually.
