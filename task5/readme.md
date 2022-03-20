## Task
Perform a Flashback Transaction Backout of three transactions with WAW dependencies using the *dbms_flashback* package without using Enterprise Manager.

## Solution

To perform a Flashback Transaction, archiving mode must be enabled, and the following presets must be performed:

![1](https://user-images.githubusercontent.com/61746700/159161431-9657b791-14e6-4e60-a03f-71a6060851c0.png)

Log in as dba1 and insert a row into the *departments* table.

![2](https://user-images.githubusercontent.com/61746700/159161435-bd8bc022-7a70-4d6f-962b-3db8f5fd5b7f.png)

As the main transaction, we will change the value of department 280.

![3](https://user-images.githubusercontent.com/61746700/159161457-cc264e55-1b3e-4d62-b359-431cb6655ffb.png)

As dependent WAW transactions, we will perform changes to the 280-th department.

![4](https://user-images.githubusercontent.com/61746700/159161499-8f70a1b9-2657-4b68-82f5-397c0cc3072a.png)

Let's check that everything is output correctly.

![5](https://user-images.githubusercontent.com/61746700/159161515-0e78f18b-bee2-4140-af16-e433906efa4b.png)

Let's make a switch of archive logs, otherwise we won't be able to make a Flashback Transaction.

![6](https://user-images.githubusercontent.com/61746700/159161530-353ec50a-ba69-4bea-88d6-e4b42d069fa6.png)

Now let's look at the transaction numbers:

![7](https://user-images.githubusercontent.com/61746700/159161540-2be90955-5ec1-4a33-ae40-b408d3e5ced3.png)

Now we will perform a flashback of the first dependant  transaction with the cascade option, the rest, thus, will also be canceled. Let's see that, indeed, we have returned to the expected information.

![8](https://user-images.githubusercontent.com/61746700/159161598-b37ed343-b8e3-4635-a7ce-50bc2dd1d977.png)

The previous transaction needs to be committed, and you can drop the presets to clear the environment.
