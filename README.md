## Calculation of the effective orifice area (EOA).
#### Data was given from two sources:
1. Spreadsheet cantaining volumetric flow in/out in $m^3/s$, pressure in/out in $Pa$ and corresponding timesteps in seconds.
2. Spereadsheet containing the adjusted flow rate in $ml/s$ corresponding to time in seconds. Calculation of the mean pressure gradient:
$$\Delta P_{mean} = \dfrac{1}{T_{systole}} \int_{T_{systole}} (P_{vent} - P_{aortic}) dt,$$
where $P_{vent}$ and $P_{aortic}$ are the ventricular and aortic pressures, respectively. The mean pressure difference is calculated by integrating the pressure difference over the duration of systole. Was calculated with data from source 1. Calculation of the effective orifice area:
$$EOA = \dfrac{Q_{RMS}}{51.6\sqrt{\dfrac{\Delta P}{\rho}}},$$
where $Q_{RMS}$ is the root mean square of the flow rate, $\Delta P$ is the mean pressure difference and $\rho$ is the density of blood. Was calculated with data from source 2. Calculation of the root mean square of the flow rate:
$$q_{v_{RMS}} = \sqrt{\dfrac{\int_{t_1}^{t_2}q_v^2(t)dt}{t_2 - t_1}}$$
