# Install the required libraries
!pip install ipywidgets

import ipywidgets as widgets
from IPython.display import display, clear_output

def calculate_gear_design(module, teeth, speed, torque, gear_type, material):
    try:
        # Sample Calculations
        pitch_diameter = module * teeth  # D = m * Z
        center_distance = pitch_diameter / 2  # Approximate center distance

        # Power calculation example (Power = Torque * Speed / 9.5488)
        power = torque * speed / 9.5488

        # Display Results
        result = (
            f"Results:\n"
            f"Pitch Diameter: {pitch_diameter:.2f} mm\n"
            f"Center Distance: {center_distance:.2f} mm\n"
            f"Calculated Power: {power:.2f} kW\n"
            f"Material: {material}\n"
            f"Gear Type: {gear_type}"
        )
    except ValueError:
        result = "Invalid input. Please enter valid numbers."
    return result

def on_calculate(button):
    clear_output()
    display(title, module_input, teeth_input, speed_input, torque_input, gear_type_input, material_input, calculate_button, result_output)
    
    module = float(module_input.value)
    teeth = int(teeth_input.value)
    speed = float(speed_input.value)
    torque = float(torque_input.value)
    gear_type = gear_type_input.value
    material = material_input.value
    
    result = calculate_gear_design(module, teeth, speed, torque, gear_type, material)
    result_output.value = result

# Create UI components
title = widgets.Label(value="Mechanical Gear Design Calculator")

module_input = widgets.FloatText(value=2.0, description='Module:')
teeth_input = widgets.IntText(value=20, description='Number of Teeth:')
speed_input = widgets.FloatText(value=100.0, description='Speed (RPM):')
torque_input = widgets.FloatText(value=10.0, description='Torque (Nm):')

gear_type_input = widgets.Dropdown(
    options=["Spur Gear", "Helical Gear", "Bevel Gear", "Worm Gear"],
    description='Gear Type:'
)

material_input = widgets.Dropdown(
    options=["Steel", "Aluminum", "Brass", "Titanium"],
    description='Material:'
)

calculate_button = widgets.Button(description="Calculate")
calculate_button.on_click(on_calculate)

result_output = widgets.Textarea(value="", description='Result:', layout=widgets.Layout(width='100%', height='200px'))

# Display the UI
display(title, module_input, teeth_input, speed_input, torque_input, gear_type_input, material_input, calculate_button, result_output)
