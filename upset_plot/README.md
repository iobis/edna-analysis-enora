In this folder you will find the upset plots for each amplicon for 3 different taxonomic ranks: species, genus and family

To generate the needed files to run the Rscripts you need to first run the following code:

```
station_file=https://github.com/iobis/edna-tracker-data/blob/master/supplementary_info/stations.csv
occurence_files=https://github.com/iobis/pacman-pipeline-results/tree/master/eDNAexpeditions_batch*/runs/${site}_12SMifish/05-dwca/Occurrence*
site=Scandola
mkdir ${site}_genus
cd ${site}_genus
Stations=`grep "Scandola" $station_file | cut -d',' -f3 | sort | uniq`
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
