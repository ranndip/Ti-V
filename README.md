# TiV Training Database and LAMMPS Simulations

This repository(.tar.gz file) contains the training database for Density Functional Theory (DFT) simulations, specifically for the TiV alloy system. The database is in the `TiV_training_database` folder and follows the LAMMPS dump format. Additionally, LAMMPS simulation files are available for use with the RANN potential, located in the `TiV_training_lammps_simulation` folder.

## DFT Training Database

The DFT training database, located in the `TiV_training_database` folder, is structured in the LAMMPS dump format. It can be visualized using the OVITO software. Below is a description of the format used in the DUMP file:

### DUMP File Format

1. **ITEM: TIMESTEP**  
   Contains information about each DFT simulation step:
   - `energy`: Total energy of the system (eV) obtained from VASP.
   - `energy_weight`, `force_weight`: Weights used in training.
   - `nsims`: Number of simulations included in this file.

2. **ITEM: NUMBER OF ATOMS**  
   Specifies the total number of atoms for each timestep.

3. **ITEM: BOX BOUNDS xy xz yz pp pp pp**  
   Describes the LAMMPS simulation box. Refer to [LAMMPS Triclinic Box Format](https://docs.lammps.org/Howto_triclinic.html) for more details.

4. **ITEM: ATOMS id type x y z fx fy fz**  
   - `id`: Atom ID.
   - `type`: Atom type (`Ti=1`, `V=2`).
   - `x, y, z`: Coordinates of the atom.
   - `fx, fy, fz`: Forces on the atom from VASP (in eV/Å).

## DFT INCAR Settings

The same INCAR file was used for all DFT calculations. Below are the key parameters:

- **System**: TiV
- **ALGO**: Normal
- **EDIFF**: 1E-07
- **PREC**: Accurate
- **LASPH**: True
- **LORBIT**: 10
- **LREAL**: .FALSE
- **NELM**: 300
- **ENCUT**: 520.0
- **IBRION**: -1
- **ISIF**: 2
- **ISMEAR**: 0
- **SIGMA**: 0.2
- **ISYM**: 0
- **ADDGRID**: .TRUE.
- **NCORE**: 4
- **LWAVE**: F
- **LCHARG**: F
- **LELF**: F

## KPOINTS

All KPOINTS were generated using a K-Spacing value of 0.020 to create the K-Mesh.

## POTCAR Files

- **Ti_sv**: PAW_PBE Ti_sv (26Sep2005)
- **V_sv**: PAW_PBE V_sv (02Aug2007)

## LAMMPS Simulations

The LAMMPS simulation files are located in the `TiV_training_lammps_simulation` folder. These files use the RANN potential.

### Running LAMMPS Simulations

To run LAMMPS simulations, follow these steps:

1. Navigate to the `TiV_training_lammps_simulation` folder.
2. Use the `mcswap.in` file to initiate the LAMMPS simulation.
3. The LAMMPS source code is available in the `TiV_training_lammps_simulation/lammps-23Jun2022` folder.
4. The RANN source code is already placed in the `src` directory. To build LAMMPS with the RANN potential, use the following command:
   ```
   cd src
   make -j10 mpi
```
