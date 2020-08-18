## Critical duration ArcHydro toolkit

An ArcHydro toolkit for calculating time of concentration, critical duration, and peak flows from hillslopes of complex curvature.

This repository contains files used in the development of the ArcHydro Critical Duration toolbox. This includes: (1) the ArcHydro toolbox with python scripts and tool UI; (2) example datasets; and (3) tool documentation.

## Getting started

* Ensure you have ArcGIS 10.7 (or greater) for Desktop installed.
* Ensure that you have the Spatial Analyst extension and the most recent version of ArcHydro tools. ArcHydro is available for download at the following link: http://downloads.esri.com/archydro/archydro/
* The Critical Duration toolbox is available in ArcHydro tools, or can be downloaded separately here. If you download it separately, place it in an appropriate folder on your machine. Navigate to the folder in Catalog. If you expand all the toolsets, you will see the following:

<img src="https://github.com/anneliesesytsma/archydro_criticalduration/blob/master/figures/Toolbox.JPG">

## Inputs for Critical Duration Toolkit

### Data inputs
1. Digital elevation model (units of m)
2. Land use raster (NLCD)

### User supplied constants
1. Flow accumulation threshold for stream delineation
2. Number of points to use to estimate hillslope width function (default is 24)
3. Parameters *K* and *b* from intensity-duration-frequency curve function of the form: I = K/(D^b)
4. Rational method curve number *C* or saturated hydraulic conductivity *K_s*


## Toolboxes

The toolkit contains 4 separate toolboxes, which must be executed in order. These toolboxes are outlined in the figure below, and described breifly here. For additional detail on these toolboxes, see the [documentation](https://github.com/anneliesesytsma/archydro_criticalduration/tree/master/documentation) folder.

<img src="https://github.com/anneliesesytsma/archydro_criticalduration/blob/master/figures/gis_process.JPG">


### Step 1 Hillslope Partitioning

**1a. Stream Delineation**
* Inputs: DEM, flow accumulation threshold
* Process: Fills sinks, computes flow direction, flow accumulation, and delineates stream network. 
* Outputs: strm_lnk (stream link polyline), strm (stream raster), fac (flow accumulation raster), fdr (flow direction raster)
 
 **1b. Hillslope Delineation**
* Inputs: strm_lnk, strm, fac, fdr (from above)
* Process: identifies stream inlet points and delineates catchments draining to stream inlet points to give headwater hillslopes; delineates full catchments, mosaics headwater and full catchments, and bisects with stream channel to give lateral hillslopes.
* Outputs: hillslope (shapefile) with field "hs_type" to designate if hillslope is "headwater" or "lateral", stream_network (polyline)

### Step 2 Hillslope Roughness

* Inputs: hillslope (shapefile)
* Process: computes hillslope roughness coefficient, alpha, from slope and manning's roughness coefficient. Manning's roughness coefficient estimated from land use.
* Outputs: hillslope (shapefile) with field containing area-weighted alpha value.

### Step 3 Hillslope Width Function

* Inputs: hillslope (shapefile), stream_network (polyline), n_points (integer)
* Process: fits each hillslope delineated with a best-fit exponential hillslope width function of the form W = ce^ax, where W is the width of the hillslope and X is the distance from the hillslope divide. 
* Outputs: hillslope (shapefile) with fields containing *a*, *C*, *L*, *x_0*, *x_end*, *pt_error*, and *shape_error* 


### Step 4 Rational Method Optimization

* Inputs: hillslope (shapefile) with fields containing *a*, *C*, *L*, *x_0*, *x_end*, *pt_error*, and *shape_error*; Parameters *K* and *b* from intensity-duration-frequency curve function of the form: I = K/(D^b); Rational method curve number *C* or saturated hydraulic conductivity *K_s*
* Process: simulates overland flow across each hillslope using analytical solution, calculates *D_crit* (time of max flow), *Tc* (time that the entire hillslope contributes to flow at the outlet),  *Qmax* (peak flow for the return interval), and ratio *D_crit/Tc*.
* Outputs: hillslope (shapefile) with fields containing *D_crit*, *Tc*, *Qmax* and *D_crit/Tc*

## Citations

Lapides, D. A., Sytsma, A., Djokic, D., & Thompson, S. "Arc-Rational: an ArcHydro tool for predicting hillslope critical duration and peak flow"



