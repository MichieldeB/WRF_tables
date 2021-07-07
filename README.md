# WRF_tables
WRF V4.0.2 tables of VEGPARM and LANDUSE with additions to use CLC with 44 classes

# How to use:

## In WRF run directory:

Copy tables and replace your current LANDUSE.TBL and VEGPARM.TBL with the two here provided.
(Or extend your tables with the additions at the bottom of the here provided tables)

## Other WRF code changes

For most parameterizations no additional code changes are needed in WRF
I think that NOAH-ruc has additional work with the different types and also includes lakes. 
This would need additional code to match the CLC classes to the correct surface handling.

This is not yet included!

## Preparation of the LAND USE files

1) Convert the vector file to a raster with resolution similar to that needed for the domain. 

*In the near future I will reference to a paper of mine that treats the vector to raster process. (Submission planned soon)*

3) Convert the raser file to a binary file, such that it is readable by WRF

*A program that can do this is: convert_geotiff-master*

4) Check the index file, to see if it is correctly created

*Make sure that the 'category_min' and 'category_max' are set to correct values (such as 1 and 44)*

5) Add a line to 

*The land use files in your geographic data directory all need an additional line in their index, setting the mminlu to "CLC"*

**mminlu="CLC"**



