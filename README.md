# L2 Sea Benchmark

## NATO AVT-331 — Goal-driven, multi-fidelity approaches for military vehicle system-level design

**L2 Sea Benchmark**  
Andrea Serani, Matteo Diez

📄 [Paper](./doc/2022-M-Pellegrini_etal.pdf)  
📊 [Presentation](./doc/NATO-AVT-331%20Sea%20Team%20L2%20Problem.pdf)  

---

## 🌊 Overview

This repository distributes the **L2 Sea Benchmark**, developed within the NATO AVT-331 context.

The benchmark provides a **multi-fidelity hydrodynamic test case** based on the **DTMB-5415 hull**, and is used in:

- multi-fidelity optimization  
- uncertainty quantification (UQ)  
- surrogate-based modeling  

The repository is primarily intended to **share the benchmark**.  
The source code is included and can be used for simulations, but it should be considered a **reference implementation**.

---

## 🖼️ Benchmark geometry

![DTMB 5415 hull](docs/images/dtmb5415.png)

*(Add here a representative image of the DTMB-5415 hull or benchmark setup)*

---

## 🔗 External usage

This benchmark is included in the benchmark library of :contentReference[oaicite:0]{index=0} and is used for uncertainty quantification and optimization studies.

In this context, the L2 Sea benchmark is exposed through a standardized model interface and can be accessed within containerized workflows.

Reference implementation:

- https://github.com/UM-Bridge/benchmarks/tree/main/benchmarks/l2-sea-optimization  
- https://um-bridge-benchmarks.readthedocs.io/en/docs/

---

## ⚙️ Tool description

- Computes **calm-water resistance** of the **DTMB-5415 hull** (model scale)
- Operating condition: **Fr = 0.28**
- Solver: **linear potential flow**
- Language: **Fortran**

Platform support:

- Linux  
- Windows Linux Subsystem (WSL)  

Compilers:

- GNU (`gfortran`)
- Intel (`ifort`)

Required libraries:

- GNU:
  - LAPACK
  - BLAS
- Intel:
  - MKL

Parallelization:

- OpenMP supported (optional)

---

## 📁 Repository structure

- `src/` → source code  
- `bin/` → compiled executables  
- `doc/` → documentation and references  
- `examples/DTMB-5415/` → example benchmark setup  
- `results/` → archived results  
- `scripts/` → auxiliary scripts  

---

## 🛠 Compilation

### 1. Stack size

Add to `.bashrc`:

    ulimit -s unlimited

---

### 2. Configure Makefile

Open the `Makefile` in the root directory and select the compiler.

#### Intel compiler

    FC       = ifort
    FCOPT    = -O5
    FCOPTOMP = -qopenmp
    LIB      = -mkl

#### GNU compiler

    FC       = gfortran
    FCOPT    = -O3
    FCOPTOMP = -fopenmp
    LIB      = -llapack -lblas

⚠️ Under WSL, ensure OpenMP is available.  
Otherwise, comment out `FCOPTOMP`.

---

### 3. Build

    make

---

## 🎯 Benchmark setup

The potential flow solver can be run:

- at **even keel**
- with **2DoF**

For benchmark purposes:

- simulations are performed at **even keel**
- example files are already configured accordingly

---

## 🔢 Fidelity levels

Up to **7 fidelity levels** are available.

They are controlled through the `SBDF.nml` file.

---

## 📄 Input files

Only two files need to be modified:

- `SBDF.nml`
- `variables.inp`

---

### SBDF.nml

Contains all namelists.

To select the fidelity level, edit:

    igrid = 7    ! Grid/fidelity level (1 = highest)

Total number of levels:

    ngrid = 7

---

### variables.inp

- Column text file  
- 14 lines → 14 design variables  
- Each value must be within:

    [-1, 1]

---

## 🚀 How to run

Move to the example directory:

    cd examples/DTMB-5415

Run the executable from the `bin/` directory.

---

## 📊 Output

A folder named:

    CPU000

will be created containing all input and output files.

Objective function and constraints are stored in:

    objective.out

---

## 📦 Example

A ready-to-run benchmark case is available in:

    examples/DTMB-5415/

It includes:

- `SBDF.nml`
- `variables.inp`
- all required auxiliary files

---

## 📚 References

References are available in the `doc/` folder.

Key publications:

- Pellegrini, R., Serani, A., Liuzzi, G., Rinaldi, F., Lucidi, S., & Diez, M. (2022).  
  *A Derivative-Free Line-Search Algorithm for Simulation-Driven Design Optimization Using Multi-Fidelity Computations*.  
  Mathematics, 10(3), 481.

- Serani, A., Stern, F., Campana, E. F., & Diez, M. (2021).  
  *Hull-form stochastic optimization via computational-cost reduction methods*.  
  Engineering with Computers.

- Serani, A., Diez, M., Wackers, J., Visonneau, M., & Stern, F. (2019).  
  *Stochastic shape optimization via design-space augmented dimensionality reduction and RANS computations*.  
  AIAA SciTech Forum.

Additional documents:

- `doc/2022-M-Pellegrini_etal.pdf`
- `doc/2021-AIAA-SciTech-Liuzzi_etal.pdf`
- `doc/2019-AIAA-SciTech-Serani_etal-ECN.pdf`
- `doc/NATO-AVT-331 Sea Team L2 Problem.pdf`

---

## 📜 License

See:

    LICENSE

---

## 🌐 Links

MAO Research Group:  
https://cnr-inm-mao.github.io/

