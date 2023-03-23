# Assessment--Brinerds-Ventures-Pvt-Ltd

This project calculates the following questions for the test datasets and for the dataset orders.csv
- Compute the total revenue generated by the online store for each month in the dataset.
- Compute the total revenue generated by each product in the dataset.
- Compute the total revenue generated by each customer in the dataset.
- Identify the top 10 customers by revenue generated.

## Datasets

Tests and actual datasets are not provided it is created with the python script `generate_Dataset.py` which will create records dynamically.
This script creates 
- 3 test datasets each with 100 records (`test/datasets/test1.csv`,`test/datasets/test2.csv`,`test/datasets/test3.csv`)
- an actual orders datasets with 1000000 records for which our main application will work. (`dataset/orders.csv`)
Each dataset has these columns - `order_id`,`customer_id`,`order_date`,`product_id`,`product_name`,`product_price`,`quantity`.

## Test code with test datasets

There is a python script `test/processdata.py` which will give results based on the datasets under `test/datasets/` directory.

Note: </br>
- I need to learn the pytest framework to write test cases and test it. But for now I'll just execute the script  `test/processdata.py` to get the results for the test datasets `test/datasets/`
- I you want to test your test datasets, you can paste your csv file under directory `test/datasets/`. Python script will automatically take those csv file and will give you the results.

## Application Code

There is a python script `processdata.py` which will give results based on the dataset  `dataset/orders.csv`.

## Application Containerization

There are 2 Dockerfiles `test/Dockerfile` and `Dockerfile`
```
FROM python:latest
WORKDIR /usr/app/src
COPY processdata.py ./
RUN mkdir -p dataset/
COPY requirements.txt ./
RUN pip install -r requirements.txt
CMD [ "python3", "./processdata.py"]
```
 
## Docker Compose

There are 2 services :
1. Test_app_service: 
    - Run the docker container created with `test/Dockerfile`
    - Bind Mount the `test/datasets/` directory.
2. App_service:
    - Run the docker container created with `Dockerfile`
    - Bind Mount the `dataset/` directory.

## Continuous Deployment with GitHub Action

workflow file - `.github/workflows/test-build-deploy.yml`.

Workflow:</br>
- UnitTest:
    - Checkout repository
    - Setup Python
    - Install depedencies
    - Execute test script
- Build:
    - Checkout repository
    - Install Docker
    - Login to Docker Registry
    - Build & Push docker image for testing application
    - Build & Push application docker image
    - Logout docker registry
- Deploy:
    - Checkout repository
    - Install Docker
    - Docker compose up
    - Upload results artifact

## Check Results
- Check the test cases




