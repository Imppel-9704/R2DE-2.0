# Road to Data Engineer - Workshop 3
## Upload file to Google Cloud Storage

This workshop we are going to learn about uploading file to Google Cloud Storage, using gsutil command. Input file is the .csv file from workshop 2.

Documentation for gsutil : https://cloud.google.com/storage/docs/gsutil  
gsutil fundamental cheatsheet : https://gist.github.com/fonylew/480ab35656572c5341510b59785ac2e8

## Google Cloud Storage
1. create bucket
- using Cloud console on google cloud website
- using gsutil command by cloud shell

2. upload data
- uploading by using Cloud console
- uploading by using gsutil command
- uploading by using Python SDK library

## gsutil command
**Create a new Bucket**
gsutil mb gs://[BUCKET]
- -c: Specify the default storage class of your bucket. For example, NEARLINE.
- -l: Specify the location of your bucket. For example, US-EAST1.
- -b: Specify the uniform bucket-level access setting for your bucket. For example, ON.

For example : gsutil mb -c standard -l asia-southeast2 -b on gs://r2de-data-lake

## List files in bucket
gsutil ls gs://[BUCKET]

## Copy (upload) file to bucket
gsutil cp [File] gs://[BUCKET]

![Image](https://drive.google.com/uc?id=1a-3zGRtPQmco6RDbc9TRcGZpcgEEAe1L)

## Remove file or directory 
**remove file**
gsutil rm gs://[BUCKET]/path/to/file
**remove directory**
gsutil rm -r gs://[BUCKET]/path/to/directory    
