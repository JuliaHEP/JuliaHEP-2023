# Installing and Running Julia

## Installing Julia

If you haven't already done so, visit the Julia [downloads](https://julialang.org/downloads/) page

- Pick the installer for your platform, use the *current stable release*
- Unpack/install locally

If you installed a tarball release, you may need to add the location of the Julia `bin` directory to your `PATH`

## Run Julia

Check that when you execute `julia` the REPL starts, like this:

```
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.9.3 (2023-08-24)
 _/ |\__'_|_|_|\__'_|  |  Official https://julialang.org/ release
|__/                   |

julia> println("hello, world!")
hello, world!

julia> (2+3)^2
25

julia> 
```

As shown above, try typing a few commands and checking that they execute as expected.

## You should have learned...

1. How to install Julia
2. How to start the Julia REPL and execute commands
