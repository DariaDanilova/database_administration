## Task
Use DBNEWID to change the database name, not DBID. Write the progress to the utility's log file. Check the performance of the databases.

## Solution
First, make a backup copy of the database.

Then add the connection of the Student database to the Listener to Net Manager so that there are no errors in SQL Plus when executing the startup and startup mount commands.

![3](https://user-images.githubusercontent.com/61746700/159163532-ff3b4fc3-0258-4c32-85df-82e181dce9bd.png)

![4](https://user-images.githubusercontent.com/61746700/159163538-8846ceb5-c042-4845-b992-34843cbdd96b.png)

Now stop the database and run it in startup mount mode.

![5](https://user-images.githubusercontent.com/61746700/159163575-f9996848-4653-4069-9af1-c71c898baf8d.png)

Change the database name.

![6](https://user-images.githubusercontent.com/61746700/159163595-523a9071-f384-4688-bdc9-c0f5224745d8.png)

Update the DB_NAME in SPFILE to a new name.

Create a new password file and SPFILE.


Due to the fact that an error occurs when connecting to the database, you need to delete the old instance and create a new one.

Add the required information to the Net Manager.

Now in tnsnames.ora change the old name to the new one.

Restart listener.

Start the database with new name.

Check that the instance is what you expected. And you see that the requests are being executed.

Let's check that the DBID has not changed.
