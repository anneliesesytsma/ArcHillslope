## Hillslope delineation

**1. Dealineate headwater watersheds**

* Creates a stream network grid that represents the flow path length of the stream segment. This is achieved by creating a stream network grid with constant value of 1, multiplying this grid by the flow direction, and then using the ArcGIS tool "Flow Length" to compute the length of the flowpath along each stream segment. 
* Uses the resulting flowpath length grid to extract the origin of the stream network, or where the flowpath length is equal to 0, exports stream origin to points.
* The origin points represent the the "outlet" points to which the headwater hillslopes are delineated using the "Batch Watershed Dealineation" tool in ArcHydro.

**2. Dealineate full watersheds**

* Delineates watersheds drained by stream network using the ArcHydro watershed grid delineation tool. 

**3. Combine headwater and full watersheds**

* Mosaics the headwater watersheds and full watersheds into a new raster. 
* Exports mosaiced watershed raster to a shapefile.

**4. Bisect watershed with stream network**

* Bisects the mosaiced watershed shapefile by the stream network (using the "Union" tool) to create two lateral and one headwater hillslope. 
* Cleans and groups resulting hillslopes to merge small hillslopes with larger hillslopes (using "Region Group", "Region Lookup", and "Nibble" tools)
* Exports to  final shapefile format. A column in the final hillslope shapefile titled "hs_type" designates whether the hillslope is a 'headwater' or 'lateral' hillslope.
