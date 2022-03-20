## Task
Use DBNEWID to change the database name, not DBID. Write the progress to the utility's log file. Check the performance of the databases.

## Solution
First, make a backup copy of the database.

![1](https://user-images.githubusercontent.com/61746700/159165356-aff8e2b9-4044-4e75-af36-ff2079b34988.png)

Then add the connection of the Student database to the Listener to Net Manager so that there are no errors in SQL Plus when executing the startup and startup mount commands.

![2](https://user-images.githubusercontent.com/61746700/159165385-cb47afc0-15d9-4e09-a0c3-1e6c20a60d42.JPG)

![3](https://user-images.githubusercontent.com/61746700/159163532-ff3b4fc3-0258-4c32-85df-82e181dce9bd.png)

![4](https://user-images.githubusercontent.com/61746700/159163538-8846ceb5-c042-4845-b992-34843cbdd96b.png)

Now stop the database and run it in startup mount mode.

![5](https://user-images.githubusercontent.com/61746700/159163575-f9996848-4653-4069-9af1-c71c898baf8d.png)

Change the database name.

![6](https://user-images.githubusercontent.com/61746700/159163595-523a9071-f384-4688-bdc9-c0f5224745d8.png)

![7](https://user-images.githubusercontent.com/61746700/159165479-0e80abc6-b40a-4998-9749-edccd6bdd4aa.png)

Update the DB_NAME in SPFILE to a new name.

![8](https://user-images.githubusercontent.com/61746700/159165145-d824527a-12d1-4661-b4de-2fd5dfeeea89.png)

Create a new password file and SPFILE.

![9](https://user-images.githubusercontent.com/61746700/159165160-ac4acf51-6e73-4eaf-be1f-a8f826d4e8e6.png)

![10](https://user-images.githubusercontent.com/61746700/159165162-073ab7d6-2a23-4ab4-8b9a-27810913fb03.png)
![11](https://user-images.githubusercontent.com/61746700/159165163-cb4648db-54ba-4c40-b5de-36a97d730c67.png)

Due to the fact that an error occurs when connecting to the database, you need to delete the old instance and create a new one.
![12](https://user-images.githubusercontent.com/61746700/159165198-d83baad4-031a-4d69-b050-18e4e91fb373.png)
![13](https://user-images.githubusercontent.com/61746700/159165206-8e427dc1-7045-441e-9a26-fdaf71a14329.png)

Add the required information to the Net Manager.

![14](https://user-images.githubusercontent.com/61746700/159165214-78048133-c2f5-41b4-8c58-15956af8ebbe.png)

Now in tnsnames.ora change the old name to the new one.

Restart listener.

Start the database with new name.

![16](https://user-images.githubusercontent.com/61746700/159165279-6b470501-4590-457c-9216-eadec8a77d8f.png)

Check that the instance is what you expected. And you see that the requests are being executed.

![17](https://user-images.githubusercontent.com/61746700/159165288-b589fc03-5e48-44ac-bc82-7cedfe2de5b4.png)

Let's check that the DBID has not changed.

![18](https://user-images.githubusercontent.com/61746700/159165415-3d1ce97c-f4fa-4377-93eb-889f65d9be10.png)

![19](https://user-images.githubusercontent.com/61746700/159165416-b512fd18-eac4-45e6-8c00-7809f09a1556.png)
