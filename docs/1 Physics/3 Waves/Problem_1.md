# Problem 1

import numpy as np

# --- Constants and Basic Wave Parameters ---
# These can be adjusted as needed for simulations

# A: Amplitude of the wave at the source
DEFAULT_AMPLITUDE = 1.0
# k: Wave number (k = 2*pi / lambda)
DEFAULT_WAVE_NUMBER = 1.0  # Corresponds to lambda = 2*pi
# omega: Angular frequency (omega = 2*pi * f)
DEFAULT_ANGULAR_FREQUENCY = 1.0 # Corresponds to f = 1 / (2*pi)
# phi: Initial phase
DEFAULT_PHASE = 0.0

# --- Helper Function for Distance ---
def calculate_distance(x, y, x_source, y_source):
    """
    Calculates the distance from a source to a point (x,y).
    
    Args:
        x (float or np.ndarray): x-coordinate(s) of the observation point(s).
        y (float or np.ndarray): y-coordinate(s) of the observation point(s).
        x_source (float): x-coordinate of the wave source.
        y_source (float): y-coordinate of the wave source.
        
    Returns:
        float or np.ndarray: Distance(s) from the source to the point(s).
    """
    return np.sqrt((x - x_source)**2 + (y - y_source)**2)

# --- 1. Single Wave Source ---
def single_wave_source_displacement(x, y, t, source_pos, 
                                    amplitude=DEFAULT_AMPLITUDE, 
                                    wave_number=DEFAULT_WAVE_NUMBER, 
                                    angular_frequency=DEFAULT_ANGULAR_FREQUENCY, 
                                    phase=DEFAULT_PHASE):
    """
    Calculates the displacement of the water surface due to a single circular wave source.
    Equation: eta(x,y,t) = (A / sqrt(r)) * cos(k*r - omega*t + phi)
    
    Args:
        x (float or np.ndarray): x-coordinate(s) of the observation point(s).
        y (float or np.ndarray): y-coordinate(s) of the observation point(s).
        t (float): Time.
        source_pos (tuple): (x0, y0) coordinates of the wave source.
        amplitude (float): Initial amplitude of the wave.
        wave_number (float): Wave number (k).
        angular_frequency (float): Angular frequency (omega).
        phase (float): Initial phase (phi).
        
    Returns:
        float or np.ndarray: Displacement(s) eta(x,y,t) at the given point(s) and time.
                           Returns 0 if distance r is 0 to avoid division by zero,
                           though physically the model breaks down at r=0.
    """
    x_source, y_source = source_pos
    r = calculate_distance(x, y, x_source, y_source)
    
    # Avoid division by zero at the source location
    # In reality, the model isn't perfect at r=0.
    # We can return a large amplitude or handle it as a special case.
    # For simplicity, if r is very small, we can cap the amplitude or return 0 for the numerical calculation.
    # Let's return 0 if r is exactly 0, and for very small r, sqrt(r) will be small, leading to large amplitude.
    displacement = np.zeros_like(r)
    
    # Calculate only for r > 0 to avoid division by zero and sqrt of zero.
    # A very small epsilon can be used if strict r > 0 is needed.
    non_zero_r_mask = r > 1e-9 # Avoid issues very close to the source
    
    if np.any(non_zero_r_mask):
        r_safe = r[non_zero_r_mask]
        displacement[non_zero_r_mask] = (amplitude / np.sqrt(r_safe)) * \
                                        np.cos(wave_number * r_safe - angular_frequency * t + phase)
    
    # Handle the case where r is exactly zero (at the source)
    # Physically, amplitude is undefined or extremely large.
    # For simulation, you might want to set a max cap or a specific behavior.
    # Here, if r=0, it will remain 0 due to the mask.
    
    return displacement

# --- 2. Two Wave Sources (Interference) ---
def two_wave_sources_interference(x, y, t, source1_pos, source2_pos,
                                  amplitude=DEFAULT_AMPLITUDE, 
                                  wave_number=DEFAULT_WAVE_NUMBER, 
                                  angular_frequency=DEFAULT_ANGULAR_FREQUENCY, 
                                  phase=DEFAULT_PHASE):
    """
    Calculates the total displacement due to interference from two identical wave sources.
    
    Args:
        x (float or np.ndarray): x-coordinate(s) of the observation point(s).
        y (float or np.ndarray): y-coordinate(s) of the observation point(s).
        t (float): Time.
        source1_pos (tuple): (x1, y1) coordinates of the first wave source.
        source2_pos (tuple): (x2, y2) coordinates of the second wave source.
        amplitude (float): Initial amplitude of the waves (assumed same for both).
        wave_number (float): Wave number (k) (assumed same for both).
        angular_frequency (float): Angular frequency (omega) (assumed same for both).
        phase (float): Initial phase (phi) (assumed same for both).
        
    Returns:
        float or np.ndarray: Total displacement eta_total(x,y,t).
    """
    eta1 = single_wave_source_displacement(x, y, t, source1_pos, 
                                           amplitude, wave_number, angular_frequency, phase)
    eta2 = single_wave_source_displacement(x, y, t, source2_pos,
                                           amplitude, wave_number, angular_frequency, phase)
    
    return eta1 + eta2

# --- 3. Multiple Wave Sources (Interference) ---
def multiple_wave_sources_interference(x, y, t, sources_params):
    """
    Calculates the total displacement due to interference from multiple wave sources.
    
    Args:
        x (float or np.ndarray): x-coordinate(s) of the observation point(s).
        y (float or np.ndarray): y-coordinate(s) of the observation point(s).
        t (float): Time.
        sources_params (list of dicts): A list where each dictionary contains
            parameters for a single source:
            {
                'pos': (xs, ys),          # Source position
                'amplitude': A_s,         # Source amplitude
                'wave_number': k_s,       # Source wave number
                'angular_frequency': w_s, # Source angular frequency
                'phase': phi_s            # Source initial phase
            }
            If a parameter is not provided for a source, default values will be used.
            
    Returns:
        float or np.ndarray: Total displacement eta_total(x,y,t).
    """
    total_displacement = np.zeros_like(x, dtype=float) # Ensure it's float for accumulation
    
    for params in sources_params:
        pos = params.get('pos')
        if pos is None:
            print("Warning: Source position missing for one of the sources. Skipping this source.")
            continue # Skip this source if position is not defined

        amp = params.get('amplitude', DEFAULT_AMPLITUDE)
        k = params.get('wave_number', DEFAULT_WAVE_NUMBER)
        omega = params.get('angular_frequency', DEFAULT_ANGULAR_FREQUENCY)
        phi = params.get('phase', DEFAULT_PHASE)
        
        eta_i = single_wave_source_displacement(x, y, t, pos, amp, k, omega, phi)
        total_displacement += eta_i
        
    return total_displacement

# --- Example Usage (Conceptual - for testing the functions) ---
if __name__ == "__main__":
    # Define a grid of points (e.g., for a heatmap)
    grid_size = 100
    x_coords = np.linspace(-10, 10, grid_size)
    y_coords = np.linspace(-10, 10, grid_size)
    X, Y = np.meshgrid(x_coords, y_coords)
    
    current_time = 0.0 # Snapshot at t=0

    # --- Test Single Source ---
    print("Testing Single Source...")
    source1_location = (0, 0)
    displacement_single = single_wave_source_displacement(X, Y, current_time, source1_location)
    print(f"Displacement at (1,1) for single source at (0,0): {single_wave_source_displacement(1, 1, current_time, source1_location):.4f}")
    # To visualize this, you would plot displacement_single as a heatmap or 3D plot.

    # --- Test Two Sources ---
    print("\nTesting Two Sources...")
    source2_location = (3, 0)
    source3_location = (-3, 0)
    displacement_two = two_wave_sources_interference(X, Y, current_time, source2_location, source3_location)
    print(f"Displacement at (0,0) for two sources at (3,0) and (-3,0): {two_wave_sources_interference(0, 0, current_time, source2_location, source3_location):.4f}")

    # --- Test Multiple Sources (Triangle) ---
    print("\nTesting Multiple Sources (Triangle)...")
    # Assuming identical sources for simplicity
    triangle_sources = [
        {'pos': (0, 5)},    # Top vertex
        {'pos': (-4, -3)},  # Bottom-left vertex
        {'pos': (4, -3)}    # Bottom-right vertex
        # We can add custom amplitude, k, omega, phi for each if needed
        # e.g., {'pos': (0,5), 'amplitude': 1.2, 'wave_number': 0.8}
    ]
    displacement_triangle = multiple_wave_sources_interference(X, Y, current_time, triangle_sources)
    print(f"Displacement at (0,0) for triangle sources: {multiple_wave_sources_interference(0, 0, current_time, triangle_sources):.4f}")

    # --- Test Multiple Sources (Pentagon) ---
    print("\nTesting Multiple Sources (Pentagon)...")
    pentagon_radius = 5
    pentagon_sources = []
    for i in range(5):
        angle = 2 * np.pi * i / 5 + (np.pi / 2) # Start from top point
        px = pentagon_radius * np.cos(angle)
        py = pentagon_radius * np.sin(angle)
        pentagon_sources.append({'pos': (px, py)})
        
    displacement_pentagon = multiple_wave_sources_interference(X, Y, current_time, pentagon_sources)
    print(f"Displacement at (0,0) for pentagon sources: {multiple_wave_sources_interference(0, 0, current_time, pentagon_sources):.4f}")

    print("\nPython functions for wave interference are ready.")
    print("Next steps would involve using these functions to generate data for heatmaps, 3D plots, and animations.")

