# Prolog Programs for Online "One Compiler"
## Index
1. [sum program](#sum-implementation)
2. [max program](#max-implementation)
3. [Factorial Program](#factorial-implementation)

### sum program <a name="sum-implementation"></a>
```prolog
:- initialization(main).
% Prolog program to calculate the sum of two numbers

sum(X,Y) :- S is X+Y,write(S).

main :- sum(3,9),nl.
```
### max program <a name="max-implementation"></a>
```prolog
:- initialization(main).
% prolog program to find the maximum of two numbers

max(X,Y) :-
	X=Y -> write("both are equal");
	X>Y -> write(X);
	X<Y -> write(Y).
main :- max(3,9),nl.
```
### factorial program <a name="factorial-implementation"></a>

```prolog
:- initialization(main).
% Base case: factorial of 0 is 1
fact(0, 1).

% Recursive case: factorial of N is N * factorial of N-1
fact(N, R) :-
    N > 0,
    N1 is N - 1,
    fact(N1, R1),
    R is N * R1.

% Entry point: compute factorial of a predefined number
main :-
    % Define the input number here
    N = 5,
    (   integer(N) ->
        (   N >= 0 ->
            fact(N, Result),
            format('Factorial of ~w is ~w~n', [N, Result])
        ;   write('Factorial is not defined for negative numbers.'), nl
        )
    ;   write('Invalid input. Please enter an integer.'), nl
    ).
```

