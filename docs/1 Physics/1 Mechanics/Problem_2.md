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