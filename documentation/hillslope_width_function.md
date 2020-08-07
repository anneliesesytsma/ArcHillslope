## Hillslope width function tool

A hillslope width function (HWF) represents the topographic shape of a hillslope. We denote a line from the divide of a hillslope to the outlet as the $x$-axis. At each value $x$ along the hillslope, the width $w(x)$ represents the linear distance between contour endpoints. For analytical tractability, Lapides et al. (2020) assumed an exponential shape for the HWF given by: *W(x) = ce^x*

This definition requires reconciliation of actual hillslopes with idealized exponential hillslope shapes. We applied two criteria to the process of delineating hillslope width functions, following Noel et al. (2014): (1) monotonicity and (2) conservation of area. Montonicity ensures that the hillslope width function is convergent (monotonically increasing), divergent (monotonically decreasing), or constant (uniform), while conservation of area fulfills mass conservation requirements.

<img src="./figures/hwf_process.jpg">


**1. Hillslope outlines** 

* Hillslopes are converted to polylines and the stream network is erased from the polyline, resulting in hillslope outlines with a discontinuity at the outlet location. 
* Two points were generated along the hillslope outlet (we will refer to these as the "outlet points"), placed at either endpoint of the discontinuity, and a line was formed from these two points ("outlet line"). 
* n equally spaced points are generated along the hillslope polyline ("hillslope points").

**2. Hillslope point pairs**

* Next, the n hillslope points are paired with the corresponding point across the hillslope, and a midline is drawn up the vertical axis of the hillslope, given by the best fit line for the midpoints of each point pair. This midline is the $x$-axis for defining the HWF. 
* The midline separates the hillslope points into points to the left and right of the midline. 
* For each point on the right, the perpendicular distance to the midline is the width of the right half, and the perpendicular distance to the outlet is used to find the position along the $x$-axis as a distance from the divide. 

**3. Exponential fit**

* From these paired distances and widths, the tool calculates the parameters *C* and *a*, which provide the optimal best fit for the right side of the hillslope. The same is done for the left side of the hillslope. 
* An overall exponential fit is found by calculating the exponential function which equates to the sum of the left and right sides to calculate final values of *C* and *a*. 

**4. Area conservation**

* To ensure that area is conserved in the exponential fit, we keep the location of the outlet (so as to maintain the same outlet width) and calculate the location of the divide that preserves the area of original hillslope. 
* Using the $x$-location of the hillslopes divide ($x_0$) and outlet ($x_end$) and the exponential best fit parameters for $C$ and $a$, we fully describe the exponential HWF.

**4. Error metrics** 

* To evaluate the error associated with the exponential fit and the actual hillslope width values, we computed the normalized root mean square error (NRMSE) between the observed width and width predicted by the exponential function, normalized by the difference between the maximum and minimum observed widths.


