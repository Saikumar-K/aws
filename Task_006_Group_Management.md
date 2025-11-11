Task 6 → Group Management

	task6.1 Create an IAM group named Developers.
		Attach the AmazonS3ReadOnlyAccess policy to the group.
	task6.2 Add two IAM users (DevUser1 and DevUser2) to the Developers group.
		Log in as DevUser1 and verify:
			Access to view S3 buckets is allowed.
			Attempting to upload a file results in an error due to insufficient permissions.
------------------------------------------------------------------------------------------------------------------------
