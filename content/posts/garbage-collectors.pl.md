---
title: Garbage Collectory w Javie
author:
    name: Krzysztof Pobożan
    image: /images/KP-20230630-KPOB7318-Edit.jpg
theme: Toha
---

Garbage Collector (GC) to jeden z kluczowych elementów zarządzania pamięcią w języku Java. Dzięki niemu programista nie musi ręcznie zwalniać pamięci zajmowanej przez nieużywane obiekty, co znacząco ułatwia pracę i zmniejsza ryzyko błędów. W tym artykule przyjrzymy się rodzajom Garbage Collectorów dostępnych w Javie oraz ich zastosowaniom.

---
## Czym jest Garbage Collector?
Garbage Collector to mechanizm wbudowany w Java Virtual Machine (JVM), który automatycznie zwalnia pamięć zajmowaną przez obiekty, do których nie ma już referencji. Dzięki temu aplikacja nie wycieka pamięci, a programista może skupić się na logice biznesowej, zamiast ręcznie zarządzać alokacją i dealokacją pamięci.

### Jak działa Garbage Collector?
GC regularnie skanuje obiekty w pamięci i sprawdza, które z nich nie są już używane. Jeśli obiekt nie ma żadnych aktywnych referencji, zostaje oznaczony jako „śmieć” i może zostać usunięty podczas jednej z kolejnych operacji czyszczenia.

---

## Rodzaje Garbage Collectorów w Javie
JVM oferuje kilka implementacji Garbage Collectorów, które różnią się podejściem do zarządzania pamięcią i wydajnością. Wybór odpowiedniego GC zależy od charakterystyki aplikacji, ilości dostępnej pamięci oraz wymagań dotyczących wydajności.

1. Serial Garbage Collector
    - Charakterystyka:

        Najprostszy GC w Javie, odpowiedni dla aplikacji działających na jednowątkowych środowiskach.
        Wykorzystuje algorytm stop-the-world, który zatrzymuje wszystkie wątki podczas czyszczenia pamięci.
    - Zastosowanie:

        Małe aplikacje działające w środowisku o ograniczonych zasobach.
        Aplikacje desktopowe o niewielkim zużyciu pamięci.
        💡 Aktywacja:
        Można go włączyć w JVM przy pomocy flagi:

```bash
-XX:+UseSerialGC
```
2. Parallel Garbage Collector (Throughput Collector)

    - Charakterystyka:

        Równoległa wersja Serial GC, która uruchamia wiele wątków do czyszczenia pamięci.
        Priorytetem jest przepustowość aplikacji (throughput) – maksymalizacja wydajności kosztem dłuższych pauz stop-the-world.
    - Zastosowanie:

        Aplikacje serwerowe, które działają na wielordzeniowych procesorach.
        Aplikacje wymagające wysokiej wydajności, ale tolerujące krótkie pauzy GC.
    - Aktywacja:

```bash
-XX:+UseParallelGC
```
3. G1 Garbage Collector (Garbage-First GC)

    - Charakterystyka:

        Jeden z najbardziej uniwersalnych GC, który został wprowadzony w Javie 7.
        Dzieli pamięć na regiony i zarządza nimi dynamicznie, minimalizując pauzy stop-the-world.
        Nadaje się zarówno do małych, jak i dużych aplikacji.
    - Zastosowanie:

        Aplikacje o dynamicznie zmieniającym się obciążeniu.
        Systemy, które wymagają niskich opóźnień i wysokiej responsywności.
    - Aktywacja:

```bash
-XX:+UseG1GC
```
4. Z Garbage Collector (ZGC)
 - Charakterystyka:

    Nowoczesny GC wprowadzony w Javie 11.
    Zaprojektowany dla systemów o dużej ilości pamięci RAM i wymagających minimalnych pauz GC.
    Może działać na ogromnych stertach pamięci (nawet terabajty!).
 - Zastosowanie:

    Systemy o bardzo niskich wymaganiach czasowych.
    Aplikacje działające w chmurze i systemy Big Data.
 - Aktywacja:

```bash
-XX:+UseZGC
```
5. Shenandoah Garbage Collector
    - Charakterystyka:

        GC zoptymalizowany pod kątem minimalizacji pauz stop-the-world.
        Używa algorytmu, który czyści pamięć współbieżnie z wykonywaniem aplikacji.
    - Zastosowanie:

        Aplikacje wymagające ultra-niskich opóźnień.
        Gry, aplikacje wrażliwe na przerwy w działaniu.
    - Aktywacja:

```bash
-XX:+UseShenandoahGC
```
## Który Garbage Collector wybrać?
|Garbage Collector | Zalety | Wady | Zastosowanie |
|------------------|--------|------|--------------|
| Serial GC | Prostota, niskie zużycie zasobów | Długie pauzy stop-the-world | Małe aplikacje |
|Parallel GC | Dobra wydajność na wielordzeniowych procesorach | Pauzy mogą być długie | Aplikacje serwerowe |
| G1 GC | Zbalansowane zarządzanie pamięcią, krótki stop-the-world | Większe zużycie CPU	Duże systemy, aplikacje o zmiennym obciążeniu |
| ZGC | Minimalne pauzy, dobra skalowalność | Większe wymagania sprzętowe | Systemy w chmurze, Big Data |
| Shenandoah GC	| Ultra-niskie opóźnienia | Wysokie wymagania | Gry, aplikacje real-time |

## Podsumowanie
Garbage Collectory w Javie pozwalają na efektywne zarządzanie pamięcią i różnią się od siebie pod względem wydajności oraz sposobu działania. Wybór odpowiedniego GC powinien zależeć od rodzaju aplikacji i dostępnych zasobów.

**Jeśli dopiero zaczynasz pracę z Javą, warto poznać podstawowe zasady działania GC i eksperymentować z różnymi ustawieniami JVM, aby dostosować je do swoich potrzeb.**