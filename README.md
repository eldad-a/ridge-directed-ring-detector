ridge directed ring detector
============================

Robust and highly performant ring detection algorithm for 3d particle tracking using 2d microscope imaging
----------------------------------------------------------------------------------------------------------

The source for the ring detection algorithm described in [Sci. Rep. 5, 13584; doi: 10.1038/srep13584 (2015)](http://www.nature.com/articles/srep13584).

Some usage examples can be found in the accompanying ipython-notebook `code/demo.ipynb`; a static view is available [here](http://nbviewer.ipython.org/github/eldad-a/ridge-directed-ring-detector/blob/master/code/demo.ipynb);

An easy way to get the required dependencies is using [Anaconda](http://continuum.io/downloads), which is cross-platform, or any other Python distribution which includes [Cython](http://cython.org/), [Scipy](http://cython.org/) and [OpenCV](http://opencv.org/).

Acknowledgements would be highly appreciated; for academic citation please use:

Afik, E. Robust and highly performant ring detection algorithm for 3d particle tracking using 2d microscope imaging. Sci. Rep. 5, 13584; doi: 10.1038/srep13584 (2015).


##### Related projects and publications:

+ E. Afik, [Robust and highly performant ring detection algorithm for 3d particle tracking using 2d microscope imaging](http://www.nature.com/articles/srep13584). Sci. Rep. 5, 13584; doi: 10.1038/srep13584 (2015)
+ E. Afik and V. Steinberg. [Pair dispersion in a chaotic flow reveals the role of the memory of
initial velocity](http://arxiv.org/abs/1502.02818). _ArXiv e-prints arXiv:1502.02818_. submitted.
+ [particle-tracking](https://github.com/eldad-a/particle-tracking) -- A linking algorithm for particle tracking in n-dimensions, implementing a kinematic model and a memory feature to account for occasional misses.
+ [natural-cubic-smoothing-splines](https://github.com/eldad-a/natural-cubic-smoothing-splines) -- a natural cubic smoothing splines module to smooth-out noise and obtain an estimate of the first two derivatives, i.e. velocity and acceleration in the case of a particle trajectory.
