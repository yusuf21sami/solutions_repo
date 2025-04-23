#Problem 1
# 🌍 Kepler's Third Law: Orbital Period and Radius

## 🧮 1. Derivation of the Kepler's Third Law for Circular Orbits

We start by considering the centripetal force required to keep a body in a circular orbit:

$$
F_c = \frac{mv^2}{r}
$$

This centripetal force is provided by gravitational attraction:

$$
F_g = \frac{G M m}{r^2}
$$

Where:
- \( m \): mass of the orbiting body
- \( M \): mass of the central body (e.g., the Sun)
- \( G \): gravitational constant
- \( r \): orbital radius

Equating the two forces:

$$
\frac{mv^2}{r} = \frac{G M m}{r^2}
$$

Canceling \( m \) and solving for \( v \):

$$
v^2 = \frac{G M}{r}
$$

Now, the orbital period \( T \) is the time to complete one orbit:

$$
T = \frac{2\pi r}{v}
$$

Substituting for \( v \):

$$
T = \frac{2\pi r}{\sqrt{\frac{G M}{r}}} = 2\pi \sqrt{\frac{r^3}{G M}}
$$

Squaring both sides:

$$
T^2 = \frac{4\pi^2}{G M} r^3
$$

✅ This is **Kepler's Third Law** in the form:

$$
T^2 \propto r^3
$$

---

## 🔭 2. Astronomical Implications

- This relationship allows astronomers to:
  - Compare orbital periods and distances of planets.
  - Estimate **masses** of celestial bodies using known \( T \) and \( r \).
  - Calibrate models of exoplanet systems.
  - Predict satellite behavior and planetary motion.

If \( T \) and \( r \) are known, we can solve for \( M \):

$$
M = \frac{4\pi^2 r^3}{G T^2}
$$

---
# Earth's orbit
r = 1.496e11  # meters
T = 3.154e7   # seconds

M_sun = (4 * np.pi**2 * r**3) / (G * T**2)
print(f"Estimated Mass of the Sun: {M_sun:.2e} kg")

r_moon = 3.84e8  # meters
T_moon = 2.36e6  # seconds

M_earth = (4 * np.pi**2 * r_moon**3) / (G * T_moon**2)
print(f"Estimated Mass of Earth: {M_earth:.2e} kg")

## 🌌 3. Real-World Example: Inner Planets of the Solar System

Let’s consider four planets:

| Planet   | Orbital Radius (AU) | Orbital Period (years) |
|----------|---------------------|-------------------------|
| Mercury  | 0.387               | 0.241                   |
| Venus    | 0.723               | 0.615                   |
| Earth    | 1.000               | 1.000                   |
| Mars     | 1.524               | 1.881                   |

We will plot \( T^2 \) vs \( r^3 \) to visually confirm the linear relationship.

---

## 💻 4. Python Simulation of Kepler’s Law (T² vs r³)

```python
import numpy as np
import matplotlib.pyplot as plt

# AU to meters and years to seconds
AU = 1.496e11  # meters
yr = 3.154e7   # seconds
G = 6.67430e-11  # m^3 kg^-1 s^-2

# Data for 4 planets: Mercury, Venus, Earth, Mars
planets = {
    "Mercury": (0.387, 0.241),
    "Venus": (0.723, 0.615),
    "Earth": (1.000, 1.000),
    "Mars": (1.524, 1.881),
}

# Prepare lists
r_AU = []
T_years = []

for name, (r, T) in planets.items():
    r_AU.append(r)
    T_years.append(T)

r_AU = np.array(r_AU)
T_years = np.array(T_years)

# Calculate r^3 and T^2
r3 = r_AU**3
T2 = T_years**2

# Plotting T^2 vs r^3
plt.figure(figsize=(6, 4))
plt.plot(r3, T2, 'o-', label="Planets", color="navy")
plt.xlabel(r"$r^3$ (AU$^3$)")
plt.ylabel(r"$T^2$ (years$^2$)")
plt.title(r"Kepler's Third Law: $T^2$ vs $r^3$")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

