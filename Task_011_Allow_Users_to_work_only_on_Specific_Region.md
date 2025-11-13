Task 11 → Allow_Users_to_work_only_on_Specific_Region

	task11.1 Create a policy to allow an IAM user to perform all operations on S3 service, but limited to a specific region.
	task11.2 Test the behavior:
		Create an IAM policy (name: region-limit) that allows all operations on S3, but add a condition RequestedRegion with ap-south-1
		Create an IAM user with Name Region-Task, attach region-limit policy, 
			--login and try to create a bucket by selecting Region as "Hyderabad". Observe the output. 
			--This should not allow to create a bucket.
		Switch to "Mumbai" region, then try to create an S3 bucket. This should work.
------------------------------------------------------------------------------------------------------------------------

---

CreatedPolicy "region-limit"
<img width="946" height="440" alt="image" src="https://github.com/user-attachments/assets/26971fc5-05f5-47b3-a27d-77116db50adb" />
<img width="942" height="437" alt="image" src="https://github.com/user-attachments/assets/d9f4f63d-7635-4c1c-a383-498f27d47d2a" />


---

Created IAM user with Name "Region-Task" and attached above created region-limit policy
<img width="943" height="439" alt="image" src="https://github.com/user-attachments/assets/435d8ffd-2cc4-4fa2-889c-52df4a8a6820" />
<img width="946" height="437" alt="image" src="https://github.com/user-attachments/assets/a2c46d2b-8518-45d4-ab76-8f9cce14c366" />


---

Not allowing to create bucket from Other regions 
<img width="935" height="401" alt="image" src="https://github.com/user-attachments/assets/fe52fc43-ef10-4f2c-b6ce-32fc38c826d1" />


---

Allowing to create bucket from RequestedRegion ap-south-1 regions ("aws:RequestedRegion": "ap-south-1")
<img width="941" height="303" alt="image" src="https://github.com/user-attachments/assets/facb5326-d917-4c43-8d0f-91222711816a" />






