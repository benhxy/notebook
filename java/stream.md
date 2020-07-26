# Java Stream

## Overview
* Introduced in Java 8.
* Allow Linux pipeline style processing for collections.
* Similar to IEnumerable/LINQ in C#/.Net.

## Concepts
* Only-once iterator-style consumption
* Lazy evaluation
* Terminal operation vs intermediate operation

## Comparison with IEnuberable in C#
* Syntax

---
## Creation and collection
### Stream.of()
### Arrays.stream()
### Collection.stream()
### Stream.builder(), accept(), build()
### Stream.collect()
### Collectors.joining()
### Collectors.groupingBy()

---
## Selection
### skip()
### limit()
### filter()
### find()
### findFirst(), orElse()
### allMatch(), anyMatch(), nonMatch()
### flatMap()

---
## Transformation
### forEach()
### map()
### peek()
### sorted()

---
## Aggregation
### reduce()
### min(), max()

---
## Other features
### Stream.parallel()