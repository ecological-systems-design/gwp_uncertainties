Welcome to gwp_uncertainties!
=============================

This package allows computation of uncertainties in GWP and AGWP values for environmental flows with known radiative efficiencies, lifetimes and their respective perturbations.

Table values for all flows are stored in the data/ipcc2013.json file and have been taken from the following resources

- Molecular weights from https://pubchem.ncbi.nlm.nih.gov/
- Radiative efficiencies and lifetimes
  - for most flows can be found in the IPCC Climate Change report from 2013, Chapter 8 and Table 8.A.1
  - data/ipcc2013.json contains "_comment" field with the exact source table and matching name of a given flow in the IPCC report

Here we only consider flows that are present in the Life Cycle Assessment method ("IPCC 2013", "climate change") with time horizons of 20 and 100 years.

For the uncertainty calculations we employ a method based on first-order Taylor expansion as suggested in the Supplementary Material of the IPCC Climate Change report from 2013 (see Chapter 8.SM). Given a function $$y = f(x_1,...,x_k),$$ the uncertainty in `f` can be computed as follows:

$$\Delta f = \sqrt{\sum_i (\Delta f_i)^2} = \sqrt{\sum_i \big( \frac{\partial f}{\partial x_i} \Delta x_i  \big)^2}, $$

where in our case, `f` is a function that computes GWP values, and inputs `x` depend on the flow:
- `x = (lifetime, radiative efficiency)` for all flows except for methane and nitrous oxide
- `x = (lifetime, radiative efficiency, f1, f2)` for methane and nitrous oxide (see 8.SM.11.3.2 and 8.SM.11.3.3 of the IPCC supplementary materials), where `f1` is added due to effects on ozone and `f2` is due to stratospheric H2O.

Uncertainties in the inputs `x` are given in Table 8.SM.12 and Section 8.3.1. Uncertainty ![\Delta f
](https://render.githubusercontent.com/render/math?math=%5Ctextstyle+%5CDelta+f%0A%0A) corresponds to a 90% confidence interval, and is converted to standard deviation of normal distribution by scaling it down by 1.645. 

A special case is carbon monoxide, where we assume uniform distribution (see Table 8.A.4).

Note that
- Uncertainties in NOx and VOC have not been taken into account in the current implementation. GWP values are given in Tables 8.A.3 and 8.A.5 respectively.

Results
=======
![flows_gwp_uncertainties](docs/gwp_uncertainties.svg)

![table values](docs/gwp_uncertainties_table.png)
