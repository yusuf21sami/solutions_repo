# Problem 2
# Forced Damped Pendulum: Complete Analysis and Simulation

## 1. **Theoretical Foundation**

### Governing Equation

The motion of a forced damped pendulum is described by the nonlinear differential equation:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \sin\theta = A \cos(\omega t)
$$

Where:
- \( \theta(t) \): angular displacement
- \( b \): damping coefficient
- \( \frac{g}{L} \): gravitational term
- \( A \): amplitude of external forcing
- \( \omega \): angular frequency of external force

---

### Small-Angle Approximation

For small oscillations \( (\theta \ll 1) \), we approximate \( \sin\theta \approx \theta \). The equation becomes linear:

$$
\frac{d^2\theta}{dt^2} + b \frac{d\theta}{dt} + \frac{g}{L} \theta = A \cos(\omega t)
$$

---

### Analytical Approximate Solution

The general solution is the sum of homogeneous and particular solutions.

**Homogeneous solution**:

$$
\theta_h(t) = e^{-\frac{b}{2}t} \left( C_1 \cos(\omega_0 t) + C_2 \sin(\omega_0 t) \right)
$$

Where:

$$
\omega_0 = \sqrt{\frac{g}{L} - \left(\frac{b}{2}\right)^2}
$$

**Particular solution** (steady-state response):

$$
\theta_p(t) = B \cos(\omega t - \phi)
$$

With:

$$
B = \frac{A}{\sqrt{\left(\frac{g}{L} - \omega^2\right)^2 + b^2 \omega^2}}, \quad \tan\phi = \frac{b\omega}{\frac{g}{L} - \omega^2}
$$

---

### Resonance

Resonance occurs when the driving frequency approaches the system’s natural frequency. The amplitude \( B \) reaches a maximum near:

$$
\omega_{res} = \sqrt{\frac{g}{L} - \frac{b^2}{2}}
$$

---

## 2. **Analysis of Dynamics**

We analyze the behavior under different values of:
- Damping \( b \)
- Forcing amplitude \( A \)
- Driving frequency \( \omega \)

---

### Python Simulation (Phase Space, Chaotic Behavior)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Parameters
g, L = 9.81, 1.0
b = 0.5       # damping coefficient
A = 1.2       # driving amplitude
omega = 2/3   # driving frequency

# ODE system
def pendulum(t, y):
    theta, v = y
    dydt = [v, -b*v - (g/L)*np.sin(theta) + A*np.cos(omega*t)]
    return dydt

# Initial conditions and time
y0 = [0.2, 0.0]
t = np.linspace(0, 100, 10000)

# Solve
sol = solve_ivp(pendulum, [t[0], t[-1]], y0, t_eval=t, method='RK45')

# Plot Phase Diagram
plt.figure(figsize=(8, 4))
plt.plot(sol.y[0], sol.y[1], linewidth=0.7)
plt.xlabel(r"$\theta$")
plt.ylabel(r"$\dot{\theta}$")
plt.title("Phase Space of Forced Damped Pendulum")
plt.grid(True)
plt.tight_layout()
plt.show()

# Sample Poincaré section (stroboscopic map)
t_sampled = np.arange(0, 100, 2*np.pi/omega)
sampled_theta = []
sampled_omega = []

for t0 in t_sampled:
    index = np.argmin(np.abs(sol.t - t0))
    sampled_theta.append(sol.y[0][index] % (2*np.pi))  # mod 2π for visualization
    sampled_omega.append(sol.y[1][index])

plt.figure(figsize=(6, 4))
plt.plot(sampled_theta, sampled_omega, 'o', markersize=2)
plt.xlabel(r"$\theta$ mod $2\pi$")
plt.ylabel(r"$\dot{\theta}$")
plt.title("Poincaré Section")
plt.grid(True)
plt.tight_layout()
plt.show()
