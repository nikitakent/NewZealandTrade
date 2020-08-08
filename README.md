# NewZealandTrade
International trading routes through New Zealand

#Changing the World Map Centre through GIS or qGIS:
Most world maps have New Zealand on the right hand side, with Europe in the center. This README covers how to change the epicentre of a world shapefile with Miller or Robinson Projection.
Hack: The preset 'EPSG 3832' [search bar: 'PDC'] as a CRS enables Pacific Ocean centre, but also distort some parts of the world. Is suitable for APEC maps that exclude the extreme north or south. 
Please see https://docs.qgis.org/3.4/en/docs/user_manual/working_with_projections/working_with_projections.html for the official qGIS documentation. 


View -> Toolbar -> Layers.
Right click on Properties for the world-vector layer (should be .shp)

##FOR GIS: 

CoordinateSystem tab -> Projected Coordinate Systems-> World->WGS 1984 World Mercator. Copy and modify this system (does not necessarily have to be WGS 1984 but is the most commonly used) the central meridian to 105E (for China) or to whatever meridian
you need. 
Apply your new custom projection. Click OK. Done. 

##FOR qGIS:

Source tab -> 'Select CRS' (small button) -> Choose WGS 1984 World Mercator -> 'OK'. 
Note to disable "On-The-Fly" projection, turn back on at the end of the project (Project-> Properties-> CRS ->"No Projection" [un/checkbox].
Layer -> Add Layer -> Add DLM File, use the PacificOceanMeridian.txt, load as CSV, Choose 'Custom Delimiter' as  semicolon (;), 'WKT' (well known text) with Geometry Type 'polygon' -> 'Close'. 
Right click on the layer, save as an ESRI shapefile with a CRS of WGS 1984. To save: Right click on layer -> Export -> Save Features As -> then specify file location, name and type. 
Your file path should look something like: /Users/YourName/dev/GIS/PacificOceanMeridian.shp
Add the shapefile to canvas, then remove the text file from your layers. 

Use Vector -> Geoprocessing -> Difference with the two polygon layers

Add custom CRS: Settings > Custom CRS... ADD: 
Robinson Projection
+proj=robin +lon_0=-150 +x_0=0 +y_0=0 +ellps=WGS84 +datum=WGS84 +units=m +no_defs

or
Miller Projection.
+proj=mill +lon_0=-150 +lat_0=0 +R=6371000 +units=m +no_defs
