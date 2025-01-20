## Finance Dashboard

I used Blob Storage, Azure Data Factory, Snowflake, and Power BI. I built an ETL pipeline in ADF to get the raw data from the source, performed unpivot and stored the cleaned data at the destination. I created another pipeline to send the data to the Snowflake table from the container where clean data is stored. In the end, I created a Dashboard in Power BI.



This is our data which needs to be processed further to get the Date and Value columns that are required for our dashboard.<br>
![s1](https://github.com/user-attachments/assets/5c83b42c-2aa3-4cb3-8835-02c61c4bcd61)

Now we need to create an Azure Factory and storage account as follows. <br>

![s2](https://github.com/user-attachments/assets/c03cd39e-f0c8-4a67-a2c7-841f5255c763)

Here I have created two folders *rawdata* where I put uncleaned data and *cleaneddata* where I put cleaned data after cleanup.<br>
![s3](https://github.com/user-attachments/assets/62b8bae5-9d83-4db7-88ea-2fa31d645005)

I created two link services one for the *storage account* and the other for *Snowflake* .<br>

![s4](https://github.com/user-attachments/assets/89ec7c00-31c8-404a-b58c-307434c2bcaa)
![s5](https://github.com/user-attachments/assets/40200f10-430a-4235-a8ff-030ceb15144a)

I created four datasets for unclean data, clean data, a snowflake table, and one to get which connects to clean data.<br>

![s6](https://github.com/user-attachments/assets/07e184d6-c3ad-4947-bb65-c0a934d4bbeb)

Below is the *pipeline1* that cleans the data, here I used a source, an unpivot, and a sink to perform the cleaning.<br>

![s7](https://github.com/user-attachments/assets/370abea7-9f6a-49a0-8bcb-f68f337e0913)

I ungrouped the data on the *Type* and *Component* columns.

![s8](https://github.com/user-attachments/assets/c4a0b335-4818-4ef5-8c07-eb635119cc7c)
![s9](https://github.com/user-attachments/assets/06777aa2-b5e4-4716-bc4b-bdefa16066ce)

I created a table called finance_table with columns Type, Component, Entdate, and Value.

![s10](https://github.com/user-attachments/assets/07297b91-b9f7-4ab9-a237-e023cddc055c)

I Debugged the Pipeline1.

![s11](https://github.com/user-attachments/assets/ca0eb703-c65c-4727-98a4-52246e517dd5)
![s12](https://github.com/user-attachments/assets/76afa7d4-e753-4c53-ac4e-9eb39ec8868d)
![s13](https://github.com/user-attachments/assets/d381e9b5-8cdf-4407-8f67-fdbf2799307d)

After running the debug, we got the *data.csv* file in the *cleaneddata* folder.

![s14](https://github.com/user-attachments/assets/e48f4633-0948-4b87-b955-1ac0913dec6a)
![s15](https://github.com/user-attachments/assets/39cbe099-4a20-4622-af56-03689b082e21)

Now let's debug pipeline2

![s16](https://github.com/user-attachments/assets/8b1bc027-8d72-4a47-baf6-0e3bd1d95a87)
![s17](https://github.com/user-attachments/assets/72b85404-60d3-4065-a089-df2b28fb2b01)
![s18](https://github.com/user-attachments/assets/8db6eabe-782c-4acf-8f46-99b77a1e49bc)

Let's go to Snowflake, after running the *select* query we can see that data have been copied to finance_table.

![s19](https://github.com/user-attachments/assets/b34d3866-d5ec-42f6-8944-85492aee19e2)

I already created a dashboard, then I had to connect the Snowflake table to Power BI and change the data source from Power BI.
![s20](https://github.com/user-attachments/assets/d3013cfb-0056-4021-80c0-a2e662f218c4)
![s22](https://github.com/user-attachments/assets/f01c10f3-a18e-409a-8486-f32d13937f13)
![s23](https://github.com/user-attachments/assets/6d3f7f6e-5158-4aec-bb8a-5a87515dbe91)
![s24](https://github.com/user-attachments/assets/1a67a08c-37b3-4b64-a198-b8dc0fe58763)
![s25](https://github.com/user-attachments/assets/6d912a1f-e6d6-419b-8920-57c379ff9edf)
![s26](https://github.com/user-attachments/assets/bcc45ed5-0308-4715-9da6-b0d9524cb319)

Now let's change the column name according to the measures I created.

*We are All Done !!!*

![s27](https://github.com/user-attachments/assets/a7b869ce-a783-4da1-8dce-04cac0490dcd)

Let's check if I add data in the snowflake table is reflected in Power BI or not

![s29](https://github.com/user-attachments/assets/95f6bbe0-e957-45d4-9da4-00becdc801c6)

Yes, It is reflecting

![s30](https://github.com/user-attachments/assets/361a7428-8458-4eab-9552-3c1a9c973ad5)



