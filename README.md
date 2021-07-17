# WRF_tables
WRF V4.0.2 tables of VEGPARM and LANDUSE with additions to use CLC with 44 classes

# How to use:

## In WRF run directory:

Copy tables and replace your current LANDUSE.TBL and VEGPARM.TBL with the two here provided.
(Or extend your tables with the additions at the bottom of the here provided tables)

## Other WRF code changes

For most parameterizations no additional code changes are needed in WRF.
I think that NOAH-ruc has additional work with the different types and also includes lakes. 
This would need additional code to match the CLC classes to the correct surface handling.

The newer land use datasets also include categories for lakes and have WRF code to handle them accordingly.
This is not yet included!

Required code might be put online when I find the time to work on it.

## Preparation of the LAND USE files

1) Convert the vector file to a raster with resolution similar to that needed for the domain. 

*In the near future I will reference to a paper of mine that treats the vector to raster process. (Submission planned soon)*

3) Convert the raser file to a binary file, such that it is readable by WRF

*A program that can do this is: convert_geotiff-master*

4) Check the index file, to see if it is correctly created

*Make sure that the 'category_min' and 'category_max' are set to correct values (such as 1 and 44)*
*Check the missing value parameter for correctness*

5) Add a line to 

*The land use files in your geographic data directory all need an additional line in their index, setting the mminlu to "CLC"*

**mminlu="CLC"**

## Preparation of geogrid/GEOGRID.TBL (in WPS)

1) set rel_path, give it a local abriviation from the GEO_DATA file

for example a dataset called CLC12_44classes_3arcmin could be named CLC44_03m

**rel_path=     CLC12_44classes_3arcmin:CLC44_03m/**

2) set the landmask_water

Full CLC has water at 40,41,42,43,44. It is possible to add the missing data values as well (often 0 and/or 45) 

**landmask_water = CLC44_03m:40,41,42,43,44**

3) Set interpretation option\

Only the nearest_neighbor is a sensible option available within WRF, but feel free to try others

**interp_option =     CLC44_03m:nearest_neighbor**
