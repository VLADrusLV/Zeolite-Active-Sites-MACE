# Data for "Common structural motifs of Fe-species at paired Al sites in MFI, FER, and FAU zeolites for DeNOx applications"

This repository contains the supplementary data, optimized atomic coordinates (`.xyz` files), and machine learning datasets associated with the manuscript submitted to *Molecular Catalysis*. 

The study investigates the structure-activity relationships of Fe-modified zeolites (MFI, FER, and FAU) for DeNOx applications. By combining Genetic Algorithms (GA), equivariant neural network potentials (MACE), and periodic Density Functional Theory (DFT), we modeled large adaptive zeolite clusters (~140 atoms) to evaluate the "Redox Strain" and "topological ceiling" of binuclear iron active sites.

## Repository Structure

The repository is rigorously organized to reflect the computational workflow and clustering parameters:

* **`GA_Structures/`**
  Contains the raw `.xyz` structural ensembles and ASE trajectory (`.traj`) files generated during the high-throughput screening. The .traj files preserve all comprehensive meta-information in population from the Genetic Algorithm runs in the Atomic Simulation Environment (ASE).
  * **Hierarchy:** `[Framework Name] (e.g., MFI, FER, FAU) / [Fe Species] (e.g., Fe, Fe2O, Fe2O2)`
  * **`*CORE_CLUSTERS/`**: A dedicated subfolder containing the initial, bare zeolite clusters prior to the introduction of iron species.

* **`Optimized_Clusters/`**
  Contains all final `.xyz` coordinates optimized using MACE potentials. This directory is divided into two main parts:
  * **`XYZ_FILES/`**: Features a deep hierarchical structure that precisely tracks the framework, species, clustering thresholds, and specific substitution sites.
    * **Hierarchy Path:** `XYZ_FILES / [Framework] / [Species] / [AHC Accuracy Threshold] / [Al Substitution Indices] / [Unique GA Index] / [filename.xyz]`
    * *Example:* `Optimized_Clusters/XYZ_FILES/MFI/Fe2O/0.03/240_269/11/MFI_240_269_iter5_132_mace_omat_pbe_d3.xyz`
  * **`FINAL_PAIR/`**: A dedicated subfolder containing the rigorously matched pairs of optimized $[Fe_2O]^{2+}$ and $[Fe_2O_2]^{2+}$ clusters anchored at the *exact same* cation-exchange site. These specific pairs are used to calculate the "Redox Strain" descriptor.
    * **Hierarchy Path:** `FINAL_PAIR / [Framework] / [Al Substitution Index] / [Fe2O.xyz or Fe2O2.xyz]`
    * *Example:* `Optimized_Clusters/FINAL_PAIR/FER/11/Fe2O.xyz`

* **`ML_Dataset/`**
  Contains the comprehensive `features.xlsx` database. This file includes the labeled features of all extracted cluster structures from the zeolite frameworks, which were utilized for the unsupervised learning, Recursive Feature Elimination (RFE), and Lasso regression analysis.

## Computational Details

The structural models and data provided herein were generated using the following computational workflow:
* **Periodic optimization:** CP2K
* **Genetic Algorithm screening:** Atomic Simulation Environment (ASE) with TBLite
* **Machine Learning Potentials:** MACE-MH-1 (for geometry optimization of ~140-atom clusters)
* **Single-point energy & validation:** ORCA (PBEh-3c, MN15/def2-TZVPP)
* **Structural Diversity Analysis:** SOAP descriptors, Agglomerative Hierarchical Clustering (AHC), and DBSCAN

## Authors

* **Vladislav A. Koveza** (koveza.vladislav@yandex.ru)
* **Elena O. Kuziuberdina**
* **Oleg V. Potapenko**

