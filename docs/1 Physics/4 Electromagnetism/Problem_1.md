# Problem 1
# Simulating the Effects of the Lorentz Force

## 1. Motivation

The Lorentz force is a crucial concept in physics that governs the motion of charged particles in electric and magnetic fields. Mathematically, the Lorentz force is given by:

$$
\mathbf{F} = q (\mathbf{E} + \mathbf{v} \times \mathbf{B})
$$

where:
- $\mathbf{F}$ is the force acting on a particle,
- $q$ is the charge of the particle,
- $\mathbf{E}$ is the electric field,
- $\mathbf{B}$ is the magnetic field,
- $\mathbf{v}$ is the velocity of the particle.

This force plays a key role in a variety of systems such as particle accelerators, mass spectrometers, and plasma confinement devices. Understanding and simulating the effects of this force helps us explore particle trajectories and optimize the design of such systems.

## 2. Task

### 2.1 Exploration of Applications

The Lorentz force governs the behavior of charged particles in several key systems:

- **Particle Accelerators:** The Lorentz force is used to accelerate particles to high speeds within electric and magnetic fields. Systems like cyclotrons and linear accelerators rely on this force to control particle motion and increase their energy.
  
- **Mass Spectrometers:** The magnetic field in a mass spectrometer applies the Lorentz force to charged particles to separate them based on their mass-to-charge ratio.
  
- **Plasma Confinement:** In fusion reactors and magnetic confinement devices (e.g., Tokamaks), the Lorentz force helps contain plasma by guiding the motion of charged particles within a magnetic field.

The electric field $\mathbf{E}$ and magnetic field $\mathbf{B}$ influence the motion of the particle in distinct ways:
- The electric field directly accelerates the particle along its direction.
- The magnetic field causes the particle to move in circular or helical trajectories, depending on the initial velocity.

### 2.2 Simulating Particle Motion

The goal of this task is to implement a simulation to compute and visualize the trajectory of a charged particle under various field configurations. We will simulate three key scenarios:

1. **Uniform Magnetic Field**: The particle experiences only a magnetic field, resulting in a circular motion (if velocity is perpendicular to the magnetic field).
   
2. **Combined Uniform Electric and Magnetic Fields**: The particle is subject to both electric and magnetic fields, leading to helical motion.
   
3. **Crossed Electric and Magnetic Fields**: In this configuration, the electric and magnetic fields are perpendicular to each other, producing drift motion.

We will use numerical methods such as the Euler method or Runge-Kutta method to solve the equations of motion. Below is a Python code that simulates the particle's motion under the effect of the Lorentz force.

### 2.3 Python Code

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.6e-19  # Charge (Coulombs, e.g., electron)
m = 9.1e-31  # Mass (kg, e.g., electron)
dt = 1e-9    # Time step (s)

# Lorentz force function: F = q(E + v x B)
def lorentz_force(r, v, E, B):
    F = q * (E + np.cross(v, B))
    return F / m  # Acceleration (F = ma)

# RK4 solver for position and velocity
def rk4_step(r, v, E, B):
    # Position update
    k1_r = v
    k1_v = lorentz_force(r, v, E, B)
    
    k2_r = v + 0.5 * dt * k1_v
    k2_v = lorentz_force(r + 0.5 * dt * k1_r, v + 0.5 * dt * k1_v, E, B)
    
    k3_r = v + 0.5 * dt * k2_v
    k3_v = lorentz_force(r + 0.5 * dt * k2_r, v + 0.5 * dt * k2_v, E, B)
    
    k4_r = v + dt * k3_v
    k4_v = lorentz_force(r + dt * k3_r, v + dt * k3_v, E, B)
    
    r_new = r + (dt / 6.0) * (k1_r + 2 * k2_r + 2 * k3_r + k4_r)
    v_new = v + (dt / 6.0) * (k1_v + 2 * k2_v + 2 * k3_v + k4_v)
    return r_new, v_new

# Simulation function
def simulate_trajectory(r0, v0, E, B, t_max):
    r = np.array(r0, dtype=float)
    v = np.array(v0, dtype=float)
    positions = [r.copy()]
    velocities = [v.copy()]
    t = 0
    
    while t < t_max:
        r, v = rk4_step(r, v, E, B)
        positions.append(r.copy())
        velocities.append(v.copy())
        t += dt
    
    return np.array(positions), np.array(velocities)

# Plotting function
def plot_trajectory(positions, title, is_3d=True):
    if is_3d:
        fig = plt.figure(figsize=(8, 6))
        ax = fig.add_subplot(111, projection='3d')
        ax.plot(positions[:, 0], positions[:, 1], positions[:, 2])
        ax.set_xlabel('X (m)')
        ax.set_ylabel('Y (m)')
        ax.set_zlabel('Z (m)')
    else:
        plt.figure(figsize=(8, 6))
        plt.plot(positions[:, 0], positions[:, 1])
        plt.xlabel('X (m)')
        plt.ylabel('Y (m)')
    plt.title(title)
    plt.grid(True)
    plt.show()

# Case 1: Uniform Magnetic Field (B along z-axis)
B = np.array([0, 0, 1.0])  # Tesla
E = np.array([0, 0, 0])    # V/m
r0 = [0, 0, 0]             # Initial position
v0 = [1e5, 0, 0]          # Initial velocity (m/s)
t_max = 1e-7               # Simulation time (s)

pos, vel = simulate_trajectory(r0, v0, E, B, t_max)
plot_trajectory(pos, "Uniform Magnetic Field (Circular Motion)")

# Case 2: Combined Electric and Magnetic Fields
E = np.array([0, 1e5, 0])  # Electric field in y-direction
pos, vel = simulate_trajectory(r0, v0, E, B, t_max)
plot_trajectory(pos, "Combined E and B Fields (Helical Motion)")

# Case 3: Crossed Fields (E perpendicular to B)
E = np.array([0, 1e5, 0])  # E in y-direction
B = np.array([0, 0, 1.0])  # B in z-direction
v0 = [1e5, 0, 0]          # Velocity in x-direction
pos, vel = simulate_trajectory(r0, v0, E, B, t_max)
plot_trajectory(pos, "Crossed E and B Fields (Drift Motion)")
```
![image](https://github.com/user-attachments/assets/62abdd36-e8c9-4c0b-b743-da9d5b85fa70)



## 2.4 Explanation of the Code

- **lorentz_force()**: This function computes the Lorentz force acting on the particle at each step, considering both the electric and magnetic fields. The force is calculated using the formula:

  $$
  \mathbf{F} = q (\mathbf{E} + \mathbf{v} \times \mathbf{B})
  $$

  where:
  - $q$ is the charge of the particle,
  - $\mathbf{E}$ is the electric field,
  - $\mathbf{v}$ is the velocity of the particle,
  - $\mathbf{B}$ is the magnetic field.

- **update_position_velocity()**: Using Euler's method, this function updates the particle's position and velocity at each time step. The particle's new position is calculated by adding the product of the velocity and the time step ($\mathbf{r}_{\text{new}} = \mathbf{r} + \mathbf{v} \cdot \Delta t$), while the velocity is updated based on the acceleration, which is derived from the Lorentz force.

- **Initial Conditions**: The particle starts at the origin (position $\mathbf{r_0} = [0, 0, 0]$) with an initial velocity along the x-axis ($\mathbf{v_0} = [1 \times 10^5, 0, 0]$). The magnetic field is set along the z-axis ($\mathbf{B} = [0, 0, 1]$), and the electric field is zero for the magnetic-only case.

- **Trajectory Simulation**: The loop iterates over a predefined number of time steps. At each step, the position and velocity are updated using the Lorentz force and Euler's method. This allows us to track the particle's motion under the influence of the fields.

- **Plotting**: The final trajectory is plotted in 3D space using Matplotlib. The plot visualizes the path of the particle, showing its movement over time in the magnetic field.

## 2.5 Parameter Exploration

To explore the effects of different parameters, we can modify:

- **Field Strengths ($B$ and $E$)**: Changing the magnetic or electric field strengths alters the particle's trajectory. A stronger magnetic field results in a tighter circular path, while a stronger electric field can influence the particle's acceleration and velocity.

- **Initial Velocity ($v_0$)**: The initial velocity direction and magnitude determine the radius of the circular path in the magnetic field. If both electric and magnetic fields are present, the particle will follow a helical motion with the pitch of the helix determined by the relative strengths of the fields and the particle's velocity.

- **Charge and Mass ($q$ and $m$)**: The charge and mass of the particle influence the curvature of the path. Heavier particles (greater mass) have a larger radius of curvature, while lighter particles move more quickly in response to the Lorentz force. The charge also affects the direction of motion, with positively and negatively charged particles moving in opposite directions in the presence of a magnetic field.

## 2.6 Visualization

The simulation can be visualized by plotting the particle's trajectory in 2D or 3D, as shown in the code above. By varying the field strengths and initial conditions, we can observe different types of motion:

- **Circular motion**: A result of only the magnetic field. The particle moves in a circle with a radius determined by the particle's velocity and the magnetic field strength.

- **Helical motion**: A result of both electric and magnetic fields. The particle moves in a helix, with the pitch of the helix determined by the relative strengths of the fields and the particle's velocity.

- **Drift motion**: Occurs when the electric and magnetic fields are crossed. The particle exhibits motion along a straight path with a constant drift velocity in the direction of the electric field.

## 3. Results

Running the simulation for various initial conditions and field configurations will produce the following observations:

- In a **uniform magnetic field**, the particle will move in a circular trajectory, with the radius determined by the particle's velocity and the magnetic field strength.

- When both **electric and magnetic fields** are present, the particle will follow a helical path, with the pitch of the helix determined by the relative strengths of the fields and the particle's velocity.

- In the case of **crossed electric and magnetic fields**, the particle exhibits drift motion, where the velocity components in the electric and magnetic directions result in motion along a straight path with constant drift velocity.

## 4. Conclusion

This simulation provides an intuitive understanding of the effects of the Lorentz force on charged particles. By varying the parameters and visualizing the resulting trajectories, we gain insight into the fundamental principles that govern particle motion in electric and magnetic fields. These principles have practical applications in systems such as particle accelerators, plasma confinement, and mass spectrometers.

The simulation also highlights key phenomena such as:

- **Larmor radius**: The radius of the circular motion of a charged particle in a magnetic field.
- **Drift velocity**: The velocity of the particle along the direction of the crossed fields.

This hands-on approach to the Lorentz force can be extended to more complex scenarios, such as non-uniform magnetic fields, and can be adapted for use in real-world systems.
