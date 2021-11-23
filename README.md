# ch-serv-instructions

Things you will need
1. Time
2. A Debit/Credit Card (you won't be paying for anything, it's just needed for creating an account)

Things that will be helpful
1. Some Linux Experience
2. Common Sense

Let's begin.

## Step 1: Create an Oracle Cloud account.
Go to https://www.oracle.com/cloud/free/ and sign up for your account. Keep your username and password in mind.

![image](https://user-images.githubusercontent.com/41555495/142959375-fa1e4dd5-6edc-475d-bd7d-82f30b83971b.png)

## Step 2: Log in to your Oracle Cloud account. 
Go to https://www.oracle.com/cloud/sign-in.html and type in the username you signed up with.

Process through the rest of the options as shown in the screenshots.
![image](https://user-images.githubusercontent.com/41555495/142959583-294cb563-fa1f-4359-88cf-17ffc4c18b83.png)
![image](https://user-images.githubusercontent.com/41555495/142959598-743d4c5d-c68b-4818-893a-122df47245e0.png)
![image](https://user-images.githubusercontent.com/41555495/142959630-6edb665f-b022-41cc-a9d3-d4ac7374cf5c.png)

## Step 3: Once you're at the "Get Started" page, click on "Create a VM Instance".
![image](https://user-images.githubusercontent.com/41555495/142959819-03939954-759c-4567-90f5-7159e792886f.png)

## Step 4: Set the name of your machine at the top.

Possible names would be "chserv" or "clonline" or just whatever you choose. This will be the name of the VM. For the purpose of this tutorial, I will reference the name as "clonline".
![image](https://user-images.githubusercontent.com/41555495/142959939-ad2a8614-0d0f-4125-a0c2-3be0ffc70557.png)

## Step 5: Edit the Image and shape.

Press on the "Edit" button"
![image](https://user-images.githubusercontent.com/41555495/142960009-80cca254-787c-46da-befd-aa6891334362.png)

For the purpose of this tutorial, we will be use Canonical Ubuntu so click on "Change image" on the right side and change the option from Oracle Linux to Canonical Ubuntu. Press "Select Image" once you have it selected.
![image](https://user-images.githubusercontent.com/41555495/142960072-5768c7b5-ec1d-4ee6-ac7c-cf288648294f.png)
![image](https://user-images.githubusercontent.com/41555495/142960116-035b8342-8410-42db-b972-3c9a8de2e813.png)

Press on "Change shape" on the right side.
![image](https://user-images.githubusercontent.com/41555495/142960232-74d3983b-b5d8-46e7-b099-aff5198f1ae5.png)

Change the "Shape series" from Specialy and previous generation to Ampere. Select "VM.Standard.A1.Flex". If you want to dedicate all of your free resources to one VM, set the number of OCPUs to 4 and amount of memory to 24. If you want the bare minimum, I would suggest 1 OCPU and 4gb of memory.
Press "Select shape" at the bottom once you're finished selecting.
![image](https://user-images.githubusercontent.com/41555495/142960552-b356ca34-4151-4db0-8dcc-dac7b5a94e80.png)
(ignore the service limits from the screenshot. this is solely due to me using up all my resources already)

## Step 6: In the "Add SSH keys" section, click on "Save Private Key" and save it to some location where you can access it.
![image](https://user-images.githubusercontent.com/41555495/142960658-a4feab4c-8bc7-41d8-97b3-7dbd0bf0c92a.png)

## Step 7: Press "Create" at the bottom of the page and wait for your machine to be done provisioning.

## OPTIONAL STEP: Creating 

