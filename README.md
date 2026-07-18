
# Parametric Simulation of Electromagnetic Braking Systems via Finite Element Analysis
## 1. Project Overview
This project delivers an automated structural and physical optimization tool written in Python,
leveraging the FEMM (Finite Element Method Magnetics) core solver API via the pyfemm
library. The primary objective is to evaluate the mitigation of eddy current losses (Joule heating)
in rotary braking systems by introducing radial slots into a conductive aluminum disk.


## 2. Theoretical Overview

In standard electromagnetic brakes, a conductive disk rotating through a magnetic field experiences induced eddy currents, leading to a braking torque via Lorentz forces. However, excessive continuous current pathways cause significant thermal stress through Joule heating:

```math
P_{Joule} = \iiint_{V} \frac{\mathbf{J}^2}{\sigma} dV
```
Where:
• J is the current density vector (A/m2).
• σ is the electrical conductivity of the material (S/m).
• V is the volume of the conductive medium.
By introducing N radial slots filled with air (acting as a dielectric insulator where σ ≈ 0),
the macroscopic continuous pathways of the induced current loops are mechanically obstructed.
This simulation computes the structural efficiency factor η, defined as:
```math
\eta = \frac{P_N}{P_0}
```
Where $P_N$ represents the total integrated Joule losses for N radial slots, and  $P_0$  is the
unslotted reference baseline.
## 3. Automation Pipeline Features
1. **Parametric Mesh Geometry**: Automated generation, rotation, and placement of the
N radial slot boundaries using custom coordinate rotation matrices.
2. **Defensive Meshing**: Application of a dynamic angular offset to the initial slot boundary
to prevent critical overlapping on the axis limits   (Y = 0), eliminating mesh singularities.
3. **Integrated Execution Pipeline**: Autonomous generation of planar current flow files
(.fec), execution of the numerical finite element solver (femm.ci_analyze()), seamless
solution loading in the post-processor, and automated extraction of volume integrals.
## 4.Analytical Results & Visualization
The automated extraction routine tracks the structural degradation of power losses. As the
number of radial slots (N ) increases, geometric constraints force the current density field to
redistribute, dropping the overall loss profile.
The resulting relative efficiency curve η = f (N ) is plotted and saved locally at runtime as
Courbe_Efficacite_Eta.png, validating the direct correlation between structural geometry and
thermomechanical performance
## 5. Execution & Installation

**Prerequisites**: Ensure you have the standalone desktop application **FEMM** installed on your machine and linked to your system path.

**Run the Pipeline**

Clone the repository and run the simulation:

```bash
git clone https://github.com/zizozozo/electromagnetic-simulation-via-femm.git
cd electromagnetic-simulation-via-femm
python simulation_disque.py
