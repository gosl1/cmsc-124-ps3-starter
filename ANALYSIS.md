# Environments and the Toy Evaluator

Replace this paragraph after your checks pass. Trace one form through your own
`eval-expr`, point to the line that captures the defining environment, say what
would change if application joined the arguments to the caller's environment
instead, and explain why the host CLISP needs `funcall` where the toy language
doesn't.


The defining environment is captured in the lambda branch of `eval-expr`, specifically through `(make-closure (second expr) (third expr) env)`. The `make-closure` function stores this environment alongside the parameters and body using `(list :closure params body env)`. In the scope-discrimination case, when `(lambda (y) (+ x y))` is evaluated, the environment contains the binding `x = 2`. The binding for f is not present yet because eval-let evaluates the lambda initializer first, before adding the new bindings to the environment. Hence, the closure captures the environment containing `x = 2`, which it retains even when called from a different environment.