## Installation of the conda
1. Go to the [anaconda web-site](https://www.anaconda.com/products/distribution) and download distribution.
2. After installation update anaconda navigator, if needed.
3. Open *enviroments* tab and create new enviroment.<img style="display: block; margin-left: auto;margin-right: auto;width: 100%;"src="./images/step1.jpg"> </img>
4. Name it, e.t. *For_EOA*. Change Python version, if necessary.<img style="display: block; margin-left: auto;margin-right: auto; width: 100%;"src="./images/step2.jpg"> </img>
5. Install VS Code from home panel or [download it](https://code.visualstudio.com).<img style="display: block;  margin-left: auto; margin-right: auto; width: 100%;" src="./images/step3.jpg"> </img>
---

## Calculation of the effective orifice area (EOA).
#### Data was given from two sources:
1. Spreadsheet cantaining volumetric flow in/out in $m^3/s$, pressure in/out in $Pa$ and corresponding timesteps in seconds.
2. Spereadsheet containing the adjusted flow rate in $ml/s$ corresponding to time in seconds. Calculation of the mean pressure gradient:
$$\Delta P_{mean} = \dfrac{1}{T_{systole}} \int_{T_{systole}} (P_{vent} - P_{aortic}) dt,$$
where $P_{vent}$ and $P_{aortic}$ are the ventricular and aortic pressures, respectively.

#### The mean pressure difference is calculated by integrating the pressure difference over the duration of systole.
$\Delta P_{mean}$ was calculated with data from source 1. In `Python` realisation of the integral is basically Rimman's sum, since $dt \rightarrow 0$ and  $\Sigma\equiv$ $\Delta P_{mean}$. Mentioned goes in two steps:

1. `df['d_P'] = (df.query('flow > 0')['p_vent'] - df.query('flow > 0')['p_aort']) * df.query('flow > 0 and time < 0.26')['timestep']`,

where difference in the parenthesis equivalent to $(P_{vent} - P_{aortic})$ and multiplication is given by
`df.query('flow > 0 and time < 0.26')['timestep']`.

2. `d_P = df.query('d_P > 0')['d_P'].sum() / (df.query('flow > 0')['timestep'].sum())`,
where `d_P = df.query('d_P > 0')['d_P'].sum()` - mentioned sum and `df.query('flow > 0')['timestep'].sum()` - $T_{systole}$. $T_{systole}$ is the duration of systole
$$T_{systole} = t_2 - t_1,$$
where $t_1$ is the time at the start of the positive differential pressure period (time period between start of positive differential pressure and end of positive differential pressure)

Calculation of the effective orifice area:
$$EOA = \dfrac{Q_{RMS}}{51.6\sqrt{\dfrac{\Delta P}{\rho}}},$$
where $Q_{RMS}$ is the root mean square of the flow rate, $\Delta P$ is the mean pressure difference and $\rho$ is the density of blood. Was calculated with data from source 2. Calculation of the root mean square of the flow rate:
$$q_{v_{RMS}} = \sqrt{\dfrac{\int_{t_1}^{t_2}q_v^2(t)dt}{t_2 - t_1}}$$


<img 
    style="display: block; 
           margin-left: auto;
           margin-right: auto;
           width: 85%;"
    src="./images/main_plot.svg">
</img>
