# OCI-object-storage-mount-guide
The process of mounting Object Storage for use as file storage.

## Steps
1. Verify information to access object storage.

2. Install the tool (s3fs-fuse) for mounting and register environment variables.

3. Mount the object storage.

4. Add a ZDM repository.

---

### Step 1.
1.	Generate an access-key and secret-key to access object storage.

    ![user.png](/images/user.png)

2.	Click the Generate Secret Key button to generate the secret-key and access-key.

    ![user.png](/images/create_secretkey.png)

    Save the printed secret key and access key.

3.	Create an OCI bucket.

4.	Save the namespace value for the bucket.

    ![namespace.png](/images/namespace.png)

5.	Verify and save the OCI object storage endpoint. here is [endpoint list](https://docs.oracle.com/en-us/iaas/api/#/en/s3objectstorage/).

### Step 2.
Install s3fs-fuse, a tool for mounting object storage, and register environment variables.

1.	Install s3fs-fuse on the ZDM server with the command below.
    ```
    apt install -y s3fs
    ```

2.	Save the secret key and access key values to the .passwd-s3fs file.
    ```
    echo <Access key>:<Secret key> > .passwd-s3fs
    ```

### Step 3.

1.	Mount to the repository with the command below.
    ```
    s3fs <BUCKET_NAME> <MOUNT_PATH> -o passwd_file=<PASSWORD_FILE_PATH> -o url=https://<BUCKET_NAMESPACE>.compat.objectstorage.<REGION>.oraclecloud.com -o allow_other -o use_path_request_style -o nomultipart -o endpoint=<REGION>
    ```

### Step 4.
1.	Modify the ***`/etc/samba/smb.conf`*** file to share the mounted folder.

2.	Register the repository in the ZDM portal.
    
    a.	***Access the ZDM portal, and click the Management-ZDM tab.***
        ![zdm.png](/images/zdm.png)

    b.	***Select the ZDM where you want to register the repository.***
        ![select.png](/images/select.png)

    c.	***Click the Add Repository button.***
        ![add_repository.png](/images/add_repository.png)

    d.	***After entering the information according to the given form, click the Add button to register the repository.***
    <p align="center">
        <img src="./images/register_repository.png" alt="register_repository"/>
    </p>
