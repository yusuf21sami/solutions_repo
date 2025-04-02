# Problem 1

import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, g):
    """
    Farklı açılar için yatay menzili hesaplar.
    :param v0: Başlangıç hızı (m/s)
    :param g: Yerçekimi ivmesi (m/s^2)
    :return: Açılar (derece) ve karşılık gelen menziller (m)
    """
    angles = np.linspace(0, 90, 100)  # 0 ile 90 derece arasında açılar
    angles_rad = np.radians(angles)  # Radyana çevir
    ranges = (v0**2 * np.sin(2 * angles_rad)) / g  # Menzil formülü
    return angles, ranges

# Parametreler
initial_velocity = 20  # m/s
gravity = 9.81  # m/s^2

# Hesaplama
angles, ranges = projectile_range(initial_velocity, gravity)

# Grafik çizimi
plt.figure(figsize=(8, 5))
plt.plot(angles, ranges, label=f'Başlangıç hızı: {initial_velocity} m/s')
plt.xlabel('Fırlatma Açısı (derece)')
plt.ylabel('Yatay Menzil (m)')
plt.title('Fırlatma Açısına Göre Menzil')
plt.legend()
plt.grid()
plt.show()

