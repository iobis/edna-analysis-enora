# Folder containing the rarefaction curves for each amplicon

There is 3 differerent kinds of rarefaction curves:
- Sample-size-based rarefaction curves = Look at number of reads against number of identified species in sample
- Sample completeness curves = Look at number of reads against sample coverage
- Coverage-based rarefaction curves = Look at sample coverage against number of identified species in sample

Each kind of curves are plotted with confidence intervals

## Informations on the figures
For each site one curve represents one filter and each filter is colored based on the station it belongs too (same colors as for the upset plots).

## Information on the scripts
For each amplicon there is 2 .Rmd files, one generating the iNEXT objects (converted in .rds and available in the folders `iNEXT_objects_?`) and one producing the html report with all the plots.
