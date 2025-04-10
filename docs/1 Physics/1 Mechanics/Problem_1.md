# Problem 1

# Investigating the Range as a Function of the Angle of Projection

## Theoretical Foundation

We begin by considering the motion of a projectile under the influence of gravity. The motion in both the horizontal and vertical directions can be described using the following equations:

### Equations of Motion

For a projectile launched with an initial velocity \( v_0 \) at an angle \( \theta \) to the horizontal, we can break the velocity into horizontal and vertical components:

- Horizontal velocity component: 
  $$ v_{0x} = v_0 \cos(\theta) $$

- Vertical velocity component: 
  $$ v_{0y} = v_0 \sin(\theta) $$

The equations of motion in the horizontal (\(x\)) and vertical (\(y\)) directions are given by:

1. Horizontal motion:
   $$ x(t) = v_{0x} t = v_0 \cos(\theta) t $$

2. Vertical motion:
   $$ y(t) = v_{0y} t - \frac{1}{2} g t^2 = v_0 \sin(\theta) t - \frac{1}{2} g t^2 $$

Where:
- \( g \) is the acceleration due to gravity
- \( t \) is the time of flight

### Time of Flight

To find the time of flight \( T \), we set the vertical displacement \( y(t) \) equal to zero when the projectile lands:

$$ 0 = v_0 \sin(\theta) T - \frac{1}{2} g T^2 $$

Solving for \( T \), we get:

$$ T = \frac{2 v_0 \sin(\theta)}{g} $$

### Range of the Projectile

The range \( R \) is the horizontal distance the projectile travels before landing. Using the time of flight \( T \), the range can be determined from the horizontal motion equation:

$$ R = x(T) = v_0 \cos(\theta) T $$

Substituting the expression for \( T \):

$$ R = v_0 \cos(\theta) \cdot \frac{2 v_0 \sin(\theta)}{g} $$

Simplifying the expression for the range:

$$ R = \frac{v_0^2 \sin(2\theta)}{g} $$

### Variations with Initial Conditions

As the angle \( \theta \) changes, the range of the projectile also changes. The sine function \( \sin(2\theta) \) shows how the range is maximized at an angle of \( 45^\circ \), where the value of \( \sin(2\theta) \) is 1.

Thus, the range is a function of the launch angle \( \theta \), initial velocity \( v_0 \), and gravity \( g \). Variations in any of these initial conditions lead to a family of solutions for the range, allowing us to analyze how changes in conditions affect projectile motion.

import numpy as np
import matplotlib.pyplot as plt

import numpy as np
import matplotlib.pyplot as plt

# Sabitler
v0 = 20  # Başlangıç hızı (m/s)
g = 9.81  # Yerçekimi ivmesi (m/s^2)

# Açılar (0° - 90° arası, derece cinsinden)
angles_deg = np.linspace(0, 90, 500)
angles_rad = np.radians(angles_deg)  # Radyana çevir

# Menzil hesaplama
range_vals = (v0 ** 2 * np.sin(2 * angles_rad)) / g

# Grafik çizimi
plt.figure(figsize=(8, 5))
plt.plot(angles_deg, range_vals, color='blue')
plt.title("Açıya Göre Menzil")
plt.xlabel("Atış Açısı (°)")
plt.ylabel("Menzil (m)")
plt.grid(True)
plt.axvline(45, color='red', linestyle='--', label='Maksimum menzil (45°)')
plt.legend()
plt.tight_layout()
plt.show()



## Analysis of the Range:

# Investigating the Range as a Function of the Angle of Projection

## Analysis of the Range

### Dependence of Range on the Angle of Projection

From the previous derivation, we know the range \( R \) of the projectile is given by the equation:

$$ R = \frac{v_0^2 \sin(2\theta)}{g} $$

Where:
- \( v_0 \) is the initial velocity
- \( \theta \) is the angle of projection
- \( g \) is the acceleration due to gravity

We can analyze the behavior of the range as a function of the angle of projection \( \theta \).

The term \( \sin(2\theta) \) in the range equation indicates that the range varies as a sinusoidal function of \( 2\theta \). The sine function reaches its maximum value of 1 when \( 2\theta = 90^\circ \), i.e., when \( \theta = 45^\circ \). Therefore, the maximum horizontal range is achieved when the angle of projection is \( 45^\circ \).

The relationship between the range and the angle of projection is symmetric. For angles greater than \( 45^\circ \), the range decreases as the sine function decreases after reaching its maximum. For angles less than \( 45^\circ \), the range also decreases as the angle moves further away from \( 45^\circ \).

Thus, the range is maximized when \( \theta = 45^\circ \), and for other angles, the range decreases symmetrically on either side of this optimal angle.

### Influence of Initial Velocity

The range \( R \) is directly proportional to the square of the initial velocity \( v_0 \):

$$ R \propto v_0^2 $$

This means that if the initial velocity \( v_0 \) is increased, the range of the projectile increases as well. For example, doubling the initial velocity would quadruple the range, assuming the angle of projection and gravitational acceleration remain constant.

### Influence of Gravitational Acceleration

The range \( R \) is