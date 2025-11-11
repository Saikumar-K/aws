Task 8 → Fine-Grained Permissions for S3

	task8.1 Create an IAM user named S3RestrictedUser.
	task8.2 Attach a customer-managed policy to allow:
		Access to only a specific S3 bucket (e.g., Yourname-24-12-2024).
		Allow Only GetObject, ListBucket, and ListAllMyBuckets actions from the Policy.
	task8.3 Log in as S3RestrictedUser and verify:
		Attempt to access other buckets results in access denied.
		Downloading/uploading files from my-restricted-bucket is allowed.
------------------------------------------------------------------------------------------------------------------------
