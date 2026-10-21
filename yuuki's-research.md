< [[yuuki]]

## String generation

Generating all possible strings over a given alphabet is difficult. In Python, you can use `itertools.product` in a simple case:

```py
from itertools import product

MAX_LENGTH = 5

alphabet = (
    "a", "b", "c", "d", "e", "f", "g",
    "h", "i", "j", "k", "l", "m", "n",
    "o", "p", "q", "r", "s", "t", "u",
    "v", "w", "x", "y", "z",
)

for length in range(1, MAX_LENGTH + 1):
    for chars in product(alphabet, repeat=length):
        print("".join(chars))

# Output:
# a
# b
# ...
# z
# aa
# ab
# ...
# zz
# aaa
# ...
# zzzzz
```

<details>
<summary>Total number of strings</summary>

There are 26 strings from "a" to "z", and $`26^2`$ from "aa" to "zz". The total number of strings of length $`n`$ or less is

$`26 + 26^2 + \cdots + 26^n = \displaystyle \frac{26(26^n - 1)}{25}`$.

In general, the sum of $`n`$ terms of a geometric sequence with first term $`r`$ and common ratio $`r`$ is $`\frac{r(1 - r^n)}{1 - r}`$:

$`
\begin{aligned}
r + r^2 + \cdots + r^n &= \frac{(r + r^2 + \cdots + r^n)(1 - r)}{1 - r} \\
&= \frac{\begin{aligned}
  r &+ r^2 + \cdots + r^n \\
    &- r^2 - \cdots - r^n - r^{n + 1}
\end{aligned}}{1 - r} \\
&= \frac{r - r^{n + 1}}{1 - r} \\
&= \frac{r(1 - r^n)}{1 - r}
\end{aligned}
`$

</details>

The following are 44 elements of the Japanese alphabet (gojūon) written in rōmaji. Including "n" causes collisions; "na", "ni", etc. are generated twice.

```py
alphabet = (
    "a", "i", "u", "e", "o",
    "ka", "ki", "ku", "ke", "ko",
    "sa", "shi", "su", "se", "so",
    "ta", "chi", "tsu", "te", "to",
    "na", "ni", "nu", "ne", "no",
    "ha", "hi", "fu", "he", "ho",
    "ma", "mi", "mu", "me", "mo",
    "ya", "yu", "yo",
    "ra", "ri", "ru", "re", "ro",
    "wa",
)
```

The number of rōmaji strings of length $`n`$ satisfies the third-order homogeneous linear recurrence relation with constant coefficients

$`a_n = 5a_{n - 1} + 36a_{n - 2} + 3a_{n - 3}`$,

with initial conditions $`a_1 = 5`$, $`a_2 = 61`$, and $`a_3 = 488`$.

| $`n`$ | $`a_n`$ | $`26^n`$ |
| --- | --- | --- |
| 1 | 5 | 26 |
| 2 | 61 | 676 |
| 3 | 488 | 17,576 |
| 4 | 4,651 | 456,976 |
| 5 | 41,006 | 11,881,376 |
| 6 | 373,930 | 308,915,776 |
