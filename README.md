# spring-crud-benchmark

**A benchmarking suite for evaluating the performance of different Spring-based CRUD service implementations.**  
This project analyzes how various architectural and concurrency models impact throughput, latency, and resource efficiency in web applications that interact with a relational database.

## Benchmark Scope

The project covers the following implementations:

1. **Spring MVC + JDBC**  
   Classic blocking I/O model using the Servlet stack and JDBC. Each request is handled on a dedicated thread; database access is synchronous.

2. **Spring MVC + JDBC + Project Loom**  
   Same as the classic model, but with virtual threads (Project Loom) to reduce thread overhead and improve scalability.

3. **Spring WebFlux + JDBC (Reactive)**  
   Reactive web layer using Spring WebFlux. Blocking JDBC operations are offloaded to worker threads to prevent blocking the event loop.

4. **Spring WebFlux + JDBC + Loom**  
   Hybrid model that combines a reactive web layer with virtual threads for executing JDBC calls. Frees the event loop while avoiding custom thread pools.

5. **Spring WebFlux + JDBC + Kotlin Coroutines**  
   Uses Kotlin coroutines to write asynchronous JDBC logic in a sequential style via suspend functions, integrated into Spring WebFlux.

6. **Spring WebFlux + R2DBC (Fully Reactive)**  
   Fully reactive stack using R2DBC for PostgreSQL. All I/O operations are non-blocking and managed by the reactive runtime.

7. **Spring WebFlux + R2DBC + Kotlin Coroutines**  
   Combines Kotlin coroutines with R2DBC to express asynchronous logic in an imperative style on top of a reactive database driver.

## Project Goals

- Compare performance of blocking and non-blocking CRUD implementations
- Evaluate the practical benefits of Project Loom and Kotlin coroutines
- Identify scalability trade-offs across different concurrency models
- Provide reproducible benchmarks for informed decision-making
