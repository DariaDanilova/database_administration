## Task
Run a TSPITR on the HRTEST tablespace, adding to the RECOVERY SET all existing tablespaces with dependent objects, without removing or disabling the objects from HRTEST. Solve the problem without using EM by means of RMAN. Consider using debug mode and RMAN activity tracing. Analyze the operations performed by RMAN while solving the problem.

## Solution

Perform export.

![image](https://user-images.githubusercontent.com/61746700/165924745-20455b4d-b921-42dd-81e3-b26824c4fab9.png)

Create a new user and a tablespace.

![image](https://user-images.githubusercontent.com/61746700/165924926-ba271b9b-024d-4ba7-8b08-75239bbae2ae.png)

Perform import.

![image](https://user-images.githubusercontent.com/61746700/165924968-84ca3d2c-a171-41fe-b79a-dd58eccf70c0.png)

Determine if there are any dependencies interfering with TSPITR.

![image](https://user-images.githubusercontent.com/61746700/165925060-d44182c8-d581-44a1-b528-5f154136a8ac.png)

Make a backup of the database.

![image](https://user-images.githubusercontent.com/61746700/165925128-2bac5474-a6b9-468a-96dd-9f23b9450341.png)

Look at the current SCN to which will be restored.

![image](https://user-images.githubusercontent.com/61746700/165925359-4c06485a-7969-4f01-b664-1e6ad08eeb3c.png)

Assign a relationship for the tables hrtest.departments (child table) and hr.locations (parent table).

![image](https://user-images.githubusercontent.com/61746700/165925818-4058881a-13c7-4e5b-84b8-b8b7b341f952.png)

Look, there are dependencies that will interfere TSPITR.

![image](https://user-images.githubusercontent.com/61746700/165925946-dd824690-52c1-4ce8-9b0d-042a55f66593.png)

To do this, make export and import.

![image](https://user-images.githubusercontent.com/61746700/165926034-4f5c083c-4139-4cd2-9f11-26614a7b4018.png)

![image](https://user-images.githubusercontent.com/61746700/165926051-b69ecfaf-43ef-4020-a556-110a4b251f23.png)

The dependencies are gone.

![image](https://user-images.githubusercontent.com/61746700/165926122-793c8126-52ac-40de-9ca9-63517ae68c99.png)

Now execute TSPITR by providing a debugging mode and tracing RMAN actions. You also need to create a TSPITR folder in advance.

![image](https://user-images.githubusercontent.com/61746700/165926237-1f6dbf8f-7da4-4889-8c29-d7245991240c.png)

Next, switch HRTEST to online mode and check that there is no connection between the tables.

![image](https://user-images.githubusercontent.com/61746700/165926877-29fa6d9b-6f71-484e-9db7-1dca43e0dfe0.png)

The insertion into the child table of hrtest.departments was successful, which means there is no connection between hrtest.departments and hr.locations.

![image](https://user-images.githubusercontent.com/61746700/165927012-a5563f88-8212-4269-a18f-a113f3bc6880.png)

The contents of the TSPITR folder.

![image](https://user-images.githubusercontent.com/61746700/165927067-73a16c10-e95e-4bbc-aba9-2ca77300ba74.png)

Example of the contents of a trace file.

![image](https://user-images.githubusercontent.com/61746700/165927124-4ad5a83a-45ff-4aa8-9966-e6d0fb3cfbf4.png)

Let's analyze the operations from the debug file performed by RMAN when solving the problem.

First, an automatic instance is created with SID='tspitr', initialization parameters are shown in the image.

![image](https://user-images.githubusercontent.com/61746700/165927231-b57785d9-ef88-46df-824b-e41e9d83012a.png)

An instance is started, and the TRANSPORT_SET_CHECK procedure is run to check whether the set of tablespaces (for migration) is autonomous.

![image](https://user-images.githubusercontent.com/61746700/165927379-a61cecc0-0bfc-4af2-aeca-3baf1ba7c0b2.png)

The Memory script is launched for execution: the table space is restored offline and the control files are restored to the auxiliary instance at the required point in time.

![image](https://user-images.githubusercontent.com/61746700/165933693-bf33fd25-3f1b-4f1e-b5b7-f75b17028724.png)

![image](https://user-images.githubusercontent.com/61746700/165933753-550bcded-8ff7-4e9a-8f87-ede964be2e0f.png)

Restoring the recovered data files to the specified SCN in the auxiliary instance.

![image](https://user-images.githubusercontent.com/61746700/165933883-f31f8cf9-5a19-49ed-8d5f-5d398e18511f.png)

Switching the tablespace to be exported to read only mode. Creating datapump directories for export and import. Performing metadata export and metadata import.

![image](https://user-images.githubusercontent.com/61746700/165933997-859703d4-d599-495d-af57-11c70ce25cda.png)

![image](https://user-images.githubusercontent.com/61746700/165934018-80e05482-f797-437e-8ea6-5bc5f49cf5f9.png)

Switching of the HRTEST tablespace into read write mode and offline mode. And deleting the auxiliary instance.

![image](https://user-images.githubusercontent.com/61746700/165934280-d262ecad-eb23-4e99-9ecb-14d7a3fab421.png)



