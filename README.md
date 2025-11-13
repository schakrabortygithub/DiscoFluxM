# DiscoFluxM: Dislocation Transport-based Crystal Plasticity material model

LANL code no: O4684

All right belongs to Los Alamos National Laboratory(LANL)

Also hosted at LANL Github page: [https://github.com/lanl/DiscoFluxM](https://github.com/lanl/DiscoFluxM)

=====
This is a Dislocation Transport-based Crystal Plasticity Material Model(DiscoFlux), implemented within MOOSE framework(https://mooseframework.inl.gov/index.html).

# Features
1. The material model represents the dislocation within a crystalline material in the form of density.
2. Total dislocation density is split into four categories: edge_positive, edge_negative, screw_positive, screw_negative.
3. Dislocation densities in each of the slip_systems are represented as an independent solution variable(coupled). As an example, this leads to 48 solution variables for fcc crystal plus three displacements. Total 51 DOFs per node. Solution variables are grouped into four array variables.
4. Dislocation densities have both local and nonlocal evolution terms in it. The local evolution is represented in the rate form. The nonlocal evolution is relaized by the transport of dislocation within the grain and transfer of dislocation across the grain boundary(GB).
5. At the GB, dislocations can get transferred from one slip_system to a different one acording to the mis-orientation between the two grains. A geometric criterion, incorporating slip_direction, slip_plane_normal and gb_plane_normal in the rotated configuration, is used to determine the direction of transfer at the grain boundary.
6. Implemented using Total Lagrangian Formulation and implicit time integration. 
7. Discretization used is Finite ELemet Method.
8. This one implementation can be used for three types of crystal plasticity models:
  (a) Local Crystal Plasticity.
  (b) Nonlocal crystal plasticity with dislocation transport within the grain.
  (c) Nonlocal crystal plasticity with dislocation transport within the grain and across the grain boundary.

# Sample results
![Polycrystal Geometry](https://github.com/lanl/DiscoFluxM/blob/master/test/tests/SimulationResults/G18_Comp_Geometry_Stress_Strain.png?raw=true)
![Polycrystal Geometry](https://github.com/lanl/DiscoFluxM/blob/master/test/tests/SimulationResults/G18_Comp_VMStress.png?raw=true)
![Polycrystal Geometry](https://github.com/lanl/DiscoFluxM/blob/master/test/tests/SimulationResults/G18_Comp_GNDdensity.png?raw=true)

# Installation instruction
1. Download/clone the modified version of moose from LANL-Gitlab.
2. Set-up the conda and required libraries according to the instruction given in moose website: https://mooseframework.inl.gov/getting_started/installation/conda.html
3. Download/clone 'DiscoFluxM' repository. 
4. Go inside the repository: cd ./DiscoFluxM
5. Compile the code: make -j 2


# Instruction to run simulation
1. Generate the polycrystal mesh for your problem of interest.
2. Make sure the the mesh contains each grain as a seprate element-set. 
3. All boundary-sets should be there to impose any boundary_condition as well as interface_condition(for dislocation transfer across GB).
4. 

# Things to keep in mind
1. The gradient based terms in the computation of back_stress are sensitive to physical dimension of the domain and mesh size. This may cause convergence issue, if numerical parameters are not set properly. Even one highly skewed element can cause convergence issue. 
2. It's worthwhile to do some experiment to find proper preconditioner when using Jacobian Free(kind of) solvers (e.g., PJFNK).
3. 

# Known Issues
1.

# Features under development
1. 



