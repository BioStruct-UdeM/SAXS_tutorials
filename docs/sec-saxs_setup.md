---
title: Running a SEC-SAXS experiment
author: Normand Cyr
<<<<<<< HEAD
date: 2020-04-17
...

Complementing a SAXS experiment with a size-exclusion chromatography (SEC) step upstream is a powerful approach when dealing with mixtures, partial aggregation and dynamic systems (*eg* monomer-dimer equilibrium).
=======
date: 2020-11-09
...

# Running a SEC-SAXS experiment

Complementing a SAXS experiment with a [size-exclusion chromatography](https://en.wikipedia.org/wiki/Size-exclusion_chromatography) (SEC) step upstream is a powerful approach when dealing with mixtures, partial aggregation and dynamic systems (*eg* monomer-dimer equilibrium) as the additional inline separation step provides a mean to isolate individual molecular states.

![Overview SEC-SAXS diagram](img/sec-saxs_diagram.svg)


## Sample requirement

As stated previously, SAXS is a contrast method. Whereas in batch mode we need to record data for both the buffer alone and the sample in buffer, in SEC-SAXS, we continuously record SAXS images as the chromatography takes place. These images will include data from both the buffer (the actual mobile phase from the chromatography - before the sample elution for example) and from the samples in buffer (during elution).

Despite this convenience, and due to the dilution effect of the chromatography step, a higher quantity of sample is required for a SEC-SAXS experiment. Generally speaking, for proteins, we need to use **250 – 500 µl of sample at 5 – 10 mg/ml** (the higher, the better). Nucleic acids scatter X-rays approximately 5 times more than proteins (because of their higher electron density), thus allowing lower concentrations.

If possible, avoid high concentrations of [osmolytes](https://en.wikipedia.org/wiki/Osmolyte) (glycine, betaine, sucrose, glycerol *etc*) as they will decrease the scattering contrast with the sample. High salt concentrations above 1 M should also be avoided for the same reason. Likewise, if detergents are required for the stability of the sample, avoid concentrations above [critical micelle concentration](https://en.wikipedia.org/wiki/Critical_micelle_concentration) (CMC) (some exceptions may apply).

Once you know your sample can meet the SEC-SAXS requirements, you can reserve some time on the instrument by contacting me by email ([normand.cyr@umontreal.ca](mailto:normand.cyr@umontreal.ca)). I need to know at least **24 hours in advance** in order to start up the X-ray source and install the size-exclusion chromatography equipment on the SAXS.


## Sample preparation

On the day of the SEC-SAXS experiment:

* Determine the exact sample concentration
* Centrifuge particles down from your sample (*eg* 5 minutes at 14,000 rpm)
* Transfer to a new sample tube


## Instrument setup

As illustrated above, in the case of a SEC-SAXS experiment, a size-exclusion chromatography system (an [ÄKTAmicro](https://www.cytivalifesciences.com/en/us/support/products/aktamicro-28948303) in our case) is connected inline with the SAXS instrument. This is all done in advance by Normand Cyr and should not require any user input. You can therefore ski this section if the details do not interest you.

### Disabling the robotic mode on the SAXS instrument

1. Disable the robotics system of the SAXS by pressing the large red button on the size of the sample platform.
2. Slide the whole sample platform/robotic arm to the right by about 15-20 cm.
3. Vent the detector chamber. This is done by entering the command `vent_system` in the SPEC window of the control computer. A click will be heard and then a loud hissing sound will start coming from the pneumatic exhaust valve located at the very end of the SAXS detector chamber. The pressure in the chamber should go up (watch the pressure gauge above the instrument).
4. Once the chamber gets close to atmospheric pressure (> 900 mbar), open the black manual exhaust valve, also located at the very end of the SAXS detector chamber.
5. Once the pressure in the detector chamber has equilibrated with the atmosphere (~ 1000 mbar), disassemble the sample funnel located at the entrance of the SAXS capillary by unscrewing the two M4 socket head screws using the 3 mm hex key (Allen key). Be careful to not lose the O-rings.
6. From the exit side of the capillary, unscrew the outlet tubing. **Failing to doing so will result in excessive pressure in the capillary and potentially breaking of the capillary and fluid leaks in the detector chamber.**

### Connecting the size-exclusion chromatography system

1. Install the SEC-SAXS capillary entrance adapter where the sample funnel used to be installed. Make sure the two O-rings are properly seated and screw the two M4 socket head screws using the 3 mm hex key (Allen key).
2. Bring the ÄKTAmicro system next to the SAXS instrument.
3. Using a short length of blue PEEK tubing (0.25 mm internal diameter), connect the outlet of the UV detector from the ÄKTAmicro to the entrance of the capillary of the SAXS via the SEC-SAXS capillary entrance adapter.
4. Connect an outlet tubing at the exit of the capillary and redirect it to the waste bottle. Alternatively, the outlet may be directed to a fraction collector. *However, this setup has not been tested yet*


## Data acquisition

Data acquisition in SEC-SAXS mode starts by injecting the sample (via a 500 µl loop) onto the gel filtration column using the dedicated software of the size-exclusion chromatography system. There is currently no way to synchronize the data acquisition on the ÄKTAmicro with the SAXS.

SAXS data acquisition is typically started right before the exclusion volume exits the chromatography column (at around the 8 ml mark on a [Superdex 200 Increase 10/300](https://www.sigmaaldrich.com/catalog/product/sigma/ge28990944)). This ensures that data is collected throughout the whole elution. Nonetheless, ff the elution time of the sample is known, it is possible to start collecting SAXS data just before that moment.

The SAXS instrument is equipped with a UV-Vis detector (the biocube) and absorbance at a given wavelength can be monitored continuously.


The

### Radial averaging of the scattering

X-ray scattering will be detected and a 2D image representing the scattering intensity over the detector plane will be recorded. Then, from the center of the beam, radial averaging of the intensity is performed at a specific q-value interval. The resulting average intensity (I) is finally plot against the q-value (q) to generate the scattering curve.

![SAXS traces](img/sec-saxs_bsa_multiple-traces.png)
>>>>>>> 7efc30f (- Adding redirect link to the Wiki page of the Platform)
