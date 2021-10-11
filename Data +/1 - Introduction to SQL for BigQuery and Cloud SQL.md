```
https://www.cloudskillsboost.google/focuses/2802?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D
```


```
https://console.cloud.google.com/sql/instances/create;engine=MySQL?cloudshell=true
```

```
https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=london_bicycles&page=dataset
```



```
gsutil mb gs://$DEVSHELL_PROJECT_ID

```


```
echo "SELECT start_station_name, COUNT(*) AS num FROM \`bigquery-public-data.london_bicycles.cycle_hire\` GROUP BY start_station_name ORDER BY num DESC;" > Query1.txt
bq query --format=csv --use_legacy_sql=false < Query1.txt > start_station_name.csv
echo "SELECT end_station_name, COUNT(*) AS num FROM \`bigquery-public-data.london_bicycles.cycle_hire\` GROUP BY end_station_name ORDER BY num DESC;" > Query2.txt
bq query --format=csv --use_legacy_sql=false < Query2.txt > end_station_name.csv
gsutil cp *.csv gs://$DEVSHELL_PROJECT_ID


```


```
qwiklabs-demo
```
