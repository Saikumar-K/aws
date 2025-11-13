Task 9 → Create a Custom Managed Policy

	task9.1 Create a customer-managed policy named DenyS3Access to deny all actions on S3.
	task9.2 Attach the DenyS3Access policy to AdminUser (Task-4 User).
	task9.3 Log in as AdminUser and test:
		Attempt to create an S3 bucket.
		Note the denied access and share the output.
Note: This demonstrates how explicit deny statements take precedence over allow statements.
------------------------------------------------------------------------------------------------------------------------

---
	task9.1 Created a customer-managed policy named DenyS3Access to deny all actions on S3.
<img width="938" height="464" alt="image" src="https://github.com/user-attachments/assets/d3e57b8c-58f9-4c61-bfd3-71d544e1d40c" />

---

	task9.2 Attached DenyS3Access policy to AdminUser (Task-4 User).
<img width="938" height="440" alt="image" src="https://github.com/user-attachments/assets/536ea983-a349-4b01-86b1-d25419ff268b" />
<img width="942" height="447" alt="image" src="https://github.com/user-attachments/assets/0199ec2a-410b-4f92-8a03-afcf1ba36ec2" />

---

	task9.3 Logged in as AdminUser and Verified as below:
		Attempted to create an S3 bucket. Noted that access is denied and shared the output below.
<img width="953" height="451" alt="image" src="https://github.com/user-attachments/assets/d7e46de0-00a2-45b4-ae4d-36b2683cb20a" />
<img width="932" height="345" alt="image" src="https://github.com/user-attachments/assets/084fcd50-7210-45af-a43f-c710edd08de5" />

---
