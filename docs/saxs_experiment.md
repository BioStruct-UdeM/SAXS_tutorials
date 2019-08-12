---
title: Running a SAXS experiment
author: Normand Cyr
date: 2019-03-11
...

# SAXS experiment


## Sample requirement

Sample and buffer **must** match:

* Dialysis overnight is the best method
* Alternatively: SEC buffer

Need a monodisperse sample:

* Verify by gel filtration, non-denaturing gel or DLS

Appropriate concentration for good signal:

* 1 – 10 mg/ml
* Lower concentrations will not give meaningful data

Volume required: at least 50 µl

* Absolute minimum is 20 µl
* More volume to prepare dilution series

Avoid detergents above CMC (some exceptions)

Salt concentration up to 1M is ok

Once you know your sample meets the SAXS requirements, you can reserve some time on the instrument by contacting me by email ([normand.cyr@umontreal.ca](mailto:normand.cyr@umontreal.ca)).

I need to know **at least 8 hours in advance** in order to start up the X-ray source.

## Sample preparation

On the day of the SAXS experiment:

* Determine exact sample concentration after dialysis
* Keep ~10 ml of dialysis buffer
* Centrifuge particles down from your sample and filter the dialysis buffer
* Prepare serial dilutions (3-5) using the dialysis buffer (*Eg* 10, 5, 2.5, 1.25, 0.625 mg/ml)
* Load the 96-well plate with your samples

## Setup

Setup the plate configuration on the computer:

* Sample name is important!
* Save the configuration for later use

Setup the run program:

* Detector configuration (start with MAXS_INT (0.01 < q < 0.58 Å<sup>-1</sup>))
* Exposure time (start with 120 seconds - we can test different exposure times for best signal-to-noise)
* Number of replicates (*Eg* 10 exposures of 120 seconds)
* Temperature of the sample cell (20 °C is a good start, unless the sample is temperature sensitive)

## Data acquisition

Once the plate and the program are set, the data acquisition can be started by pressing the start button.

### Radial averaging of the scattering

X-ray scattering will be detected and a 2D image representing the scattering intensity over the detector plane will be recorded. Then, from the center of the beam, radial averaging of the intensity is performed at a specific q-value interval. The resulting average intensity (I) is finally plot against the q-value (q) to generate the scattering curve.
