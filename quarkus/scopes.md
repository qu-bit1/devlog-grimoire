## Scopes in CDI
CDI gives different scopes for different lifecycles:
- `@ApplicationScoped` → one instance for entire app (singleton)
- `@RequestScoped` → one per HTTP request (good for REST endpoints)
- `@SessionScoped` → one per user session (rare in APIs)
- `@Dependent` → default, not a singleton; new instance every time it’s injected
- `@Singleton` → similar to `@ApplicationScoped`, but plain Jakarta EE singleton (less integration)

In Quarkus, prefer `@ApplicationScoped` over `@Singleton` because:
- It plays better with dependency injection
- Lifecycle events (e.g. `@PostConstruct`, `@PreDestroy`) work better

refer to an example in [[cdi]]

---
