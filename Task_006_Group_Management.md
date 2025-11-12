Task 6 → Group Management

	task6.1 Create an IAM group named Developers.
		Attach the AmazonS3ReadOnlyAccess policy to the group.
	task6.2 Add two IAM users (DevUser1 and DevUser2) to the Developers group.
		Log in as DevUser1 and verify:
			Access to view S3 buckets is allowed.
			Attempting to upload a file results in an error due to insufficient permissions.
------------------------------------------------------------------------------------------------------------------------

task6.1 Created an IAM group named Developers by attaching the AmazonS3ReadOnlyAccess policy to the group.
	<img width="914" height="221" alt="image" src="https://github.com/user-attachments/assets/72d79efa-4d5e-416d-8066-c58340631b59" />




Added two IAM users (DevUser1 and DevUser2) to the Developers group.
<img width="938" height="392" alt="image" src="https://github.com/user-attachments/assets/9c352970-5389-4aa4-970f-8429ad9dc298" />
<img width="939" height="376" alt="image" src="https://github.com/user-attachments/assets/91ede783-9d68-461b-8e45-a01845ab80d0" />




Unable to create the bucket with DevUser1 login:
<img width="935" height="399" alt="image" src="https://github.com/user-attachments/assets/11e52de1-0b91-49b0-b01e-70ca8734eb4e" />




Verifying that=> Access to view S3 buckets is allowed:
<img width="966" height="322" alt="image" src="https://github.com/user-attachments/assets/9e1a40b7-66e9-4591-9eda-75677ed1bc29" />




Verifying that=> Attempting to upload a file results in an error due to insufficient permissions
<img width="944" height="408" alt="image" src="https://github.com/user-attachments/assets/eb62642c-d230-4912-ae5b-950a9353876a" />

