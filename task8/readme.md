## Task
Clone *ORCL* database using Enterprise Manager in *Copy database files via staging area* mode.
Create 2 tables in the cloned database, establish a relationship between them and fill them with data.
Create a backup copy of the cloned database.
Restore the cloned database to the moment when the relationship between the tables has not yet been created.

## Solution
Go to the Data Movement tab in the Clone Database section.
![1](https://user-images.githubusercontent.com/61746700/159166975-6ce92578-9c7a-41a7-bdf9-ef238a072210.png)

Choose Copy database files via staging areas.
![2](https://user-images.githubusercontent.com/61746700/159166983-ef56fff3-aca5-432b-9b76-75e389de263e.png)

Received a message that it is impossible to clone while the data files of the tablespaces are OFFLINE.
![3](https://user-images.githubusercontent.com/61746700/159167009-92914676-76b6-4e95-9461-b5eff8f17ff0.png)

Let's see which files have this status.

![4](https://user-images.githubusercontent.com/61746700/159167128-411475f4-75b6-44ba-b9a2-324a86a4210d.png)

Let's switch this file to ONLINE mode.

![5](https://user-images.githubusercontent.com/61746700/159167130-d1c05746-93e2-41f0-a49d-5bcb4c90a570.png)

![6](https://user-images.githubusercontent.com/61746700/159167137-f061c000-f331-44b9-b636-31f15ead6daa.png)

Cloning can now be performed.

<img width="513" alt="7" src="https://user-images.githubusercontent.com/61746700/159168068-20931dbd-313d-4152-931d-66a429719499.png">

Set the name of the database clone and the instance – *neworcl*.

<img width="387" alt="8" src="https://user-images.githubusercontent.com/61746700/159168129-4c94f8ba-c3f6-4920-8eb5-64aa9b699724.png">

<img width="416" alt="9" src="https://user-images.githubusercontent.com/61746700/159168192-9adda738-2ef9-423e-af5e-2635fd3d67b7.png">

Set passwords for SYS, SYSMAN, DBSNMP. Leave the other parameters as default.
![10](https://user-images.githubusercontent.com/61746700/159167304-ab50a50f-10ee-4699-b823-ffb8150f9cde.png)

The clone was successfully created.
![12](https://user-images.githubusercontent.com/61746700/159167343-88248b07-9e7c-42ed-8e1e-45dfa1c51561.png)

Let's add the clone information to tnsnames.ora.
Let's check that the clone is working.

![14](https://user-images.githubusercontent.com/61746700/159167428-b1ae7ff8-0485-46fb-8a2a-a3532b006708.png)

Let's create tables TAB1 and TAB2.

![15](https://user-images.githubusercontent.com/61746700/159167467-050ba184-9410-4d3c-8b4e-a6dedc93bfc7.png)

![16](https://user-images.githubusercontent.com/61746700/159167468-23e6acc8-0691-4d67-90cf-72355da66f79.png)

Make a backup and find out the current SCN.

![17](https://user-images.githubusercontent.com/61746700/159167480-af7160c7-49ef-466d-a0af-75efb4381462.png)

![18](https://user-images.githubusercontent.com/61746700/159167481-fe68dc09-0d6b-4365-8169-df8660933bfa.png)

Let's establish a relationship between the tables: TAB1 - parent, TAB2 - child.

![19](https://user-images.githubusercontent.com/61746700/159167591-6af9bcb9-70c0-4343-8672-ae44dd01bca6.png)

Let's insert the data into TAB1, then into TAB2.

![20](https://user-images.githubusercontent.com/61746700/159167608-efd1718a-5c5c-4b46-9f58-54534b6f138d.png)

![21](https://user-images.githubusercontent.com/61746700/159167611-a2ed8d96-bcee-438d-94a7-c302ff0128ab.png)

Now backup the clone again and check the SCN.

![22](https://user-images.githubusercontent.com/61746700/159167644-e996206c-cf18-47ad-840b-88a9d639fd19.png)

![23](https://user-images.githubusercontent.com/61746700/159167646-8226d0ca-d041-42dc-8f95-83ef69f64ba8.png)

Let's do a check of the tables.

![24](https://user-images.githubusercontent.com/61746700/159167689-03c11d22-face-4e5f-9b7e-44ad090070dd.png)

Let's open the database in MOUNT mode.

![25](https://user-images.githubusercontent.com/61746700/159167710-6ce243f8-127c-4229-84da-61c96ff9ccb7.png)

Restore a database clone at a time when the relationship between the tables has not yet been created.

![26](https://user-images.githubusercontent.com/61746700/159167733-1202b743-d414-43a5-a944-b9c42c8d46af.png)

Let's open the database with the RESETLOGS option. And check that there is no data in the tables.

![27](https://user-images.githubusercontent.com/61746700/159167797-ff923a7a-67a4-4cee-9ee4-1a77bcef4723.png)

![28](https://user-images.githubusercontent.com/61746700/159167810-f4d3c41b-9539-4776-9e7d-d8547d5a23fd.png)

The insertion into the TAB2 child table was successful, which means there are no relationships between TAB2 and TAB1.
![29](https://user-images.githubusercontent.com/61746700/159167812-c972c712-fd56-4a91-b5f0-c60372f4f022.png)

Sources:
http://www.dba-oracle.com/t_rman_68_incomplete_recovery.htm
