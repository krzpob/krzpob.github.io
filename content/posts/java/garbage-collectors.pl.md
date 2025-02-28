---
title: Garbage Collectory w Javie
author:
    name: Krzysztof Pobożan
    image: /images/KP-20230630-KPOB7318-Edit.jpg
theme: Toha
menu:
  sidebar:
    name: Garbage Collectory w Javie
    identifier: garbage-collectors-in-java
    weight: 10
    parent: java-site-pl
---

Garbage Collector (GC) to jeden z kluczowych elementów zarządzania pamięcią w języku Java. Dzięki niemu programista nie musi ręcznie zwalniać pamięci zajmowanej przez nieużywane obiekty, co znacząco ułatwia pracę i zmniejsza ryzyko błędów. W tym artykule przyjrzymy się rodzajom Garbage Collectorów dostępnych w Javie oraz ich zastosowaniom.

---
## Czym jest Garbage Collector?
Garbage Collector to mechanizm wbudowany w Java Virtual Machine (JVM), który automatycznie zwalnia pamięć zajmowaną przez obiekty, do których nie ma już referencji. Dzięki temu aplikacja nie wycieka pamięci, a programista może skupić się na logice biznesowej, zamiast ręcznie zarządzać alokacją i dealokacją pamięci.

### Jak działa Garbage Collector?
The GC regularly scans objects in memory and checks which ones are no longer in use. If an object has no active references, it is marked as “junk” and can be removed during one of the next cleaning operations.

---

## Rodzaje Garbage Collectorów w Javie
The JVM offers several Garbage Collector implementations that differ in their approach to memory management and performance.Choosing the right GC depends on the characteristics of the application, the amount of available memory and performance requirements.

1. Serial Garbage Collector
    - Chracteristic:

         Java's simplest GC, suitable for applications running on single-threaded environments.
        Uses a stop-the-world algorithm that stops all threads during memory cleanup.
    - Application:

        Small applications running in a resource-constrained environment.
        Desktop applications with low memory consumption.
    - Activation:
        Can be enabled in the JVM using a flag:

```bash
-XX:+UseSerialGC
```
2. Parallel Garbage Collector (Throughput Collector)

    - Characteristics:

        Parallel version of Serial GC that runs multiple threads to clean memory.
        Prioritizes application throughput - maximizing performance at the expense of longer stop-the-world pauses.
    - Application:

        Server applications that run on multi-core processors.
        Applications that require high performance but tolerate short GC pauses.
    - Activation:

```bash
-XX:+UseParallelGC
```
3. G1 Garbage Collector (Garbage-First GC)

    - Characteristics:

        One of the most versatile GCs that was introduced in Java 7.
        It divides memory into regions and manages them dynamically, minimizing stop-the-world pauses.
        It is suitable for both small and large applications.
    - Application:

        Applications with dynamically changing workloads.
        Systems that require low latency and high responsiveness.
    - Activation:

```bash
-XX:+UseG1GC
```
4. Z Garbage Collector (ZGC)
 - Characteristics:

    Modern GC introduced in Java 11.
    Designed for systems with large amounts of RAM and requiring minimal GC pauses.
    Can run on huge memory heaps (even terabytes!).
 - Application:

    Systems with very low time requirements.
    Cloud-based applications and Big Data systems.
 - Activation:

```bash
-XX:+UseZGC
```
5. Shenandoah Garbage Collector
    - Characteristics:

        GC optimized to minimize stop-the-world pauses.
        Uses an algorithm that cleans memory concurrently with application execution.
    - Application:

        Applications requiring ultra-low latency.
        Games, applications sensitive to interrupts.
    - Activation:

```bash
-XX:+UseShenandoahGC
```
## Który Garbage Collector wybrać?
| Garbage Collector | Advantages | Disadvantages | Usage |.
|------------------|--------|------|--------------|

| Serial GC | Simplicity, low resource consumption | Long stop-the-world pauses | Small applications |
| Parallel GC | Good performance on multi-core processors | Pauses can be long | Server applications.|
| G1 GC | Balanced memory management, short stop-the-world | Larger CPU usage Large systems, applications with variable loads |
| ZGC | Minimal pauses, good scalability | Larger hardware requirements | Cloud systems, Big Data |
| Shenandoah GC | Ultra-low latency | High requirements | Games, real-time applications. |

## Summary
Garbage Collectors in Java allow for efficient memory management and differ in performance and operation. Choosing the right GC should depend on the type of application and available resources.

**If you're just getting started with Java, it's a good idea to learn the basics of GC and experiment with different JVM settings to suit your needs.**