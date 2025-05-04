4. [Factorial Program](#factorial-implementation)
### factorial program for one compiler <a name="factorial-implementation"></a>

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

