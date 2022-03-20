## Task
Create a backup copy of the metadata on the disks of the disk group, create a backup copy of the data from these ASM disks. Delete disks. Restore disks by metadata and then restore data from a backup.

## Solution
Open cmd, set sid to +asm and enter SQL Plus.

![1](https://user-images.githubusercontent.com/61746700/159161938-2afa3365-5223-41b8-b286-07679ef25b9e.png)

Connect as sysasm (sysdba will not work). Replace the compatibility versions for rdbms and asm. Otherwise, there will be an error in the future when restoring metadata.

![2](https://user-images.githubusercontent.com/61746700/159161986-38939888-9415-4e96-8ba7-de3486b16c61.png)

![3](https://user-images.githubusercontent.com/61746700/159161988-72a58afe-48f8-440d-a34d-026c481a3d57.png)

The error looks like this.

![5](https://user-images.githubusercontent.com/61746700/159162179-850446d2-8d04-4a6b-a7f1-86fe513cdf2d.png)

Open the file.

<img width="270" alt="4" src="https://user-images.githubusercontent.com/61746700/159162766-2c830280-01a5-4c37-9941-269adb68a44f.png">

Now let's make a backup copy of the metadata for the DATA disk group.

![6](https://user-images.githubusercontent.com/61746700/159162220-c0a74f16-4c10-427b-8e4d-8a07583f6081.png)

And create a backup copy of the data.

![7](https://user-images.githubusercontent.com/61746700/159162249-70f27639-32ec-4366-9a84-69edf8157321.png)

Dismount the DATA disk group.

![8](https://user-images.githubusercontent.com/61746700/159162259-61ec70ef-2017-4c5f-a520-0800d51b48b3.png)

And delete this group.

![9](https://user-images.githubusercontent.com/61746700/159162331-b16d93ae-bd84-401d-8d83-f0060796bdc9.png)

In both cases, force is required, otherwise there will be the following errors:

![10](https://user-images.githubusercontent.com/61746700/159162344-e0d75106-e635-46fa-931a-bb122dd5901c.png)

Let's restore the disks using metadata.

![11](https://user-images.githubusercontent.com/61746700/159162355-cdff17bf-f73e-4379-99da-949ed693eca4.png)

Let's restore the data from the backup. Write *controlfile*, because only SPFILE or control file can be restored from AUTOBACKUP.

![12](https://user-images.githubusercontent.com/61746700/159162460-db2def60-9e6d-485b-a34b-7098d50c78db.png)
