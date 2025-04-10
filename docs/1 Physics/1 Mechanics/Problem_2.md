# Problem 2
# Investigating the Dynamics of a Forced Damped Pendulum

## 1. Theoretical Foundation

We begin by examining the differential equation that governs the motion of a forced damped pendulum system:

$$
\frac{d^2 \theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \sin \theta = A \cos(\omega t)
$$

Where:
- \( \theta(t) \) is the angular displacement as a function of time.
- \( b \) is the damping coefficient.
- \( \frac{g}{L} \sin\theta \) represents the restoring torque due to gravity.
- \( A \cos(\omega t) \) is the external periodic driving force with amplitude \( A \) and angular frequency \( \omega \).
- \( g \) is the gravitational acceleration.
- \( L \) is the length of the pendulum.

This second-order non-linear differential equation encapsulates the complexity of the system due to the presence of both damping and driving forces.

---

## 2. Small-Angle Approximation

For small angular displacements (\( \theta \ll 1 \) rad), we can use the approximation:

$$
\sin \theta \approx \theta
$$

Thus, the governing equation simplifies to a linear second-order non-homogeneous differential equation:

$$
\frac{d^2 \theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(\omega t)
$$

This form is analytically tractable and allows us to derive approximate solutions for understanding the oscillatory behavior of the system.

---

## 3. Resonance and Energy Considerations

Under the small-angle approximation, the system behaves similarly to a driven harmonic oscillator. Resonance occurs when the driving frequency \( \omega \) approaches the system’s natural frequency:

$$
\omega_0 = \sqrt{\frac{g}{L}}
$$

At resonance, the amplitude of oscillation increases significantly, especially when damping is low. This results in a dramatic increase in the system’s energy.

We will later explore:
- The steady-state amplitude response as a function of driving frequency
- The effect of varying damping \( b \) on resonance sharpness
- The transient and long-term energy behavior of the system

---

> **Next Step:** In the following sections, we will numerically simulate this system and visualize the time-domain and frequency-domain characteristics using Python.

![alt text](image-2.png)

import numpy as np
import matplotlib.pyplot as plt

# Parameters
b = 0.5        # damping coefficient
g = 9.81       # gravity
L = 1.0        # pendulum length
A = 1.2        # amplitude of driving force
omega = 1.5    # driving frequency
omega_0 = np.sqrt(g / L)  # natural frequency

# Time array
t = np.linspace(0, 20, 1000)

# Steady-state amplitude and phase
denominator = np.sqrt((omega_0**2 - omega**2)**2 + (b * omega)**2)
theta_amplitude = A / denominator
delta = np.arctan2(b * omega, (omega_0**2 - omega**2))

# Solution
theta = theta_amplitude * np.cos(omega * t - delta)

# Plotting
plt.figure(figsize=(10, 5))
plt.plot(t, theta, label='Angular Displacement θ(t)', color='blue')
plt.title("Forced Damped Pendulum - Steady-State Oscillation")
plt.xlabel("Time (s)")
plt.ylabel("Angular Displacement (rad)")
plt.grid(True)
plt.legend()

# Add explanation below plot
explanation = (
    "The graph demonstrates how the pendulum reaches a sinusoidal oscillation\n"
    "with constant amplitude and phase relative to the driving force.\n"
    "This is the steady-state response of a forced damped pendulum."
)

# Display explanation as annotation (outside plot area)
plt.figtext(0.5, -0.2, explanation, wrap=True, horizontalalignment='center', fontsize=10)

plt.tight_layout()
plt.show()
