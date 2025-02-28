---
title: Garbage Collectory in Javie
author:
    name: Krzysztof Pobożan
    image: /images/KP-20230630-KPOB7318-Edit.jpg
theme: Toha
menu:
  sidebar:
    name: Garbage Collectory in Javie
    identifier: garbage-collectors-in-java
    weight: 10
    parent: java-site
---
Garbage Collector (GC) is one of the key elements of memory management in Java. Thanks to it, the programmer does not have to manually release the memory occupied by unused objects, which significantly simplifies work and reduces the risk of errors. In this article we will look at the types of Garbage Collectors available in Java and their applications.

---
## What is a Garbage Collector?
Garbage Collector is a mechanism built into the Java Virtual Machine (JVM) that automatically frees memory occupied by objects that are no longer referenced. This prevents the application from leaking memory, and allows the programmer to focus on business logic instead of manually managing memory allocation and deallocation.

### How does the Garbage Collector work?
The GC regularly scans objects in memory and checks which ones are no longer in use. If an object has no active references, it is marked as “garbage” and can be removed during one of the next cleaning operations.
