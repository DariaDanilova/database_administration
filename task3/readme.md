## Task
Organize an audit of the sys user, which allows you to control the execution of DDL operations. Test the operation of the system when executing various commands by different users with sysdba and sysoper privileges.

## Solution

To begin with, let's look at the values of the audit_sys_operations, audit_file_dest and audit_trail parameters.

![1](https://user-images.githubusercontent.com/61746700/159139931-6b961b3d-3e30-4f62-beee-438c647ce27d.png)

To enable auditing for privileged users, set audit_sys_operations to TRUE, change the value of audit_trail, because in this case, the audit information must be stored outside the database (create a folder in the directory in advance), and accordingly set audit_file_dest to XML, not DB.

![2](https://user-images.githubusercontent.com/61746700/159139968-1c34c24e-5120-4488-a54e-e4ba9b28db73.png)

Now restart the database.

![3](https://user-images.githubusercontent.com/61746700/159139976-f7731e6d-5b02-49d7-a5c0-cccd0e8010df.png)

Let's check that the parameter changes have been applied.

![4](https://user-images.githubusercontent.com/61746700/159139996-89ef9eee-5598-482e-a010-0b9136537d2b.png)

Let's look at the list of all users who have been granted the SYSDBA or SYSOPER privilege.

![5](https://user-images.githubusercontent.com/61746700/159140013-df7290da-989e-4a12-9785-4fa17d802ad8.png)

Let's connect with the sysoper privilege and execute the DDL command. This command will fail, because sysoper only serves to connect/disconnect from the database, so everything is correct.

![6](https://user-images.githubusercontent.com/61746700/159140046-405ddca5-e8bc-4ab3-8b99-0d09bc625793.png)

Information about the execution of this command got into the audit log.


Now let's connect as dba1 without the sysdba privilege. The command will be executed, but there will be no information about the command in the xml file, because dba1  in this case does not have privileges of privileged users. So the result is also correct.

![8](https://user-images.githubusercontent.com/61746700/159140130-46324ca0-5bbb-439b-83e8-f0270f6eecd0.png)

Next, let's conncet with the sysdba privilege, everything is fixed correctly.

![10](https://user-images.githubusercontent.com/61746700/159140155-3b9d357c-9748-4d39-a657-ba510fd85c1f.png)

<img width="257" alt="11" src="https://user-images.githubusercontent.com/61746700/159140272-1dc0dcf6-b821-45c4-b2db-ef2900dcd9c1.png">

And even if the command is incorrect (for example, the wrong scheme is specified), the information will still get into the log.
