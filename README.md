# Loading-data-into-BigQuery

In some labs, we worked on public datasets available in Cloud Storage. In this lab, we will ingest NYC taxi trips into tables inside of BigQuery.

In this lab, we will learn how to load data from different sources. Create tables using DDL.

# Lets Start

First log in to GCP platform, and from the navigation side menu, select BigQuery. Make sure you have selected your project, while creating dataset.

![Test Image 4]( https://github.com/acadali/Loading-data-into-BigQuery/blob/main/1.png)

After clicking on **Create Dataset**, a window will open to enter dataset information.

![Test Image 4]( https://github.com/acadali/Loading-data-into-BigQuery/blob/main/2.png)

Fill the form and click **Create Dataset**. Dataset will be created, and it will be added in your project. Create table in your dataset.

![Test Image 4]( https://github.com/acadali/Loading-data-into-BigQuery/blob/main/3.png)

Download a subset of NYC from <a download="nyctaxi.csv" href="https://github.com/acadali/Loading-data-into-BigQuery/blob/main/nyc_tlc_yellow_trips_2018_subset_1.csv" title="ImageName">
    <img alt="ImageName" src="https://github.com/acadali/Loading-data-into-BigQuery/blob/main/nyc_tlc_yellow_trips_2018_subset_1.csv">here
</a>

. Select nyctaxi dataset then click **Create Table**.

Add the below options.

1. Create table from: **Upload**
2. Choose file: **select the file where you downloaded locally.**
3. File format: **csv**
4. Table name: **2018trips.**
5. Schema: **check auto detect**

Click **Create Table**

![Test Image 4]( https://github.com/acadali/Loading-data-into-BigQuery/blob/main/4.png)

You should see the table below the nyctaxi dataset. Select **2018trips** and view the schema and data.

![Test Image 4]( https://github.com/acadali/Loading-data-into-BigQuery/blob/main/5.png)

In the query editor, write a query to list the top 5 most expensive trips of the year. Paste the query in query editor and run the query.

    SELECT * FROM nyctaxi.2018trips ORDER BY fare_amount DESC LIMIT 5

![Test Image 4]( https://github.com/acadali/Loading-data-into-BigQuery/blob/main/6.png)

Now, we will try to load another data of same 2018 trip data, that is available on Cloud Storage.

In the Cloud Shell, paste the following commands.

    bq load \ --source\_format=CSV \ --autodetect \ 
    --noreplace \ nyctaxi.2018trips \ 
    gs://cloud-training/OCBL013/nyc_tlc_yellow_trips_2018_subset_2.csv

![Test Image 4]( https://github.com/acadali/Loading-data-into-BigQuery/blob/main/7.png)

We can also create tables from other tables with DDL.

Paste the query in query editor and run the query. It will select the data from nyctaxi.2018trips and create a new table &quot;January\_trips&quot; and add data from the select query.

    CREATE TABLE nyctaxi.january_trips AS SELECT * FROM nyctaxi.2018trips WHERE EXTRACT(Month FROM pickup_datetime)=1;

![Test Image 4]( https://github.com/acadali/Loading-data-into-BigQuery/blob/main/8.png)

Now we can use January-trips table as well.
