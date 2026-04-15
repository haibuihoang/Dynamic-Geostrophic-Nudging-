# Dynamic Geostrophic Nudging (DGN)

### Manuscript Under Review
**The methodology demonstrated in this repository is associated with the following manuscript, which is currently submitted to *Wind Energy Science*:**

> **Title:** Dynamic Geostrophic Nudging (DGN): A Novel Method for Controlling the Background Flow in Large Eddy Simulation  
> **Authors:** Hai Bui*, Mostafa Bakhoday-Paskyabi, Joachim Reuder  
> **Affiliation:** Geophysical Institute and Bergen Offshore Wind Centre, University of Bergen, Norway.  
> *\*Corresponding author: hai.bui@uib.no*

---

## Overview

Initializing idealized Large-Eddy Simulations (LES) for wind energy and boundary-layer meteorology presents a persistent challenge. Traditional methods of forcing the domain with a constant geostrophic wind ($\mathbf{G}$) result in slow convergence due to the Ekman spiral and severe inertial oscillations. This typically requires 12 to 24 hours of computational spin-up time before the boundary layer reaches a stationary target state.

**Dynamic Geostrophic Nudging (DGN)** is a novel, closed-loop control strategy designed to solve this problem. Instead of applying unphysical Newtonian relaxation directly to the velocity field, DGN acts dynamically on the large-scale forcing parameters (the geostrophic wind components). 

By explicitly incorporating the flow's current tendency and the error from the target velocity, DGN:
1. **Actively damps inertial oscillations**, changing the system response from oscillatory to a pure exponential decay.
2. **Reduces spin-up time** from 12–24 hours to approximately 2 hours.
3. **Automatically discovers the required forcing**, eliminating the need for expensive trial-and-error initialization.
4. **Preserves physical turbulence structures**, as it modifies large-scale forcing without adding artificial source terms to the resolved turbulent eddies.

## Core Formulation

The controller dynamically adjusts the geostrophic wind components ($U_g, V_g$) to achieve a target wind vector ($u_r, v_r$) at a specific reference height. The required updates are calculated as:

$$ \Delta U_g = -\frac{1}{f} \left[ \left(\frac{d\overline{v}}{dt}\right)_{\text{prior}} + \frac{\overline{v} - v_{r}}{\tau} \right] $$

$$ \Delta V_g = \frac{1}{f} \left[ \left(\frac{d\overline{u}}{dt}\right)_{\text{prior}} + \frac{\overline{u} - u_{r}}{\tau} \right] $$

Where $f$ is the Coriolis parameter, $\tau$ is the relaxation timescale, and $\overline{u}, \overline{v}$ are the filtered, horizontally-averaged wind components at the target height. Refer to the associate paper for the complete description of the method.

This repository contains a **Jupyter Notebook** that provides an 1D theoretical demonstration of the DGN method.

For the complete **3D WRF-LES implementation** used in our research, which is built upon the WRF-SADLES framework, please refer to the main manuscript and our official Zenodo archive:
 **[https://doi.org/10.5281/zenodo.19591182](https://doi.org/10.5281/zenodo.19591182)**


## Citation

If you use the DGN method or the associated code in your research, please cite our paper (Update pending publication):

```bibtex
@article{bui202Xdynamic,
  title={Dynamic Geostrophic Nudging (DGN): A Novel Method for Controlling the Background Flow in Large Eddy Simulation},
  author={Bui, Hai and Bakhoday-Paskyabi, Mostafa and Reuder, Joachim},
  journal={Wind Energy Science},
  year={202X},
  note={Submitted}
}
```

## Contact

For questions or bug reports regarding the 1D demonstration, please open an issue in this repository or contact **Hai Bui** at [hai.bui@uib.no](mailto:hai.bui@uib.no).

