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

