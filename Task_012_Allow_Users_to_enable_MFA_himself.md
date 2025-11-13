Task 12 → Allow Users to enable MFA himself

	task12.1 Create a policy to allow an IAM user to enable MFA in your AWS account.

	task12.2 Test the behavior:
		Create an IAM user with Name MFA-Task attach Just S3FullAccess policy,
		login and try to enable MFA from "Security Credentials" option.
		
		Switch to root/IAM user who has permissions on IAM service.
		Create a Policy to "enable/disable/resync MFA" For all resources and attach to MFA-Task user.
		Switch to MFA-Task user, verify if the MFA-Task user can enable/disable/sync MFA after the policy is attached.
------------------------------------------------------------------------------------------------------------------------

Here’s how you can perform it, step by step 👇

---

### 🎯 **Task 12: Allow Users to Enable MFA Themselves**

**Objective:**
Allow an IAM user to enable, disable, or resync MFA devices in your AWS account.

---

### 🧩 **Step-by-Step Process**

#### **1️⃣ Create the IAM user**

* Go to **IAM → Users → Add Users**
* Name the user: `MFA-Task`
* Give **AWS Management Console Access**
* Attach **AmazonS3FullAccess** policy (as per task requirement).
* Complete creation.

Now log in as the `MFA-Task` user and try to enable MFA from:
**My Security Credentials → Assign MFA device.**
You’ll notice it **fails**, because the user doesn’t have IAM permissions yet — that’s expected.

---

#### **2️⃣ Create the MFA Management Policy**

Log in as **root** or an **IAM admin** user and create a new policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iam:EnableMFADevice",
        "iam:DeactivateMFADevice",
        "iam:ResyncMFADevice",
        "iam:ListMFADevices",
        "iam:ListVirtualMFADevices",
        "iam:CreateVirtualMFADevice",
        "iam:DeleteVirtualMFADevice"
      ],
      "Resource": "*"
    }
  ]
}
```

Save it with the name: **`MFA-ManagePolicy`**

---

#### **3️⃣ Attach the Policy**

Attach the newly created **MFA-ManagePolicy** to the `MFA-Task` user in addition to the existing **S3FullAccess** policy.

---

#### **4️⃣ Verify**

* Log back in as the **MFA-Task** user.
* Navigate to **My Security Credentials → Assign MFA Device.**
* Now you’ll be able to **enable, disable, or resync MFA** successfully.

---

### ✅ **Expected Outcome**

Before attaching the new policy → MFA setup fails (access denied).
After attaching the policy → `MFA-Task` user can manage their own MFA device.

---

That’s it — this demonstrates how to delegate **self-service MFA management** securely without giving full IAM access.

---
---
---

---

Created an IAM user with Name "MFA-Task" attach Just S3FullAccess policy,
<img width="944" height="438" alt="image" src="https://github.com/user-attachments/assets/5c626335-5bca-43d8-9958-3ffbb79fc1ed" />
<img width="941" height="371" alt="image" src="https://github.com/user-attachments/assets/feb95dfe-9db3-43b7-9996-10474682a802" />

---

Logged in and tried to enable MFA from "Security Credentials", But not Allowed:
<img width="948" height="399" alt="image" src="https://github.com/user-attachments/assets/cd2398e5-59ee-4aa9-bac5-8f61ad5d76e9" />

---

CreatedCustomPolicy for MFA
<img width="644" height="444" alt="image" src="https://github.com/user-attachments/assets/b6506413-70d4-4dcc-816c-0e3811f21641" />

---

attached policy to user:
<img width="943" height="365" alt="image" src="https://github.com/user-attachments/assets/73294c31-ea54-4010-8ae9-bf7d391bcb91" />
<img width="803" height="426" alt="image" src="https://github.com/user-attachments/assets/61d30c54-ec02-4cd6-8716-a5214baa0787" />

---

 Logged in as a MFA-Task user, verified that **MFA-Task** user can enable/disable/sync MFA after the policy is attached
<img width="962" height="346" alt="image" src="https://github.com/user-attachments/assets/0f073ef0-436d-4708-bb28-b63bb3f225c0" />

---

