ridge directed ring detector
============================

Robust and highly performant ring detection algorithm for 3d particle tracking using 2d microscope imaging
----------------------------------------------------------------------------------------------------------

The source for the ring detection algorithm described in [Sci. Rep. 5, 13584; doi: 10.1038/srep13584 (2015)](http://www.nature.com/articles/srep13584).

Some usage examples can be found in the accompanying ipython-notebook `code/demo.ipynb`; a static view is available [here](http://nbviewer.ipython.org/github/eldad-a/ridge-directed-ring-detector/blob/master/code/demo.ipynb);

An easy way to get the required dependencies is using [Anaconda](http://continuum.io/downloads), which is cross-platform, or any other Python distribution which includes [Cython](http://cython.org/), [Scipy](http://cython.org/) and [OpenCV](http://opencv.org/).

Acknowledgements would be highly appreciated; for academic citation please use:

Afik, E. [Robust and highly performant ring detection algorithm for 3d particle tracking using 2d microscope imaging](https://www.nature.com/articles/srep13584). Sci. Rep. 5, 13584; doi: 10.1038/srep13584 (2015).


##### Related projects and publications:

+ E. Afik, [Robust and highly performant ring detection algorithm for 3d particle tracking using 2d microscope imaging](http://www.nature.com/articles/srep13584). Sci. Rep. 5, 13584; doi: 10.1038/srep13584 (2015)
+ E. Afik and V. Steinberg. [On the role of initial velocities in pair dispersion in a microfluidic chaotic flow](https://www.nature.com/articles/s41467-017-00389-8). _Nature Communications_ __8__, Article number: 468 (2017) [doi: 10.1038/s41467-017-00389-8](http://dx.doi.org/10.1038/s41467-017-00389-8).
+ E. Afik and V. Steinberg. A Lagrangian approach to elastic turbulence in a curvilinear microfluidic channel. figshare [doi: 10.6084/m9.figshare.5112991](http://dx.doi.org/10.6084/m9.figshare.5112991) (2017).
+ E. Afik, A. Lamura, and V. Steinberg. [Long-range hydrodynamic effect due to a single
vesicle in linear flow](http://dx.doi.org/10.1209/0295-5075/113/38003). EPL (Europhysics Letters), 113(3):38003, Feb 2016. [using the directed ridge detection analysis]
+ [particle-tracking](https://github.com/eldad-a/particle-tracking) -- A linking algorithm for particle tracking in n-dimensions, implementing a kinematic model and a memory feature to account for occasional misses.
+ [natural-cubic-smoothing-splines](https://github.com/eldad-a/natural-cubic-smoothing-splines) -- a natural cubic smoothing splines module to smooth-out noise and obtain an estimate of the first two derivatives, i.e. velocity and acceleration in the case of a particle trajectory.

* * *

Here's a quick description of the parameters. The explanations refer to the terms as introduced in [Afik 2015](https://www.nature.com/articles/srep13584) and its Supplementary Information.

`sigma`
 is the width of the Gaussian Kernel to smooth the image; a typical good value should be the width (measured in pixels) of the ridge you would like to detect (to clarify, this is not the radius of the ring but the thickness of the curve).

`ksize` 
 is the size of the [Sobel kernel](http://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_gradients/py_gradients.html?highlight=sobel) to estimate the image spatial derivatives (the default should work in most cases)

`curv_thresh`
  this sets a threshold for preliminary search for ridges; pixels of least [principal curvature](https://en.wikipedia.org/wiki/Principal_curvature) (the smaller value of the two eigenvalues of the [Hessian](https://en.wikipedia.org/wiki/Hessian_matrix) applied to the image) _larger_ than `curv_thresh` would not be considered. This can be used to spare unnecessary calculations (speed-up) and avoid ridges which are too flat (reduce noise). [Fig. 2b](https://www.nature.com/articles/srep13584#f2) shows the output which is affected by `sigma`, `ksize` and `curv_thresh`.

`Rmin`
 smallest radius to consider in the search for circles (measured in pixels)

`Rmax`
 largest radius to consider in the search for circles (measured in pixels)

`vote_thresh`
 this sets a threshold for preliminary search for circle candidates in the parameter (Hough) space; see [Fig. 2c](https://www.nature.com/articles/srep13584#f2). Elements with vote count _smaller_ than `vote_thresh` would not be examined. This can be used to spare unnecessary calculations (speed-up).

`circle_thresh`
 this sets a threshold to filter detected circle candidates; ideally one would expect a circle to have 2 * pi * `r` votes per circle of radius `r`; given image quality and the optimisation of the parameters applied in earlier stages, one may like to be satisfied with a fraction of a circle. `circle_thresh` should be a value between 0 and 2*pi; note that the radius `r` should not be included; e.g. for 50% of the circumference one should set `circle_thresh = pi` (for `pi = np.pi` or roughly `3.14`). Circle candidates with vote count smaller than `circle_thresh` would be discarded. See [Figure 2d](https://www.nature.com/articles/srep13584#f2).

`dr`
 as part of sub-pixel evaluation, a best fit is being applied to the detected ridges. To include ridge pixels which are expected to belong to the candidate circle, an annulus mask of thickness `dr` (measured in pixels) is created, based on the circle parameters found in earlier stages in the algorithm. See the example in [Fig. 2e](https://www.nature.com/articles/srep13584#f2). 

`eccentricity`
 if `eccentricity` is non-zero, a fit to ellipse will be applied, instead of a circle; this is far from optimal.
