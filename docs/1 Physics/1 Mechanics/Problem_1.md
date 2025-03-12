# Investigating the Range as a Function of the Angle of Projection

Projectile motion is a cornerstone of classical mechanics, offering a blend of simplicity and depth that makes it an ideal subject for exploration. In this investigation, we’ll derive the equations governing projectile motion, analyze how the horizontal range depends on the angle of projection, explore real-world applications, and implement a computational tool to visualize the results. Let’s embark on this journey through physics, mathematics, and computation.

## 1. Theoretical Foundation

### Derivation of the Governing Equations

Projectile motion occurs when an object is launched with an initial velocity and moves under the influence of gravity alone (neglecting air resistance for now). We define the initial velocity \( v_0 \) at an angle \( \theta \) to the horizontal, with components:

- Horizontal: \( v_{0x} = v_0 \cos\theta \)
- Vertical: \( v_{0y} = v_0 \sin\theta \)

Gravity acts downward with acceleration \( g \) (typically \( 9.8 \, \text{m/s}^2 \) on Earth), affecting only the vertical motion. We assume the launch point is at the origin \((x_0, y_0) = (0, 0)\) unless specified otherwise.

#### Horizontal Motion
Since no forces act horizontally:
$$ \frac{d^2 x}{dt^2} = 0 $$
Integrating once:
$$ \frac{dx}{dt} = v_{0x} = v_0 \cos\theta $$
Integrating again:
$$ x(t) = v_0 \cos\theta \cdot t $$

#### Vertical Motion
Gravity provides a constant acceleration:
$$ \frac{d^2 y}{dt^2} = -g $$
First integration (initial velocity \( v_{0y} \)):
$$ \frac{dy}{dt} = v_{0y} - g t = v_0 \sin\theta - g t $$
Second integration:
$$ y(t) = v_0 \sin\theta \cdot t - \frac{1}{2} g t^2 $$

These equations form the parametric description of the projectile’s trajectory. The path is a parabola, as we can eliminate \( t \) from the equations:
$$ t = \frac{x}{v_0 \cos\theta} $$
Substitute into the vertical equation:
$$ y = v_0 \sin\theta \cdot \frac{x}{v_0 \cos\theta} - \frac{1}{2} g \left( \frac{x}{v_0 \cos\theta} \right)^2 $$
$$ y = x \tan\theta - \frac{g x^2}{2 v_0^2 \cos^2\theta} $$

This is the equation of a parabola, confirming the trajectory’s shape.

### Family of Solutions
The parameters \( v_0 \), \( \theta \), and \( g \) define a family of solutions. Varying \( v_0 \) scales the size of the parabola, \( \theta \) adjusts its tilt, and \( g \) (e.g., different on the Moon) alters the curvature. Launch height \( h \) (if \( y_0 \neq 0 \)) shifts the parabola vertically, adding complexity to the range calculation.

## 2. Analysis of the Range

### Range Derivation
The range \( R \) is the horizontal distance traveled when the projectile returns to \( y = 0 \). Set \( y(t) = 0 \):
$$ 0 = v_0 \sin\theta \cdot t - \frac{1}{2} g t^2 $$
Factor out \( t \):
$$ t \left( v_0 \sin\theta - \frac{1}{2} g t \right) = 0 $$
Solutions:
- \( t = 0 \) (launch)
- \( t = \frac{2 v_0 \sin\theta}{g} \) (landing)

Substitute into the horizontal equation:
$$ R = x\left( \frac{2 v_0 \sin\theta}{g} \right) = v_0 \cos\theta \cdot \frac{2 v_0 \sin\theta}{g} $$
Using the identity \( \sin 2\theta = 2 \sin\theta \cos\theta \):
$$ R = \frac{v_0^2 \sin 2\theta}{g} $$

### Dependence on Angle
- **Maximum Range**: \( R \) is maximized when \( \sin 2\theta = 1 \), i.e., \( 2\theta = 90^\circ \), so \( \theta = 45^\circ \). Then:
  $$ R_{\text{max}} = \frac{v_0^2}{g} $$
- **Symmetry**: \( R(\theta) = R(90^\circ - \theta) \) because \( \sin 2\theta = \sin (180^\circ - 2\theta) \). E.g., \( \theta = 30^\circ \) and \( 60^\circ \) yield the same range.
- **Limits**: At \( \theta = 0^\circ \) or \( 90^\circ \), \( \sin 2\theta = 0 \), so \( R = 0 \).

### Influence of Parameters
- **Initial Velocity (\( v_0 \))**: \( R \propto v_0^2 \), a quadratic relationship. Doubling \( v_0 \) quadruples the range.
- **Gravity (\( g \))**: \( R \propto 1/g \). On the Moon (\( g \approx 1.62 \, \text{m/s}^2 \)), the range is about 6 times that on Earth.
- **Launch Height**: If \( h > 0 \), the range increases due to longer flight time. The quadratic equation for \( y = -h \) must be solved, complicating the formula.

## 3. Practical Applications

This model applies to:
- **Sports**: Optimizing the launch angle in basketball (e.g., jump shots) or golf (drives). The ideal \( 45^\circ \) shifts with height differences or air resistance.
- **Engineering**: Artillery design requires adjusting for terrain and drag.
- **Astrophysics**: Trajectories of objects in varying gravitational fields (e.g., comets).

For uneven terrain (\( y_{\text{land}} \neq 0 \)) or air resistance (\( F = -k v \)), the differential equations become nonlinear, often requiring numerical solutions.

## 4. Implementation

Here’s a Python script using NumPy and Matplotlib to simulate and visualize the range versus angle:

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
v0 = 20.0  # initial velocity (m/s)
g = 9.8    # gravity (m/s^2)
angles_deg = np.linspace(0, 90, 91)  # angles from 0 to 90 degrees
angles_rad = np.radians(angles_deg)

# Range function
def range_projectile(v0, theta, g):
    return (v0**2 * np.sin(2 * theta)) / g

# Compute ranges
ranges = range_projectile(v0, angles_rad, g)

# Plot
plt.figure(figsize=(10, 6))
plt.plot(angles_deg, ranges, label=f'v0 = {v0} m/s, g = {g} m/s²')
plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (meters)')
plt.title('Range vs. Angle of Projection')
plt.grid(True)
plt.legend()
plt.show()

# Vary v0 and g
v0_values = [10, 20, 30]
g_values = [9.8, 1.62]  # Earth and Moon

plt.figure(figsize=(10, 6))
for v0 in v0_values:
    for g in g_values:
        ranges = range_projectile(v0, angles_rad, g)
        plt.plot(angles_deg, ranges, label=f'v0 = {v0} m/s, g = {g} m/s²')
plt.xlabel('Angle (degrees)')
plt.ylabel('Range (m)')
plt.title('Range for Different v0 and g')
plt.legend()
plt.grid(True)
plt.show()