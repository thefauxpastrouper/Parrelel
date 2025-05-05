# Prolog Programs for Online "One Compiler"

## Index
1. [Write a PROLOG program to implement the family tree and demonstrate the family relationship.](#family-implementation)
2. [Write a PROLOG program to implement conc(L1, L2, L3) where L2 is the list to be appended with L1 to get the resulted list L3.](#concat-implementation)
3. [Write a PROLOG program to implement reverse(L, R) where List L is original and List R is reversed list.](#reverse-implementation)
4. [Write a PROLOG program to calculate the sum of two numbers.](#sum-implementation)
5. [Write a PROLOG program to implement max(X, Y, M) so that M is the maximum of two numbers X and Y.](#max-implementation)
6. [Write a program in PROLOG to implement factorial (N, F) where F represents the factorial of a number N.](#factorial-implementation)
7. [Write a program in PROLOG to implement generate_fib(N,T) where T represents the Nth term of the Fibonacci series.](#fibonacci-implementation)
8. [Write a PROLOG program to implement power (Num, Pow, Ans) : where Num is raised to the power Pow to get Ans.](#power-implementation)
9. [PROLOG program to implement multi (N1, N2, R) : where N1 and N2 denotes the numbers to be multiplied and R represents the result.](#multi-implementation)
10. [Write a PROLOG program to implement memb(X, L): to check whether X is a member of L or not](#memb-implementation)
11. [Write a PROLOG program to implement sumlist(L, S) so that S is the sum of a given list L.](#sumlist-implementation)
12. [Write a PROLOG program to implement two predicates evenlength(List) and oddlength(List) so that they are true if their argument is a list of even or odd length respectively.](#predicate-implementation)
13. [Write a PROLOG program to implement maxlist(L, M) so that M is the maximum number in the list.](#maxlist-implementation)
14. [Write a PROLOG program to implement insert(I, N, L, R) that inserts an item I into Nth position of list L to generate a list R.](#insert-implementation)
15. [Write a PROLOG program to implement delete(N, L, R) that removes the element on Nth position from a list L to generate a list R.](#delete-implementation)

### 1. Write a PROLOG program to implement the family tree and demonstrate the family relationship.<a name="family-implementation"></a>
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
### 2. Write a PROLOG program to implement conc(L1, L2, L3) where L2 is the list to be appended with L1 to get the resulted list L3.<a name="concat-implementation"></a>
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
### 3. Write a PROLOG program to implement reverse(L, R) where List L is original and List R is reversed list.<a name="reverse-implementation"></a>
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
### 4. Write a PROLOG program to calculate the sum of two numbers.<a name="sum-implementation"></a>
```prolog
:- initialization(main).
% Prolog program to calculate the sum of two numbers

sum(X,Y) :- S is X+Y,write(S).

main :- sum(3,9),nl.
```
### 5. Write a PROLOG program to implement max(X, Y, M) so that M is the maximum of two numbers X and Y.<a name="max-implementation"></a>
```prolog
:- initialization(main).

% max(X, Y, M) succeeds if M is the maximum of X and Y
max(X, Y, X) :- X >= Y.
max(X, Y, Y) :- X < Y.

% Main predicate to demonstrate the max/3 predicate
main :-
    X = 5,
    Y = 8,
    max(X, Y, M),
    write('The maximum of '), write(X), write(' and '), write(Y),
    write(' is '), write(M), nl.

```
### 6. Write a program in PROLOG to implement factorial (N, F) where F represents the factorial of a number N. <a name="factorial-implementation"></a>

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

### 7. Write a program in PROLOG to implement generate_fib(N,T) where T represents the Nth term of the Fibonacci series. <a name="fibonacci-implementation"></a>
```prolog
:- initialization(main).

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
### 8. Write a PROLOG program to implement power (Num, Pow, Ans) : where Num is raised to the power Pow to get Ans.<a name="power-implementation"></a>
```prolog
:- initialization(main).

% Base case: any number raised to the power of 0 is 1
power(_, 0, 1).

% Recursive case: Num raised to the power of Pow is Num multiplied by Num raised to the power of (Pow - 1)
power(Num, Pow, Ans) :-
    Pow > 0,
    Pow1 is Pow - 1,
    power(Num, Pow1, Ans1),
    Ans is Num * Ans1.

% Main predicate to compute and display 2 raised to the power of 3
main :-
    Num = 2,
    Pow = 3,
    power(Num, Pow, Ans),
    write(Num), write(' raised to the power of '), write(Pow),
    write(' is '), write(Ans), nl.
```
### 9. PROLOG program to implement multi (N1, N2, R) : where N1 and N2 denotes the numbers to be multiplied and R represents the result.<a name="multi-implementation"></a>
```prolog
:- initialization(main).

% Base case: any number multiplied by 0 is 0
multi(_, 0, 0).

% Recursive case: N1 multiplied by N2 is N1 added to the result of N1 multiplied by (N2 - 1)
multi(N1, N2, R) :-
    N2 > 0,
    N2_1 is N2 - 1,
    multi(N1, N2_1, R1),
    R is R1 + N1.

% Main predicate to compute and display the product of 4 and 3
main :-
    N1 = 4,
    N2 = 3,
    multi(N1, N2, R),
    write('The product of '), write(N1), write(' and '), write(N2),
    write(' is '), write(R), nl.

```
### 10. Write a PROLOG program to implement memb(X, L): to check whether X is a member of L or not.<a name="memb-implementation"></a>
```prolog
```prolog
:- initialization(main).

% Base case: X is a member of a list if X is the head of the list
memb(X, [X|_]).

% Recursive case: X is a member of the list if it is a member of the tail
memb(X, [_|T]) :-
    memb(X, T).

% Main predicate to demonstrate the memb/2 predicate
main :-
    List = [apple, banana, cherry],
    memb(banana, List),
    write('banana is a member of the list.'), nl,
    \+ memb(grape, List),
    write('grape is not a member of the list.'), nl.
```
### 11. Write a PROLOG program to implement sumlist(L, S) so that S is the sum of a given list L.<a name="sumlist-implementation"></a>
```prolog
:- initialization(main).

% Base case: The sum of an empty list is 0
sumlist([], 0).

% Recursive case: The sum of a list is the head plus the sum of the tail
sumlist([H|T], S) :-
    sumlist(T, Rest),
    S is H + Rest.

% Main predicate to compute and display the sum of a list
main :-
    List = [1, 2, 3, 4, 5],
    sumlist(List, S),
    write('The sum of the list is: '),
    write(S), nl.
```

### 12. Write a PROLOG program to implement two predicates evenlength(List) and oddlength(List) so that they are true if their argument is a list of even or odd length respectively.<a name="predicate-implementation"></a>
```prolog
:- initialization(main).

% evenlength(List): true if List has even length
evenlength([]).
evenlength([_|T]) :-
    oddlength(T).

% oddlength(List): true if List has odd length
oddlength([_]).
oddlength([_|T]) :-
    evenlength(T).

% Main predicate to demonstrate evenlength/1 and oddlength/1
main :-
    List1 = [a, b, c, d],
    List2 = [1, 2, 3],
    (evenlength(List1) ->
        write('List1 has even length.'), nl ;
        write('List1 does not have even length.'), nl),
    (oddlength(List2) ->
        write('List2 has odd length.'), nl ;
        write('List2 does not have odd length.'), nl).
```
### 13. Write a PROLOG program to implement maxlist(L, M) so that M is the maximum number in the list. <a name="maxlist-implementation"></a>
```prolog
:- initialization(main).

% Base case: The maximum of a single-element list is the element itself
maxlist([X], X).

% Recursive case: The maximum is the greater of the head and the maximum of the tail
maxlist([H|T], Max) :-
    maxlist(T, TailMax),
    Max is max(H, TailMax).

% Main predicate to demonstrate the maxlist/2 predicate
main :-
    List = [3, 1, 4, 1, 5, 9, 2, 6],
    maxlist(List, Max),
    write('The maximum value in the list is: '),
    write(Max), nl.
```
### 14. Write a PROLOG program to implement insert(I, N, L, R) that inserts an item I into Nth position of list L to generate a list R. <a name="insert-implementation"></a>
```prolog
:- initialization(main).

% Base case: Insert at the first position
insert(I, 1, L, [I|L]).

% Recursive case: Decrement position and traverse the list
insert(I, N, [X|L], [X|R]) :-
    N > 1,
    N1 is N - 1,
    insert(I, N1, L, R).

% Main predicate to demonstrate the insert/4 predicate
main :-
    List = [a, b, c, d],
    insert(x, 3, List, Result),
    write('Original List: '), write(List), nl,
    write('After inserting x at position 3: '), write(Result), nl.
```
### 15. Write a PROLOG program to implement delete(N, L, R) that removes the element on Nth position from a list L to generate a list R. <a name="delete-implementation"></a>
```prolog
% delete_nth(N, L, R): Remove the element at position N from list L to get list R.

% Base case: Removing the first element
delete_nth(1, [_|T], T).

% Recursive case: Traverse the list until the Nth position
delete_nth(N, [H|T], [H|R]) :-
    N > 1,
    N1 is N - 1,
    delete_nth(N1, T, R).

% Main predicate to demonstrate delete_nth/3
main :-
    List = [a, b, c, d, e],
    delete_nth(3, List, Result),
    write('Original List: '), write(List), nl,
    write('After deleting element at position 3: '), write(Result), nl.
```
