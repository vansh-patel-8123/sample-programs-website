---

---

Welcome to the Reverse String in Vimscript page! Here, you'll find the source code for this program as well as a description of how the program works.

## Current Solution

Note: The solution shown here is the current solution in the Sample Programs repository. Documentation below may be outdated.

```Vimscript
func! Reverse(str)
    let l:r = join(reverse(split(a:str, '\zs')), '')
    call append(0, l:r)
endfunc

```

## How to Implement the Solution

No how to implement the solution available. Please consider contributing.

## How to Run the Solution

No how to run the solution available. Please consider contributing.