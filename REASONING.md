# Reasoning for the Predictions Table

Write one entry under every heading below, then commit this file together with
`predictions.tsv`, before you run a case or open `tests/expected.tsv`.

Each entry names the rule that produces the four predicted fields for that
case. One to three sentences is enough. The grader checks structure only. It
does not judge quality, and it sets no word minimum.

After you run the cases, add a short correction under each case you predicted
wrongly. Say what you predicted, what CLISP printed, and which rule you
misread. Those entries belong in the correction commits.

## P01
`(+ 1 (* 2 3))` heads with the function `+`. A function evaluates all its arguments before it runs, so `(* 2 3)` becomes 6 first, and then adds 1 to get 7. That is an integer, so the length is none, and the head is a function.

## P02
`'(+ 1 2)` heads with the special operator `quote`. Quote returns its argument without evaluating it, so the result is the list `(+ 1 2)` and the addition never runs. That is a cons, so the length is 3, and the head is a special operator.

## P03
`nil` is an atom, so it has no head. It evaluates to itself, the empty list, and reads that as null. That is a null, the length is 0, and the head is none.

## P04
`t` is an atom, so it has no head. It evaluates to itself, which is a symbol that is not nil. That is a symbol, the length is none, and the head is none.

## P05
`(symbolp nil)` heads with the function `symbolp`. A function evaluates its arguments first, so nil stays nil, and symbolp then asks whether it is a symbol, since nil is a symbol, the result is t. That is a symbol, the length is none, and the head is function.

## P06
`(car '())` heads with the function `car`. The quote hands car the empty list unevaluated, and an empty list returns nil since there is no first element. That is a null, the length is 0, and the head is a function.

## P07
`(cons 1 '(2 3))` heads with the function `cons`. The quote hands the list `(2 3)`, and cons puts 1 in front of it to make `(1 2 3)`. That is a cons, the length is 3, and the head is a function.

## P08
`(if (null '()) 'empty 'full)` heads with the special operator `if`. The condition (null '()) is true because the list is empty, so if evaluates only the first branch and returns its value which is empty. That is a symbol, the length is none, and the head is a special operator.

## P09
`(and 1 nil 3)` heads with the special operator `and`, which CLISP reports ahead of macro. It evaluates left to right and stops at the first nil, so 3 is never evaluated and the result is nil. That is a null, the length is 0, and the head is a special operator.

## P10
`(progn ...)` heads with the special operator `progn`. It evaluates the forms in order and returns the value of the last one, so defvar and defun are basically just setups, ps3-rate is also a special variable, so the let rebinding to 10 is visible inside ps3-scale when it runs, and the last line gives 3 * 10 is 30. That is an integer, so the length is none, and the head is a special operator.

## P11
`(defun ps3-twice (n) (* n 2))` heads with the macro `defun`. The macro defines the function ps3-twice and returns the name, so the body never runs. That is a symbol, so the length is none and the head is a macro.

## P12
`(labels ...)` heads with the special operator `labels`. It makes a small function down that can call itself, and down puts n at the front of the list and calls itself with one less until n is 0, where it stops with the empty list, so it gives `(3 2 1)`. That is a cons, so the length is 3 and the head is a special operator.

## P13
`(mapcar #'length '((1 2) () (3)))` heads with the function `mapcar`. It gets the length of each inner list and the empty list has length 0, so the result is `(2 0 1)`. That is a cons, so the length is 3 and the head is a function.

## P14
`(mapcar (lambda (n) (* n n)) '(1 2 3))` heads with the function `mapcar`. It runs the lambda on each number in which it  squares each value, so the result would be `(1 4 9)`. That is a cons, so the length is 3 and the head is a function.

## P15
`(lambda (n) (* n 2))` heads with the macro `lambda`. It only builds a function and does not call it, so the body never runs and the result is a function object. That is a function, so the length is none and the head is a macro.

## P16
`(let ((factor 2)) ...)` heads with the special operator `let`. The function f remembers the factor that was 2 when it was made, so the later factor of 10 doesn't affect it and `(funcall f 3)` is 6. That is an integer, so the length is none and the head is a special operator.