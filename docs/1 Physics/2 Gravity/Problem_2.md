# Problem 2
# Escape Velocities and Cosmic Velocities

Understanding escape and cosmic velocities is essential in orbital mechanics and spaceflight dynamics. These velocities represent the minimum speeds required for different types of motion in a gravitational field.

---

##  What Are Cosmic Velocities?

Cosmic velocities are defined based on the gravitational influence of a planetary body, such as Earth. They are theoretical thresholds that determine different outcomes for an object launched from a planet's surface.

---

## 1️ First Cosmic Velocity (Orbital Velocity)

**Definition**:  
The first cosmic velocity is the minimum horizontal speed an object must have to enter a stable **circular orbit** close to the surface of a planet, without additional propulsion.

### Derivation:

To stay in orbit, the gravitational force must equal the centripetal force:

$$
\frac{mv^2}{r} = G \frac{Mm}{r^2}
$$

Solving for \( v \):

$$
v_1 = \sqrt{\frac{GM}{r}}
$$

Where:

- \( v_1 \) = first cosmic velocity (orbital velocity)
- \( G \) = gravitational constant (\(6.674 \times 10^{-11} \, \text{m}^3 \text{kg}^{-1} \text{s}^{-2}\))
- \( M \) = mass of the Earth (or central body)
- \( r \) = radius from the center of the Earth

### Physical Meaning:

- This velocity allows satellites to **orbit** the Earth in a circular trajectory.
- For Earth:  
  $$ v_1 \approx 7.9 \, \text{km/s} $$

---

## 2️ Second Cosmic Velocity (Escape Velocity)

**Definition**:  
The second cosmic velocity is the minimum speed an object must reach to **completely escape** a planet's gravitational field, assuming no further propulsion and neglecting air resistance.

### Derivation:

From conservation of energy:

$$
\frac{1}{2}mv^2 = G \frac{Mm}{r}
$$

Solving for \( v \):

$$
v_2 = \sqrt{\frac{2GM}{r}}
$$

### Relation to First Cosmic Velocity:

$$
v_2 = \sqrt{2} \cdot v_1
$$

### Physical Meaning:

- Reaching this speed means the object will **escape** Earth’s gravity and move into **interplanetary space**.
- For Earth:  
  $$ v_2 \approx 11.2 \, \text{km/s} $$

---

## 3️ Third Cosmic Velocity (Interstellar Escape Velocity)

**Definition**:  
The third cosmic velocity is the minimum speed required to **escape the Sun's gravitational field**, starting from Earth’s orbit.

This is the velocity needed to **leave the Solar System**.

### Derivation:

The object must escape both Earth’s gravity and the Sun’s gravity. The formula typically used assumes the object has already escaped Earth and is now influenced mainly by the Sun:

$$
v_3 = \sqrt{2GM_\odot \left( \frac{1}{r_\text{Earth}} \right)}
$$

Where:

- \( M_\odot \) = mass of the Sun
- \( r_\text{Earth} \) = distance from the Sun to Earth (\( \approx 1 \, \text{AU} \))

More accurately, you subtract the Earth's orbital velocity from the total velocity required:

$$
v_3 = \sqrt{2GM_\odot / r} - v_\text{Earth-orbit}
$$

### Physical Meaning:

- This is the speed needed to leave the **Solar System**, e.g., like Voyager 1.
- From Earth’s orbit:  
  $$ v_3 \approx 16.7 \, \text{km/s} $$

---

##  Parameter Analysis

Each cosmic velocity depends on key physical parameters:

| Velocity | Depends on | Formula | Implication |
|----------|------------|---------|-------------|
| \( v_1 \) | \( G, M, r \) | \( \sqrt{\frac{GM}{r}} \) | Increases with central mass, decreases with orbital radius |
| \( v_2 \) | \( G, M, r \) | \( \sqrt{\frac{2GM}{r}} \) | Similar dependencies, but requires more energy than \( v_1 \) |
| \( v_3 \) | \( G, M_\odot, r \) | \( \sqrt{\frac{2GM_\odot}{r}} - v_{\text{Earth}} \) | Adds solar parameters, combines planetary and heliocentric escape |

---

##  Summary

- **First cosmic velocity**: Orbit around a planet  
- **Second cosmic velocity**: Escape from planet  
- **Third cosmic velocity**: Escape from Solar System  
- All are derived from Newtonian gravity and energy conservation.
- The higher the gravitational pull or the closer you are to the mass center, the **greater** the required velocity.

---

*Next: We will visualize these velocities using comparative plots and explore real-world mission data (e.g., Apollo, Voyager, Parker Solar Probe).*

![alt text](image-5.png)

"""
First Cosmic Velocity (blue): decreases with altitude — the orbital speed needed for low Earth orbit
Second Cosmic Velocity (red): also decreases with altitude — the speed needed to escape Earth's gravity.
Third Cosmic Velocity (green dashed line): constant — the speed needed to escape the Solar System, starting from Earth's orbit.
"""