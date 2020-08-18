## Stream Delineation steps


**1. DEM pre-processing: fill sinks, flow direction, flow accumulation**

* The fill sinks procedure (ArcHydro "Fill sinks" tool) modifies a DEM to eliminate topographic sinks, where a cell is surrounded by higher elevation cells.  Sinks can cause issues in hydrologic analysis since water flowing into the sink becomes 'trapped' and cannot flow out. The Fill Sinks tool eliminates this issue and creates a new depression-free DEM, with sinks filled to match surrounding elevations.
* Computation of flow direction follows (ArcHydro 'Flow Direction' tool), which applies D8 flow direction algorithm to the depression-free DEM to indicate the direction in which water is flowing in each cell based on the elevation of the cell and its neighbors. The value of the cells (1-8) in the flow direction grid indicates the direction of steepest descent from that cell. 
* The flow direction grid is then input into the flow accumulation tool (ArcHydro "Flow Accumulation" tool), which computes the accumulated number of upstream cells for each cell in the flow direction grid. 

**2. Stream delineation: stream definition, stream segmentation**

* The flow accumulation grid is used as input for stream definition (ArcHydro "Stream Definition" tool), which computes a stream grid based on a user-defined threshold. The chosen threshold determines the density of the stream network and the scale of the resulting watersheds and hillslopes; it is a sensitive parameter and should be chosen iteratively. 
* The stream grid resulting from the stream definition step is used as an input to the ArcHydro "Stream Segmentation" tool which creates a grid of stream segments with unique identifiers. 
