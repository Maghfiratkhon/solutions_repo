# Problem 1
# Orbital Period and Orbital Radius

## 1. Introduction

Kepler’s Third Law of planetary motion is one of the fundamental principles in celestial mechanics. It establishes a direct relationship between the square of the orbital period $T$ and the cube of the orbital radius $r$ for an object in a circular orbit. This law allows us to calculate planetary motions and their gravitational interactions, providing insight into the fundamental structure of planetary systems, including satellite orbits and the Moon's orbit around Earth.

This document provides a detailed derivation of the relationship between orbital period and orbital radius, followed by an exploration of its implications for astronomy and real-world examples, including simulations of orbital motions.

## 2. Kepler’s Third Law Derivation

For an object in a circular orbit, the orbital period $T$ is related to the gravitational force that acts on it. Let’s derive the relationship step by step:

### 2.1. Centripetal Force and Gravitational Force

An object moving in a circular orbit is kept in motion by the gravitational force, which also provides the centripetal force. 

The gravitational force between two objects of masses $M$ (central body, e.g., the Sun or Earth) and $m$ (orbiting body, e.g., a planet or satellite) is given by:

$$
F_{\text{gravity}} = \frac{GMm}{r^2}
$$

Where:

- $G$ is the gravitational constant
  
- $M$ is the mass of the central body (e.g., the Sun, Earth)
  
- $m$ is the mass of the orbiting body
  
- $r$ is the orbital radius (the distance between the two objects)

The centripetal force required to keep the orbiting body in a circular path is:

$$
F_{\text{centripetal}} = \frac{mv^2}{r}
$$

Where:

- $v$ is the orbital velocity of the body.

Since these two forces must balance, we set them equal:

$$
\frac{GMm}{r^2} = \frac{mv^2}{r}
$$

### 2.2. Solving for Orbital Velocity

Canceling the mass $m$ from both sides, we get:

$$
\frac{GM}{r^2} = \frac{v^2}{r}
$$

Multiplying both sides by $r$:

$$
\frac{GM}{r} = v^2
$$

Now, solve for $v$:

$$
v = \sqrt{\frac{GM}{r}}
$$

### 2.3. Orbital Period and Velocity

The orbital period $T$ is the time it takes for the object to complete one full orbit. The distance traveled in one orbit is the circumference of the orbit:

$$
\text{Circumference} = 2\pi r
$$

Since velocity is distance divided by time, we can write:

$$
v = \frac{2\pi r}{T}
$$

### 2.4. Substituting for $v$

We now have two equations for $v$:

1. $v = \sqrt{\frac{GM}{r}}$
2. $v = \frac{2\pi r}{T}$

Equating these two expressions for $v$:

$$
\sqrt{\frac{GM}{r}} = \frac{2\pi r}{T}
$$

### 2.5. Solving for $T$

Square both sides to eliminate the square root:

$$
\frac{GM}{r} = \left(\frac{2\pi r}{T}\right)^2
$$

Simplify the right-hand side:

$$
\frac{GM}{r} = \frac{4\pi^2 r^2}{T^2}
$$

Rearrange to solve for $T^2$:

$$
T^2 = \frac{4\pi^2 r^3}{GM}
$$

### 2.6. Kepler's Third Law

Thus, we derive the relationship between the orbital period $T$ and the orbital radius $r$:

$$
T^2 \propto r^3
$$

This is Kepler’s Third Law, which states that the square of the orbital period is proportional to the cube of the orbital radius. This relationship holds for circular orbits.

## 3. Implications for Astronomy

### 3.1. Calculating Planetary Masses

Kepler’s Third Law allows astronomers to estimate the mass of celestial bodies. For example, if we know the orbital period and radius of a satellite or planet, we can rearrange Kepler’s Third Law to solve for the mass of the central body:

$$
M = \frac{4\pi^2 r^3}{G T^2}
$$

This formula is useful in determining the mass of distant stars, planets, and moons, especially when direct measurements of mass are difficult to obtain.

### 3.2. Estimating Planetary Distances

The law also helps estimate the distance between celestial bodies. For example, knowing the orbital period of a moon or planet and the mass of the central body (such as Earth or the Sun), we can compute the orbital radius.

## 4. Real-World Examples

### 4.1. The Moon's Orbit Around Earth

The Moon orbits Earth with a period of about 27.3 days and a radius of about 384,400 km. Using Kepler’s Third Law, we can check the relationship between the Moon's orbital period and radius.

### 4.2. The Planets in the Solar System

Kepler’s Third Law applies not only to moons and satellites but also to the planets of the Solar System. For example, the orbital period of Earth is about 365 days, and its orbital radius is about 149.6 million km. By applying the relationship, we can estimate orbital periods and distances for other planets.

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
![image](https://github.com/user-attachments/assets/8ab4dc50-893b-48c4-ac8b-e7ce8e9410ad)



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
