Task 8 → Fine-Grained Permissions for S3

	task8.1 Create an IAM user named S3RestrictedUser.
	task8.2 Attach a customer-managed policy to allow:
		Access to only a specific S3 bucket (e.g., Yourname-24-12-2024).
		Allow Only GetObject, ListBucket, and ListAllMyBuckets actions from the Policy.
	task8.3 Log in as S3RestrictedUser and verify:
		Attempt to access other buckets results in access denied.
		Downloading/uploading files from my-restricted-bucket is allowed.
------------------------------------------------------------------------------------------------------------------------

---

ask8.1 Created an IAM user named S3RestrictedUser.
	task8.2 Attached customer-managed policy ="S3RestrictedUserAccess", 

<img width="948" height="325" alt="image" src="https://github.com/user-attachments/assets/a76f6caa-0c79-4ec6-8913-229ead722bce" />
<img width="952" height="413" alt="image" src="https://github.com/user-attachments/assets/e163db21-5306-4a6b-be53-e5f4d1fc3d2c" />
<img width="945" height="421" alt="image" src="https://github.com/user-attachments/assets/af21dbce-43dc-4198-b3d5-84d2e471b425" />

---

Veryfying that=> Access to only a specific S3 bucket (my-restricted-bucket).
for otherBuckets, No Access
<img width="940" height="392" alt="image" src="https://github.com/user-attachments/assets/d7a0ada6-3740-45e0-837e-228f010ebfde" />
for the sepcific bucket: my-restricted-bucket-for-s3restricted-user, Access provided
<img width="932" height="377" alt="image" src="https://github.com/user-attachments/assets/de0d927a-0759-4db5-af11-63e551f7fddc" />

---

Veryfying that=> Allow Only GetObject, ListBucket, and ListAllMyBuckets actions from the Policy.
not able to upload, Error saying that permission denied
<img width="940" height="442" alt="image" src="https://github.com/user-attachments/assets/f2fa36b0-f839-464d-a3b6-3a4ca796066c" />

---
Able to ListAllMyBuckets
<img width="960" height="399" alt="image" src="https://github.com/user-attachments/assets/82dbe69d-75fd-41c1-a87d-a1cb17b6c095" />

---

Able to GetObject
<img width="967" height="458" alt="image" src="https://github.com/user-attachments/assets/082cbbac-ab52-44e3-8f1b-4abb80917df1" />

---
