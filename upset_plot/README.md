In this folder you will find the upset plots for each amplicon for 3 different taxonomic ranks: species, genus and family

To generate the needed files to run the Rscripts you need to first run the following code:

```
station_file=https://github.com/iobis/edna-tracker-data/blob/master/supplementary_info/stations.csv
occurence_files=https://github.com/iobis/pacman-pipeline-results/tree/master/eDNAexpeditions_batch*/runs/${site}_12SMifish/05-dwca/Occurrence*
site=Argentina
mkdir ${site}_genus
cd ${site}_genus
Stations=`grep "Peninsula Vald" $station_file | cut -d',' -f3 | sort | uniq`
for i in $Stations
do
  filters=`grep "$i" $station_file | cut -d',' -f2`
  for f in $filters
  do
    grep "$f" $occurence_files | cut -f13 | sort | uniq | sed '/^[[:space:]]*$/d' > ${site}_${i}_${f}.txt
  done
done
for i in $Stations
do
  cat ${site}_${i}_*.txt | sort | uniq > ${site}_${i}.txt
done
cd ..
```

**/!\\** Be careful with the creation of the **Stations** variable because the names of the sites doesn't match between the Occurence files and the station file.
To choose the correct name refers to the _correspondance_names.txt_ file.

**/!\\** Be careful with Scandola site, the stations are situated in the 5th column and the filters in the 4th column so you need to change `grep "Scandola" $station_file | cut -d',' -f3 | sort | uniq` to `grep "Scandola" $station_file | cut -d',' -f5 | sort | uniq` and `grep "$i" $station_file | cut -d',' -f2` to `grep "$i" $station_file | cut -d',' -f4`

**/!\\** Be careful with SharkBay site, the stations are situated in the 4th column and the filters in the 3rd column so you need to change `grep "Shark Bay" $station_file | cut -d',' -f3 | sort | uniq` to `grep "Shark Bay" $station_file | cut -d',' -f4 | sort | uniq` and `grep "$i" $station_file | cut -d',' -f2` to `grep "$i" $station_file | cut -d',' -f3`. Also, the folder name of SharkBay site is a little bit different: `eDNAexpeditions_batch*/runs/${site}_12SMiFish/05-dwca/Occurrence*` instead of `eDNAexpeditions_batch*/runs/${site}_12SMifish/05-dwca/Occurrence*` (**MiFish** instead of **Mifish**)

**/!\\** Be careful when working at species rank you need to add the following command just after the last `grep` command: `sed -i '/ /!d' ${site}_${i}_${f}.txt`

