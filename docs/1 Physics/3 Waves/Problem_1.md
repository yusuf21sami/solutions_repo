# Problem 1

# 🌊 Circular Water Wave Interference Simulation

## 📘 Task Overview

We simulate circular water waves emitted from point sources placed at the vertices of a regular polygon. Using the principle of superposition, we analyze interference patterns (constructive and destructive) formed on the water surface.

---

## 📐 Mathematical Model

### Single Disturbance Equation

The displacement \( \eta(x, y, t) \) of the water surface at point \( (x, y) \) and time \( t \) from a single point source located at \( (x_0, y_0) \) is:

$$
\eta(x, y, t) = \frac{A}{\sqrt{r}} \cdot \cos(kr - \omega t + \phi)
$$

where:

- \( A \): amplitude of the wave  
- \( r = \sqrt{(x - x_0)^2 + (y - y_0)^2} \): distance from source  
- \( k = \frac{2\pi}{\lambda} \): wave number  
- \( \omega = 2\pi f \): angular frequency  
- \( \phi \): initial phase (assumed 0 for coherence)

---

### Multiple Sources: Superposition

For \( N \) sources placed at the vertices of a regular polygon, the net displacement is:

$$
\eta_{\text{sum}}(x, y, t) = \sum_{i=1}^{N} \eta_i(x, y, t)
$$

---

## 🧠 Assumptions

- All sources have identical parameters: same \( A, \lambda, f, \phi \)
- Coherent waves (same phase relation)
- Simulation performed in a 2D grid using NumPy

---

## 🐍 Python Code (Simulation Setup)

```python
import numpy as np

# Wave parameters
A = 1.0           # Amplitude
λ = 2.0           # Wavelength
f = 1.0           # Frequency (Hz)
k = 2 * np.pi / λ # Wave number
ω = 2 * np.pi * f # Angular frequency
φ = 0             # Initial phase

# Grid setup
x = np.linspace(-10, 10, 500)
y = np.linspace(-10, 10, 500)
X, Y = np.meshgrid(x, y)

# Time parameter for snapshot
t = 0

def wave_from_source(x0, y0, X, Y, t):
    r = np.sqrt((X - x0)**2 + (Y - y0)**2)
    # To avoid division by zero at r=0
    r[r == 0] = 1e-6
    η = A / np.sqrt(r) * np.cos(k * r - ω * t + φ)
    return η

# Example: Single source at origin
sources = [(0, 0)]

# Calculate superposition
η_sum = np.zeros_like(X)
for x0, y0 in sources:
    η_sum += wave_from_source(x0, y0, X, Y, t)
