Task 11 → Allow_Users_to_work_only_on_Specific_Region

	task11.1 Create a policy to allow an IAM user to perform all operations on S3 service, but limited to a specific region.
	task11.2 Test the behavior:
		Create an IAM policy (name: region-limit) that allows all operations on S3, but add a condition RequestedRegion with ap-south-1
		Create an IAM user with Name Region-Task, attach region-limit policy, 
			--login and try to create a bucket by selecting Region as "Hyderabad". Observe the output. 
			--This should not allow to create a bucket.
		Switch to "Mumbai" region, then try to create an S3 bucket. This should work.
------------------------------------------------------------------------------------------------------------------------
