## Task
There is an *employees* table in the student database. Transfer data from the *employees* table to the *employees2* table in the *ODMT* database, while the new table should contain information about employees who receive salary of more than $ 10,000 and whose surnames begin with the letters A-M.

## Solution
Let's see which rows satisfy the condition of the task.

![1](https://user-images.githubusercontent.com/61746700/159160579-009535ac-76b7-441a-8470-285e31e92dbb.png)

Let's create directories in the *Student4* database and the *ODMT* database.

![2](https://user-images.githubusercontent.com/61746700/159160607-da69ebd2-e293-4f13-b6d4-d570d6becea5.png)

![3](https://user-images.githubusercontent.com/61746700/159160608-82304974-e860-4e6d-b31e-b97ad3be0d55.png)

In the ODMT database create the *hr_test* tablespace, the *hr_test_role* role, grant this role the necessary privileges and create the *hr_test* user, assigning him the created role. And give this user the privilege of reading, writing to the directory created earlier.

![4](https://user-images.githubusercontent.com/61746700/159160671-00ff3eae-444b-4b22-9456-bd28f080e342.png)

Let's create an *employees2* table in the *hr_test* schema, with the same structure as the employees table in the *hr* schema. And execute TRUNCATE command to clear it of data.

![5](https://user-images.githubusercontent.com/61746700/159160711-cf563178-2279-47a1-9995-db2052170639.png)

Now you can create an external table in the *Student4* database, specifying the necessary conditions for data sampling.

![6](https://user-images.githubusercontent.com/61746700/159160745-1405ab54-c620-48bc-b65f-7bb1564b14e2.png)

Next, create an external table in the *ODMT* database.

![7](https://user-images.githubusercontent.com/61746700/159160759-dacd2c56-e2fb-4666-b130-0a9de7123600.png)

Now you can insert data into *employees2* from an external table.

![8](https://user-images.githubusercontent.com/61746700/159160775-ae230c47-22e9-45af-b439-85954bff102d.png)

Let's check that the necessary data has been imported.

![9](https://user-images.githubusercontent.com/61746700/159160781-7b770f68-4307-4b59-80a5-6e567f547b06.png)


