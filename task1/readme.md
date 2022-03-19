## Task
Now there are two control files, make it so that there are three control files. Place it in oradata/student/mycontrolfiles folder.

## Solution
The third file will be a complete copy of the other files. So, in fact, you need to do multiplexing, that is, duplication of files.
Let's see the location of the current control files.

![image](https://user-images.githubusercontent.com/61746700/159138076-28e9f8d2-a061-411b-a769-6c9a0e421dae.png)

Now we need to change the CONTROL_FILES parameter in the initialization parameters file, so add the name of the third file.

![image](https://user-images.githubusercontent.com/61746700/159138139-cfaaacac-aaef-4807-a10d-4b9667948f5f.png)

Let's look at the control files in the V$PARAMETER view, nothing should change.

![image](https://user-images.githubusercontent.com/61746700/159138151-f4f1cbc0-3322-404c-8d66-33d079c1a71a.png)

Next, before copying, you need to shutdown the database to disable all possible transactions and user sessions to ensure that the control files do not change during copying.

![image](https://user-images.githubusercontent.com/61746700/159138180-ab31cd23-6b38-4707-8b0a-0dde084ea4e6.png)

Now you can copy the file and put it in the required directory. Then you need to rename it. In Oracle, a special naming system is set for control files: controln.ctl, where n is the number of the control file.
So it will be control03.ctl.

![image](https://user-images.githubusercontent.com/61746700/159138206-c97fd9d4-e3ae-4c3c-9606-bfff39d49ad5.png)

Now you can start the database.

![image](https://user-images.githubusercontent.com/61746700/159138215-059441bd-bec4-440e-bdd2-47ceb681fd5b.png)

Let's check that the third file is really interpret.

![image](https://user-images.githubusercontent.com/61746700/159138272-3f0fe1e1-6dfc-46b8-a4ad-906111506ede.png)

![image](https://user-images.githubusercontent.com/61746700/159138275-108a181b-c696-404a-89a8-f204527988ca.png)

Now let's create pfile from spfile.

![image](https://user-images.githubusercontent.com/61746700/159138311-e2b819e8-f838-41aa-88f7-810314756842.png)

Look, the file has appeared.

![image](https://user-images.githubusercontent.com/61746700/159138321-9c3fc9ae-77b9-42f7-b5f3-d8ac6ea43800.png)
