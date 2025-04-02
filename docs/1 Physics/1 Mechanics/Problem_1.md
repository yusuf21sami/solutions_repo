# Problem 1

import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, theta, g=9.81):
    """
    Atış menzilini hesaplar.

    Parametreler:
    v0: Başlangıç hızı (metre/saniye)
    theta: Atış açısı (derece)
    g: Yerçekimi ivmesi (metre/saniye^2)

    Dönüş Değeri:
    Atış menzili (metre)
    """
    theta_rad = np.radians(theta)  # Dereceyi radyana çevir
    return (v0**2 * np.sin(2 * theta_rad)) / g

v0 = 20  # Başlangıç hızı (metre/saniye)
angles = np.linspace(0, 90, 100)  # 0 ile 90 derece arasında 100 nokta oluştur
ranges = projectile_range(v0, angles)  # Her açı için menzili hesapla

plt.plot(angles, ranges)  # Grafiği çiz
plt.xlabel("Atış Açısı (derece)")  # X ekseni etiketi
plt.ylabel("Menzil (metre)")  # Y ekseni etiketi
plt.title("Menzil vs. Atış Açısı")  # Grafik başlığı
plt.grid(True)  # Grid çizgilerini göster
plt.show()  # Grafiği göster
