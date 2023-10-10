# Prolog Language(Syntax and Semantics): 

## Prolog Terms:
- Prolog terms naturally correspond to [trees](https://www.metalevel.at/prolog/optimization#tree). There is a [standard order](https://www.metalevel.at/prolog/sorting#order) on terms.

### Variable:
- Starts with an uppercase letter or `_`
- A single underscore denotes an *anonymous variable* and can be read as "any term"
Examples: X, Y, `_#`, Prolog

### Atomic Terms:
#### Atom:
- Sequence of letters and digits starting with a lowrcase letter or in single quotes ('').
Example: a, at, atom, 'Prolog'

#### Integers:
- Basically write down integers and they are considered as integers.
Example: 12, 10,20_20

### Compound Term:
- These terms have no real meaning and simply stand for themselves
- A compound term is called *partially instantiated* if one of its subterms is a variable.
- F(Arg1,.......,ArgN)
 
```prolog
F -> functor name
Argk -> k-th argument (Atoms)
N -> arity
functor -> functor name together with arity
F/N -> principal functor
```

- `f(a(X), b, g(c,d))`
- `node (node (leaf (a), leaf (b)), leaf (c))`

<img width="400" alt="Screenshot 2023-10-10 at 6 13 36 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/360be52f-f537-4bfb-9753-8bf5fe0e57eb">
<img width="363" alt="Screenshot 2023-10-10 at 6 20 57 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/782d5710-9ebb-41d5-9cad-e645ea33a72a">

## Prolog Lists:
- Prolog **lists** are a special case of [*terms*](https://www.metalevel.at/prolog/data#term).
