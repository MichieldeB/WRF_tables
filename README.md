# WRF_tables
WRF V4.0.2 tables of VEGPARM, MPTABLE.TBL and LANDUSE with additions to use CLC with 44 classes

# How to use:

## In WRF run directory:

Copy tables and replace your current MPTABLE.TBL, LANDUSE.TBL and VEGPARM.TBL with the two here provided.
(Or extend your tables with the additions at the bottom of the here provided tables)
MPTABLE.TBL is not yet tested and would only be required for the NOAHMP option (option 4). 

## Other WRF code changes

For most parameterizations no additional code changes are needed in WRF.
I think that NOAH-ruc has additional work with the different types and also includes lakes. 
This would need additional code to match the CLC classes to the correct surface handling.

The newer land use datasets also include categories for lakes and have WRF code to handle them accordingly.
This is done in a second check of all land cover types during the real.exe step, turning the lake classes into the water class. 
It can only handle one class of lake and water at a time. (the river coarses and other water classes will not be included in the landmask. 

Thus to include all 5 water classes the WRF model needs to accept lists for islake or iswater. Or we precombine the classes into the lake and water class.
I have combined water flows and lakes into lakes, the estuaries, I have combined the other water classes (coastal lagoons and sea and ocean) into the sea and ocean class. Since these classes were all still the same, this should not give a difference in the end result. 

Required code might be put online when I find the time to work on it.

## Preparation of the LAND USE files

1) Convert the vector file to a raster with resolution similar to that needed for the domain. 

*In the near future I will reference to a paper of mine that treats the vector to raster process. (Submission planned soon)*

2) Convert the raser file to a binary file, such that it is readable by WRF

*A program that can do this is: convert_geotiff-master*


3) Check the index file, to see if it is correctly created

*Make sure that the 'category_min' and 'category_max' are set to correct values (such as 1 and 44)*
*Check the missing value parameter for correctness*
*Check if the index file is created correctly, see  an example file in the repository*

4) Add a line to 

*The land use files in your geographic data directory all need a few additional line in their index, setting the mminlu to "CLC"*

**mminlu="CLC"**

**iswater = 44**

**islake = 41**

**isice = 34**

(**isurban = 1**)

Note: that if you add the islake line the values will initialize wrong. (This has something todo with the real requirement of the lake category to be outside of the regular range of the VEGPARM and LANDUSE tables, thus it has selected the USGS values to initialize, but after one calculation step this problem is corrected)

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
