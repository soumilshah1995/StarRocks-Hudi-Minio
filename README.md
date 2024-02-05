# StarRocks-Hudi-Minio
StarRocks+Hudi+Minio
![Screenshot 2024-02-03 at 5 30 11 PM](https://github.com/soumilshah1995/StarRocks-Hudi-Minio/assets/39345855/2c1747d2-866f-4fa4-a265-1a98ba1dfe98)


# steps 
# Step 1: Spin up stack 
```
docker-compose up --build -d
```
# step 2:  Create Bucket
```agsl

Head http://localhost:9001/login
username as admin 
password password 

create a bucket called huditest

```
# Step  3: Run python file hudi_job_hive_sync.py

# step 4: 
docker exec -it starrocks-hudi-minio-starrocks-fe-1 /bin/bash -c 'mysql -P 9030 -h 127.0.0.1 -u root --prompt="StarRocks > "'

# Step 5: Create External Catlog 
```
CREATE EXTERNAL CATALOG hudi_catalog_hms

PROPERTIES
(
    "type" = "hudi",
    "hive.metastore.type" = "hive",
    "hive.metastore.uris" = "thrift://hive-metastore:9083",
    "aws.s3.use_instance_profile" = "false",
    "aws.s3.access_key" = "admin",
    "aws.s3.secret_key" = "password",
    "aws.s3.region" = "us-east-1",
    "aws.s3.enable_ssl" = "false",
    "aws.s3.enable_path_style_access" = "true",
    "aws.s3.endpoint" = "http://minio:9000"
);


set catalog hudi_catalog_hms;
show databases;
use default;
show tables;
select * from customers;
```

## Special Thanks to Albert  Wong 
