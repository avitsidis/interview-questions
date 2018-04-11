# Architecture

## SOLID

* Single Responsablity
* Open/close : Open to extensibility(new functions, new fields, new functionality), close to modification(if Used by other module  less impact) 
* Liskov : si S < T, alors les programmes qui utilisent des T doivent pouvoir utiliser des S sans invalidé ces programmes
* Interface segregation : do not depends on method you do not use
* Depedency inversion: dépendances avec les interfaces pas les implémentations + injection via framework au lieu de faire des news dans le code

## Composition over inheritance

Composition over inheritance is a design principle that gives the design higher flexibility. It is more natural to build business-domain classes out of various components than trying to find commonality between them and creating a family tree.

## High cohesion/low coupling

High cohesion means that class should do one thing and do this one thing very well. High cohesion is closely related to Single responsibility principle.
Low coupling suggest that class should have least possible dependencies. Also, dependencies that must exist should be weak dependencies - prefer dependency on interface rather than dependency on concrete class, or prefer composition over inheritance.

## 3-tiers

* Presentation
* Logic
* Data

## Clean architecture

* Entities (Enterprise wide)
* Core
* Use cases
* Gateways
* ...

[source 8thlight](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html)