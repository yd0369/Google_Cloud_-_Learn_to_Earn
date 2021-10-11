```
https://www.cloudskillsboost.google/focuses/3616?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog
```

```
&cloudshell=true
```

```
echo "
SELECT
  name, gender,
  SUM(number) AS total

FROM
  \`bigquery-public-data.usa_names.usa_1910_2013\`
GROUP BY
  name, gender
ORDER BY
  total DESC
LIMIT
  10
" > Query1.txt

echo "Emma,F,20943
Olivia,F,19823
Sophia,F,18630
Isabella,F,17108
Ava,F,15709
Mia,F,13517
Emily,F,12652
Abigail,F,12095
Madison,F,10323
Charlotte,F,10118
Harper,F,9609
Sofia,F,9600
Elizabeth,F,9576" > yob2014.txt

echo "
SELECT
 name, count
FROM
 \`babynames.names_2014\`
WHERE
 gender = 'M'
ORDER BY count DESC LIMIT 5;
" > Query2.txt


bq mk --location=US babynames 

```
```
bq query --use_legacy_sql=false < Query1.txt

bq load babynames.names_2014 yob2014.txt name:string,gender:string,count:integer

bq query --use_legacy_sql=false < Query2.txt

```