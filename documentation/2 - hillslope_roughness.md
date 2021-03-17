## Hillslope roughness tool

The kinematic roughness equations require a roughness parameter *alpha*, given by *alpha = SQRT(S_o)/n*, where *S_o* is slope [L/L] and *n* is Manning's roughness coefficient.  This step computes: (1) the average slope *S_o*; and (2) the area-weighted Manning's roughness coefficient *n*. 

**1. Slope**

* Computes pointwise slope from the input DEM, averages over the hillslope area to give the average hillslope slope *S_o*

**2. Manning's roughness coefficient**

* Converts land cover raster from NLCD to $n$ using a look up table developed by Kalyanapu (2009). 
* Computes area weighted manning coefficient for each hillslope
* Alternatively, if a landcover dataset is not available or if the tool is applied outside of the United States, the user may supply an estimate of Manning's roughness coefficient or any land cover raster with values that match the NLCD land cover categories. 


Land Cover| Description	| Manning's n
------------ | ------------- | -------------
11		| Open water	| 	0.001
21		| Developed, open space		| 0.0404
22		| Developed, low intensity		| 0.0678
23		| Developed, medium intensity		| 0.0678
24		| Developed, high intensity		| 0.0404
31		| Barren lan		| 0.0113
41		| Deciduous forest		| 0.36
42		| Evergreen forest		| 0.32
43		| Mixed forest		| 0.4
52		| Shrub/scrub		| 0.4
71		| Grassland/herbaceous		| 0.368
81		| Pasture/hay	| 	0.325
82		| Cultivated crops		| 0.037
90		| Woody wetlands		| 0.086
95		| Emergent herbaceous wetlands	| 	0.1825

Kalyanapu, A. J. (2009). Effect of land use-based surface roughness on hydrologic model output. *Journal of Spatial Hydrology*, 9(2), 21.


**2. Alpha**

* Computes  *alpha = SQRT(S_o)/n* for each hillslope.



