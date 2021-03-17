## About ArcHillslope

Arc Hydro Hillslope and Critical Duration tools partition landscapes into hillslopes, calculate hillslope curvature, and apply these in an analytical overland flow model to compute time of concentration, critical duration, and peak flows for each hillslope. 

This repository contains files used in the development of the Arc Hydro tools. This includes: (1) example datasets; and (2) tool documentation.


## Getting started

* Ensure you have ArcGIS Pro for Desktop installed.
* Ensure that you have the Spatial Analyst extension and the most recent version of Arc Hydro tools. Arc Hydro is available for download at the following link: http://downloads.esri.com/archydro/archydro/
* The hillslope and Critical Duration tools are available in Arc Hydro tools, https://downloads.esri.com/archydro/archydro/Setup/Pro/

## Inputs for Critical Duration Toolbox

### Data inputs
1. Digital elevation model (units of m)
2. Land use raster (NLCD)

### User supplied constants
1. Flow accumulation threshold for stream delineation
2. Number of points to use to estimate hillslope width function (default is 24)
3. Parameters *K* and *b* from intensity-duration-frequency curve function of the form: I = K/(D^b)
4. Saturated hydraulic conductivity *K_s*


## Toolbox Overview

The toolbox contains 4 ArcPython tools which must be executed in order. These tools are outlined in the figure below, and described breifly here. For additional detail on these tools, see the [documentation](https://github.com/anneliesesytsma/archydro_criticalduration/tree/master/documentation) folder.


### Step 1 Hillslope Partitioning

**1a. Hillslope Delineation**
* Inputs: DEM, flow accumulation threshold, drainage line (stream link polyline), strm (stream raster), fac (flow accumulation raster), fdr (flow direction raster)
* Process: identifies stream inlet points and delineates catchments draining to stream inlet points to give headwater hillslopes; delineates full catchments, mosaics headwater and full catchments, and bisects with stream channel to give lateral hillslopes.
* Outputs: hillslope (shapefile) with field "hs_type" to designate if hillslope is "headwater" or "lateral", stream_network (polyline)

### Step 2 Hillslope Roughness

* Inputs: hillslope (shapefile)
* Process: computes hillslope roughness coefficient, alpha, from slope and manning's roughness coefficient. Manning's roughness coefficient estimated from land use.
* Outputs: hillslope (shapefile) with field containing area-weighted alpha value.

### Step 3 Hillslope Width Function

* Inputs: hillslopes (shapefile), drainage line (polyline), n_points (integer)
* Process: fits each hillslope delineated with a best-fit exponential hillslope width function of the form W = ce^ax, where W is the width of the hillslope and X is the distance from the hillslope divide. 
* Outputs: hillslope (shapefile) with fields containing *a*, *C*, *L*, *x_0*, *x_end*, *pt_error*, and *shape_error* 

### Step 4 Optimize Critical Duration

* Inputs: hillslope (shapefile) with fields containing *a*, *C*, *L*, *x_0*, *x_end*, *pt_error*, and *shape_error*; Parameters *K* and *b* from intensity-duration-frequency curve function of the form: I = K/(D^b); saturated hydraulic conductivity *K_s*
* Process: simulates overland flow across each hillslope using analytical solution, calculates *D_crit* (time of max flow), *Tc* (time that the entire hillslope contributes to flow at the outlet),  *Qmax* (peak flow for the return interval), and ratio *D_crit/Tc*.
* Outputs: hillslope (shapefile) with fields containing *D_crit*, *Tc*, *Qmax* and *D_crit/Tc*

## Citations

Lapides, D. A., Sytsma, A., Djokic, D., & Thompson, S. "Arc Hydro Hillslope: an ArcHydro tool for predicting hillslope critical duration and peak flow"



