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

for i in range(0, n):
    print("x" + str(i) + ": " + str(xi_values[i]))

# print(x_values)
```

Defines:

* `h`: step size (3)
* `n`: number of steps (4)
* `xi_values`: generates x-values from 2 to 11 with step size of 3 → `[2, 5, 8, 11]`

Output:
```
x0: 2
x1: 5
x2: 8
x3: 11
```

---

### 3. **Exact Solution of f(x)**

```python
# real y values (using the normal integral method):
def real_f(x):
  return np.round((4*(x**5)/5) - (4*(x**3)), 2)

f_real = real_f(xi_values)

for i in range(0, n):
    print("Real f(" + str(i) + "): " + str(f_real[i]))

# print(y_real)
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
# f(x, y) values
def y(x):
  return np.round((4*(x**4))-(12*(x**2)), 2)

yi_values = y(xi_values)

for i in range(0, n):
    print("y" + str(i) + ": " + str(yi_values[i]))
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
# euler method
euler_y = np.zeros(4)

# initialize y0 to the real value of y0
euler_y[0] = f_real[0]

for i in range(0, n-1):
  euler_y[i+1] = euler_y[i] + (h*yi_values[i])

for i in range(0, n):
  print("euler y" + str(i) + ": " + str(euler_y[i]))
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
# errors = (abs(euler_y-f_real))/f_real*100

def error(i):
  return abs(((euler_y[i]-f_real[i]))/f_real[i]*100)
# errors = np.where(np.abs(f_real) > 1e-8,
#                   np.abs(euler_y - f_real) / np.abs(f_real) * 100,
#                   0)

errors = [round(error(i), 2) for i in range(n)]
errors[0] = "-"
```

* Computes relative error percentage between Euler’s approximation and real values
---

## Final Output Table
```python
print("Initial conditions:")
print("h = 3")
print("n = 4")
print("x0 = 2 to x3=11\n")
print("if f'(x) = 4x^4 - 12x^2, find the values of f(x) using the Euler method")

print("\n")

print("Results:")
print("i  x  Euler y  Exact y  Error")
print("------------------------------------------------------")

for i in range(0, n):
  print(f"{i}  {xi_values[i]}  {euler_y[i]}      {f_real[i]}     {errors[i]}")
```
Output :
```
Initial conditions:
h = 3
n = 4
x0 = 2 to x3=11

if f'(x) = 4x^4 - 12x^2, find the values of f(x) using the Euler method


Results:
i  x  Euler y  Exact y  Error
------------------------------------------------------
0  2  -6.4      -6.4     -
1  5  41.6      2000.0     97.92
2  8  6641.6      24166.4     72.52
3  11  53489.6      123516.8     56.69
```

---
