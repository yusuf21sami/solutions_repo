# Problem 1

# Investigating the Range as a Function of the Angle of Projection

## 1. Theoretical Foundation

### Derivation of Governing Equations

Let's consider a projectile launched from the origin $(0, 0)$ with an initial velocity $v_0$ at an angle $\theta$ with respect to the horizontal. We'll neglect air resistance and assume constant gravitational acceleration $g$ acting downwards.

The initial velocity components are:

* $v_{0x} = v_0 \cos(\theta)$
* $v_{0y} = v_0 \sin(\theta)$

The acceleration components are:

* $a_x = 0$
* $a_y = -g$

Using the kinematic equations, we can find the velocity and position components as a function of time $t$:

* $v_x(t) = v_{0x} = v_0 \cos(\theta)$
* $v_y(t) = v_{0y} - gt = v_0 \sin(\theta) - gt$

* $x(t) = v_{0x}t = v_0 \cos(\theta)t$
* $y(t) = v_{0y}t - \frac{1}{2}gt^2 = v_0 \sin(\theta)t - \frac{1}{2}gt^2$

### Family of Solutions

By varying the initial velocity $v_0$ and the launch angle $\theta$, we generate a family of parabolic trajectories. Each set of $(v_0, \theta)$ defines a unique trajectory.

## 2. Analysis of the Range

### Range Equation

To find the range $R$, we need to determine the time $T$ when the projectile lands ($y(T) = 0$).

$0 = v_0 \sin(\theta)T - \frac{1}{2}gT^2$

$T(v_0 \sin(\theta) - \frac{1}{2}gT) = 0$

$T = 0$ (initial time) or $T = \frac{2v_0 \sin(\theta)}{g}$ (time of flight)

The range $R$ is the horizontal distance traveled during this time:

$R = x(T) = v_0 \cos(\theta)T = v_0 \cos(\theta) \frac{2v_0 \sin(\theta)}{g}$

Using the trigonometric identity $2\sin(\theta)\cos(\theta) = \sin(2\theta)$, we get:

$R = \frac{v_0^2 \sin(2\theta)}{g}$

### Influence of Parameters

* **Initial Velocity ($v_0$)**: The range is proportional to the square of the initial velocity. Higher velocities result in significantly larger ranges.
* **Launch Angle ($\theta$)**: The range is proportional to $\sin(2\theta)$. The maximum range occurs when $\sin(2\theta) = 1$, which means $2\theta = 90^\circ$ or $\theta = 45^\circ$.
* **Gravitational Acceleration ($g$)**: The range is inversely proportional to $g$. On planets with lower gravity, the range will be greater.

## 3. Practical Applications

* **Sports**: Optimizing the launch angle in sports like golf, baseball, and football to achieve maximum distance.
* **Military**: Calculating the trajectory of artillery shells and rockets.
* **Engineering**: Designing sprinkler systems, fireworks displays, and other systems involving projectiles.
* **Astrophysics**: Calculating the trajectories of celestial bodies.
* **Uneven Terrain**: By adjusting the landing height, the range equations can be modified to model projectiles landing on slopes.
* **Air Resistance**: Adding a drag term to the differential equations can model the effects of air resistance. This complicates the equations significantly, usually requiring numerical solutions.

## 4. Implementation

```python
import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, theta, g=9.81):
    """Calculates the range of a projectile."""
    theta_rad = np.radians(theta)
    return (v0**2 * np.sin(2 * theta_rad)) / g

def plot_range_vs_angle(v0_values, g=9.81):
    """Plots range vs. angle for given initial velocities."""
    angles = np.linspace(0, 90, 100)
    plt.figure(figsize=(10, 6))
    for v0 in v0_values:
        ranges = projectile_range(v0, angles, g)
        plt.plot(angles, ranges, label=f'v0 = {v0} m/s')
    plt.xlabel('Launch Angle (degrees)')
    plt.ylabel('Range (meters)')
    plt.title('Projectile Range vs. Launch Angle')
    plt.legend()
    plt.grid(True)
    plt.show()

# Example usage
v0_values = [10, 20, 30]
plot_range_vs_angle(v0_values)

# Example with different gravity.
v0_values = [20]
plot_range_vs_angle(v0_values, g=1.62) # Moon gravity.
