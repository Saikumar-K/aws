Task 2 → Create a Basic IAM User and Test Permissions

	task2.1 Create an IAM user with the name S3User and assign the AmazonS3FullAccess managed policy.
	task2.2 Use the AWS Management Console to log in as S3User.
	task2.3 Verify the access:
				Create a new S3 bucket with a unique name.
				Upload a test file to the bucket.
----------------------------------------------------------------------------------------------------------------

---

This one’s all about **IAM users and S3 access** — a foundational AWS skill.

---

### 🎯 **Task 2: Create a Basic IAM User and Test Permissions**

**Objective:**
Create an IAM user with **AmazonS3FullAccess**, and verify access by creating an S3 bucket and uploading a file.

---

### 🧩 **Step-by-Step Implementation**

#### **1️⃣ Log in to your AWS Account (Root or Admin User)**

Use your root account or an IAM admin account.

---

#### **2️⃣ Create an IAM User**

1. Go to **IAM → Users → Add users**
2. Enter username:
   👉 `S3User`
3. Under **Access type**, select:

   * ✅ **AWS Management Console Access**
   * Choose: *I want to create an IAM user for accessing the console*
4. Check **Require user to create a new password at next sign-in** (recommended).
5. Click **Next: Permissions**

---

#### **3️⃣ Assign Permissions**

Now you’ll attach a **managed policy**:

1. Choose → **Attach policies directly**
2. Search for and select ✅ `AmazonS3FullAccess`
3. Click **Next → Create User**

✅ Done — you’ve created an IAM user with full S3 permissions.

---

#### **4️⃣ Log in as S3User**

* Copy the IAM sign-in URL from your root dashboard (it looks like:
  `https://<alias>.signin.aws.amazon.com/console`)
* Log in using:

  * **Username:** `S3User`
  * **Password:** (temporary password from step 2)

When prompted → set a new password.

---

#### **5️⃣ Test the Access**

Now we’ll verify the permissions.

**In the AWS Management Console:**

1. Go to **S3 service**
2. Click **Create Bucket**

   * Enter a unique name: `testbuckett-demo-<yourname>-s3`
   * Choose a region (e.g., `ap-south-1`)
   * Leave defaults → click **Create bucket**
3. Once created → open your bucket
4. Click **Upload → Add Files → Choose any small test file**

   * For example: `sample.txt` or `image.jpg`
   * Click **Upload**

✅ You should see the file successfully uploaded — proving the policy is working.

---

#### **6️⃣ Verify Permissions (Optional)**

Try deleting the object or creating another bucket — everything should work since the user has **full S3 access**.

---

### ✅ **Expected Output**

| Action                                | Expected Result |
| ------------------------------------- | --------------- |
| Create S3 Bucket                      | ✅ Successful    |
| Upload File to Bucket                 | ✅ Successful    |
| View Bucket & Object Details          | ✅ Allowed       |
| Access Other Services (like EC2, IAM) | ❌ Denied        |

---

---

💡 **Quick Trainer Tip:**
Always avoid giving users **AdministratorAccess** unless absolutely required.
Instead, use **service-specific policies** like `AmazonS3FullAccess`, as you did here — that’s the *least privilege principle* in action.

---


---

---
task2.1 Create an IAM user with the name S3User and assign the AmazonS3FullAccess managed policy:
<img width="975" height="426" alt="image" src="https://github.com/user-attachments/assets/2c9213c0-86c5-420c-b678-186827661259" />

<img width="975" height="413" alt="image" src="https://github.com/user-attachments/assets/e3737be2-8dc3-4fee-a778-ad7e6e973895" />

------------------------------------------------------------------------------------------------------------------
task2.2 Use the AWS Management Console to log in as S3User.
task2.2 Use the AWS Management Console to log in as S3User.
	task2.3 Verify the access:
				Create a new S3 bucket with a unique name.
				Upload a test file to the bucket.
<img width="975" height="406" alt="image" src="https://github.com/user-attachments/assets/1f65f76e-9c55-4ac5-8856-8abefcc38539" />
