Problem #1

# 1. Investigating the Range as a Function of the Angle of Projection

## 1.1 Theoretical Foundation

Projectile motion is a two-dimensional motion governed by Newtonian mechanics. It consists of horizontal and vertical components, which evolve independently under uniform acceleration due to gravity. The range of a projectile is given by:

$$
R = \frac{v_0^2 \sin(2\theta)}{g}
$$

where:
- $$ R $$
 is the horizontal range,
- $$ v_0 $$
is the initial velocity,
- $$ \theta $$ 
is the angle of projection,
- $$ g $$
 is the gravitational acceleration (9.81 m/s² on Earth).

### 1.2 Derivation of the Range Equation

The horizontal and vertical displacements of the projectile as a function of time \(t\) are:

$$
 x = v_0 \cos(\theta) t,
$$
$$
 y = v_0 \sin(\theta) t - \frac{1}{2} g t^2.
$$

The total time of flight \(T\) is found by setting \(y=0\) and solving for \(t\):

$$
T = \frac{2 v_0 \sin(\theta)}{g}.
$$

Since the projectile lands back at its original height, we substitute \(T\) into the horizontal displacement equation to obtain:

$$
R = v_0 \cos(\theta) \times \frac{2 v_0 \sin(\theta)}{g}.
$$

Using the trigonometric identity 
$$ 2 \sin(\theta) \cos(\theta) = \sin(2\theta) $$ 
 we derive the final range formula:

$$
R = \frac{v_0^2 \sin(2\theta)}{g}.
$$

## 2. Analysis of the Range

The range is a function of the projection angle and initial velocity. Notably:
- The maximum range occurs at 
$$ \theta = 45^\circ $$.
- The range is symmetric about 
$$ \theta = 45^\circ $$, meaning angles equidistant from 45° yield the same range (e.g., 30° and 60°).
- Increasing \(v_0\) results in a quadratic increase in range, while an increase in \(g\) reduces the range.

Additionally, in practical situations where air resistance exists, the theoretical prediction may differ from actual results, making real-world considerations essential.

## 3. Implementation

Below is a Python script to compute and visualize the range as a function of the projection angle.

```python

def projectile_range(theta, v0, g=9.81):
    """
    Computes the range of a projectile given the launch angle (theta),
    initial velocity (v0), and gravitational acceleration (g).
    """
    theta_rad = np.radians(theta)
    return (v0**2 * np.sin(2 * theta_rad)) / g

# Parameters
v0 = 50  # Initial velocity in m/s
theta_values = np.linspace(0, 90, 100)  # Angle range from 0 to 90 degrees
ranges = [projectile_range(theta, v0) for theta in theta_values]

# Plotting
plt.figure(figsize=(10, 5))
plt.plot(theta_values, ranges, label=f'Initial Velocity = {v0} m/s')
plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (meters)')
plt.title('Projectile Range as a Function of Angle of Projection')
plt.legend()
plt.grid()
plt.show()
```
## 4.  Practical Applications

Projectile motion is fundamental in many real-world applications, including:
- **Sports physics:** Determining optimal angles for maximum distance in soccer, golf, or javelin throws.
- **Engineering:** Designing artillery, missile trajectories, and launch mechanisms.
- **Astronomy:** Calculating planetary lander descent paths and space exploration projections.
- **Video games & simulations:** Creating realistic physics-based animations.

## 5. Limitations and Future Considerations

While the idealized model provides valuable insights, real-world conditions introduce additional complexities:
- **Air resistance:** The presence of drag significantly reduces range and modifies the optimal launch angle.
- **Varying gravity:** On planets with different gravitational strengths, the projectile behavior changes accordingly.
- **Uneven terrain:** A non-level landing surface alters the computed range.
- **Wind effects:** External forces can influence trajectory, making real-world predictions more complex.

### 5.1  Future Improvements
- Incorporate **air resistance** to analyze realistic projectile motion.
- Extend the model to **uneven terrains** with different elevations.
- Introduce **spin effects** to study Magnus forces in sports applications.

## 6. Conclusion

This study demonstrates the dependence of projectile range on the angle of projection, with a clear maximum occurring at 45 degrees. The derived mathematical framework provides a fundamental understanding of projectile motion, while the implemented Python simulation offers a visual and computational verification of these principles. 

However, real-world deviations from this model highlight the importance of considering external forces such as air resistance and wind. Future studies incorporating these factors will provide more accurate and applicable results for various scientific and engineering domains. Understanding projectile motion remains crucial for fields ranging from sports science to aerospace engineering, emphasizing the enduring relevance of classical physics in modern applications.
