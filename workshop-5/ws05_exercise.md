# Road to Data Engineer - Workshop 5

![Image](https://drive.google.com/uc?id=1h8NFuUZcBiUk5p97li5MhBZjITuQsekR)


### What we gonna do in this workshop?
1. Create dataset on Bigquery
2. Import data
  - Import by Cloud Console (Web UI) on browser.
  - Import by using BQ command within BashOperator on Airflow.
  - Import by GCSTOBigQueryOperator on Airflow
3. Explore data on Bigquery.

## Create Airflow
Same as workshop 4. I'm going to create Cloud Composer. Click create button on the top of page.

![Image](https://drive.google.com/uc?id=1FHNEr-eMsLQ5g8Cc6lPrAzTXeZCF1-LO)

## Install package
it will takes time around 5-10 minutes.

![Image](https://drive.google.com/uc?id=1I3hAnPfnQuKwzfkOmhc3LZiLVtceoDnm)

## Create Dataset on Bigquery

![Image](https://drive.google.com/uc?id=1WFS2WXYCGtTacHD2B-YnbEwuLKo330Uo)

****It have to be same region with the Cloud Composer.**

## Upload file to BigQuery

**1. Upload by using UI**
  - Select the exported file from the workshop 4.
  - Select native table and name the table.
  - Select auto detect schema (in case having header row) or fill column name on your own
  - Create table

![Image](https://drive.google.com/uc?id=1BdexlvJvVYI2gn6Em3L15HJZTbYpllS3)

**2. using BQ load command**
Example code:
  ```
  bq load \
  -- source_format=CSV --autodetect \
  [DATASET].[TABLE_NAME] \
  gs://[GCS_BUCKET]/data/[FILE_NAME].csv
  ```

 - Same as workshop 4. I upload python file to DAGs folder.
![Image](https://drive.google.com/uc?id=1U8oZwtbUvZbWHXGRsPTlE4e3-R__swfd)

 - wait it run
![Image](https://drive.google.com/uc?id=1Alu5xk8mVRp9gTbsiIb9zcd-c50792nY)

 - check the output on BigQuery
![Image](https://drive.google.com/uc?id=1X0nIECsx3z_60TRYt1oGJb8vgWmae-N-)

**3. using GCSTOBigQueryOperator**
use Airflow operator named "GCSToBigQueryOperator"

Example code:
```
from airflow.providers.google.cloud.transfers.gcs_to_bigquery import GCSToBigQueryOperator

load_csv = GCSToBigQueryOperator(
  task_id = "gcs_to_bq_example",
  bucket = "cloud_samples_data",
  source_objects = ['bigquery/us-states/us-states.csv'],
  destination_project_dataset_table = "dataset.table_name",
  autodetect = True,
  write_disposition = "WRITE_TRUNCATE",
)
```

Autodetect mean let's BigQuery automatically set datatypes. In case no need "autodetect". You have to fill schema_fields in json.

write_disposition = "WRITE_TRUNCATE", This code will create new table everytimes. If you want to append data in the same table. Please user "WRITE_APPEND"

** *Autodetect can't be used rightnow for some reason.*
Therefore use this instead.

```
from airflow.providers.google.cloud.transfers.gcs_to_bigquery import GCSToBigQueryOperator

load_csv = GCSToBigQueryOperator(
  task_id='gcs_to_bq_example',
  bucket='cloud-samples-data',
  source_objects=['bigquery/us-states/us-states.csv'],
  destination_project_dataset_table='dataset.table_name',
  schema_fields=[
  {
    "mode": "NULLABLE",
    "name": "timestamp",
    "type": "TIMESTAMP"
  },
  {
    "mode": "NULLABLE",
    "name": "user_id",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "country",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Book_ID",
    "type": "INTEGER"
  },
  {
    "mode": "NULLABLE",
    "name": "Book_Title",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Book_Subtitle",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Book_Author",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Book_Narrator",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Audio_Runtime",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Audiobook_Type",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Categories",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Rating",
    "type": "STRING"
  },
  {
    "mode": "NULLABLE",
    "name": "Total_No__of_Ratings",
    "type": "FLOAT"
  },
  {
    "mode": "NULLABLE",
    "name": "Price",
    "type": "FLOAT"
  },
  {
    "mode": "NULLABLE",
    "name": "conversion_rate",
    "type": "FLOAT"
  },
  {
    "mode": "NULLABLE",
    "name": "THBPrice",
    "type": "FLOAT"
  }
],
  write_disposition='WRITE_TRUNCATE',
)
```

- upload .py to DAGs folder.
![Image](https://drive.google.com/uc?id=1GJYny3V9ECP_8Li2nsw8qaqmRFSJ9KA3)

- wait Airflow run
![Image](https://drive.google.com/uc?id=1rf6rFHVautNYQH8n0lYNm6181GD69-IK)

- indentify log
![Image](https://drive.google.com/uc?id=1NkWT6ONdQLlhOEnntkQav_Dl-M4FceBx)

- check the output on BigQuery
![Image](https://drive.google.com/uc?id=1yAdwhQ44Cz7gAuMxPB9054b7wTmxQWrz)

- try to query to check result
![Image](https://drive.google.com/uc?id=1CuXGLBJn57RIQHX6GVwG5aJTyI6GLAX_)

## Bonus : How to get BigQuery Table Schema in .json
run the code below, using command line on cloud shell to get table schema.

```
bq show --schema --format prettyjson dataset.table_name
```

![Image](https://drive.google.com/uc?id=1GbHxvG8_2Zm62f6vGJyiSQC0h_rpRPVB)