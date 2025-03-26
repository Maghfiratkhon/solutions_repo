# Problem 2
# Estimating π Using Monte Carlo Methods

# 1. Motivation

Monte Carlo simulations are a powerful class of computational techniques that leverage randomness to solve problems or estimate values. One elegant application is estimating the value of $π$ through geometric probability. By generating random points or objects and analyzing their positions relative to geometric shapes, we can approximate $π$ in an intuitive and visually engaging way.

This problem bridges probability, geometry, and numerical computation, offering insights into how randomness can address complex challenges in fields like physics, finance, and computer science. Estimating $π$ using Monte Carlo methods showcases the simplicity and versatility of this approach while revealing practical lessons about convergence and computational efficiency.

---

# 2.  Part 1: Estimating π Using a Circle

### 2.1 Theoretical Foundation

Consider a unit circle (radius = 1) centered at the origin, inscribed within a square of side length 2 (spanning from -1 to 1 on both x and y axes). The area of the circle is $πr^2 = π(1)^2 = π$, and the area of the square is $2 \times 2 = 4$. The ratio of the circle’s area to the square’s area is $π/4$.

If we randomly generate points uniformly within the square, the probability that a point falls inside the circle is equal to this area ratio, $π/4$. For $N$ total points, if $M$ points land inside the circle (where $x^2 + y^2 \leq 1$), the ratio $M/N$ approximates $π/4$. Thus:

$$
π \approx 4 \times \frac{M}{N}
$$

### 2.2 Simulation

We’ll use Python to simulate this process:

```python
import numpy as np
import matplotlib.pyplot as plt

def estimate_pi_circle(n_points):
    # Generate random x and y coordinates in [-1, 1]
    x = np.random.uniform(-1, 1, n_points)
    y = np.random.uniform(-1, 1, n_points)
    
    # Calculate distance from origin
    distance = np.sqrt(x**2 + y**2)
    
    # Count points inside the unit circle
    inside_circle = distance <= 1
    m = np.sum(inside_circle)
    
    # Estimate pi
    pi_estimate = 4 * m / n_points
    return x, y, inside_circle, pi_estimate

# Run simulation
n_points = 10000
x, y, inside_circle, pi_estimate = estimate_pi_circle(n_points)
print(f"Estimated π with {n_points} points: {pi_estimate}")
```
## 2.3 Visualization
We’ll plot the points, coloring those inside the circle differently from those outside:

```python
plt.figure(figsize=(6, 6))
plt.scatter(x[inside_circle], y[inside_circle], color='blue', s=1, label='Inside Circle')
plt.scatter(x[~inside_circle], y[~inside_circle], color='red', s=1, label='Outside Circle')
plt.gca().set_aspect('equal')
plt.title(f"Monte Carlo Estimation of π\nEstimate: {pi_estimate:.5f}")
plt.legend()
plt.show()
```
![image](https://github.com/user-attachments/assets/d5798ae0-9968-46c8-a9d7-40073ed65c07)


**Description**: The plot shows a square with a cloud of points. Blue points (inside $x^2 + y^2 \leq 1$) form a circular pattern, while red points fill the remaining square. The title includes the estimated $π$ value.

## 2.4 Analysis
To study convergence, we’ll test different sample sizes:
```python
n_values = [100, 1000, 10000, 100000]
estimates = []
errors = []

for n in n_values:
    _, _, _, pi_est = estimate_pi_circle(n)
    estimates.append(pi_est)
    errors.append(abs(pi_est - np.pi))

plt.plot(n_values, errors, marker='o')
plt.xscale('log')
plt.xlabel('Number of Points (log scale)')
plt.ylabel('Absolute Error')
plt.title('Convergence of π Estimate')
plt.show()
```
![image](https://github.com/user-attachments/assets/f581a6af-ff0f-442d-8d13-da67282536cd)

## Estimating π Using Monte Carlo Methods

## 2.4 Analysis

**Description**: The graph shows error decreasing as the number of points increases, though with fluctuations due to randomness. The convergence rate is approximately $O(1/\sqrt{N})$, typical of Monte Carlo methods, reflecting the statistical nature of the estimate.

**Computational Considerations**: The method is simple but slow to converge. Increasing $N$ improves accuracy but linearly increases computation time.

## 3. Part 2: Estimating π Using Buffon’s Needle

### 3.1 Theoretical Foundation

In Buffon’s Needle problem, a needle of length $L$ is dropped randomly onto a plane with parallel lines spaced $D$ units apart (assume $L \leq D$ for simplicity). The probability that the needle crosses a line depends on its position and orientation. For a needle with endpoints determined by its center at $(x, y)$ and angle $θ$ (from the horizontal), it crosses a line if its vertical projection spans one of the parallel lines.

The probability of crossing is derived as:

$$
P = \frac{2L}{π D}
$$

If we drop $N$ needles and $M$ cross a line, then:

$$
P \approx \frac{M}{N}
$$

Equating the two expressions for $P$:

$$
\frac{M}{N} \approx \frac{2L}{π D}
$$

Solving for $π$:

$$
π \approx \frac{2L N}{M D}
$$

For simplicity, set $L = D = 1$:

$$
π \approx \frac{2N}{M}
$$

### 3.2 Simulation

Here’s a Python implementation:

```python
def estimate_pi_buffon(n_drops, L=1, D=1):
    # Random x position of needle center (between 0 and D)
    x_center = np.random.uniform(0, D, n_drops)
    # Random angle (0 to pi/2, due to symmetry)
    theta = np.random.uniform(0, np.pi/2, n_drops)
    
    # Vertical extent of needle
    y_extent = (L/2) * np.sin(theta)
    
    # Check if needle crosses a line (y ranges from 0 to D)
    crosses = x_center + y_extent > D/2
    m = np.sum(crosses)
    
    # Estimate pi
    pi_estimate = (2 * L * n_drops) / (m * D) if m > 0 else 0
    return x_center, theta, crosses, pi_estimate

# Run simulation
n_drops = 10000
x_center, theta, crosses, pi_estimate = estimate_pi_buffon(n_drops)
print(f"Estimated π with {n_drops} drops: {pi_estimate}")
```

## 3.3 Visualization
Visualize the needles:

```python
import numpy as np
import matplotlib.pyplot as plt

# Assuming L represents the length of the needle
# and needs to be defined before use
L = 1  # You might need to adjust this value based on your simulation setup

plt.figure(figsize=(8, 4))
for i in range(min(n_drops, 100)):  # Plot first 100 for clarity
    x_c = x_center[i]
    th = theta[i]
    dx = (L/2) * np.cos(th)
    dy = (L/2) * np.sin(th)
    color = 'green' if crosses[i] else 'black'
    plt.plot([x_c - dx, x_c + dx], [0 - dy, 0 + dy], color=color)
plt.axhline(0, color='blue', linestyle='--')
plt.axhline(1, color='blue', linestyle='--')
plt.title(f"Buffon’s Needle Simulation\nEstimate: {pi_estimate:.5f}")
plt.show()
```
![image](https://github.com/user-attachments/assets/7ec66170-1333-4279-8f06-beac748cc49d)

**Description**: The plot shows horizontal lines at $y=0$ and $y=1$, with needles as line segments. Green needles cross a line; black ones don’t. The title displays the $π$ estimate.

## 3.4 Analysis
Test convergence:

```python 
n_values = [100, 1000, 10000, 100000]
estimates_buffon = []
errors_buffon = []

for n in n_values:
    _, _, _, pi_est = estimate_pi_buffon(n)
    estimates_buffon.append(pi_est)
    errors_buffon.append(abs(pi_est - np.pi))

plt.plot(n_values, errors_buffon, marker='o')
plt.xscale('log')
plt.xlabel('Number of Drops (log scale)')
plt.ylabel('Absolute Error')
plt.title('Convergence of π Estimate (Buffon)')
plt.show()
```
![image](https://github.com/user-attachments/assets/cdfade46-b438-446f-81ee-feee29154de6)

### 3.4 Analysis

**Description**: Similar to the circle method, error decreases with more drops, following $O(1/\sqrt{N})$.

**Comparison**: Buffon’s Needle converges similarly but requires more geometric computation per iteration, making it less efficient than the circle method for the same number of samples.

## 4. Deliverables Summary

- **Markdown Document**: This document provides explanations, formulas, and results.

- **Python Code**: Included above for both methods.

- **Graphical Outputs**: Described and coded for visualization.

- **Analysis**: Convergence is $O(1/\sqrt{N})$ for both, with the circle method being simpler and faster per iteration.

## 5. Conclusion

The exploration of Monte Carlo methods for estimating $π$ through the circle-based approach and Buffon’s Needle problem demonstrates the power and elegance of leveraging randomness in computational mathematics. Both methods successfully approximate $π$, with the circle method relying on the geometric simplicity of area ratios and Buffon’s Needle utilizing the probabilistic interplay of needle drops and line crossings. The simulations confirm that accuracy improves with larger sample sizes, converging at a rate of $O(1/\sqrt{N})$, though not without the inherent fluctuations of stochastic processes.

Comparatively, the circle method proves more computationally efficient due to its straightforward point-in-circle check, while Buffon’s Needle, though conceptually intriguing, demands additional geometric calculations that slow its performance per iteration. These trade-offs highlight a key lesson in Monte Carlo techniques: simplicity often enhances practicality, even if convergence remains gradual.

This exercise underscores the versatility of Monte Carlo methods beyond mere estimation of $π$, offering a foundation for tackling complex problems in diverse fields. By blending theory, simulation, and visual analysis, we gain not only a numerical approximation but also an appreciation for how randomness can illuminate the constants that shape our universe.

