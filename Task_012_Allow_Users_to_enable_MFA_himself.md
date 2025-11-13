Task 12 → Allow Users to enable MFA himself

	task12.1 Create a policy to allow an IAM user to enable MFA in your AWS account.

	task12.2 Test the behavior:
		Create an IAM user with Name MFA-Task attach Just S3FullAccess policy,
		login and try to enable MFA from "Security Credentials" option.
		
		Switch to root/IAM user who has permissions on IAM service.
		Create a Policy to "enable/disable/resync MFA" For all resources and attach to MFA-Task user.
		Switch to MFA-Task user, verify if the MFA-Task user can enable/disable/sync MFA after the policy is attached.
------------------------------------------------------------------------------------------------------------------------

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

