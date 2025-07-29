
# Tokyo-Olympics-DE-Project



## Description
This project outlines a complete data engineering and analytics workflow using the Tokyo Olympic dataset. Beginning with a CSV file hosted on GitHub, the data is ingested into the Azure ecosystem through Azure Data Factory. It is first stored in Azure Data Lake Storage Gen2, then processed and transformed using Azure Databricks. The enriched data is saved back to ADLS Gen2 and further analyzed using Azure Synapse Analytics. Finally, insights are visualized using either Azure Synapse or Power BI, delivering a comprehensive analysis of the dataset.
## Architecture 
<img src="Images/architecture.PNG">

## Dataset Used 
This dataset includes information on over 11,000 athletes across 47 disciplines, representing 743 teams that participated in the Tokyo Olympics held in 2021. It captures detailed records of athletes, coaches, and teams, as well as gender-based entry data. Key attributes include names, represented countries, disciplines, gender of participants, and names of the coaches.

Source(Kaggle): [2021 Olympics in Tokyo](https://www.kaggle.com/datasets/arjunprasadsarkhel/2021-olympics-in-tokyo)

## Azure Services Used
1. **Azure Data Factory:** For data ingestion from GitHub.
2. **Azure Data Lake Storage Gen2**: As the primary data storage solution.
3. **Azure Databricks:** For data transformation tasks.
4. **Azure Synapse Analytics:** To perform in-depth data analytics.
   
## Workflow 

## Initial Setup
Sign up for an Azure Free Subscription account.Create a new Resource Group named tokyo-olympic-data to centrally manage all Azure resources related to the project.Within this resource group, set up a Storage Account configured to use Azure Data Lake Storage (ADLS) Gen2 features.Inside the Storage Account, create a container to store project data. Organize the data using two directories: raw-data for unprocessed files and transformed-data for cleaned and processed files.

  <img src="Images/storage.png"> 

## Data Ingestion using Azure Data Factory
1. Begin by creating an Azure Data Factory workspace within the previously established resource group.
2. After setting up the workspace, launch the Azure Data Factory Studio. 
3. Upload the Tokyo Olympics dataset from kaggle to GitHub.
4. Within the studio, initialize a new data integration pipeline. Now use the task Copy Data to move data efficiently between various supported sources and destinations.
5. Configuring the Data Source with HTTP template as we are using http request to get the data from GitHub repo.
6. Establishing the Linked Service for source.
7. Configuring the File Format for and setting up the Linked Service Sink.
8. Repeat above steps to load all the datasets.
9. You can connect all the copy data activity together and run them all at once.
<img src="Images/datafactory_pipeline.png">  
10. After the pipeline completes its execution, navigate to your Azure Data Lake Storage Gen2. Dive into the "raw_data" folder and validate that the files, like "athletes.csv", "medals.csv", etc., are present and populated with the expected data.

 <img src="Images/raw_data_in_storage.png">

## Data Transformation using Azure Databricks
1. Navigate to Azure Databricks within the Azure portal and create a workspace within the previously established resource group and launch it.
2. Configuring Compute in Databricks
3. Create a new notebook within Databricks and rename it appropriately, reflecting its purpose or the dataset it pertains to.
4. Establishing a Connection to Azure Data Lake Storage (ADLS)
5. Using the credentials (Client ID, Tenant ID, Secret), write the appropriate code in the Databricks notebook to mount ADLS. 
6. Writing Data Transformations mount ADLS Gen2 to Databricks.
7. Writing Transformed Data to ADLS Gen2.
 <img src="Images/transformed_data_tables.png">
  <img src="Images/transformed_data_contents.png">
Refer below notebook to transformations and code used to mount ADLS Gen2 to Databricks.

[Tokyo Olympics Transformation.ipynb](https://github.com/shubhammirajkar/tokyo_olympic_de_project/blob/main/Tokyo%20Olympics%20Transformation.ipynb)

## Setting Up and Using Azure Synapse Analytics
1. Creating a Synapse Analytics Workspace.
2. Within Workspace navigate to the "Data" section , choose "Lake Database"  and create a Database "TokyoOlympicDB"
3. Creating Table from Data Lake  from the Transformed Data folder within your ADLS Gen2 storage.
 <img src="Images/synapse_database_creation.png">
 
## Performing Data Analysis on the Data

Create SQL script to Perform Exploratory data analysis using SQL.
You can aslo use PowerBI to generate your analysis reports.
 <img src="Images/synapse_analytics_report.png">

Refer to the SQL scripts used for data analysis 
[Tokyo Olympics SQL script.sql](https://github.com/shubhammirajkar/tokyo_olympic_de_project/blob/main/Tokyo%20Olympics%20SQL%20script.sql)
