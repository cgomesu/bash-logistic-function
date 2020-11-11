# bash-logistic-function
An implementation of the [**logistic function**](#) written in [**GNU bash**](#) and [**GNU basic calculator** (bc)](#). It requires four parameters (`-x`, `-m`, `-L`, `-k`) to output the value of *f(x)*. If there is an error, the function exits with `status 1`; otherwise, it exists with `status 0`. (Errors won't generate any message unless the function is called in debug mode with the argument `-d`.)

This code was meant to be used programatically to output values of a given logistic model across values of a random variable *X*.  See [**Examples**](#examples).

# Usage
```
  ./logistic-function -x VALUE -m VALUE -L VALUE -k VALUE [OPTIONS]

  Logistic function:
    -x  real*  value of a variable X
    -m  real*  m = x0: Midpoint of X
    -L  real*  max value of f(x)
    -k  real*  growth rate

  * acceptable inputs:
    integers:       ..., -1, 0, 1, ...
    fractions:      ..., -1/2, -.25, 0, .25, 1/2, ...
    positive exps:  ..., "-(2^2)", 0, 2^2, ...
    natural exps:   "e(VALUE)"
    natural logs:   "l(VALUE)"
    square roots:   "sqrt(VALUE)"
    sines:          "s(VALUE)"
    cosines:        "c(VALUE)"
    arctangents:    "a(VALUE)"

  Options:
    -d       enable debug messages.
    -h       show this help message.
    -s  int  # of decimals to compute f(x). default: 20.
    -S  int  # of decimals in the output. default: 2.

  Example:
    logistic-function -x .5 -m 0 -L 1 -k 1 -s 10 -S 4

Author: cgomesu
Repo: https://github.com/cgomesu/bash-logistic-function
```

# Demo
TBD

# Examples
For the examples below, it was assumed that `logistic-function` is in the current user's `$PATH` (e.g., `/usr/local/bin`).  In addition, the logistic model was always the **standard logistic sigmoid function** with parameters *m* = 0, *L* = 1, and *k* = 1:
<p align="center">
	<img width="400" src="https://upload.wikimedia.org/wikipedia/commons/8/88/Logistic-curve.svg">
</p>

## If test
Test if a value of X (provided as the first argument) returns a valid status 
```
#!/bin/bash
if logistic-function -x "$1" -m 0 -L 1 -k 1 &>/dev/null; then
  # do something if valid
else
  # do something else
fi
exit 0
```

## For loop
Output values of *f(x)* for *x* = -1 to *x* = 1 in .1 increments
```
#!/bin/bash
# in GNU systems, make use of seq to handle non-integers in a sequence
for x in $(seq '-1' .1 1); do logistic-function -x "$x" -m 0 -L 1 -k 1; done
exit 0
```
