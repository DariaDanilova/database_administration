## Task
1. Create an ODM database with dictionary-managed tablespaces. Provide sample schemas.
2. Using EM, create a dictionary-managed TSD tablespace with two files with increasing extents. When creating, use AMD technology.
3. Display information about the types of management and characteristics of tablespaces.
4. Move the EMPLOYEES and DEPARTMENTS tables with relationships between them to the TSD tablespace.
5. Convert the EXAMPLES tablespace to a locally managed tablespace.
6. Create a locally managed TSL tablespace with a fixed file size (100 M) with the LOCATIONS table.
7. Convert the TSL tablespace into a dictionary-managed tablespace.

## Solution
1) Create a table space controlled by a dictionary. Select Custom Database, because if you select a template with data files, you will not be able to change the properties of table spaces. This means that they will be created locally managed. And it is impossible to make locally managed tablespaces dictionary-managed, and the reverse transition is possible.

![1](https://user-images.githubusercontent.com/61746700/159139280-e6e89901-da1c-4dec-abc6-18815127adc8.png)

![2](https://user-images.githubusercontent.com/61746700/159139292-f25d4583-f270-436c-a604-6facaf8d1e76.png)

Select OMF, you will need it for further work.

![3](https://user-images.githubusercontent.com/61746700/159139299-4b0f072d-7ba0-49af-84ff-b899d526e533.png)

You will not be able to check the box to create sample schemas, this option is not available.

![4](https://user-images.githubusercontent.com/61746700/159139302-c66dd4fe-77f6-4a8a-8c2e-f95af514b4bc.png)

Now, for each tablespace, select “dictionary-managed". This option is not available for the Undo tablespace.

![5](https://user-images.githubusercontent.com/61746700/159139305-f5443a35-f219-46ea-82fb-aa719df43e27.png)

Adding a tablespace, we get:

![6](https://user-images.githubusercontent.com/61746700/159139310-2baeac2f-459c-46ec-955b-0c8f50bd1cd5.png)

![7](https://user-images.githubusercontent.com/61746700/159139313-95518707-c5ea-42c8-85f5-1a90fa320dc3.png)

Now let's add the HR schema and all its tables.

![8](https://user-images.githubusercontent.com/61746700/159139317-a64e0cbf-b828-4a25-ba01-0fa16d69021d.png)

![9](https://user-images.githubusercontent.com/61746700/159139323-b4d2b91c-d60f-4804-b997-cf8c8d9893bb.png)

2) Let's create a TSD dictionary-managed tablespace.
When creating data files, we check the auto extensibility box and do not specify anything in the filename, OMF will create the name itself.

![10](https://user-images.githubusercontent.com/61746700/159139223-c655cbac-eac0-4149-bab5-01de84320522.png)

We get:![11](https://user-images.githubusercontent.com/61746700/159139205-6fdb72e9-9b1b-4732-b036-0b8665f1a148.png)

3)	Let's look at the types of management and characteristics of tablespaces.
![12](https://user-images.githubusercontent.com/61746700/159139253-34148ac9-6649-4dfa-b58a-815a95de1826.png)

We can output this information to SQL Plus.

![13](https://user-images.githubusercontent.com/61746700/159139265-74e8cb70-e1af-4be3-a8a3-f70b70276115.png)

![14](https://user-images.githubusercontent.com/61746700/159139269-4f6f2b00-6ab6-41ee-b3cd-fd587ac934f8.png)

4) Move the employees and departments tables, as well as the relationships between them, to the TSD tablespace.
Go to the Schema >Database Objects > Tables tab. First, let's look at the constraints and indexes of the employees table.

![15](https://user-images.githubusercontent.com/61746700/159139380-22b9c11c-d6d1-4e35-ba2a-7aefe2e53b36.png)

Now let's look at the constraints and indexes of the departments table.
![16](https://user-images.githubusercontent.com/61746700/159139388-3d0143fb-d866-44aa-a4ca-c73a2e7a8692.png)

Select the desired table, select Reorganize and click Go.

![17](https://user-images.githubusercontent.com/61746700/159139399-9e8a3a65-61ff-473f-989b-58f73d4f75d4.png)

We get here and click on the table.
![18](https://user-images.githubusercontent.com/61746700/159139406-08d5a3fb-4481-4e16-880f-0f26432e9b79.png)

Select Relocate and enter the name TSD.
![19](https://user-images.githubusercontent.com/61746700/159139414-09eb5dee-e644-48d2-940e-0fa1990128a4.png)

We get
![20](https://user-images.githubusercontent.com/61746700/159139423-5233c555-5b1c-4427-bdec-26c574189180.png)

Further actions are left by default and we get the following script.

![21](https://user-images.githubusercontent.com/61746700/159139429-afdbc1d0-0a82-4ffd-b95e-dbc2698ba47e.png)

Let's do the same for the employees table.
![22](https://user-images.githubusercontent.com/61746700/159139449-892b0cd2-e200-4f7c-a64e-0e97a1908717.png)
![23](https://user-images.githubusercontent.com/61746700/159139450-15ab9dcb-938d-48b0-9bda-9405ecb8275c.png)
![24](https://user-images.githubusercontent.com/61746700/159139451-a6ea8126-98aa-4ff9-9346-12001d86a034.png)
![25](https://user-images.githubusercontent.com/61746700/159139452-49645869-c1af-4594-8ee7-7c73d07fee76.png)

Check that everything has moved.

![26](https://user-images.githubusercontent.com/61746700/159139483-ff3f8f46-5cd0-41c9-915e-e8529002e5f1.png)
![27](https://user-images.githubusercontent.com/61746700/159139484-decd1046-3532-477d-8e59-3a6ad6352080.png)
![28](https://user-images.githubusercontent.com/61746700/159139486-c2359261-cb49-4537-8fbe-13dc0150ca9f.png)

Let's double-check that everything works.

![29](https://user-images.githubusercontent.com/61746700/159139494-e76eda10-0401-4ebc-8f0c-25ade606004c.png)

5) Convert the EXAMPLE tablespace to a locally managed one.
These changes cannot be made in EM, only with the help of a special package procedure DBMS_SPACE_ADMIN.TABLESPACE_MIGRATE_TO_LOCAL.

![30](https://user-images.githubusercontent.com/61746700/159139525-4c6a1d47-0f4d-4752-8441-2ccaf3b84594.png)

![31](https://user-images.githubusercontent.com/61746700/159139526-fe5edbff-3333-4ad2-aea4-3546fa357fe4.png)

6) Create a TSL tablespace with a fixed file size.
The Auto Extend column will have NO.

![32](https://user-images.githubusercontent.com/61746700/159139564-8b39ae91-4c43-4122-ad98-9d0df97cd43c.png)

Now let's create a LOCATIONS table in this tablespace.
![33](https://user-images.githubusercontent.com/61746700/159139577-a2a180db-6a88-44cb-9c94-a8d2bdd9df66.png)

7) Now let's transform the TSL tablespace into a dictionary-managed one.
To do this, use DBMS_SPACE_ADMIN.TABLESPACE_MIGRATE_FROM_LOCAL.

![34](https://user-images.githubusercontent.com/61746700/159139594-9f4b1795-d77c-4709-af69-d710a7d75f76.png)

Let's double-check.

![35](https://user-images.githubusercontent.com/61746700/159139600-991ba8d9-5183-4a6a-8915-c802e73a7153.png)

As a result , we get:

![36](https://user-images.githubusercontent.com/61746700/159139614-3b2acdc6-b2ce-4510-9cb0-4f283b0f9409.png)
