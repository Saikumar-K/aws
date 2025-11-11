Task 5 → Enable Billing Access for an IAM User

	task5.1 Observe that AdminUser (Task-4 User) does not have billing access by default.
	task5.2 Enable billing access for AdminUser.
	task5.3 Do R&D and enable billing access for IAM user.
		Note: Billing access requires additional configuration at the account level.
------------------------------------------------------------------------------------------------------------------------
	task5.1 Observe that AdminUser (Task-4 User) does not have billing access by default.
	Done, in the task4 last screenshots confirmed that Access is Denied. Do not have access.

	task5.2 Enable billing access for AdminUser.
	task5.3 Do R&D and enable billing access for IAM user.
	Logged in as root User and Go to Account -> IAM user and role access to Billing information -> check the "Activate IAM Access"
<img width="956" height="233" alt="image" src="https://github.com/user-attachments/assets/cbe08423-30f7-49e3-8d5a-d17f63f7c84f" />
<img width="976" height="153" alt="image" src="https://github.com/user-attachments/assets/9c3590c9-013e-4096-9f05-697112823aea" />

## Note: Billing access requires additional configuration at the account level. this can be done using root user login.
	Now checking back with AdminUser now and verified that information is accessed and shown properly to user as well:
<img width="948" height="416" alt="image" src="https://github.com/user-attachments/assets/1861c799-9555-4b16-b630-4d029cf8deaa" />
<img width="940" height="395" alt="image" src="https://github.com/user-attachments/assets/c6a1ebc7-d8cd-42d1-9f71-a7e41c1239eb" />



