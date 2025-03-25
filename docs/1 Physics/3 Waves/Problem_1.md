# Problem 1
# Interference Patterns on a Water Surface

## Motivation

Interference occurs when waves from different sources overlap, creating new patterns. On a water surface, this can be easily observed when ripples from different points meet, forming distinctive interference patterns. These patterns can show us how waves combine in different ways, either reinforcing each other or canceling out.

Studying these patterns helps us understand wave behavior in a simple, visual way. It also allows us to explore important concepts like the relationship between wave phase and the effects of multiple sources. This task offers a hands-on approach to learning about wave interactions and their real-world applications, making it an engaging way to dive into wave physics.

---

## Task

A circular wave on the water surface, emanating from a point source located at $(x_s, y_s)$, can be described by the **Single Disturbance equation**:

$$
\eta(x, y, t) = A \cos(k r - \omega t + \phi)
$$

Where:
- $\eta(x, y, t)$ is the displacement of the water surface at point $(x, y)$ at time $t$,
- $A$ is the amplitude of the wave,
- $k$ is the wave number, related to the wavelength $\lambda$ by $k = \frac{2\pi}{\lambda}$,
- $\omega$ is the angular frequency, related to the frequency $f$ by $\omega = 2\pi f$,
- $r = \sqrt{(x - x_s)^2 + (y - y_s)^2}$ is the distance from the source to the point $(x, y)$,
- $\phi$ is the initial phase.

### Problem Statement

The task is to analyze the interference patterns formed on the water surface due to the superposition of waves emitted from point sources placed at the vertices of a chosen regular polygon. This involves:

1. Selecting a regular polygon (e.g., equilateral triangle, square, pentagon).
2. Positioning point wave sources at the vertices of the selected polygon.
3. Writing the equations describing the waves emitted from each source.
4. Applying the principle of superposition to sum the wave displacements.
5. Visualizing the resulting interference patterns.

---

## Solution

### 1. Wave Equation for a Single Source

We begin by considering the wave equation for a single point source on the water surface. The displacement at a point $(x, y)$ caused by a single wave source at $(x_s, y_s)$ is given by:

$$
\eta(x, y, t) = A \cos(k r - \omega t + \phi)
$$

Where:
- $r = \sqrt{(x - x_s)^2 + (y - y_s)^2}$ is the distance between the source and the point $(x, y)$,
- $A$ is the amplitude of the wave,
- $k$ is the wave number, $k = \frac{2\pi}{\lambda}$,
- $\omega$ is the angular frequency, $\omega = 2\pi f$.

### 2. Superposition of Waves

When there are multiple sources, the total displacement at a point $(x, y)$ is the sum of the displacements caused by all individual sources. This is the principle of **superposition**:

$$
\eta_{\text{total}}(x, y, t) = \sum_{i=1}^{N} \eta_i(x, y, t)
$$

Where $N$ is the number of sources (vertices of the polygon).

### 3. Regular Polygon Selection

We choose a **regular polygon** with $N$ vertices (e.g., equilateral triangle, square, pentagon). The positions of the sources are given by the vertices of the polygon. For a regular polygon with radius $R$ centered at the origin, the coordinates of the vertices are:

$$
(x_i, y_i) = (R \cos(\theta_i), R \sin(\theta_i)) \quad \text{where} \quad \theta_i = \frac{2\pi(i-1)}{N}, \quad i = 1, 2, \dots, N
$$

### 4. Numerical Simulation of the Interference Pattern

Using Python, we can simulate the interference pattern and visualize the results. Below is the Python code that computes and visualizes the interference pattern from multiple wave sources:

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
A = 1            # Amplitude of the wave
lambda_ = 1      # Wavelength of the wave
f = 1            # Frequency of the wave
omega = 2 * np.pi * f  # Angular frequency
k = 2 * np.pi / lambda_  # Wave number

# Function to calculate displacement from a single wave source
def wave_source(x, y, x_s, y_s, A, k, omega, t, phi=0):
    r = np.sqrt((x - x_s)**2 + (y - y_s)**2)
    return A * np.cos(k * r - omega * t + phi)

# Function to calculate the total displacement from multiple sources
def total_displacement(x, y, sources, A, k, omega, t):
    displacement = np.zeros_like(x)
    for (x_s, y_s) in sources:
        displacement += wave_source(x, y, x_s, y_s, A, k, omega, t)
    return displacement

# Define the number of vertices (e.g., 5 for a pentagon)
N = 5
angle_step = 2 * np.pi / N
radius = 2  # Distance from the center

# Generate the coordinates of the sources (vertices of a regular polygon)
sources = [(radius * np.cos(i * angle_step), radius * np.sin(i * angle_step)) for i in range(N)]

# Create a grid for the simulation
x_vals = np.linspace(-3, 3, 400)
y_vals = np.linspace(-3, 3, 400)
X, Y = np.meshgrid(x_vals, y_vals)

# Time variable (you can loop over different times to see the dynamic patterns)
t = 0

# Calculate total displacement on the grid
Z = total_displacement(X, Y, sources, A, k, omega, t)

# Plot the interference pattern
plt.figure(figsize=(8, 8))
plt.contourf(X, Y, Z, cmap='jet')
plt.colorbar(label='Displacement (m)')
plt.title(f'Interference Pattern for {N}-Point Sources')
plt.xlabel('X Position (m)')
plt.ylabel('Y Position (m)')
plt.show()
```
![image](https://github.com/user-attachments/assets/99aa2f8b-9c47-41d1-b3fc-ffe6936c51fb)

## 5. Code Explanation

The **`wave_source`** function calculates the displacement at a given point $(x, y)$ due to a wave emitted from a source at $(x_s, y_s)$. This is based on the wave equation.

The **`total_displacement`** function computes the total displacement at each point on the grid by summing the contributions from all wave sources using the superposition principle.

The positions of the sources are determined based on the vertices of the chosen regular polygon (triangle, square, pentagon, etc.).

A **contour plot** is generated to visualize the interference pattern, showing regions of constructive interference (where the waves add up) and destructive interference (where the waves cancel out).

---

## 6. Results

Running the simulation for different polygons will give interference patterns that depend on the number of sources:

- **Equilateral Triangle**: With 3-point sources, the pattern will exhibit symmetry with distinct regions of constructive and destructive interference.
- **Square**: With 4-point sources, the interference pattern will show more intricate regions due to the additional symmetry.
- **Pentagon**: With 5-point sources, the pattern will be more complex, with more vertices influencing the wave interactions.

---

## 7. Conclusion

In this task, we analyzed the interference patterns created by waves emitted from point sources placed at the vertices of a regular polygon. By using the principle of superposition, we were able to understand how waves interact to create constructive and destructive interference patterns. 

This hands-on approach to wave physics provides valuable insight into wave behavior and its real-world applications, such as acoustics, optics, and water wave dynamics.
