# The (Newton)-Raphson-Simpson method

$x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$

Commonly known as "Newton's method", despite the most significant developments in its modern form being due to Joseph Raphson and Thomas Simpson (and Newton's version being independently developed in historically and geographically disparate locations, from the Middle East to Japan), this iterative method of finding the roots of a function `f`, given its known derivative `f'` should be familiar to most of you.

In this exercise, we will explore the implementation of the (Newton)-Raphson-Simpson method - henceforth "NRS" - in Julia, as a way to experience many of the features of the language.

## A) Getting Started

If you haven't already, launch a `julia` REPL - or a Jupyter notebook with a Julia kernel. 

For the first parts of this exercise, you will not need to load any additional packages, everything is just core Julia.

Firstly, we'll write a simple function to represent the delta between one estimate for the root, $x_n$ and the next, $x_{n+1}$, given the function and its derivative. 
Remember, in Julia you can type most special characters by typing their $\LaTeX$ representation, and then pressing tab.

So, our "nrs_delta" can be defined as, typing into the REPL, and pressing enter:

```julia
nrsδ(x, f, f') = - f(x) / f'(x)
```


where you can type $\delta$ with `\delta` and then `tab`, and the prime on the f' as `\prime` and then `tab` .

We'll also define some test `F` and `dF` functions so we can easily test our code: 

```julia
F(x) = x^3 - 8
dF(x) = 3x^2
```

notice, also, how Julia lets us write multiplication by juxtaposing a number and a variable, if it isn't ambiguous.

### NRS function, on Numbers

The NRS algorithm itself needs to repeatedly evaluate new deltas on our estimates, and exit when the magnitude of the delta is small enough - say, 1e-6 

To implement this as a function, it needs to take three things: an initial $x_0$ - ideally some kind of `Number` - and the function and its derivative.

Remembering that we can apply a type restriction on a function's arguments (making it a *method*), we can start this function as:

```julia
function NRS(x::Number, f, f')
```

once you press enter here, you should get - as in Python - a "continuation" in the terminal, as the REPL expects you to complete the function block.

For clarity for anyone reading our code, we should name our constants - like our `epsilon` for stopping, so:

```julia
    ϵ = 1e-6 #convergence criterion
    x_n = x
```

Now we can go write our loop - Julia doesn't support "do-while" loops, so we'll have to set up our delta outside the loop to a large initial value (here we type `\Delta` and `tab` to get the capital): 

```julia
    Δ = 1.0 
    while abs(Δ) > 1e-6
        Δ = nrsδ(x, f, f')
        x_n += Δ
    end
```

Finally, the value we want to return from our function should be just the final value of `x_n`, which we can do just by mentioning it by itself on a line:

```julia
    x_n
end
```

Try the function out with a few test values - you should find that, as it's defined for all types that are subtypes of `Number`, it works not just for floating point values, but also Complex values (which, of course, may converge to roots other than $2$).

### Extension - Limits

At present, this function is flawed - if a particular value for $x_0$ doesn't lead to a converging solution, it will iterate for ever.

By adding a new variable inside our function, called `count`, try modifying the NRS function we just wrote to also stop if it loops more than 40 times.

(You can either add a second condition to the `while` loop, or use `break` inside the loop to break out).

## B) Extending the NRS function to store history

Currently, our NRS algorithm is perfectly fine, but it might be nice to have an alternative version which takes a Vector (a 1-d Array) with an initial element representing $x_0$, and appends the history of all $x_n$ to it.

That way, we have a record of the path the function has taken to converge to the root it finds.

We'll define a new method for the NRS function that does this - multiple dispatch will select the right version for us based on the type of the first argument.

We'll need to make only a few changes relative to the first method for NRS:

**Firstly** - this method's first argument is a Vector of values of type T, where T must be some kind of Number.

We can express this using the "where" clause in our function definition like so

```julia
function NRS(xs::Vector{T}, f, f') where T <: Number
```

**Secondly**, rather than `x_n` being assigned to from `xs` directly, it needs to take the first element of `xs`.

Remembering that Julia arrays index from 1, we can either use `xs[1]` or `xs[begin]` to get that value.

**Thirdly**, we need to add each new value of `x_n` to the `xs` vector.

The `push!` method takes a Vector as its first argument, and a value as its second, and modifies the Vector in-place to append the value.

We can add a suitable call to `push!` inside the loop, immediately after `x_n` is updated.

**Finally**, we need to return `xs` and not `x_n` at the end of the function.

### Testing it out

Make a version of NRS with the above changes. 

Test it out: try passing the value `5.0` to NRS, and check it still just returns a single value. Then try passing `[5.0]` and see what you get as a result!

### An Aside

*Technically*, this method will actually modify the Vector we pass to it, as Julia implements *pass by sharing*. 

The convention in Julia is that functions that modify their arguments - or other state - should have a `!` at the end of their name. So, this should really be a new function called `NRS!`. 

However, the pedagogic value of showing how multiple dispatch works outweighs Julia's conventions in this one case...


## C) Plotting!

