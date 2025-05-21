# Problem 1

# 🌊 Interference Patterns from Circular Water Waves

## 📘 Introduction

A circular wave on the water surface, emanating from a point source located at $$(x_0, y_0)$$, can be described using the Single Disturbance Equation:

$$
\eta(x, y, t) = \frac{A}{\sqrt{r}} \cdot \cos(kr - \omega t + \phi)
$$

where:

- $$\eta(x, y, t)$$: Displacement of the water surface at point $$(x, y)$$ and time $$t$$.
- $$A$$: Amplitude of the wave.
- $$k = \frac{2\pi}{\lambda}$$: Wave number, related to wavelength $$\lambda$$.
- $$\omega = 2\pi f$$: Angular frequency, related to frequency $$f$$.
- $$r = \sqrt{(x - x_0)^2 + (y - y_0)^2}$$: Distance from source to point $$(x, y)$$.
- $$\phi$$: Initial phase.

---

## 🧠 Problem Statement

Analyze the interference patterns formed due to superposition of water waves emitted from point sources placed at the vertices of a regular polygon.

---

## 📌 Steps to Follow

1. **Select a Regular Polygon** (e.g., triangle, square, pentagon).
2. **Position the Sources** at the polygon vertices.
3. **Define Wave Equations** for each source.
4. **Apply Superposition**:

$$
\eta_{\text{sum}}(x, y, t) = \sum_{i=1}^{N} \eta_i(x, y, t)
$$

5. **Analyze Interference Patterns**: Locate regions of constructive and destructive interference.
6. **Visualize** the result using 2D heatmaps and 3D surface plots.

---

## 🛠️ Assumptions

- All sources emit waves with same amplitude $$A$$, wavelength $$\lambda$$, and frequency $$f$$.
- Waves are coherent (constant phase difference).
- Simulation tools such as **Python** with **Matplotlib**, **NumPy**, and **Pillow** (for animations) are used.

---

## 🐍 Python Simulation Code

Below is the code for visualizing interference from:
- A single point source
- Two point sources

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import cm

# Parameters
A = 1            # Amplitude
λ = 1            # Wavelength
f = 1            # Frequency
ω = 2 * np.pi * f
k = 2 * np.pi / λ
phi = 0
t = 0            # Initial time
grid_size = 500
domain = 10      # Physical range [-domain, domain]

# Spatial grid
x = np.linspace(-domain, domain, grid_size)
y = np.linspace(-domain, domain, grid_size)
X, Y = np.meshgrid(x, y)

def wave_from_source(x0, y0, X, Y, t):
    R = np.sqrt((X - x0)**2 + (Y - y0)**2)
    with np.errstate(divide='ignore', invalid='ignore'):
        η = (A / np.sqrt(R)) * np.cos(k * R - ω * t + phi)
        η[R == 0] = A  # Avoid divide-by-zero
    return η

# --- ONE SOURCE ---
source1 = (0, 0)
η1 = wave_from_source(*source1, X, Y, t)

# --- TWO SOURCES ---
source2 = (3, 0)
η2 = wave_from_source(*source2, X, Y, t)
η_sum_two = η1 + η2

# Plotting function
def plot_surface(data, title=""):
    fig = plt.figure(figsize=(10, 8))
    ax = fig.add_subplot(111, projection='3d')
    surf = ax.plot_surface(X, Y, data, cmap=cm.viridis, linewidth=0, antialiased=False)
    ax.set_title(title)
    ax.set_xlabel("x")
    ax.set_ylabel("y")
    ax.set_zlabel("η(x, y)")
    fig.colorbar(surf, shrink=0.5, aspect=5)
    plt.show()

# Plotting heatmap
def plot_heatmap(data, title=""):
    plt.figure(figsize=(8, 6))
    plt.imshow(data, extent=(-domain, domain, -domain, domain), cmap='inferno')
    plt.title(title)
    plt.colorbar(label='Displacement η(x, y)')
    plt.xlabel('x')
    plt.ylabel('y')
    plt.show()

# --- Visualizations ---
plot_heatmap(η1, "Single Point Source")
plot_heatmap(η_sum_two, "Two Point Sources - Interference Pattern")

plot_surface(η1, "3D View - Single Source")
plot_surface(η_sum_two, "3D View - Two Sources Interference")
