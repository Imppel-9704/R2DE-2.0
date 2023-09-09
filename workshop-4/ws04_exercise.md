# Road to Data Engineer - Workshop 4

## Create Cloud Composer
1. I'm going to create Cloud Composer. Click create button on the top of page.
![Image](https://drive.google.com/uc?id=1OZNVtM4-T1NoXZ86iTxDoElW0ArycAUO)

2. Config Cloud Composer. 
- Name Cloud Composer
- Set Location (I chose asia-southeast1)
- Select Image version of composer.
- Select Machine Type (In case working with large data it should be n1-standard-2 or more. Because it have more cpu and ram.)
- Select Disk Size
![Image](https://drive.google.com/uc?id=1AOAIVzLHQesbNqo24FUMwlSWoSTkW9Nb)


*After creating Airflow. Airflow bucket will be created automatically. It contains **DAGs** and **Data** folders inside.

## Go to Apache Airflow
For the Apache Airflow site. You'll find this page as following picture.
To set up connection with Database. Select **Admin** menu on the top then select **Connections**.
![Image](https://drive.google.com/uc?id=13gCJRuJLDRfrF7AqK6a-bT0wDwXZ-oYf)

In this case, I use MySQL. Select **Edit record**
![Image](https://drive.google.com/uc?id=1vFKwQB_6uB7D-XsDoiuprpKBRnalnGd-)

Name the connection ID. Then insert Host, Schema, Login, Password, and Port
![Image](https://drive.google.com/uc?id=118f7gjiK-bPLgutLXBU9s8ZQJ1kgmn9Y)

## Airflow DAGs
To load DAGs to Airflow from Python source files. I use Cloud Shell Editor to upload .py, edit, and then upload it to **DAGs**, using gsutil command.
![Image](https://drive.google.com/uc?id=1XNocl3g-cFrGCXvPLfwL9BsOZxGVm6f5)

upload data, using gsutil command.
![Image](https://drive.google.com/uc?id=1Yd2ll7D_Nij9bfZU7aA0X-KGlmNz2BVG)

Uploaded data in DAGs folder
![Image](https://drive.google.com/uc?id=1wTpO5o0sU15-LEmskBJQFi7jvL8BOb54)

## Airflow will automatically sync with DAGs folder on bucket.
![Image](https://drive.google.com/uc?id=1yzWpG6Qg4UiMnHJLy9QRQS-aHuw-dUX_)

## Run it normally
![Image](https://drive.google.com/uc?id=1fnTNP_-9sveAVG_Mn40jk9iyCAIrJI0C)

## Check the result
From my ws04_exercise4.ipynb. I set it to return output to **Data** folder on Airflow bucket. \
p.s. I changed the Airflow because my previous Airflow have some problem. to create new one I have to change the location.
![Image](https://drive.google.com/uc?id=1BsQBY79FEGSFiALZqpLeyGfXSIiLWTqg)
