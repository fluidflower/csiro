## Physics

### PDEs

One mass balance per component ![\kappa](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Ckappa) (water and CO2).

![\frac{\partial M^{\kappa}}{\partial t}  + \nabla\cdot \mathbf{F}^{\kappa} - q^{\kappa} = 0
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cfrac%7B%5Cpartial+M%5E%7B%5Ckappa%7D%7D%7B%5Cpartial+t%7D++%2B+%5Cnabla%5Ccdot+%5Cmathbf%7BF%7D%5E%7B%5Ckappa%7D+-+q%5E%7B%5Ckappa%7D+%3D+0%0A)

where the mass of each species is (summed over each phase ![\beta](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbeta))

![M^{\kappa} = \phi\sum_{\beta}S_{\beta}\rho_{\beta}\chi_{\beta}^{\kappa}](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+M%5E%7B%5Ckappa%7D+%3D+%5Cphi%5Csum_%7B%5Cbeta%7DS_%7B%5Cbeta%7D%5Crho_%7B%5Cbeta%7D%5Cchi_%7B%5Cbeta%7D%5E%7B%5Ckappa%7D)

and the flux of each component ![\mathbf{F}^{\kappa}](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cmathbf%7BF%7D%5E%7B%5Ckappa%7D) is the sum of advective and diffusive fluxes ![\mathbf{F}^{\kappa} = \mathbf{F}^{\kappa}_{\mathrm{advective}}+
\mathbf{F}^{\kappa}_{\mathrm{diffusion}}](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cmathbf%7BF%7D%5E%7B%5Ckappa%7D+%3D+%5Cmathbf%7BF%7D%5E%7B%5Ckappa%7D_%7B%5Cmathrm%7Badvective%7D%7D%2B%0A%5Cmathbf%7BF%7D%5E%7B%5Ckappa%7D_%7B%5Cmathrm%7Bdiffusion%7D%7D)

where the advective flux is given by Darcy's law, and the diffusive flux is the usual Fickian diffusion.

All parameters above are their usual values (e.g., porosity, density etc).

### Constitutive relations

#### Fluid-matrix interaction

* **Capillary pressure:** Brooks-Corey
  ![p_c(S_{l}) = p_\text{entry}S_{le}^{-1/\lambda}](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+p_c%28S_%7Bl%7D%29+%3D+p_%5Ctext%7Bentry%7DS_%7Ble%7D%5E%7B-1%2F%5Clambda%7D%0A)

* **Relative permeability:** Brooks-Corey
![ k_{\mathrm{r, w}} = \left(S_{\mathrm{eff}}\right)^{(2 + 3 \lambda)/\lambda}](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle++k_%7B%5Cmathrm%7Br%2C+w%7D%7D+%3D+%5Cleft%28S_%7B%5Cmathrm%7Beff%7D%7D%5Cright%29%5E%7B%282+%2B+3+%5Clambda%29%2F%5Clambda%7D)
and
![ k_{\mathrm{r, nw}} = (1 - S_{\mathrm{eff}})^2 \left[1 - \left(S_{\mathrm{eff}}\right)^{(2 + \lambda)/\lambda}\right]](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle++k_%7B%5Cmathrm%7Br%2C+nw%7D%7D+%3D+%281+-+S_%7B%5Cmathrm%7Beff%7D%7D%29%5E2+%5Cleft%5B1+-+%5Cleft%28S_%7B%5Cmathrm%7Beff%7D%7D%5Cright%29%5E%7B%282+%2B+%5Clambda%29%2F%5Clambda%7D%5Cright%5D)

#### Phase composition: Applied equations of state

* **CO2 in liquid phase:** Calculated using fugacity formulation of Spycher et al. (2003) and Spycher et al. (2005)

* **Water in gas phase:** Calculated using fugacity formulation of Spycher et al. (2003) and Spycher et al. (2005)

#### Density

* **Liquid phase:** Water density calculated using IAPWS Industrial Formulation, density change due to dissolved CO2 calculated using formulation by Garcia, 2001.

* **Gas phase:** Approximated as pure CO2, with properties calculated using the Span and Wagner (1996) EOS.

#### Solubility limit

CO2 solubility at base of tank 1.786 kg/m3 (0.001782 kg/kg)

### Temperature

20°C

### Domain volume

The volume of the sand region (NOT including water region at top of tank) 0.0865 m3.
The pore volume of the model is 0.0383 m3.

### Spatial parameters

The parameters ![k, \phi, p_\text{entry}, \lambda, S_{lr}, S_{gr},  k_{lr}, k_{gr}, ](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+k%2C+%5Cphi%2C+p_%5Ctext%7Bentry%7D%2C+%5Clambda%2C+S_%7Blr%7D%2C+S_%7Bgr%7D%2C++k_%7Blr%7D%2C+k_%7Bgr%7D%2C+) for the different facies are given in [spatial_parameters.csv](spatial_parameters.csv).

## Numerics

### Coupling of flow and transport, temporal and spatial discretization

Fully coupled, fully implicit, cell-centered FV.

### Linearization and Solvers

Newton with line search, direct solver (MUMPS) for the linear systems.

### Primary Variables

Persistent set of primary variables comprising fluid pressure and total mole fraction of CO2 summed over all phases, with gas saturation calculated using a compositional flash see [MOOSE documentation](https://mooseframework.inl.gov/modules/porous_flow/persistent_variables.html) for details.

### Computational Grid

Uniform structured grid of 44,284 quadrilateral elements (approx dimensions of each element is 10mm x 10mm).

### Performance

During the injection period (0 to 5 hours)

| Indicator                            |  Average |      Min |      Max | Median |
|:-------------------------------------|---------:|---------:|---------:|--------:|
| time step size [s]                   | 1.96     | 0.0078125   |        2 | 2 |
| # nonlinear iterations per time step |      3 |      1 |      15 | 3 |
| # linear iterations per solve        |      1 |      1 |      1 | 1 |

During the subsequent rest period (5 to 120 hours)

| Indicator                            |  Average |      Min |      Max | Median |
|:-------------------------------------|---------:|---------:|---------:|--------:|
| time step size [s]                   | 35.92     | 0.15625   |        60 | 20 |
| # nonlinear iterations per time step |      3 |      1 |      15 | 2 |
| # linear iterations per solve        |      1 |      1 |      1 | 1 |
