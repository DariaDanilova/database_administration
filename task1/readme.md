## Task
Now there are two control files, make it so that there are three control files. Place it in oradata/student/mycontrolfiles folder.

## Solution
The third file will be a complete copy of the other files. So, in fact, you need to do multiplexing, that is, duplication of files.
Let's see the location of the current control files.

![1](https://user-images.githubusercontent.com/61746700/159139755-27f2dc73-62cf-4f0d-9de4-c379c7eafd4a.png)

Now we need to change the CONTROL_FILES parameter in the initialization parameters file, so add the name of the third file.

![2](https://user-images.githubusercontent.com/61746700/159139761-2b836116-6757-4bea-8970-1200ac40ec33.png)

Let's look at the control files in the V$PARAMETER view, nothing should change.

![3](https://user-images.githubusercontent.com/61746700/159139765-bc3b4f96-cc09-45cd-a0ec-3ab50a216095.png)

Next, before copying, you need to shutdown the database to disable all possible transactions and user sessions to ensure that the control files do not change during copying.

![4](https://user-images.githubusercontent.com/61746700/159139771-294380b3-96da-4704-8821-466c13995d44.png)

Now you can copy the file and put it in the required directory. Then you need to rename it. In Oracle, a special naming system is set for control files: controln.ctl, where n is the number of the control file.
So it will be control03.ctl.

![5](https://user-images.githubusercontent.com/61746700/159139774-b19d0668-5cda-4c57-863f-c316085ff216.png)

Now you can start the database.

![6](https://user-images.githubusercontent.com/61746700/159139777-815ca1ae-6f81-405f-8d37-3cf12f3a18c4.png)

Let's check that the third file is really interpret.

![7](https://user-images.githubusercontent.com/61746700/159139779-b24a7d80-5e30-4674-938f-76634ba3b7a8.png)

![8](https://user-images.githubusercontent.com/61746700/159139785-11b5c75a-046a-4240-9581-b1167df27c10.png)

Now let's create pfile from spfile.

![9](https://user-images.githubusercontent.com/61746700/159139788-da77f1cb-6187-4029-9a18-73769d3cd231.png)

Look, the file has appeared.

![10](https://user-images.githubusercontent.com/61746700/159139790-bb565d1b-4a0d-40d0-aa41-5f54e65a0905.png)
