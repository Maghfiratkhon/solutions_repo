# Problem 2
# 1. Escape Velocities and Cosmic Velocities

## 1.1 Motivation

The concept of escape velocity is fundamental in astrophysics and space exploration. It determines the velocity required for an object to overcome a celestial body's gravitational pull. Extending this, the first, second, and third cosmic velocities define the conditions for orbiting, escaping a planet, and escaping a star system, respectively. Understanding these velocities is crucial for launching satellites, space missions, and potential interstellar travel.

## 2. Definitions

### 2.1 First Cosmic Velocity (Orbital Velocity)
The minimum velocity required for an object to maintain a stable circular orbit around a celestial body.

$$
v_1 = \sqrt{\frac{GM}{R}}
$$

where:

-  $G$ is the gravitational constant ($6.674 \times 10^{-11} m^3 kg^{-1} s^{-2}$)

-  $M$ is the mass of the celestial body

-  $R$ is the radius of the celestial body

### 2.2 Second Cosmic Velocity (Escape Velocity)
The velocity required for an object to escape a celestial body's gravitational influence without further propulsion.

$$
v_2 = \sqrt{\frac{2GM}{R}} = \sqrt{2} v_1
$$

### 2.3 Third Cosmic Velocity (Interstellar Escape Velocity)
The velocity required to escape the gravitational pull of a star system, such as the Solar System.

$$
v_3 = \sqrt{\frac{2GM_{\odot}}{R}}
$$

where $M_{\odot}$ is the mass of the Sun and $R$ is the distance from the Sun.

## 3. Mathematical Analysis and Parameters

The velocities depend on:

-  The mass of the celestial body

-  The radius from the center of the celestial body

-  Gravitational constant $G$

These values vary for different celestial bodies like Earth, Mars, and Jupiter, affecting their respective cosmic velocities.

## 4. Python Implementation

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.674e-11  # Gravitational constant in m^3/kg/s^2
bodies = {
    "Earth": {"mass": 5.972e24, "radius": 6371e3},
    "Mars": {"mass": 6.417e23, "radius": 3389e3},
    "Jupiter": {"mass": 1.898e27, "radius": 69911e3}
}

# Function to calculate velocities
def cosmic_velocities(mass, radius):
    v1 = np.sqrt(G * mass / radius)  # First cosmic velocity
    v2 = np.sqrt(2) * v1  # Second cosmic velocity
    return v1, v2

# Compute velocities
velocities = {body: cosmic_velocities(data["mass"], data["radius"]) for body, data in bodies.items()}

# Visualization
labels, v1_vals, v2_vals = zip(*[(body, v[0], v[1]) for body, v in velocities.items()])
x = np.arange(len(labels))
width = 0.3
fig, ax = plt.subplots()
ax.bar(x - width/2, v1_vals, width, label='First Cosmic Velocity')
ax.bar(x + width/2, v2_vals, width, label='Second Cosmic Velocity')
ax.set_ylabel('Velocity (m/s)')
ax.set_title('Cosmic Velocities for Different Celestial Bodies')
ax.set_xticks(x)
ax.set_xticklabels(labels)
ax.legend()
plt.show()
```

## 5. Discussion

### 5.1 Importance in Space Exploration

-  The first cosmic velocity is crucial for satellites to remain in orbit.

-  The second cosmic velocity enables missions to other planets and deep space.

-  The third cosmic velocity allows interstellar travel and potential exploration beyond the Solar System.

### 5.2 Challenges

-  Achieving these velocities requires significant energy and propulsion technology.

-  Interstellar travel is constrained by fuel, life support, and current propulsion limitations.

## 6. Conclusion

Understanding cosmic velocities is vital for space missions and future interstellar endeavors. With advancements in propulsion technology, we may one day achieve the speeds necessary for deep space exploration beyond our Solar System.
