# Problem 1
# **Projectile Motion Analysis**

## **Introduction**
Projectile motion is a fundamental concept in physics that describes the motion of an object launched into the air, subject to gravitational acceleration. It is widely used in physics, engineering, and real-world applications such as ballistics, sports, and space exploration. 

This analysis explores how the range of a projectile depends on the angle of projection. We derive the governing equations and implement a Python script to visualize the relationship between range and angle.

---
## **Governing Equations**
Projectile motion is described using kinematic equations that govern horizontal and vertical displacement.

### **1. Horizontal Motion**
The horizontal displacement \( x \) is given by:
\[
 x = v_0 \cos(\theta) t
\]
Since there is no horizontal acceleration (ignoring air resistance), the velocity in this direction remains constant.

### **2. Vertical Motion**
The vertical displacement \( y \) is given by:
\[
 y = v_0 \sin(\theta) t - \frac{1}{2} g t^2
\]
Gravity acts downward, causing the projectile to reach a maximum height before descending.

### **3. Time of Flight**
To find the total time the projectile stays in the air, we set the vertical displacement to zero when it returns to the initial launch height:
\[
 0 = v_0 \sin(\theta) t - \frac{1}{2} g t^2
\]
Factoring out \( t \):
\[
 t \left( v_0 \sin(\theta) - \frac{1}{2} g t \right) = 0
\]
Solving for \( t \), we get two solutions:
\[
 t = 0 \quad \text{(initial launch)}
\]
\[
 t = \frac{2 v_0 \sin(\theta)}{g} \quad \text{(total flight time)}
\]

### **4. Range Equation**
The range \( R \) is the total horizontal displacement when the projectile returns to the launch height:
\[
 R = v_0 \cos(\theta) t_{total}
\]
Substituting \( t_{total} = \frac{2 v_0 \sin(\theta)}{g} \):
\[
 R = v_0 \cos(\theta) \times \frac{2 v_0 \sin(\theta)}{g}
\]
Using the trigonometric identity \( 2 \sin(\theta) \cos(\theta) = \sin(2\theta) \), we simplify:
\[
 R = \frac{v_0^2 \sin(2\theta)}{g}
\]
This equation shows that the range is maximized when \( \theta = 45^\circ \), where \( \sin(90^\circ) = 1 \).

---
## **Implementation in Python**
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

---
## **Observations**
- The range is maximum at **45 degrees**.
- The trajectory is symmetric around **45 degrees**.
- Increasing the initial velocity increases the range **quadratically**.
- **Real-world factors** such as air resistance reduce the actual range compared to the idealized model.

---
## **Conclusion**
This analysis demonstrates the dependence of projectile range on the angle of projection. By adjusting parameters like initial velocity and gravity, we can extend this model to more complex scenarios, such as projectiles launched on different terrains or in the presence of air resistance.
