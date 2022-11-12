'''
Created by Nathan R
Used to quickly convert and format multiple shapefiles
into CAD drawings.

To use, run within ArcGIS's built in Python Terminal
'''

# Import arcpy module
import arcpy
from arcpy import env

# get map document
mxd = arcpy.mapping.MapDocument("CURRENT")

# get data frame
df = arcpy.mapping.ListDataFrames(mxd)[0]

#shp directory for iteration
env.workspace = arcpy.GetParameterAsText(0)

#list all shapefiles in workspace
fclist = arcpy.ListFeatureClasses()

#add shp to toc
for fc in fclist:
    newlayer = arcpy.mapping.Layer(fc)
    newlayer.visible = False
    arcpy.mapping.AddLayer(df, newlayer, "TOP")
    arcpy.RefreshTOC()
    arcpy.RefreshActiveView()

#apply symbology for all in toc
updatelayer = arcpy.mapping.ListLayers(mxd, "*")
lidar = arcpy.mapping.Layer(r"LiDAR.lyr") #add path to layer file

cad_directory = arcpy.GetParameterAsText(1)
for shp in updatelayer:
    arcpy.mapping.UpdateLayer(df,shp,lidar, symbology_only = True)
    arcpy.ExportCAD_conversion (shp, "DWG_R2018", cad_directory + "\\" + shp.name + ".dwg")
    arcpy.RefreshTOC()
    arcpy.RefreshActiveView()
