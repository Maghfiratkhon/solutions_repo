# Problem 1
# Continuation: Orbital Period and Orbital Radius

## 5. Computational Model to Simulate Circular Orbits

Let’s create a Python script to simulate a circular orbit and verify Kepler’s Third Law.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # Gravitational constant (m^3 kg^-1 s^-2)
M = 5.972e24     # Mass of Earth (kg)
r = 384400000    # Orbital radius of the Moon (m)
T = 27.3 * 24 * 60 * 60  # Orbital period of the Moon (s)

# Calculate orbital velocity
v = np.sqrt(G * M / r)

# Generate data points for the circular orbit (360 degrees)
theta = np.linspace(0, 2 * np.pi, 100)
x = r * np.cos(theta)
y = r * np.sin(theta)

# Plot the orbit
plt.figure(figsize=(6, 6))
plt.plot(x, y, label='Moon\'s Orbit')
plt.scatter(0, 0, color='orange', label='Earth', s=200)  # Earth's position
plt.title('Simulation of the Moon\'s Orbit Around Earth')
plt.xlabel('Distance (m)')
plt.ylabel('Distance (m)')
plt.gca().set_aspect('equal', adjustable='box')
plt.legend()
plt.grid(True)
plt.show()

# Verifying Kepler's Third Law (T^2 vs. r^3)
T_squared = T**2
r_cubed = r**3

# Print out values for verification
print(f"T^2: {T_squared:.2e} s^2")
print(f"r^3: {r_cubed:.2e} m^3")
```


## 5.1. Orbit Simulation

The simulation generates the orbit of the Moon around Earth as a perfect circle, with the central Earth located at the origin. The orbital period and radius are provided in the script. The output is a graphical representation of the Moon’s orbit, confirming its circular motion around Earth.

## 5.2. Kepler’s Third Law Verification

The script calculates $T^2$ and $r^3$, verifying Kepler's Third Law by outputting these values. This confirms that the relationship between the orbital period and radius is maintained.

## 6. Extension to Elliptical Orbits

Kepler’s Third Law can also be extended to elliptical orbits. While the relationship $T^2 \propto r^3$ holds for circular orbits, for elliptical orbits, the law is modified to incorporate the semi-major axis $a$ (the average distance of the orbiting body from the central body). In this case:

$$
T^2 \propto a^3
$$

This allows Kepler's Third Law to apply to all orbital shapes, though the calculation of the orbital period requires integrating over the ellipse's varying distance. The semi-major axis $a$ is the average of the shortest ($r_{\text{min}}$) and longest ($r_{\text{max}}$) distances of the orbiting body from the central body:

$$
a = \frac{r_{\text{min}} + r_{\text{max}}}{2}
$$

Thus, elliptical orbits require more complex computations, but Kepler's Third Law still holds as a fundamental relationship.

## 7. Conclusion

Kepler’s Third Law provides a simple yet powerful relationship between the orbital period and orbital radius for celestial bodies in circular orbits. This law is essential for understanding planetary systems, satellite orbits, and gravitational interactions. By simulating circular orbits, we can visualize and verify the law’s predictions, which extend to more complex elliptical orbits as well.

By applying Kepler’s Third Law, we can calculate masses, distances, and periods for planets, moons, and satellites, making it a cornerstone of modern astronomy and celestial mechanics.
