# BigQuery: Qwik Start - Command Line


```
bq query --use_legacy_sql=false \
'SELECT
   word,
   SUM(word_count) AS count
 FROM
   `bigquery-public-data`.samples.shakespeare
 WHERE
   word LIKE "%raisin%"
 GROUP BY
   word'

bq query --use_legacy_sql=false \
'SELECT
   word
 FROM
   `bigquery-public-data`.samples.shakespeare
 WHERE
   word = "huzzah"'


bq mk babynames


wget http://www.ssa.gov/OACT/babynames/names.zip


unzip names.zip


bq load babynames.names2010 yob2010.txt name:string,gender:string,count:integer


bq query "SELECT name,count FROM babynames.names2010 WHERE gender = 'F' ORDER BY count DESC LIMIT 5"


bq query "SELECT name,count FROM babynames.names2010 WHERE gender = 'M' ORDER BY count ASC LIMIT 5"

bq rm -r babynames





```



---
---
---

# Check Summary : 6


- [ ] Run a query (dataset: samples, table: shakespeare, substring: raisin)
- [ ] Run a query (dataset: samples, table: shakespeare, substring: huzzah)
- [ ] Create a new dataset (name: babynames)
- [ ] Load the data into a new table
- [ ] Run queries against your dataset table
- [ ] Remove the babynames dataset