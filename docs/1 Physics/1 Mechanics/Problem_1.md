# Problem 1

import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, theta, g=9.81):
    """Hesaplar menzilini."""
    theta_rad = np.radians(theta)
    return (v0**2 * np.sin(2 * theta_rad)) / g

v0 = 20  # Başlangıç hızı
angles = np.linspace(0, 90, 100)  # Açı aralığı
ranges = projectile_range(v0, angles)

plt.plot(angles, ranges)
plt.xlabel("Atış Açısı (derece)")
plt.ylabel("Menzil (metre)")
plt.title("Menzil vs. Atış Açısı")
plt.grid(True)
plt.show()
