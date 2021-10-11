```
https://www.cloudskillsboost.google/focuses/3616?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog
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

bq query --use_legacy_sql=false < Query1.txt


bq mk --location=US babynames 


echo "
SELECT
 name, count
FROM
 \`babynames.names_2014\`
WHERE
 gender = 'M'
ORDER BY count DESC LIMIT 5;
" > Query1.txt

bq query --use_legacy_sql=false < Query1.txt

```