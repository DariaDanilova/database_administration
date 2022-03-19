## Task
Now there are two control files, make it so that there are three control files. Place it in oradata/student/mycontrolfiles folder.

## Solution
The third file will be a complete copy of the other files. So, in fact, you need to do multiplexing, that is, duplication of files.
Let's see the location of the current control files.

![image1](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/1.png)

Now we need to change the CONTROL_FILES parameter in the initialization parameters file, so add the name of the third file.

![image2](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/2.png)

Let's look at the control files in the V$PARAMETER view, nothing should change.

![image3](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/3.png)

Next, before copying, you need to shutdown the database to disable all possible transactions and user sessions to ensure that the control files do not change during copying.

![image4](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/4.png)

Now you can copy the file and put it in the required directory. Then you need to rename it. In Oracle, a special naming system is set for control files: controln.ctl, where n is the number of the control file.
So it will be control03.ctl.

![image5](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/5.png)

Now you can start the database.

![image6](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/6.png)

Let's check that the third file is really interpret.

![image7](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/7.png)

![image8](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/8.png)

Now let's create pfile from spfile.

![image9](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/9.png)

Look, the file has appeared.

![image10](https://github.com/DariaDanilova/database_administration/blob/main/task1/images/10.png)
