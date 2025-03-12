# Practicing with Amazon EFS (Elastic File System)

![](assets/Apache.png)

## Overview
This guide walks through setting up and mounting an **Amazon EFS** on two EC2 instances.

## Steps

### 1. Launch Two EC2 Instances  
- Create and launch **two EC2 instances** within the same **Availability Zone (AZ)** and **VPC**.  
- Ensure both instances have **NFS access** allowed in their **Security Groups** (Port `2049`).  

### 2. Install NFS Client  
Run the following command on both EC2 instances to install the **NFS client**:  
```sh
sudo apt update && sudo apt install -y nfs-common
```

### 3. Mount EFS on the First EC2 Instance  
Run the following command to mount **EFS** to a directory:  
```sh
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 10.0.2.235:/ efs
```

### 4. Create a Folder and a Test File  
After mounting, create a test directory and file on the first instance:  
```sh
mkdir efs_test  
echo "Hello, World!" > efs_test/efs.txt  
```

### 5. Mount EFS on the Second EC2 Instance  
- Access the second EC2 instance.  
- Create the same **mount directory** and mount the **EFS**:  
```sh
mkdir efs_test  
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 10.0.2.235:/ efs_test
```

### 6. Verify Shared Access  
Check if the `efs.txt` file created on the first instance is visible on the second instance:  
```sh
ls efs_test  
cat efs_test/efs.txt  
```
If successful, you should see the text:  
```sh
Hello, World!
```

## Expected Result  
Both EC2 instances should be able to read and write to the **same EFS storage**, demonstrating **shared file system access**.

![](assets/Apache.png)
![](assets/Apache.png)

---
✅ **Success!** You have successfully set up and mounted **Amazon EFS** on multiple EC2 instances. 🚀  

