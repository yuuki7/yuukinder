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

## Planes with perspective

<img src="https://github.com/user-attachments/assets/d1cb0492-afd6-4d54-b0da-ab61ca5ddc18" alt="A human and a bot are touching each other; the distance between the centers of their bases is 50 at y = 0, but only 30 at y = 200." width="270" height="480">

When you are at $`(0, 0)`$, the bot touches you when it is at $`(50, 0)`$, a distance of 50.

However, when you are at $`(0, 200)`$, the bot touches you when it is at $`(30, 200)`$, a distance of only 30.

What is the formula to find the bot's position $`(x', y')`$ from your position $`(x, y)`$ so that the bot follows you?

<details>
<summary>Answer</summary>

When $`y = 0`$:

$`x' = x + 50`$

When $`y = 200`$:

$`x' = x + 30`$

We see that $`x'`$ depends on $`y`$. Let $`x' = x + f(y)`$. Assume $`f(y) = ay + b`$. Then:

$`
\left\{ \begin{alignedat}{3}
& f(0)   &&= b        &&= 50 \\
& f(200) &&= 200a + b &&= 30
\end{alignedat} \right.
`$

Therefore, $`f(y) = -\frac{y}{10} + 50`$. The answer is the two-dimensional affine transformation:

$`
\left\{ \begin{alignedat}{2}
& x' &&= x - \frac{y}{10} + 50 \\
& y' &&= y
\end{alignedat} \right.
`$

$`
\iff \begin{pmatrix}
x' \\
y'
\end{pmatrix} = \begin{pmatrix}
1 & -\frac{1}{10} \\
0 & 1
\end{pmatrix} \begin{pmatrix}
x \\
y
\end{pmatrix} + \begin{pmatrix}
50 \\
0
\end{pmatrix}
`$

</details>
