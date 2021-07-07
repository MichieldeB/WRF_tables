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

The land use files in your geographic data directory all need an additional line in their index, setting the mminlu to "CLC"

mminlu="CLC"

furthermore, make sure that the 'category_min' and 'category_max' are set to correct values (such as 1 and 44)

These lines are generally near the end of the index, but should not matter much. 



