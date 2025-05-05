# Prolog Programs for Online "One Compiler"
## Index
1. [Write a PROLOG program to implement the family tree and demonstrate the family
relationship.](#family-implementation)
2. [Write a PROLOG program to implement conc(L1, L2, L3) where L2 is the list to be
appended with L1 to get the resulted list L3.](#concat-implementation)
3. [Write a PROLOG program to implement reverse(L, R) where List L is original and List
R is reversed list.](#reverse-implementation)
4. [Write a PROLOG program to calculate the sum of two numbers.](#sum-implementation)
5. [max program](#max-implementation)
6. [Factorial Program](#factorial-implementation)
7. [nth Fibonacci Number](#fibonacci-implementation)

1. Write a PROLOG program to implement the family tree and demonstrate the family
relationship.<a name="family-implementation"></a>
```prolog
:- initialization(main).
% Define genders
male(john).
male(paul).
male(mike).
male(david).
male(james).

female(mary).
female(linda).
female(susan).
female(kate).
female(emma).

% Define parent relationships
parent(john, paul).
parent(mary, paul).

parent(john, linda).
parent(mary, linda).

parent(paul, mike).
parent(susan, mike).

parent(paul, kate).
parent(susan, kate).

parent(linda, david).
parent(james, david).

parent(linda, emma).
parent(james, emma).

% Define basic relationships
father(X, Y) :- male(X), parent(X, Y).
mother(X, Y) :- female(X), parent(X, Y).

% Define sibling relationships
sibling(X, Y) :-
    parent(Z, X),
    parent(Z, Y),
    X \= Y.

brother(X, Y) :- male(X), sibling(X, Y).
sister(X, Y) :- female(X), sibling(X, Y).

% Define grandparent relationships
grandparent(X, Y) :-
    parent(X, Z),
    parent(Z, Y).

grandfather(X, Y) :- male(X), grandparent(X, Y).
grandmother(X, Y) :- female(X), grandparent(X, Y).

% Define uncle and aunt relationships
uncle(X, Y) :-
    male(X),
    sibling(X, Z),
    parent(Z, Y).

aunt(X, Y) :-
    female(X),
    sibling(X, Z),
    parent(Z, Y).

% Define ancestor relationship
ancestor(X, Y) :-
    parent(X, Y).

ancestor(X, Y) :-
    parent(X, Z),
    ancestor(Z, Y).

% Main predicate to demonstrate family relationships
main :-
    write('--- Family Tree Demonstration ---'), nl,
    write('Father of Mike: '),
    (father(F, mike) -> write(F), nl ; write('Unknown'), nl),
    write('Mother of Kate: '),
    (mother(M, kate) -> write(M), nl ; write('Unknown'), nl),
    write('Siblings of Linda: '), nl,
    (sibling(linda, Sibling), write('- '), write(Sibling), nl, fail ; true),
    write('Grandparents of Emma: '), nl,
    (grandparent(GP, emma), write('- '), write(GP), nl, fail ; true),
    write('Ancestors of David: '), nl,
    (ancestor(Ancestor, david), write('- '), write(Ancestor), nl, fail ; true),
    write('Uncles of Emma: '), nl,
    (uncle(Uncle, emma), write('- '), write(Uncle), nl, fail ; true),
    write('Aunts of Mike: '), nl,
    (aunt(Aunt, mike), write('- '), write(Aunt), nl, fail ; true),
    write('--- End of Demonstration ---'), nl.

```
2. Write a PROLOG program to implement conc(L1, L2, L3) where L2 is the list to be
appended with L1 to get the resulted list L3.<a name="concat-implementation"></a>
```prolog
:- initialization(main).
% conc(L1, L2, L3)
% Concatenates list L1 and list L2 to produce list L3.

conc([], L, L).
conc([H|T], L2, [H|L3]) :-
    conc(T, L2, L3).

% main predicate to demonstrate the conc/3 predicate
main :-
    List1 = [a, b, c],
    List2 = [1, 2, 3],
    conc(List1, List2, Result),
    write('List1: '), write(List1), nl,
    write('List2: '), write(List2), nl,
    write('Concatenated List: '), write(Result), nl.
```
3. Write a PROLOG program to implement reverse(L, R) where List L is original and List
R is reversed list.<a name="reverse-implementation"></a>
```prolog
:- initialization(main).

/* 
    Prolog program to implement 
    reverse_list(List, ReverseList)
    so that ReverseList is the reverse of the List.
*/

reverse_list(List, ReverseList) :-
    reverse_list(List, ReverseList, []).

reverse_list([H|T], List, RecRvList) :-
    reverse_list(T, List, [H|RecRvList]).

reverse_list([], L, L).

% Main predicate to demonstrate the reverse_list/2 predicate
main :-
    InputList = [a, b, c, d],
    reverse_list(InputList, ReversedList),
    write('Original List: '), write(InputList), nl,
    write('Reversed List: '), write(ReversedList), nl.
```
### Write a PROLOG program to calculate the sum of two numbers.<a name="sum-implementation"></a>
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

### fibonacci program <a name="fibonacci-implementation"></a>
```prolog
% Base cases
fib(0, 0).
fib(1, 1).

% Recursive case
fib(N, F) :-
    N > 1,
    N1 is N - 1,
    N2 is N - 2,
    fib(N1, F1),
    fib(N2, F2),
    F is F1 + F2.

% Main predicate to compute and display the 10th Fibonacci number
main :-
    fib(10, F),
    write('The 10th Fibonacci number is: '),
    write(F), nl.

```
