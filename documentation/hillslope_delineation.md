## Hillslope delineation

**1. delineation of headwater watersheds**

* Creates a stream network grid that represents the flow path length of the stream segment. This is achieved by creating a stream network grid with constant value of 1, multiplying this grid by the flow direction, and then using the ArcGIS tool "Flow Length" to compute the length of the flowpath along each stream segment. 
* Uses the resulting flowpath length grid to extract the origin of the stream network, or where the flowpath length is equal to 0, exports stream origin to points.
* The origin points represent the the "outlet" points to which the headwater hillslopes are delineated using the "Batch Watershed Dealineation" tool in ArcHydro.

**2. delineation of full watersheds**


**3. combine headwater and full watersheds**

**4. 
