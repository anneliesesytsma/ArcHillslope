## Hillslope roughness tool

The kinematic roughness equations require a roughness parameter *alpha*, given by *alpha = SQRT(S_o)/n *, where *S_o* is slope [L/L] and *n* is Manning's roughness coefficient.  This step computes: (1) the average slope $S_o$; and (2) the area-weighted Manning's roughness coefficient *n*. 

**1. Slope**

* Computes pointwise slope from the input DEM, averages over the hillslope area to give the average hillslope slope *S_o*

**2. Manning's roughness coefficient**

* Converts land cover raster from NLCD to $n$ using a look up table developed by \citet{kalyanapu2009}. 
* Computes area weighted manning coefficient for each hillslope
* Alternatively, if a landcover dataset is not available or if the tool is applied outside of the United States, the user may supply an estimate of Manning's roughness coefficient or any land cover raster with values that match the NLCD land cover categories. 

**2. Alpha**

* Computes  *alpha = SQRT(S_o)/n* for each hillslope.
