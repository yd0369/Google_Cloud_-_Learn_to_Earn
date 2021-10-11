 
git clone https://github.com/GoogleCloudPlatform/data-science-on-gcp/
cd ~/data-science-on-gcp/04_streaming/simulate
virtualenv data-sci-env -p python3
source data-sci-env/bin/activate
pip install timezonefinder pytz
pip install apache-beam[gcp]
python ./df05.py
export PROJECT_ID=$(gcloud info --format='value(config.project)')
bq mk --project_id $PROJECT_ID flights

cd ~/data-science-on-gcp/04_streaming/simulate
export BUCKET=${PROJECT_ID}-ml
gsutil cp airports.csv.gz gs://$BUCKET/flights/airports/airports.csv.gz

python df06.py -p $PROJECT_ID -b $BUCKET -r us-central1

echo "
SELECT
  FL_NUM,
  ORIGIN,
  DEP_TIME,
  DEP_DELAY,
  DEST,
  ARR_TIME,
  ARR_DELAY,
  EVENT,
  NOTIFY_TIME
FROM
  \`flightssample.simevents\`
WHERE
  (DEP_DELAY > 15 and ORIGIN = 'SEA') or
  (ARR_DELAY > 15 and DEST = 'SEA')
ORDER BY
  NOTIFY_TIME ASC
LIMIT
  10
  " > Query.txt
bq query --use_legacy_sql=false < Query.txt