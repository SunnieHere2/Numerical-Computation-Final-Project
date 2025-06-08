# Numerical-Computation-Final-Project

**No 4**

* **Name**: Ramasyamsi Ahmad Shabri
* **NRP**: 5025241008
* **Class**: IUP
* **Group**: IUP05

---

## Problem Number: 44

![image](https://github.com/user-attachments/assets/aa651d31-e03b-4f7b-ab1b-dd840ce25a56)

---

## Code Explanation

### 1. **Import Libraries**

```python
import numpy as np
import math
```

---

### 2. **Initialization**

```python
h = 3
n = 4
xi_values = np.arange(2, 12, h)
```

Defines:

* `h`: step size (3)
* `n`: number of steps (4)
* `xi_values`: generates x-values from 2 to 11 with step size of 3 → `[2, 5, 8, 11]`

---

### 3. **Exact Solution of f(x)**

```python
def real_f(x):
  return np.round((4*(x**5)/5) - (4*(x**3)), 2)

f_real = real_f(xi_values)
```

This function computes the analytical (exact) value of `f(x)` using the integral of `f'(x)`.

* Formula: $f(x) = \frac{4x^5}{5} - 4x^3$

Output:

```
Real f(0): -6.4
Real f(1): 2000.0
Real f(2): 24166.4
Real f(3): 123516.8
```

---

### 4. **Derivative Function (f'(x))**

```python
def y(x):
  return np.round((4*(x**4)) - (12*(x**2)), 2)

yi_values = y(xi_values)
```

Defines the derivative function $f'(x) = 4x^4 - 12x^2$

Output:

```
y0: 16
y1: 2200
y2: 15616
y3: 57112
```

---

### 5. **Euler Method Implementation**

```python
euler_y = np.zeros(4)
euler_y[0] = f_real[0]  # Initial condition

for i in range(0, n-1):
  euler_y[i+1] = euler_y[i] + (h * yi_values[i])
```

* Applies Euler’s formula: $y_{i+1} = y_i + h \cdot f'(x_i)$

Output:

```
euler y0: -6.4
euler y1: 41.6
euler y2: 6641.6
euler y3: 53489.6
```

---

### 6. **Error Analysis**

```python
def error(i):
  return abs(((euler_y[i] - f_real[i]) / f_real[i]) * 100)

errors = [round(error(i), 2) for i in range(n)]
errors[0] = "-"
```

* Computes relative error percentage between Euler’s approximation and real values

Result:

```
Errors = ['-', 97.92, 72.52, 56.69]
```

---

## Final Output Table

```
Initial conditions:
h = 3
n = 4
x0 = 2 to x3 = 11

Results:
i  x  Euler y  Exact y  Error
------------------------------------------------------
0  2  -6.4      -6.4     -
1  5  41.6      2000.0   97.92
2  8  6641.6    24166.4  72.52
3  11 53489.6   123516.8 56.69
```

---
