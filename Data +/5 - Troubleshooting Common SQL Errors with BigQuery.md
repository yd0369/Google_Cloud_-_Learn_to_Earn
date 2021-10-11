
```
echo "
#standardSQL
SELECT
COUNT(DISTINCT hits_product_v2ProductName) as number_of_products,
hits_product_v2ProductCategory
FROM \`data-to-insights.ecommerce.rev_transactions\`
WHERE hits_product_v2ProductName IS NOT NULL
GROUP BY hits_product_v2ProductCategory
ORDER BY number_of_products DESC
LIMIT 5
" > Query3.txt
bq query --use_legacy_sql=false < Query3.txt

```


```
echo "
#standardSQL
SELECT
COUNT(DISTINCT fullVisitorId) AS visitor_count
, hits_page_pageTitle
FROM \`data-to-insights.ecommerce.rev_transactions\`
GROUP BY hits_page_pageTitle
" > Query1.txt
bq query --use_legacy_sql=false < Query1.txt


echo "
#standardSQL
SELECT
COUNT(DISTINCT fullVisitorId) AS visitor_count
, hits_page_pageTitle
FROM \`data-to-insights.ecommerce.rev_transactions\`
WHERE hits_page_pageTitle = "Checkout Confirmation"
GROUP BY hits_page_pageTitle
" > Query1.txt
bq query --use_legacy_sql=false < Query1.txt

```
---

```
echo "
#standardSQL
SELECT
geoNetwork_city,
SUM(totals_transactions) AS totals_transactions,
COUNT( DISTINCT fullVisitorId) AS distinct_visitors
FROM
\`data-to-insights.ecommerce.rev_transactions\`
GROUP BY geoNetwork_city
" > Query2.txt
bq query --use_legacy_sql=false < Query2.txt


echo "
#standardSQL
SELECT
geoNetwork_city,
SUM(totals_transactions) AS totals_transactions,
COUNT( DISTINCT fullVisitorId) AS distinct_visitors
FROM
\`data-to-insights.ecommerce.rev_transactions\`
GROUP BY geoNetwork_city
ORDER BY distinct_visitors DESC
" > Query2.txt
bq query --use_legacy_sql=false < Query2.txt

echo "
#standardSQL
SELECT
geoNetwork_city,
SUM(totals_transactions) AS total_products_ordered,
COUNT( DISTINCT fullVisitorId) AS distinct_visitors,
SUM(totals_transactions) / COUNT( DISTINCT fullVisitorId) AS avg_products_ordered
FROM
\`data-to-insights.ecommerce.rev_transactions\`
GROUP BY geoNetwork_city
ORDER BY avg_products_ordered DESC
" > Query2.txt
bq query --use_legacy_sql=false < Query2.txt

echo "
#standardSQL
SELECT
geoNetwork_city,
SUM(totals_transactions) AS total_products_ordered,
COUNT( DISTINCT fullVisitorId) AS distinct_visitors,
SUM(totals_transactions) / COUNT( DISTINCT fullVisitorId) AS avg_products_ordered
FROM
\`data-to-insights.ecommerce.rev_transactions\`
GROUP BY geoNetwork_city
HAVING avg_products_ordered > 20
ORDER BY avg_products_ordered DESC
" > Query2.txt
bq query --use_legacy_sql=false < Query2.txt


```
---
