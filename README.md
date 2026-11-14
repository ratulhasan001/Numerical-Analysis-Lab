# Numerical Analysis Lab

C++ implementations of standard numerical methods, written for the Numerical Analysis sessional (lab) course of the B.Sc. in Computer Science and Engineering at BAUET. The labs cover finding roots of non-linear equations (bisection, false position, fixed-point iteration, Newton–Raphson), Newton's forward-difference interpolation, and numerical integration with the trapezoidal and Simpson's 1/3 rules. Each function under study is hard-coded in the source, and the program reads the interval, initial guess or data points from standard input.

## Contents

### [lab-01](lab-01) – Bisection method

| File | What it does |
|---|---|
| [bisection_method.cpp](lab-01/bisection_method.cpp) | Bisection on f(x) = x³ − 2x − 5 over a user-given interval `[a, b]` with f(a)·f(b) < 0. Stops when the interval width is below 1e-15. Converges linearly: about log₂((b − a)/ε) iterations. |
| [transcendental.cpp](lab-01/transcendental.cpp) | The same bisection routine applied to a transcendental equation, f(x) = 4e⁻ˣ sin x − 1. |

### [lab-02](lab-02) – False position and fixed-point iteration

| File | What it does |
|---|---|
| [false_position_method.cpp](lab-02/false_position_method.cpp) | Regula falsi on f(x) = x − e⁻ˣ: x = (a·f(b) − b·f(a)) / (f(b) − f(a)). Stops when \|f(x)\| < 5e-4 or after 1000 iterations. |
| [iteration_method.cpp](lab-02/iteration_method.cpp) | Fixed-point iteration x = g(x) with g(x) = ∛(2x + 5), for x³ − 2x − 5 = 0. Reads the initial guess, tolerance and maximum number of iterations. |

### [lab-03](lab-03) – Newton–Raphson method

| File | What it does |
|---|---|
| [newton_raphson.cpp](lab-03/newton_raphson.cpp) | Newton–Raphson on f(x) = x sin x + cos x with f′(x) = x cos x, starting from a user-given x₀. Stops when the step is below 1e-4 and prints the root to 3 decimal places. Converges quadratically near a simple root. |

### [lab-04](lab-04) – Interpolation

| File | What it does |
|---|---|
| [interpolation.cpp](lab-04/interpolation.cpp) | Newton's forward-difference interpolation. Builds the forward-difference table for `n` equally spaced points (up to 20) and evaluates the interpolating polynomial at a given x using u = (x − x₀)/h. Building the table takes O(n²). |

### [lab-05](lab-05) – Numerical integration

| File | What it does |
|---|---|
| [trap.cpp](lab-05/trap.cpp) | Composite trapezoidal rule over `n` tabulated, equally spaced points `(x, y)`: (h/2)·[y₀ + 2(y₁ + … + yₙ₋₂) + yₙ₋₁]. |
| [simpson.cpp](lab-05/simpson.cpp) | Composite Simpson's 1/3 rule over `n` tabulated, equally spaced points: (h/3)·[y₀ + 4Σy_odd + 2Σy_even + yₙ₋₁]. Needs an odd number of points (an even number of sub-intervals). |

## Build and run

You need a GCC toolchain, because the programs include `<bits/stdc++.h>`. On macOS, use Homebrew's `g++-<version>`.

```bash
g++ -std=c++17 -O2 lab-01/bisection_method.cpp -o bisection
echo "2 3" | ./bisection          # Root value : 2.09455
```

Example inputs:

| Program | Input | Output |
|---|---|---|
| `lab-02/false_position_method.cpp` | `0 1` | `Root value : 0.567206` |
| `lab-02/iteration_method.cpp` | `2 0.00001 100` (x₀, tolerance, max iterations) | `2.09455` |
| `lab-04/interpolation.cpp` | `4`, then the points `1 1  2 8  3 27  4 64`, then `2.5` | `15.625` |
| `lab-05/simpson.cpp` | `3  0 0  1 1  2 4` (n, then the points of y = x²) | `2.66667` |

To try a different equation, edit `equation_value` / `f` (and `g` for the derivative or iteration function) in the source file.

## Author

Ratul Hasan · [ratulhasan.dev](https://ratulhasan.dev)
