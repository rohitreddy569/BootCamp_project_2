Bootcamp project 2
Architecture :
![image](https://github.com/user-attachments/assets/efb654d3-f563-43d7-8086-92dd2467b226)

BOOT CAMP PROJECT 2
RETAIL SALES 

SUBMITTED TO 
VARUN(NCPL)









Prepared by:
RohithKumar Reddy Kuraparthi
Scenario: Reading data from multiple sources such as On prem Db, Rest Api and ADLS Gen 2  to SQL DB for further analysis 
Layers covered: Raw(Bonze), Curated(Silver)
Tools Used:
My SQL DB: On prem data source 
ADLS Gen 2: Storage container 
Git Hub: To get Rest API Instance 
ADF: To create transformations using Data flow and Copy activity to copy the data o source systems to the sink(destination system).
Azure SQL DB: Acts as the final system and utilized by other teams 

Architecture:
<img width="468" alt="image" src="https://github.com/user-attachments/assets/61cf7e9e-bc7a-42c7-b81e-04dca574b261" />

 

Role: I worked mostly on the Data flow transformations, utilized multiple data flow transformation tools to create ETL job and cleaned the data in the most effective way. 
Worked on multiple joins, aggregations and transformed the data to made it readily available for the end user for further analysis.




Creating the self-hosted Integration run time to get the data from on-prem devices. 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/c42a37f3-4ea2-424c-9a67-167f71b4c50e" />

I have leveraged MY SQL as my data is residing in MSQL DB under customer_sample table
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/3d0f7421-bd34-4514-b251-d612328ddea3" />


Using ADF copy Data Activity I have successfully got the data into my Raw layer (ADLS Gen2), For the reference import schema can be visibly seen which was extracting from SQL DB
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/1c2aa770-5806-4ec1-aa53-02ba177a7279" />

Adding trigger to my activity 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/5f45a2b5-e12e-4534-a507-e539b4a00d9c" />

Schedule trigger activity with 15 mins of time gap considering my sql DB will get data in every 15 mins added the timestamp based on this 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/a87073e4-ac3d-4b9f-ba5a-80aeef5473c6" />

Exactly after 15 mins the trigger initialized.
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/3d757aaa-a6d6-4690-871d-09b072347c5c" />






The data is now successfully stored in the destination (Bronze layer)
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/72dcd6ea-e895-492f-b962-89dbf063b9c8" />

SALES Data :
Data related to the Sales are residing in Github repository 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/a4f84e4e-40f8-4d36-b6c6-f90bc8f89404" />

And can be seen in the  link 
https://raw.githubusercontent.com/rohitreddy569/BootCamp_project_2/refs/heads/main/sales_sample.json
 
Utilized Rest API services provided by Azure to get the data from Github location 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/d8c39d7c-4c7f-4ab1-9e3b-e35e5158b75f" />

Added Tumbling window trigger to the copy activity 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/80d9c64e-7f6d-49d4-ada1-3d61755de018" />




Using the simple copy activity, I can be able to transfer the data from Rest API to ADLS Gen 2
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/a144d0e9-abe8-4e56-8cc0-135e3adef5fc" />


Once the debug is On I can see ADF is successfully getting the data residing in the link 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/1134c9b1-75a4-48bb-86c2-c55e593145bd" />




Data mapping can be seen in the below screen shot where it is exactly matching the columns
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/25ab45c8-f4d9-4823-b13d-a7ad6babc0f3" />


Data is now sent to the ADLS Gen 2 (Bronx=ze layer )for further transformations 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/7aeb976c-3f7e-45e2-b4fd-0948cd990155" />


Once my data is in Bronze layer, Now I can perform the transformations, ADF is equipped with Data flows which is a great tool to work with data. It has simple drag and drop interface where there is no need to code any of the transformations. We can utilize expression builder to customize any of the transformations like removing the null values, performing aggregations, use joins to get the desired data output.
Below are the transformations I have utilized as a part of this project. I have taken three sources, indicating one for each data set that is residing in the bronze layer. Once my data is completed transformed, I have provided the sink for each source. 
The sink here Is again the ADLS Gen 2 but the Silver Layer.
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/91268aa6-b208-42d5-8bc0-ec85321ece8a" />

Using the pipeline, I have executed the data flow activity to transfer all the files to Silver layer
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/a878548b-b9b6-4c3d-81fa-45ef77bc9d28" />


Azure SQL DB has been created with the required databases and tables for customers, Products and Sales 
 
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/df09f745-9b87-4689-893c-a36b7c4f1f28" />

 <img width="468" alt="image" src="https://github.com/user-attachments/assets/9920a2af-2f58-44ae-9eb3-324d6ad4a119" />

<img width="468" alt="image" src="https://github.com/user-attachments/assets/1b2af88f-dc58-445a-b2b1-11c0ae87b0b1" />



After the transformations, Using the copy activity, now all the files has been pushed to the final destination (From Silver to SQL DB)
 <img width="468" alt="image" src="https://github.com/user-attachments/assets/4bf55167-1735-47b4-8f1c-611d96a2234b" />


Final Output can be seen in the below tables. The data is now ready for further analysis.
 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/b930a32b-3f50-47e3-8997-ff0f851c1653" />

 

  

Key Takeaways:
We can add the sample data in case if there are any issues with any of the service. Workflow should not stop.


![image](https://github.com/user-attachments/assets/0a0e3018-8687-4287-bfd1-01791e0dfce3)
<img width="468" alt="image" src="https://github.com/user-attachments/assets/df036ead-287b-412a-924e-3dc421e69d14" />
<img width="468" alt="image" src="https://github.com/user-attachments/assets/682ebec3-4f3e-4a59-a755-8e984d4ee258" />




