
```
&cloudshell=true
```



```
echo "
SELECT * FROM \`ctg-storage.bigquery_billing_export.gcp_billing_export_v1_01150A_B8F62B_47D999\`
" > Query1.txt

 bq query --use_legacy_sql=false < Query1.txt

echo "
SELECT service.description FROM \`ctg-storage.bigquery_billing_export.gcp_billing_export_v1_01150A_B8F62B_47D999\` GROUP BY service.description" > Query2.txt

 bq query --use_legacy_sql=false < Query2.txt

```

```
echo "
SELECT service.description, COUNT(*) AS num FROM \`ctg-storage.bigquery_billing_export.gcp_billing_export_v1_01150A_B8F62B_47D999\` GROUP BY service.description" > Query3.txt

 bq query --use_legacy_sql=false < Query3.txt

echo "
SELECT location.region, COUNT(*) AS num FROM \`ctg-storage.bigquery_billing_export.gcp_billing_export_v1_01150A_B8F62B_47D999\` GROUP BY location.region" > Query4.txt

 bq query --use_legacy_sql=false < Query4.txt

```