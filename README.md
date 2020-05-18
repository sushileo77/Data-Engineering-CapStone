# Data-Engineering-CapStone
Udacity-CapStone Project (Design an ETL PipeLine)

 -- The purpose of this project is to demonstrate various skills associated with data engineering projects.
 -- Implementing ETL pipelines using Airflow, constructing data warehouses through Redshift databases and S3 data storage
 -- Defining efficient data models e.g. star schema.
 
 Data into consideration :- 
    -- US immigration
    -- focusing on the type of visas being issued and the profiles associated. 
    -- The scope of this project is limited to the data sources listed below with data being aggregated across numerous dimensions such as visatype, gender, port_of_entry, nationality and month.


-- > Data Description & Sources
      -- I94 Immigration Data: 
          This data comes from the US National Tourism and Trade Office.
          Each report contains international visitor arrival statistics by world regions and select countries (including top 20), type of             visa, mode of transportation, age groups, states visited (first intended address only), and the top ports of entry (for select   countries).

      -- U.S. City Demographic Data:
         This dataset contains information about the demographics of all US cities and census-designated places with a population greater             or equal to 65,000. Dataset comes from OpenSoft found here.
         
      --Airport Code Table: This is a simple table of airport codes and corresponding cities. The airport codes may refer to either IATA         airport code, a three-letter code which is used in passenger reservation, ticketing and baggage-handling systems, or the ICAO           airport code which is a four letter code used by ATC systems and for airports that do not have an IATA airport code (from               wikipedia). It comes from here.
      
- > Data Storage and Resources
      -- Data was stored in S3 buckets in a collection of CSV and PARQUET files.
      -- This dataset was converted to PARQUET files to allow for easy data manipulation and ability to write to Redshift.
      
- > Data-PipeLine

      -- Extracting files from S3 buckets, transforming the data and then writing CSV and PARQUET files to Redshift is accomplished              in the ETL Dag graph.
      These steps include:
        - Extracting data from SAS Documents and writing as CSV files to S3 immigration bucket 
        - Extracting remaining CSV and PARQUET files from S3 immigration bucket 
        - Writing CSV and PARQUET files from S3 to Redshift
        - Performing data quality checks on the newly created tables
    
Achievements and Conclusion :-
  -- Developing an ETL Pipeline that copies data from S3 buckets into staging tables to be processed into a star schema
  -- Using Airflow to automate ETL pipelines using Airflow, Python, Amazon Redshift.
  -- Validation through data quality checks.


Challenges and Scenarios to Consider:
 <1> Data is 100x:
     - Input data should be stoted in cloud storage e.g. AWS S3, Microsoft Azure, GCP
     - Clustered Spark should be used to enable parallel processing of the data.
     - Clustered Cloud DB e.g. AWS Redshift should be used to store the data during the processing (staging and final tables).
     - Output data (parquet files) should be stored to Cloud storage for easy access or to a Cloud DB for further analysis. 
     - AWS RDS should be used to save some costs.

 <2> Data is used in dashboard and updated every day 07:00AM:
     -ETL script should be refactored to process only the changed inout information instead of processing all the inout files as it does       now to minimise the used time and shared resources.
     -Output data should be stored and updated in a Cloud DB to make it available all times for the dashboard.
     -Possibly this "always available" DB (serving the dashboard) would contain a latest sub-set of all available data to make it fast         perfoming and easier to manage.
     
 <3> DB is accessed by 100+ people:
     -Output data should be stored in a Cloud DB (e.g. AWS RDS) to make it "always available" for further analysis. 
     -Tools should be provided for the end-users to access the output DB.
