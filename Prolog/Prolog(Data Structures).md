# Prolog Language: Syntax and Semantics:
## Prolog Terms:

### Variable:
- Starts with an uppercase letter or `_`
- A single `_` denotes an anonymous variable
Examples: X, Y, `_#`, Prolog

### Atomic Terms:
#### Atom:
- Sequence of letters and digits starting with a lowrcase letter or in single quotes ('').
Example: a, at, atom, 'Prolog'

#### Integers:
- basically write down integers and they are considered as integers.
Example: 12, 10,20_20

### Compound Term:
- These terms have no real meaning and simply stand for themselves
- F(Arg1,.......,ArgN)
- The arguments are atoms
where 
```prolog
F -> functor name
Argk -> k-th argument
N -> arity
functor -> functor name together with arity
F/N -> principal functor
```

- `f(a(X), b, g(c,d))`
- `node (node (leaf (a), leaf (b)), leaf (c))`

<img width="400" alt="Screenshot 2023-10-10 at 6 13 36 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/360be52f-f537-4bfb-9753-8bf5fe0e57eb">
<img width="363" alt="Screenshot 2023-10-10 at 6 20 57 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/782d5710-9ebb-41d5-9cad-e645ea33a72a">

