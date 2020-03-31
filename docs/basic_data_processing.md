---
title: Basic SAXS data processing
author: Normand Cyr
date: 2020-03-23
...

# Basic data processing

## Plotting the data

In RAW, go to the folder where the radial averaging data from the corrected SAXS images is saved. Using the standard folder hierarchy at the Structural Biology Platform, the `.dat` files will be in

`<project_name>/scattering_data/processed/`

Select the data files you want to plot in the file browser, then click on `Plot`. The individual scattering curves will be plotted on the right, in the Main Plot area as illustrated below.

![](img/sample_plot_all.png "Individual plots, overlaid")

If you have tested multiple concentrations (you should have!), you show see the effect of concentration on the scattering intensity.

![](img/multiple_concentrations.png "Multiple concentrations")


## Averaging multiple acquisitions

Multiple acquisitions of equal duration (typically 5 to 10 acquisitions) are typically performed in order to be able to detect, and discard, data affected by radiation damage (a single, long, acquisition will mask such effect). The data can then be averaged and scattering curves differing significantly can be discarded.

To do this in RAW, go to the `Manipulation` tab, select the curves to average and click on `Average` to perform the operation. Do this for each group of acquisitions (buffer, each individual sample concentration).

You can then click on `Remove` to remove the individual curves and only keep the averaged curve.

![](img/buffer_average.png)

*Note: If certain curves are significantly different, RAW will open a dialog box and ask whether this/these profile(s) should be discarded from the rest of the group. It is important at this point to inspect the individual curves for suspicious divergence from the mean, or potential offset.*

The average scattering profile will appear in RAW and `A_` will be added at the beginning of the file name. An asterisk (`*`) in front of the file name indicates that changes to the file have not been saved.


## Buffer subtraction

Because SAXS is a contrast method where the scattering signal is obtained from the difference in electron density between a molecule in solution and bulk solvent, scattering resulting from the buffer has to be subtracted from the measured scattering of the sample to isolate the sole contribution from the molecule. This is done in RAW by subtracting the averaged buffer scattering curve from the averaged sample scattering curve.

scattering profile = sample scattering - buffer scattering

Select the buffer curve by clicking on the star next to the file name, then select the sample curve then click on `Subtract`. The subtracted scattering profile will appear in the lower panel of RAW and `S_` will be added at the beginning of the file name.

![](img/sample_buffer_subtract.png)

At this point, it is recommended to save the averaged and subtracted curves. This can be done in RAW by selecting the curve in the `Manipulation` tab and clicking on the `Save` button. Using the standard folder hierarchy at the Structural Biology Platform, the `.dat` files for averaged curves should be saved in

`<project_name>/scattering_data/averaged/`

and the `.dat` files for subtracted curves should be saved in

`<project_name>/scattering_data/subtracted/`


### Detecting buffer mismatch

It is important to pay attention and prevent over- or under-subtraction of the buffer. This may happen typically if the proper **matching** buffer was not used (see paragraphs 1 and 2 of the [Sample requirement section](/saxs_experiment/#sample-requirement)).

![](img/buffer_subtraction.png)
Source: [Skou *et al* 2014]

When the data is plotted as a Kratky plot (right curve) (more on the Kratky analysis [below](#kratky-analysis)), the effect is enhanced (note the green curve - over-subtracted - reaching large negative \(y\) values at medium and high \(q\)).


## Guinier analysis

The Guinier approximation is the first analysis step to perform following the acquisition of the data and buffer subtraction in order to assess the quality of the data. Visually, one can detect if the sample presents pathologies in terms of:

- lack of monodispersity
- particles aggregation or repulsion
- extreme deviations from globularity
- concentration-dependent scattering effects.

The Guinier approximation states that, at low \(q\):

$$I(q)\approx I(0)\exp{\frac{-q^2{R_g}^2}{3}}$$

A Guinier plot is contructed by plotting \(\ln{I(q)}\) against \(q^2\). Problematic sample behaviour will exhibit a non-linear trend towards low \(q\), where aggregation will be represented by an upward curve whereas a downward curve will be typical of particles repulsion.

![Guinier plots and aggregation example](img/guinier-aggregation.png)

Source: [Putnam *et al* (2007)]

Both the radius of gyration \(R_g\) (defined as the square root of the average distance of each scatterer from the molecule center) and the scattering intensity at zero angle \(I(0)\) (*ie* forward scattering, when \(q=0\)) can be extracted from the Guinier plot. The slope of the curve is given by \(\frac{-R_g^2}{3}\) and the vertical intercept (at \(q=0\)) will correspond to \(\ln{I(0)}\).

### Guinier plot in RAW

To get a Guinier plot of the subtracted data (`S_A_<experiment_number><sample_name>` file), select the subtracted curve, then right-click and choose the `Guinier Analysis` option. A new window will open and an initial Guinier plot will be generated using AutoRG.

![AutoRG result for Guinier analysis](img/guinier_autoRG.png)

The parameters \(I(0)\) and \(R_g\) are reported, along with their uncertainties, as well as the \(q{R_{g}}_{min}\) and \(q{R_{g}}_{max}\) values. For globular proteins, it is important to aim for \(q{R_{g}}_{max}<1.3\). It is possible that the returned values from AutoRG are a little off, or that the algorithm included initial points that diverge significantly from the linear trend. Manual intervention is possible by changing the \(q_{min}\) (or \(n_{min}\)) and \(q_{man}\) (or \(n_{man}\)) values used for the Guinier fit.

![AutoRG result for Guinier analysis - result of Rg and I0 highlighted](img/guinier_manual_q-range.png)

When you are done, take note of the results: \(R_g\) and \(I(0)\), and their respective uncertainties, and the parameters used to generate the Guinier fit (\(r^2\) of the fit, \(q_{min}\), \(q_{max}\), \(q{R_{g}}_{min}\) and \(q{R_{g}}_{max}\). These values are typically reported in the literature when SAXS data is published.

You can close the window by clicking on `OK`. The results will also be saved in the `### HEADER:` section of the `.dat` file, si it is important to save the changes to the subtracted SAXS profile.

**Quick tip**: in order to retreive the results from the Guinier analysis from the command line, you can use the following command:

`sed -n '/"guinier": {/,/#        }/p' S_A_<experiment_number><sample_name>`

which will output:

```bash
#        "guinier": {
#            "I0": "0.0117971852648",
#            "I0_autorg_err": "4.325E-06",
#            "I0_err": 2.0253688438837957e-05,
#            "I0_est_err": -1,
#            "I0_fit_err": 2.0253688438837957e-05,
#            "Rg": "14.3562754274",
#            "Rg_autorg_err": "0.0193",
#            "Rg_err": 0.04267104548707152,
#            "Rg_est_err": -1,
#            "Rg_fit_err": 0.04267104548707152,
#            "nEnd": 59,
#            "nStart": 2,
#            "qEnd": "0.08954",
#            "qRg_max": "1.28539046271",
#            "qRg_min": "0.191875269017",
#            "qStart": "0.01337",
#            "rsq": "0.995046745907"
#        }
```


## Molecular weight analysis

If the sample does not exhibit an aggregation or repulsion behaviour at high (or low) concentrations, a plot of \(I(0)\) *vs* sample concentation will give a linear correlation, and will not be affected by particle shape (\(R_g\) should remain relatively constant). In fact, in terms of absolute scale, \(I(0)\) corresponds to the square of the number of electrons in the scattering sample.

Practically, the scattering intensity \(I(q)\) is measured on a relative scale and one can use a sample of known molecular weight as standard. For example, for proteins, lysozyme (14.3 kDa) and monomeric EGFP (26.9 kDa) (as illustrated by [Myatt *et al.* 2017]) are routinely used at the Structural Biology Platform and recent scattering data at precise concentration are readily available for standardization. From the \(I(0)\) determined using the Guinier analysis above, and the \(I(0)\) of a standard sample, the molecular weight of the sample \(M_{sample}\) can be calculated using the following equation:

$$\frac{I(0)_{sample}}{I(0)_{standard}}=\frac{C_{sample}\times{M_{sample}}}{C_{standard}\times{M_{standard}}}$$

Alternatively, RAW aggregates various algorithms developped to determine the molecular weight of a biomolecule (protein or RNA) based on its SAXS profile (*ie* the buffer-subtracted profile). You simply have to right-click on the subtracted curve filename and select `Molecular weight` in order to open the dialog window.

![Molecular weight dialog window](img/molecular_weights.png)

If a protein standard was previously used and set in RAW, the `I(0) Ref. MW` will be calculated. The `Vc MW` and `Vp MW` are the methods of [Rambo and Tainer (2013)], and of [Piiadov *et al.* (2019)] respectively. More information is provided if you click on the `More info` button. Pros and cons for each method exist. Please read the additional information carefully.

There is also an associated web server, SAXS MoW2 that accompany the approach of Piiadov *et al.* and can be reached at [http://saxs.ifsc.usp.br/](http://saxs.ifsc.usp.br/).


## Kratky analysis

One way to verify the folding of a sample is to plot the data as \(q^2I(q)\) *vs* \(q\). This is called a Kratky plot and can simply be generated in RAW by right-cliking on the subtracted data plot and changing the \(y\)-axis to \(q^2I(q)\).

![](img/kratky.png)

A folded sample will display a parabolic curve in the low \(q\) region, whereas an unfolded sample will display a more linear curve, with a less distinctive shape.

![Kratky plot examples](img/kratky-examples.png)

Source: [Putnam *et al* (2007)]

It is also possible with RAW to display a normalized Kratky plot (normalization by molecular mass and concentration) or a dimensionless Kratky plot (by \(R_g\) or \(V_c\)). To do so, right-click on the subtracted SAXS profile and select `Normalized Kratky Plots` (the [Guinier analysis](#guinier-analysis) has to be done). A new window will pop up.

*Note that data may be cut to a certain \(q_{max}\). Here, 0.25 \(Å^{-1}\) would make sense.*

![Normalized Kratky plot options](img/normalized-kratky-popup.png)

By default, the plot drawn is a dimensionless \(R_g\) plot, where dashed gray lines illustrate guidelines for a globular protein: peak position at qRg of \(\sqrt{3}\) (~1.73) and peak height of 3/𝑒 (~1.1).

You can use the `SAVE` button to export the figure, or right-click on the plot and select `Export Data As CSV` to save the raw numerical data and re-plot everything in your preferred plotting software.


## Saving your workspace

Once all this hard work has been done, RAW lets you save your "workspace", which includes all the analysis results and the parameters used to display the results. This is helpful in order to re-open all the curves at a later time. Via the `File` menu, click on `Save Workspace`. Give it a meaningful name (*e.g.* `basic_data_processing`) and save it in

`<project_name>/workspaces/`


## Moving on to the next steps

[Advanced data processing and *ab initio* modelling](/advanced_data_processing/)


[Myatt *et al* 2017]: https://content.iospress.com/articles/biomedical-spectroscopy-and-imaging/bsi167
[Piiadov *et al.* (2019)]: https://www.ncbi.nlm.nih.gov/pubmed/30371978
[Putnam *et al* (2007)]: https://www.ncbi.nlm.nih.gov/pubmed/18078545
[Rambo and Tainer (2013)]: https://www.ncbi.nlm.nih.gov/pubmed/23619693
[Skou *et al* 2014]: https://www.ncbi.nlm.nih.gov/pubmed/24967622
