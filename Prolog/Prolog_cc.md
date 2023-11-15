# [Prolog](https://www.metalevel.at/prolog): 
Prolog is a **programming language** that is rooted in classical [**logic**](https://www.metalevel.at/prolog/logic). It supports *search* and *unification* as built-in features. Prolog allows us to elegantly solve many tasks with short and general programs.

- A Prolog program consists of predicates.
  - Each Prolog predicate defines a relation between its arguments.
    -  A relation is a generalization of a function. 

Prolog predicates are often more versatile than functions in other programming languages, and are typically usable in multiple directions.
## Facets of Prolog:
### Prolog is a very simple language:
#### Syntax:
There is a single language element, called a [*clause*](https://www.metalevel.at/prolog/concepts#clause). A clause is of the form:
```prolog
Head :- Body.
```
- This means that **if** `Body` holds, **then** `Head` holds. The infix operator `(:-)/2` represents an arrow from right to left: ←.
- If `Head` *always* holds, then `:- Body` can be *omitted*.

### Prolog is a declarative language:
- Prolog is a *declarative language*. This means that we focus on stating *what* we are interested in. We [express what *holds*](https://www.metalevel.at/prolog/writing) about solutions we want to find. We are less concerned about *how* the Prolog implementation finds these solutions. 
