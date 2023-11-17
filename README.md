# super-journey
Negitive Mass Electromagnetic Coil
import numpy as np

def create_coil(n_turns, radius, current):
    """
    Creates an electromagnetic coil with the specified number of turns, radius, and current.

    Args:
        n_turns (int): The number of turns in the coil.
        radius (float): The radius of the coil.
        current (float): The current in the coil.

    Returns:
        numpy.ndarray: A 3D array representing the electromagnetic field of the coil.
    """
    coil = np.zeros((n_turns, radius, 2))
    for turn in range(n_turns):
        for x in range(radius):
            for y in range(2):
                coil[turn, x, y] = calculate_field_at_point(turn, x, y, radius, current)
    return coil

def calculate_field_at_point(turn, x, y, radius, current):
    """
    Calculates the electromagnetic field at a point in space.

    Args:
        turn (int): The turn of the coil.
        x (int): The x-coordinate of the point.
        y (int): The y-coordinate of the point.
        radius (float): The radius of the coil.
        current (float): The current in the coil.

    Returns:
        tuple: A 2-tuple representing the x and y components of the electromagnetic field at the point.
    """
    Bx = 0
    By = 0
    for turn2 in range(n_turns):
        if turn2 != turn:
            for x2 in range(radius):
                for y2 in range(2):
                    Bx += calculate_field_component(turn2, x2, y2, x, y, radius, current)
                    By += calculate_field_component(turn2, x2, y2, x, y, radius, current)
    return Bx, By

def calculate_field_component(turn2, x2, y2, x, y, radius, current):
    """
    Calculates a single component of the electromagnetic field at a point in space.

    Args:
        turn2 (int): The turn of the coil.
        x2 (int): The x-coordinate of the point.
        y2 (int): The y-coordinate of the point.
        x (int): The x-coordinate of the point.
        y (int): The y-coordinate of the point.
        radius (float): The radius of the coil.
        current (float): The current in the coil.

    Returns:
        float: The value of the component of the electromagnetic field at the point.
    """
    distance = np.sqrt((x - x2) ** 2 + (y - y2) ** 2)
    return (current * np.sin(np.pi * (x - x2) / radius)) / (4 * np.pi * distance)

# Example usage
n_turns = 10
radius = 0.1
current = 1

coil = create_coil(n_turns, radius, current)

print(coil)
.
