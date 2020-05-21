# fmriprep_qa_guide
Rough draft of a guide for reviewing fmriprep's QA outputs


# Anatomicals
## Brain mask and brain tissue segmentation of the T1w
* Brain mask: make sure the red line is going around the brain and does not stray into the dura or cut off pieces of the brain.
* Segmentation: make sure the blue line follows the boundary between the white matter and the grey matter and isn't cutting off pieces of the white matter

## Spatial normalization of the anatomical T1w reference
* Look at the images as they transition back and forth and check the following:
  - Are the ventricles in the same place?
  - Is the grey matter/ white matter boundary stable?
  - Does any of the brain in the participant view look especially stretched or distorted?
A good example:
![anat_good](/images/anat_good.svg)

Dropout on the midline is also okay, as long as the rest of the slices are acceptable:
![anat_okay](/images/anat_okay.svg)
 
## Surface reconstruction
* Similar to what you check for the mask and segmentation
* The red line should outline the outer boundary of the grey matter and exclude the cerebellum
* the blue line should follow the boundary between the grey matter and the white matter
A good example:
![surf_good](/images/surf_good.svg)

Again, some dropout exclusively on the midline is fine:
![surf_okay](/images/surf_okay.svg)

A bad example, note the frontal lobe dropout at z=1:
![surf_bad](/images/surf_bad.svg)

# Functionals
## Susceptibility distortion correction
* The brains displayed here are functional volumes before and after distortion correction. The blue line is the grey matter/ white matter boundary derived from the anatomical scans
* The brain after the distortion correction should be better aligned with boundary derived from the functional
* The after should also appear less distorted and shaped more like a normal brain, this may be subtle when the distortion correction is working, but can really, really stand out when it fails.

## Alignment of functional and anatomical MRI data (surface driven)
* Mouse over to transition back and forth between "fixed" and "moving". Fixed displays the red and blue lines of the freesurfer surfaces on the anatomical image. Moving displays the functional that has been aligned to the structural while retaining the red and blue lines of the grey matter and white matter surface from the anatomical.
* Depending on you bold sequence, you may not be able to make out much, but you should still be able to see the grey matter / white matter boundary. Make sure that this boundary follows the blue line.
* You may have artifacts that cause loss of signal in the more inferior parst of the brain in the functional data. Disregard this drop out and make sure that the parts of the iimage the do have signal are well aligned.

## Brain mask and (temporal/anatomical) CompCor ROIs
* Make sure that the brain mask shown by the red contour is outside the brain in the functional image.
* Make sure the magenta lines are well inside the white matter/CSF.
* In general, areas outlined by the blue lines should be areas with high CSF or blood flow, such as between the hemispheres, in ventricles, and between the cortex and the cerebellum

This is a good example:
![func_good](/images/func_good.svg)

Some extra space in the red line is okay:
![func_okay](/images/func_okay.svg)

The striated pixelation is also okay:
![func_okay](/images/func_okay.svg)

This one is bad, the image is distorted and the red line is inside the brain:
![func_bad1](/images/func_bad1.svg)

This one is also bad due to distortion, especially apparent in the axial slices:
![func_bad2](/images/func_bad2.svg)


## Variance explained by t/aCompCor components
* I'm honestly not sure what to review here for QA

## BOLD Summary
* Look for any big spikes in any of the line plots
* Review the carpet plot (the thing that looks like static) for any columns that all seem to have a jump in values, this will look like vertical bands or lines down the plot.

## Correlations among nuisance regressors
* Again, not sure what would be a sign that something was wrong in these plots.

## ICA Components classified by AROMA
* The brain distribution of ICA components classified as noise should look like this:
<img src=https://fsl.fmrib.ox.ac.uk/fslcourse/lectures/practicals/ica/Figure1_ica.png>

* And the Temporal components should look like this for signal and noise respectively:
<img src=https://fsl.fmrib.ox.ac.uk/fslcourse/lectures/practicals/ica/Figure2_ica.png>


Image from [FSL ICA practical](https://fsl.fmrib.ox.ac.uk/fslcourse/lectures/practicals/ica/index.html)

