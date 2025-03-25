# Problem 1
# 1. Interference Patterns on a Water Surface

## 1.1 Motivation

Interference occurs when waves from different sources overlap, creating new patterns. On a water surface, this can be easily observed when ripples from different points meet, forming distinctive interference patterns. These patterns can show us how waves combine in different ways, either reinforcing each other or canceling out.

Studying these patterns helps us understand wave behavior in a simple, visual way. It also allows us to explore important concepts like the relationship between wave phase and the effects of multiple sources. This task offers a hands-on approach to learning about wave interactions and their real-world applications, making it an interesting and engaging way to dive into wave physics.

## 1.2 Task

A circular wave on the water surface, emanating from a point source located at $(x_0, y_0)$, can be described by the Single Disturbance equation:

$$
\eta(x, y, t) = A \cos(k r - \omega t + \phi)
$$

where:

- $\eta(x, y, t)$ is the displacement of the water surface at point $(x, y)$ and time $t$,
- $A$ is the amplitude of the wave,
- $k$ is the wave number, related to the wavelength $\lambda$ ($k = \frac{2\pi}{\lambda}$),
- $\omega$ is the angular frequency, related to the frequency $f$ ($\omega = 2\pi f$),
- $r$ is the distance from the source to the point $(x, y)$,
- $\phi$ is the initial phase.

Your task is to analyze the interference patterns formed on the water surface due to the superposition of waves emitted from point sources placed at the vertices of a chosen regular polygon.

---

## 2. Problem Statement

You need to:

### 2.1 Select a Regular Polygon

Choose a regular polygon (e.g., equilateral triangle, square, regular pentagon).

### 2.2 Position the Sources

Place point wave sources at the vertices of the selected polygon.

### 2.3 Wave Equations

Write the equations describing the waves emitted from each source, considering their respective positions.

### 2.4 Superposition of Waves

Apply the principle of superposition by summing the wave displacements at each point on the water surface:

$$
\eta_{total}(x, y, t) = \sum_{i=1}^{N} \eta_i(x, y, t)
$$

where $N$ is the number of sources (vertices of the polygon).

### 2.5 Analyze Interference Patterns

Examine the resulting displacement $\eta_{total}(x, y, t)$ as a function of position $(x, y)$ and time $t$. Identify regions of constructive interference (wave amplification) and destructive interference (wave cancellation).

### 2.6 Visualization

Present your findings graphically, illustrating the interference patterns for the chosen regular polygon.

---

## 3. Considerations

- Assume all sources emit waves with the same amplitude $A$, wavelength $\lambda$, and frequency $f$.
- The waves are coherent, maintaining a constant phase difference.
- You may use simulation and visualization tools such as Python (with libraries like Matplotlib), or other graphical software to aid in your analysis.

---

## 4. Deliverables

1. A Markdown document with Python script or notebook implementing the simulations.
2. A detailed explanation of the interference patterns observed for the chosen regular polygon with the goal of understanding wave superposition.
3. Graphical representations of the water surface showing constructive and destructive interference regions.

---

## 5. Numerical Simulation

The simulation can be carried out using Python, leveraging libraries such as NumPy for numerical computation and Matplotlib for graphical visualization. Below is an outline of the code to simulate and visualize the interference patterns:

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
## 5.1 Explanation of the Code

The function `wave_source(x, y, x_s, y_s, A, k, omega, t)` calculates the displacement at point $(x, y)$ due to a wave emitted from a source at $(x_s, y_s)$.

The `total_displacement(x, y, sources, A, k, omega, t)` function sums the contributions of all wave sources using the superposition principle.

The simulation generates a grid of points on the water surface and calculates the resulting displacement at each point.

A contour plot is generated to visualize the interference patterns.

---

# 6. Conclusion

In this task, we explored the interference patterns formed by the superposition of waves emitted from point sources placed at the vertices of a regular polygon. By understanding wave interactions and visualizing the resulting interference, we gained insight into wave behavior and the principle of superposition. This hands-on approach to wave physics helps demonstrate important concepts such as constructive and destructive interference and the impact of multiple wave sources on the formation of interference patterns.
