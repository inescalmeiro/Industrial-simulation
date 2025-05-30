# Dynamic Liquid Height Simulation in Reactors and Storage Tank

This Python project simulates the dynamic behavior of liquid levels in multiple reactors and a central storage tank over time using numerical integration via the Euler method.

## Overview

The simulation models **16 reactors** operating on a periodic cycle of **filling and emptying**, along with a **central storage tank** that accumulates the outflow from these reactors. The results are visualized through **graphs and animations** showing the liquid levels in both the reactors and the storage tank over time.

## How It Works

### 1. **System Parameters and Time Configuration**

The initial section of the code defines:

* Geometric parameters (heights, areas) for reactors and the storage tank
* Operating conditions such as flow rates and timing for filling and emptying cycles
* The **time scale** to simulate, which can be manually adjusted

---

### 2. **Reactor Simulation**

The `simulate_reactor` function models the liquid height in a reactor over time.

#### Key Behavior:

* Starts from an initial height `h0`
* At each time step `dt`, calculates the height change `∆H` based on inflow and outflow
* **Filling phase**: `∆H = Q_in / A` (height increases)
* **Emptying phase**: `∆H = -Q_out / A` (height decreases)
* **Idle phase**: no height change
* Height is clamped to stay within physical bounds (0 to max height)

The result is a time series array (`sol`) with the liquid height at each time step.

---

### 3. **System-Wide Simulation**

This section:

* Applies `simulate_reactor` to all 16 reactors
* Simulates the **central storage tank**:

  * Starts empty
  * At each time step, checks which reactors are discharging
  * Calculates:

    * `Q_in`: inflow to the tank from reactors
    * `Q_out`: outflow due to centrifugation (begins after a set time)
    * `∆H = (Q_in - Q_out) / A` to update tank height
  * Ensures the tank level remains non-negative

Results are stored in:

* `sol_reactors`: liquid height over time for each reactor
* `sol_storage`: liquid height over time for the tank

---

### 4. **Visualization**

#### Plot of Liquid Heights

* Generates a plot showing the variation in liquid levels for all 16 reactors and the storage tank over time
* Uses `matplotlib` with `tab20` and `tab20b` colormaps for unique coloring of each reactor

#### Animation of Reactors

* Creates an animation of 16 reactors arranged in a **4x4 grid**
* Each reactor is visualized with proportionate dimensions
* The liquid level inside each tank updates frame-by-frame according to the simulation

#### Animation of Storage Tank

* A similar animation for the central storage tank
* Displays the time on the chart
* Shows the liquid level changing in real-time based on computed simulation data

---

## Requirements

* Python 3.x
* `matplotlib`, `numpy`

Install dependencies (if needed):

```bash
pip install matplotlib numpy
```

---

## Usage

1. Configure system parameters and timing in the code
2. Run the script to:

   * Simulate the liquid height dynamics
   * Generate plots and animations
3. Visual outputs will show how the system behaves over time

---

## License

This project is intended for academic and educational use.
