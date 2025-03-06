# Problem 1
# Projectile Motion Analysis

## Introduction
Projectile motion is a fundamental concept in physics that describes the motion of an object thrown into the air under the influence of gravity. This analysis investigates how the range of a projectile depends on the angle of projection.

## Governing Equations
The motion of a projectile can be analyzed using the following kinematic equations:

### Horizontal Motion
\[
 x = v_0 \cos(\theta) t
\]

### Vertical Motion
\[
 y = v_0 \sin(\theta) t - \frac{1}{2} g t^2
\]

### Time of Flight
\[
 t_{total} = \frac{2 v_0 \sin(\theta)}{g}
\]

### Range Equation
\[
 R = \frac{v_0^2 \sin(2\theta)}{g}
\]
This equation shows that the range is maximized when \( \theta = 45^\circ \).

## Implementation in Python
The following Python script computes and visualizes the projectile range for different angles of projection.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # Gravitational acceleration (m/s^2)
v0 = 20   # Initial velocity (m/s)
theta_range = np.linspace(0, 90, 100)  # Angles in degrees

# Function to calculate range
def projectile_range(v0, theta, g=9.81):
    """
    Computes the range of a projectile for a given initial velocity and angle.
    
    Parameters:
    v0 : float - Initial velocity (m/s)
    theta : float - Launch angle (degrees)
    g : float - Gravitational acceleration (default = 9.81 m/s^2)
    
    Returns:
    float - The computed range of the projectile
    """
    theta_rad = np.radians(theta)  # Convert angle to radians
    return (v0**2 * np.sin(2 * theta_rad)) / g  # Range formula

# Compute ranges for different angles
ranges = projectile_range(v0, theta_range, g)

# Plot results
plt.figure(figsize=(8, 5))
plt.plot(theta_range, ranges, label=f'Initial Velocity = {v0} m/s', color='b')
plt.xlabel("Angle of Projection (degrees)", fontsize=12)
plt.ylabel("Range (meters)", fontsize=12)
plt.title("Projectile Range as a Function of Angle of Projection", fontsize=14)
plt.legend()
plt.grid(True, linestyle='--', alpha=0.6)
plt.show()
```

## Observations
- The range is maximum at 45 degrees.
- The trajectory is symmetric around 45 degrees.
- Increasing initial velocity increases the range quadratically.
- This model ignores air resistance, which would reduce the actual range in real-world scenarios.

## Conclusion
This analysis demonstrates the dependence of projectile range on the angle of projection. By adjusting parameters like initial velocity and gravity, we can extend this model to more complex scenarios, such as projectiles on different terrains or in the presence of air resistance.

