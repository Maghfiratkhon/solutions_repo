# Problem 1
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # gravitational acceleration (m/s^2)
v0 = 20   # initial velocity (m/s)
theta_range = np.linspace(0, 90, 100)  # angles in degrees

# Derivation of the range equation:
# The equations of motion for projectile motion are:
# Horizontal motion: x = v0 * cos(theta) * t
# Vertical motion: y = v0 * sin(theta) * t - (1/2) * g * t^2
# The total time of flight is derived from setting y = 0:
# t_total = (2 * v0 * sin(theta)) / g
# The range is given by: R = v0 * cos(theta) * t_total
# Substituting t_total, we get:
# R = (v0^2 * sin(2 * theta)) / g

# Function to calculate range
def projectile_range(v0, theta, g=9.81):
    """Computes the range of a projectile for a given initial velocity and angle."""
    theta_rad = np.radians(theta)  # Convert angle to radians
    return (v0**2 * np.sin(2 * theta_rad)) / g  # Range formula

# Compute ranges for different angles
ranges = projectile_range(v0, theta_range, g)

# Plot results
plt.figure(figsize=(8, 5))
plt.plot(theta_range, ranges, label=f'Initial Velocity = {v0} m/s', color='b')
plt.xlabel("Angle of Projection (degrees)")
plt.ylabel("Range (meters)")
plt.title("Projectile Range as a Function of Angle of Projection")
plt.legend()
plt.grid()
plt.show()

# Observations:
# - The range is maximum at 45 degrees.
# - The trajectory is symmetric around 45 degrees.
# - Increasing initial velocity increases the range quadratically.


