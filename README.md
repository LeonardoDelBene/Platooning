# Platooning

Simulation of a platoon of vehicles following a leader along variable, curved trajectories, using a feedback control law based on a constant time-headway spacing policy.

This project was developed for my bachelor's thesis in Computer Engineering (University of Florence): *Control techniques for platooning on variable trajectories*. The full thesis (in Italian) is available in [`tesi_platooning.pdf`](tesi_platooning.pdf).

## Overview

A platoon of `N` vehicles moves on the plane. The first vehicle (the **leader**) follows a prescribed acceleration and angular velocity profile; every other vehicle is controlled to follow its predecessor at a distance that grows with speed.

- **Vehicle model**: each vehicle has state `(x, y, θ, v)` and is driven by two inputs, linear acceleration `a` and angular velocity `ω`.
- **Spacing policy**: the follower tracks a point placed behind its predecessor at distance `r + h·v` along its own heading, where `r` is a constant gap and `h` the time headway.
- **Control law**: the tracking errors (position and velocity along x and y) are driven to zero with proportional gains `k1`, `k2`. The inputs `(a, ω)` are obtained by inverting the matrix that maps the inputs to the error dynamics (feedback linearization).
- **Trajectories**: two leader scenarios are provided, a circular trajectory and a more general curvilinear one made of straight and curved segments with turns in both directions.

## Repository structure

| File | Description |
|---|---|
| `main.py` | Runs the simulation, computes the inter-vehicle errors, produces plots and animations |
| `Controller_standard.py` | Control law with position and velocity error dynamics |
| `Controller_State.py` | Container for the controller state at each time step |
| `vehicle.py` | Vehicle model and state update |
| `Vehicle_State.py` | Container for the vehicle state (`x`, `y`, `θ`, velocity) |
| `tesi_platooning.pdf` | Bachelor's thesis (in Italian) |

## Getting started

Requirements: Python 3, `numpy`, `matplotlib`, `Pillow` (used to save the GIF animations).

```bash
git clone https://github.com/LeonardoDelBene/Platooning.git
cd Platooning
pip install numpy matplotlib pillow
python main.py
```

When prompted, choose the leader trajectory:

- `1` for the circular trajectory
- `2` for the curvilinear trajectory

### Default parameters (in `main.py`)

| Parameter | Value | Meaning |
|---|---|---|
| `N` | 5 | Number of vehicles |
| `r` | 1 | Constant inter-vehicle gap |
| `h` | 0.2 | Time headway |
| `k1`, `k2` | 2.5 | Controller gains |
| `T` | 0.01 s | Sampling time |
| `T_max` | 20 s | Simulation length |
| initial speed | 5 | Same for all vehicles |

## Output

Running `main.py` produces:

- trajectories of all vehicles in the plane, and their `x` and `y` positions over time
- a 3D plot of the trajectories over time
- the tracking error between each vehicle and its predecessor over time (L2 norm), and the RMS error printed for each pair
- two animations saved in the working directory: `vehicle_trajectories.gif` and `vehicle_trajectories_rectangles.gif`



## Author

Leonardo Del Bene: [GitHub](https://github.com/LeonardoDelBene)
