# Road to Data Engineer - Workshop 4

This chapter we are going to learn about building data pipeline, using Google Cloud Composer and Apache Airflow.

## Data Pipeline Orchestration
Data Pipeline Orchestration is about keeping data pipeline in order, tracking and monitoring data pipeline from the start to the end of the flow.

![Image](https://drive.google.com/uc?id=1i4QVomWDfe__7oayVfAoHIX13B4ZCewX)

If have more ETL pipelines, We need more managing dependency between pipelines.

## Elements in Apache Airflow
1. CLI : control pipeline, Backfill, see details, delete pipelines via Command Line
2. Web UI
3. Meta Data Repository : collect job status in database
4. Workers : A machine for running Airflow. control by Airflow Master Node
5. Scheduler : use cron

## DAG - Directed Acyclic Graph Concept
### DAG in Airflow
each Task can be an "Operator" that have different abilities.
Task types in Airflow
1. Sensor : Check there is the file or not
2. Operator : Command or Move data using BashOperator, PythonOperator
3. Hook : Connect with thirdparty. Often called by Sensor or Operator. example GCSHook, S3Hook

## Example of DAG to do ETL in Airflow

![Image](https://drive.google.com/uc?id=1TJ1Qc1UdV2uC1rxF1B8dfABQm5gfa1vy)

## Status Task in Airflow

![Image](https://drive.google.com/uc?id=1pRXt8uZnDTM8UglNW3VXvDqh6Anhyl3z)

## Google Cloud Composer
Google Cloud Composer is managed Apache Airflow service. The advantages of using Cloud Composer are
1. Easy to use with services in GCP
2. Easy to use with third party outside GCP service. e.g. AWS, Azure, Databricks, JIRA, SLACK, Hive, MongoDB, MySQL, and more. . .
3. High-security

**Cloud Composer architecture**
![Image](https://drive.google.com/uc?id=1Cl7wZGF6rIm245x3u8_dEJ7KGJX94f0t)

## Airflow DAG definition file
1. Importing modules
2. Default arguments
3. Instantiate a DAG
4. Tasks
5. Setting up dependencies

## Airflow DAG Example
**1. Importing modules**

```
from airflow import DAG
from airflow.operators.bash import BashOperator
from datetime import datetime, timedelta
```

Additional trick : we can use days_ago by importing library instead using time delta to calculate
```from airflow.utils.dates import days_ago```

**2. Default arguments**
default_args is center config that is used for all tasks
```
default_args ={
    'owner': 'User',
    'depends_on_past': False,
    'start_date': datetime(2015, 12, 1),
    'email': ['airflow@example.com'],
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
    'schedule_interval': '@daily',
    }
```

cron can be used for schedule interval

Schedule on Airflow
Airflow will be worked after the time that we have set.
- If set it "Daily". Airflow will be worked on the end of the day.
- If set it "Weekly". Airflow will be worked on the end of the week.

**3. Instantiate a DAG**
```
dag =DAG(
    dag_id='sample_dag',
    default_args=default_args,
    start_date=days_ago(1),
    schedule_interval='@daily',
)
```
create DAG object and insert "DAG ID" for the DAG. DAG ID should not be the same as other DAG.

**4. Tasks**

```
t1 =BashOperator(
    task_id='print_date',
    bash_command='date',
    dag=dag,
)
t2 =BashOperator(
    task_id='list_file',
    bash_command='gsutil ls gs://asia-northeast1-sample-airf-78822c0d-bucket/dags/',
    dag=dag,
)
```

Tasks is created from creating Operator. task_id is Unique ID

**5. Setting up Dependencies**

![Image](https://drive.google.com/uc?id=1G1sS7Ti1Lnlk-sxtBSLQhTYswyFIflzW)

## Example DAG file
```
from airflow import DAG
from airflow.operators.bash importBashOperator
from datetime import datetime, timedelta

default_args ={
    'owner': 'User',
    'depends_on_past': False,
    'start_date': datetime(2015, 12, 1),
    'email': ['airflow@example.com'],
    email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
    'schedule_interval': '@daily',
    }
    
dag =DAG('sample', catchup=False, default_args=default_args)

t1 =BashOperator(
    task_id='print_date',
    bash_command='date',
    dag=dag
)

t2 =BashOperator(
    task_id='list_file',
    bash_command='gsutil ls gs://asia-northeast1-sample-airf-78822c0d-bucket/dags/',
    dag=dag
)

t1 >>t2
```
