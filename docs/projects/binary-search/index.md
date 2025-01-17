---

title: Binary Search in Every Language
layout: default
date: 2019-10-25
last-modified: 2020-05-02
featured-image: binary-search-in-every-language.jpg
tags: [binary-search]
authors:
  - the_renegade_coder

---

Welcome to the Binary Search page! Here, you'll find a description of the project as well as a list of sample programs written in various languages.

## Description

Binary search is a special type of search function which relies on a few properties
of the search space. First, the search space must have constant time random access
(i.e. an array). In addition, the search space must be sorted by some attribute.
As a consequence, we're able to navigate the search space in O(log(N)) instead of
O(N). 

Jargon aside, binary search works by taking advantage of a sorted collection. As a result,
we don't have to search every element in the collection. Instead, we can try the middle.
If the middle element is greater than the element we want to find, we know that the element
must be "to the left" of that element, assuming the collection is sorted least to greatest. 
From there, we can try the element in the middle of the left half, and so on. 

Eventually, we'll find the element we're looking for, or we'll reach the end of our search.
In either case, we'll only explore O(log(N)) elements. This gives us a dramatic improvement
over linear search.


## Requirements

For the purposes of this project, we'll assume that the search space is a list of integers.
Specifically, we'll accept two inputs on the command line: the list of integers and the
integer to find:

```shell
$ ./binary-search.lang "1, 4, 5, 11, 12" "4"
```

If successful, the script should return `true`. Otherwise, the script should return `false`. 
If any user input errors occur, the script should output the following usage message:
`Usage: please provide a list of sorted integers ("1, 4, 5, 11, 12") and the integer to find ("11")`.


## Testing

Every project in the Sample Programs repo should be tested. In this section, we specify the set of tests specific to Binary Search. To keep things simple, we split up testing into two subsets: valid and invalid. Valid tests refer to tests that occur under correct input conditions. Invalid tests refer to tests that occur on bad input (e.g., letters instead of numbers).

### Valid Tests

| Description               | List Input     | Target Integer Input | Output  |
| ------------------------- | -------------- | -------------------- | ------- |
| Sample Input: First True  | `"1, 3, 5, 7"` | `"1"`                | `true`  |
| Sample Input: Last True   | `"1, 3, 5, 7"` | `"7"`                | `true`  |
| Sample Input: Middle True | `"1, 3, 5, 7"` | `"5"`                | `true`  |
| Sample Input: One True    | `"5"`          | `"5"`                | `true`  |
| Sample Input: One False   | `"5"`          | `"7"`                | `false` |
| Sample Input: Many False  | `"1, 3, 5, 6"` | `"7"`                | `false` |


### Invalid Tests

| Description           | List Input   | Target Integer Input |
| --------------------- | ------------ | -------------------- |
| No Input              |              |                      |
| Missing Input: List   | `1, 2, 3, 4` |                      |
| Missing Input: Target | `""`         | `5`                  |
| Out of Order Input    | `3, 5, 1, 2` | `3`                  |

All invalid tests should spit out a usage statement in the following
form: 

```
Usage: please provide a list of sorted integers ("1, 4, 5, 11, 12") and the integer to find ("11")
```


## Articles

- [Binary Search in C++](https://sampleprograms.io/projects/binary-search/c-plus-plus)
- [Binary Search in Go](https://sampleprograms.io/projects/binary-search/go)
- [Binary Search in Java](https://sampleprograms.io/projects/binary-search/java)
- [Binary Search in Javascript](https://sampleprograms.io/projects/binary-search/javascript)
- [Binary Search in Python](https://sampleprograms.io/projects/binary-search/python)
- [Binary Search in Rust](https://sampleprograms.io/projects/binary-search/rust)

---

<nav class="project-nav">

<div id="prev">

[<-- Previous Project (Baklava)](https://sampleprograms.io/projects/baklava)

</div>

<div id="next">

[Next Project (Bubble Sort) -->](https://sampleprograms.io/projects/bubble-sort)

</div>

</nav>