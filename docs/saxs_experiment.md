---
title: Running a SAXS experiment
author: Normand Cyr
date: 2020-04-17
...

# SAXS experiment

SAXS is a contrast method where the scattering signal is obtained from the difference in electron density between a molecule in solution (\(\rho_{sample}\)) and bulk solvent (\(\rho_{buffer}\)), scattering resulting from the buffer has to be subtracted from the measured scattering of the sample to isolate the sole contribution from the molecule (see the [Basic SAXS data processing](/basic_data_processing/#buffer-subtraction) section).

\(\Delta\rho_{molecule} =  \rho_{sample} - \rho_{buffer} \)

## Sample requirement

**TL;DR: at least 50 µL of sample at a concentration of 1 – 10 mg/ml, along with 1 ml of *matching* buffer**

Because of the nature of the SAXS method, sample (molecule + buffer) and buffer (buffer alone) **must** match. In order to achieve this, dialyzing the sample overnight in the buffer of choice is the **best** method.

Alternatively, yet *not recommended*, size-exclusion chromatography buffer or diafiltration flow-through could be used for approximate buffer blank. However, adequate buffer subtraction is not guaranteed and results may be of poor quality forbidding downstream processing of the data, or give erroneous information about the sample quality. **Use these alternative methods at your own risk!**

Also, if possible, avoid high concentrations of [osmolytes](https://en.wikipedia.org/wiki/Osmolyte) (glycine, betaine, sucrose, glycerol *etc*) as they will decrease the scattering contrast with the sample. High salt concentrations above 1 M should also be avoided for the same reason.

The sample needs to be mono-disperse. This can easily be estimated by gel filtration, non-denaturing gel electrophoresis or dynamic light scattering.

Appropriate concentration of sample for good scattering signal: **1 – 10 mg/ml** (lower concentrations will not give meaningful data). Nucleic acids scatter X rays approximately 5 times more than proteins (because of their higher electron density), thus allowing lower concentrations. At least **50 µl of sample** (more is better) is required for SAXS analysis and preparation of dilution series, and 1 ml of matching buffer should be sufficient. If detergents are required for the stability of the sample, avoid detergent concentrations above [critical micelle concentration](https://en.wikipedia.org/wiki/Critical_micelle_concentration) (CMC) (some exceptions may apply)

Once you know your sample can meet the SAXS requirements, you can reserve some time on the instrument by contacting me by email ([normand.cyr@umontreal.ca](mailto:normand.cyr@umontreal.ca)). I need to know **at least 8 hours in advance** in order to start up the X-ray source.

## Sample preparation

On the day of the SAXS experiment:

* Determine the exact sample concentration after dialysis using your preferred method
* Keep ~10 ml of dialysis buffer
* Centrifuge particles down from your sample (*eg* 5 minutes at 14,000 rpm) and filter the dialysis buffer through a 0.22 µm filter
* Prepare serial dilutions (3-5) using the dialysis buffer (*eg* 10, 5, 2.5, 1.25, 0.625 mg/ml)
* Load the 96-well plate with your samples

## Setup

Setup the plate configuration on the computer:

* Sample name is important!
* Save the configuration for later use

Setup the run program:

* Detector configuration (start with MAXS_INT (0.01 < q < 0.58 Å<sup>-1</sup>))
* Exposure time (start with 120 seconds - we can test different exposure times for best signal-to-noise)
* Number of replicates (*eg* 10 exposures of 120 seconds)
* Temperature of the sample cell (20 °C is a good start, unless the sample is temperature sensitive)

## Data acquisition

Once the plate and the program are set, the data acquisition can be started by pressing the start button.

### Radial averaging of the scattering

X-ray scattering will be detected and a 2D image representing the scattering intensity over the detector plane will be recorded. Then, from the center of the beam, radial averaging of the intensity is performed at a specific q-value interval. The resulting average intensity (I) is finally plot against the q-value (q) to generate the scattering curve.
