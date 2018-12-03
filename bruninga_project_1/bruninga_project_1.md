---
A.J. Bruninga
---
GES 486 Project 1
---
10/8/18
---


My goal for this project was to generate a rough estimate of solar power suitability
on buildings in northwestern Baltimore. My two main variables for calculating suitability were structure area and average slope aspect for each tax plot in the area. I began by downloading an elevation raster from the Baltimore City Open GIS Data Portal, and then clipped that raster by the tax plot data for zip codes 21209, 21210, and 21211 in northwestern Baltimore. Once I had the elevation raster clipped, I ran an aspect of that layer, and used the Zonal Statistics tool to get an average value for the aspect of each tax plot, which was added as a column in the tax plot attribute table.

With the average aspect per tax plot in hand, I then reclassified the aspects into four groups with different scaling factors. If the average aspect was north-facing (270 to 90 degrees) I gave it a value of zero because there is no point in installing solar panels facing north. South-facing plots (150 to 210 degrees) received a scaling factor of 1.5 according to their superior direction, while southeast-facing plots (90 to 150 degrees) had a scaling factor of 1 and southwest-facing plots (210 to 270 degrees) got a scaling factor of 1.25 because demand for electricity is higher in the evening when the sun is in the west.

The second main variable in my definition of solar suitability was structure area per tax plot, under the assumption that installing solar panels on existing structures would be easier than finding plots of open land in the city. I multiplied the structure area per tax plot by the aspect scaling factor to get a final suitability statistic, which I then mapped.

![Alt Text](https://github.com/ajbruninga/ajbruninga.github.io/blob/master/bruninga_project_1/solar_map.png)

Finally, I converted all the polygons to centroid points and did an IDW interpolation of my suitability factor to create a 3D map that shows areas in northwestern Baltimore where rooftop solar is the most viable.

![Alt Text](https://github.com/ajbruninga/ajbruninga.github.io/blob/master/bruninga_project_1/3d_map.png)
