# Transportation Data Analysis & Traffic Simulation

### NHTS Travel Behavior Analysis | NGSIM Vehicle Trajectories | Intelligent Driver Model (IDM) | Python

## Overview

This project applies **Python-based transportation data analysis and microscopic traffic simulation** using two transportation datasets:

- **National Household Travel Survey (NHTS)** data for analysis of household, vehicle, and travel characteristics
- **Next Generation Simulation (NGSIM)** data for analysis of individual vehicle trajectories and car-following behavior

The project combines transportation data analytics with traffic-flow modeling by progressing from exploratory analysis of transportation datasets to implementation of the **Intelligent Driver Model (IDM)**.

The IDM portion uses real leader-vehicle trajectory data from NGSIM and numerically simulates the response of a following vehicle through time. The simulated trajectory can then be compared with observed vehicle behavior.

The project was completed for **CIVE 202 – Civil Engineering Analysis II** at the **University of Nebraska–Lincoln**, with the project framed around transportation-analysis needs of the **Federal Highway Administration (FHWA)**.

---

## Why This Project Matters

Transportation engineers increasingly work with large datasets generated from:

- Household travel surveys
- Roadway sensors
- Connected vehicles
- GPS trajectories
- Traffic cameras
- Transportation simulation platforms

The ability to convert these datasets into engineering information requires both **transportation-domain knowledge** and **data-analysis/programming skills**.

This project demonstrates a workflow that moves from:

**Raw Transportation Data → Data Organization → Visualization → Vehicle Dynamics → Mathematical Modeling → Numerical Simulation → Engineering Interpretation**

---

# Transportation Engineering Skills Demonstrated

## Transportation Data Analysis

- Analysis of household and vehicle characteristics
- Exploration of vehicle fleet composition
- Urban-versus-rural transportation comparisons
- Vehicle-age distribution analysis
- Interpretation of transportation-related variables
- Organization and filtering of transportation datasets

## Traffic Flow & Vehicle Dynamics

- Leader-follower vehicle relationships
- Vehicle position and speed trajectories
- Following-gap analysis
- Relative velocity
- Acceleration and deceleration behavior
- Time-series traffic data

## Traffic Simulation

- Intelligent Driver Model (IDM)
- Car-following behavior
- Numerical time integration
- Euler's method
- Real-versus-simulated trajectory comparison

## Programming & Data Science

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- Data filtering and transformation
- Engineering visualization
- Reusable functions
- Array-based numerical simulation

---

# Project Architecture

The analysis consists of two primary components.

## Part 1 — Transportation Data Analysis

The first portion of the project analyzes **NHTS and NGSIM transportation data**.

The objective is to transform raw transportation data into interpretable engineering information through exploratory data analysis and visualization.

The NHTS portion focuses primarily on household and vehicle characteristics, while the NGSIM portion introduces microscopic vehicle-motion data.

## Part 2 — Traffic Simulation

The second portion implements the **Intelligent Driver Model (IDM)** to simulate the behavior of a following vehicle using an observed NGSIM leader trajectory.

The simulated follower behavior is advanced through time using numerical integration and compared with observed vehicle behavior.

This progression connects descriptive transportation data analysis with mathematical traffic-flow modeling.

---

# Dataset 1 — National Household Travel Survey (NHTS)

The NHTS dataset provides information describing household travel characteristics and vehicle ownership.

Variables available for analysis include:

- Household income
- Household size
- Number of drivers
- Household location
- Urban/rural classification
- Vehicle type
- Vehicle make
- Vehicle age
- Fuel type
- Vehicle year
- Household vehicle characteristics

These variables make it possible to investigate relationships between household characteristics and transportation behavior.

---

# NHTS Analysis

## 1. Vehicle Type Distribution

Vehicle-type frequencies were analyzed to examine the composition of vehicles represented within the NHTS dataset.

A categorical count plot was created to visualize the number of vehicles associated with each vehicle classification.

This type of analysis is relevant to transportation planning because fleet composition can influence:

- Roadway demand
- Vehicle emissions
- Energy consumption
- Parking requirements
- Transportation policy
- Long-term infrastructure needs

The analysis demonstrates how Python can quickly summarize categorical transportation data and communicate the results graphically.

---

## 2. Urban vs. Rural Vehicle Age

Vehicle-age distributions were separated between **urban and rural households** and visualized using overlapping histograms.

This provides a way to investigate whether vehicle fleet characteristics differ depending on household location.

Urban-rural transportation differences are important because transportation systems may differ substantially in:

- Trip distances
- Transit availability
- Roadway accessibility
- Vehicle dependence
- Land-use patterns

Rather than examining only a single average value, the distribution-based approach allows the complete spread of vehicle ages to be evaluated.

---

## 3. Vehicle Age by Manufacturer

A boxplot was created to compare vehicle-age distributions across vehicle manufacturers.

Boxplots provide a useful method for examining:

- Median vehicle age
- Distribution spread
- Variability
- Potential outliers
- Differences between manufacturers

This demonstrates how statistical visualization can reveal patterns that may not be immediately apparent from raw transportation data.

---

# Dataset 2 — Next Generation Simulation (NGSIM)

The NGSIM dataset contains microscopic vehicle trajectory information.

The project works with variables including:

- Time
- Leader position
- Follower position
- Leader speed
- Follower speed
- Leader acceleration
- Follower acceleration
- Trajectory number

Unlike NHTS, which primarily describes household and vehicle characteristics, NGSIM makes it possible to examine **vehicle interactions through time**.

This creates a direct connection between transportation data science and traffic-flow theory.

---

# Vehicle Trajectory Analysis

A leader-follower trajectory pair was selected from the NGSIM dataset.

The analysis examines how vehicle motion changes through time by comparing:

- Leader position
- Follower position
- Leader speed
- Follower speed

This allows the temporal relationship between two interacting vehicles to be visualized.

Vehicle trajectory analysis is useful in transportation engineering for applications including:

- Traffic-flow modeling
- Freeway operations
- Congestion analysis
- Microscopic traffic simulation
- Connected and automated vehicle research
- Traffic safety analysis
- Driver-behavior modeling

---

# Following Gap Analysis

The distance between the leader and follower vehicles was calculated as:

$$
s(t) = x_{\text{leader}}(t) - x_{\text{follower}}(t)
$$

where:

- $s(t)$ = following gap at time $t$
- $x_{\text{leader}}(t)$ = leader vehicle position
- $x_{\text{follower}}(t)$ = follower vehicle position

The resulting gap was plotted against time.

Following distance is important in microscopic traffic analysis because car-following behavior depends strongly on the spacing between consecutive vehicles.

As spacing decreases, a following vehicle generally needs to reduce acceleration or decelerate. As spacing increases, the follower may accelerate toward its desired speed.

This relationship forms an important component of the **Intelligent Driver Model**.

---

# Intelligent Driver Model (IDM)

The **Intelligent Driver Model** is a mathematical car-following model that determines the acceleration of a following vehicle based on:

- Current vehicle speed
- Desired speed
- Gap to the leading vehicle
- Relative speed
- Desired following time
- Acceleration capability
- Comfortable braking behavior

Instead of prescribing a vehicle trajectory directly, the IDM calculates acceleration based on the changing relationship between the leader and follower.

---

# Desired Dynamic Gap

The desired following gap is calculated as:

$$
s^* = s_0 + vT + \frac{v\Delta v}{2\sqrt{ab}}
$$

where:

| Parameter | Meaning |
|---|---|
| $s^*$ | Desired dynamic spacing |
| $s_0$ | Minimum spacing |
| $v$ | Follower vehicle speed |
| $T$ | Desired time headway |
| $\Delta v$ | Relative speed |
| $a$ | Maximum acceleration |
| $b$ | Comfortable deceleration |

The desired spacing therefore changes dynamically based on vehicle speed and the interaction between the follower and leader.

When the follower approaches the leader too quickly, the relative-speed component increases the desired gap and produces a stronger deceleration response.

---

# IDM Acceleration Equation

Follower acceleration is calculated using:

```math
a_{\mathrm{IDM}}
=
a
\left[
1 -
\left(\frac{v}{v_0}\right)^\delta -
\left(\frac{s^*}{s}\right)^2
\right]
```

where:

- $a_{\text{IDM}}$ = calculated vehicle acceleration
- $v$ = current follower speed
- $v_0$ = desired free-flow velocity
- $s$ = actual vehicle spacing
- $s^*$ = desired dynamic spacing
- $a$ = maximum acceleration
- $\delta$ = acceleration exponent

The equation combines two major behaviors.

## Free-Flow Behavior

The term

$$
1-\left(\frac{v}{v_0}\right)^\delta
$$

represents the tendency of a vehicle to accelerate toward its desired speed when it is not strongly constrained by a leading vehicle.

As $v$ approaches $v_0$, the amount of additional acceleration decreases.

## Vehicle-Interaction Behavior

The term

$$
\left(\frac{s^*}{s}\right)^2
$$

represents the influence of the leading vehicle.

As the actual spacing $s$ becomes smaller relative to the desired spacing $s^*$, the interaction term becomes larger and the model produces a stronger deceleration response.

This allows the simulated follower to respond dynamically to the motion of the leader.

---

# Simulation Parameters

The implemented IDM simulation used the following parameters:

| Parameter | Value | Description |
|---|---:|---|
| $v_0$ | 30 m/s | Desired velocity |
| $s_0$ | 2 m | Minimum spacing |
| $T$ | 1.5 s | Desired time headway |
| $a$ | 1.0 m/s² | Maximum acceleration |
| $b$ | 1.5 m/s² | Comfortable deceleration |
| $\delta$ | 4 | Acceleration exponent |
| $\Delta t$ | 0.1 s | Numerical simulation time step |

The simulation begins using the **observed initial position and speed of the NGSIM follower vehicle**.

The observed leader trajectory is then used as the external vehicle trajectory controlling the interaction.

---

# Numerical Simulation

The IDM produces an acceleration value at each simulation time step.

The follower vehicle is then advanced through time using **Euler's method**.

## Velocity Update

The simulated velocity is updated using:

```math
v_{i+1}
=
\max
\left(
v_i + a_i\Delta t,\,
0
\right)
```

where:

- $v_i$ = current follower speed
- $a_i$ = calculated IDM acceleration
- $\Delta t$ = simulation time step

The non-negative constraint prevents the simulated vehicle from obtaining an unrealistic negative velocity.

---

## Position Update

The simulated position is updated using:

```math
x_{i+1}
=
x_i + v_i\Delta t
```

where:

- $x_i$ = current vehicle position
- $v_i$ = current vehicle speed
- $\Delta t$ = time step

For this simulation:

$$
\Delta t = 0.1 \text{ s}
$$

At each time step, the program:

1. Determines the current leader-follower gap
2. Calculates the relative velocity
3. Evaluates the IDM acceleration equation
4. Updates follower speed
5. Updates follower position
6. Advances to the next time step

This process transforms a mathematical car-following equation into a time-dependent microscopic traffic simulation.

---

# Computational Workflow

```text
NHTS.csv
   │
   ├── Household & vehicle data
   │
   ├── Data organization
   │
   ├── Categorical analysis
   │
   ├── Distribution analysis
   │
   └── Transportation visualizations


NGSIM.csv
   │
   ├── Leader/follower trajectories
   │
   ├── Time-series analysis
   │
   ├── Following-gap calculation
   │
   └── Observed vehicle behavior
            │
            ▼
     Intelligent Driver Model
            │
            ▼
        IDM Acceleration
            │
            ▼
       Euler Integration
            │
            ▼
   Simulated Follower Trajectory
            │
            ▼
   Observed vs. Simulated Behavior
```

---

# Engineering Visualizations

The Python notebook produces several transportation-engineering visualizations.

## NHTS Analysis

### Figure 1 — Number of Vehicles by Type

Examines vehicle-type composition within the NHTS dataset.

The visualization converts categorical survey information into a form that makes differences in fleet composition easier to recognize.

### Figure 2 — Vehicle Age Distribution: Urban vs. Rural

Compares vehicle-age distributions between urban and rural households.

The overlapping histograms allow differences in the shape, range, and concentration of the two distributions to be visually evaluated.

### Figure 3 — Vehicle Age by Make

Uses boxplots to compare vehicle-age distributions across vehicle manufacturers.

The visualization highlights differences in median age, spread, and potential outliers.

---

## NGSIM Analysis

### Figure 4 — Vehicle Trajectory Comparison

Examines the behavior of a selected leader-follower vehicle pair through time.

The trajectory analysis helps demonstrate how the position and movement of one vehicle influence another vehicle in microscopic traffic flow.

### Figure 5 — Gap Distance vs. Time

Tracks the spacing between the leader and follower vehicles.

The plot provides an important intermediate step between raw trajectory data and the car-following simulation because spacing is one of the central inputs to the IDM.

---

## Traffic Simulation

### Figure 6 — NGSIM vs. IDM

Compares observed NGSIM follower behavior with the response produced by the Intelligent Driver Model.

This comparison demonstrates an important transportation-modeling principle:

**A mathematical traffic model should be evaluated against observed traffic behavior rather than assumed to reproduce real drivers exactly.**

Together, the project visualizations progress from descriptive transportation analysis to microscopic traffic modeling.

---

# What the Project Demonstrates

One of the most important aspects of the project is the progression from **observational transportation data analysis to predictive mathematical modeling**.

The NHTS analysis demonstrates how Python can be used to identify and communicate patterns within large transportation datasets.

The NGSIM analysis moves from aggregate transportation information to individual vehicle behavior.

The IDM simulation then goes one step further by using transportation theory and numerical computation to reproduce follower-vehicle motion.

This creates a complete engineering-analysis workflow:

> **Observe → Analyze → Model → Simulate → Compare → Interpret**

---

# Engineering Interpretation

A transportation model should not be treated as an exact reproduction of human driving behavior.

Real drivers may respond differently because of:

- Congestion
- Braking events
- Individual reaction times
- Perceived risk
- Driver aggressiveness
- Roadway conditions
- Surrounding traffic
- Individual preferences

The IDM instead represents driving behavior through a defined set of mathematical parameters.

The comparison between NGSIM observations and IDM simulation therefore illustrates an important principle of transportation modeling:

> **A mathematical traffic model is a simplified representation of real driver behavior and should be evaluated against observed data before being used for engineering conclusions.**

The simulated trajectory is generally smoother than real human driving because the mathematical model follows continuous governing equations, while real drivers exhibit more irregular acceleration and braking behavior.

Model calibration would therefore be an important next step for improving agreement between simulated and observed trajectories.

---

# Engineering Decision-Making

Several modeling decisions influence the results of the simulation.

These include:

- Selection of the NGSIM trajectory pair
- Choice of IDM parameters
- Selection of the numerical time step
- Initial follower position
- Initial follower speed
- Minimum-gap constraint
- Use of Euler integration
- Treatment of physical constraints such as non-negative velocity

These decisions demonstrate an important aspect of computational engineering:

**Programming does not eliminate engineering judgment.**

The computer consistently evaluates the equations provided to it, but the engineer still determines:

- Which model is appropriate
- Which assumptions are reasonable
- Which parameters should be used
- How the results should be interpreted
- Whether the model adequately represents real conditions

---

# Limitations and Future Development

Several extensions could improve the current analysis.

## IDM Calibration

Instead of using one parameter set, parameters such as:

- Desired speed
- Time headway
- Maximum acceleration
- Comfortable deceleration
- Minimum spacing

could be calibrated against observed NGSIM trajectories.

This would allow the model parameters to be selected based on actual driving behavior rather than a single assumed parameter set.

---

## Multiple Vehicle Pairs

The current simulation framework could be extended to multiple leader-follower trajectory pairs.

This would make it possible to investigate variation among drivers and determine whether one IDM parameter set can accurately represent several vehicle interactions.

---

## Quantitative Model Validation

Model performance could be evaluated using quantitative error measures such as:

- Root Mean Square Error (RMSE)
- Mean Absolute Error (MAE)
- Speed error
- Position error
- Spacing error

For example:

```math
\mathrm{RMSE}
=
\sqrt{
\frac{1}{n}
\sum_{i=1}^{n}
\left(
x_{i,\mathrm{sim}}
-
x_{i,\mathrm{obs}}
\right)^2
}
```

where:

- $x_{i,\text{sim}}$ = simulated value
- $x_{i,\text{obs}}$ = observed value
- $n$ = number of observations

This would provide a numerical measure of model performance in addition to graphical comparison.

---

## Sensitivity Analysis

IDM parameters could be systematically varied to determine which parameters have the largest influence on simulated vehicle behavior.

For example, sensitivity could be evaluated for:

$$
T,\quad a,\quad b,\quad s_0,\quad v_0
$$

This could help identify which driver-behavior assumptions most strongly affect simulation results.

---

## Traffic Safety Applications

Trajectory data could also be extended toward surrogate traffic-safety analysis using measures such as:

- Time-to-collision
- Time headway
- Vehicle spacing
- Relative velocity
- Deceleration behavior

---

## Larger Transportation Simulation Workflows

The analysis could eventually be expanded toward:

- Multiple interacting vehicles
- Lane-changing behavior
- Congested traffic conditions
- Network-level simulation
- Connected vehicles
- Automated vehicles
- Traffic-control applications
- Microscopic simulation platforms

---

# Technology Stack

| Tool | Application |
|---|---|
| Python | Engineering analysis and simulation |
| pandas | Transportation data organization and filtering |
| NumPy | Numerical computation and simulation arrays |
| Matplotlib | Engineering visualization |
| Seaborn | Statistical and time-series visualization |
| Jupyter Notebook | Reproducible engineering workflow |
| NHTS | Household and vehicle transportation data |
| NGSIM | Microscopic vehicle trajectory data |
| IDM | Car-following simulation |
| Euler's Method | Numerical time integration |

---

# Repository Contents

| File | Description |
|---|---|
| [`CIVE202_Spring2026_Group18_Project3_PythonCode.ipynb`](./CIVE202_Spring2026_Group18_Project3_PythonCode.ipynb) | Complete Python transportation analysis, visualization, and IDM simulation |
| [`CIVE202_Spring2026_Project3_Report.pdf`](./CIVE202_Spring2026_Project3_Report.pdf) | Detailed engineering report and interpretation |
| [`CIVE202_Spring2026_Group18_Project3_ACD.pdf`](./CIVE202_Spring2026_Group18_Project3_ACD.pdf) | Annotated Code Document explaining the Python workflow |
| [`CIVE202_Spring2026_Group18_Project3_Scope.pdf`](./CIVE202_Spring2026_Group18_Project3_Scope.pdf) | Project Scope of Work |
| [`CIVE202_Spring2026_Project3_GanttChart.xlsx`](./CIVE202_Spring2026_Project3_GanttChart.xlsx) | Engineering project schedule |
| [`NHTS.csv`](./NHTS.csv) | Transportation survey dataset used for household and vehicle analysis |
| [`NGSIM.csv`](./NGSIM.csv) | Vehicle trajectory dataset used for microscopic traffic analysis and simulation |

---

# Running the Analysis

Clone the repository:

```bash
git clone https://github.com/bhuwanraj-singh-parihar/Project_3-Transportation_Data_Analysis_and_Simulation.git
```

Move into the project directory:

```bash
cd Project_3-Transportation_Data_Analysis_and_Simulation
```

Install the required Python packages:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
CIVE202_Spring2026_Group18_Project3_PythonCode.ipynb
```

Keep `NHTS.csv` and `NGSIM.csv` in the same directory as the notebook so that the existing data-loading cells can run without modifying the file paths.

---

# Transportation Engineering Relevance

This project demonstrates skills applicable to transportation-engineering work involving:

- Traffic operations
- Transportation planning
- Traffic simulation
- Transportation data analytics
- Intelligent transportation systems
- Vehicle trajectory analysis
- Mobility data
- Microscopic traffic modeling
- Connected and automated vehicle research
- Data-driven engineering decision-making

The project particularly demonstrates the ability to connect **civil engineering theory with computational analysis**, rather than using Python only for generic data processing.

It also shows experience working across two different scales of transportation information:

### System and Household Level

NHTS data provides insight into broader transportation and vehicle characteristics.

### Individual Vehicle Level

NGSIM trajectory data provides detailed information about vehicle interactions through time.

### Model Level

The IDM converts those microscopic traffic concepts into a mathematical and computational representation of driver-following behavior.

---

# Key Takeaway

The central outcome of this project is the integration of three different levels of transportation analysis:

**Travel Behavior and Vehicle Characteristics**

↓

**Observed Microscopic Vehicle Trajectories**

↓

**Mathematical Car-Following Simulation**

By combining NHTS data analysis, NGSIM trajectory analysis, and IDM simulation within one Python workflow, the project demonstrates how programming can be used to investigate transportation systems from both a **data-driven** and **model-based engineering** perspective.

---

# Project Context

**Course:** CIVE 202 — Civil Engineering Analysis II  
**University:** University of Nebraska–Lincoln  
**Project:** Project #3 — NHTS and NGSIM Data Visualization & Simulation  
**Client Context:** Federal Highway Administration (FHWA)  
**Semester:** Spring 2026

---

# Author

**Bhuwanraj Singh Parihar**  
Civil Engineering  
University of Nebraska–Lincoln

**Engineering Interests:** Transportation Data Analysis • Traffic Simulation • Structural Engineering • Engineering Automation
