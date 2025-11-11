Task 12 → Allow Users to enable MFA himself

	task12.1 Create a policy to allow an IAM user to enable MFA in your AWS account.

	task12.2 Test the behavior:
		Create an IAM user with Name MFA-Task attach Just S3FullAccess policy, login and try to enable MFA from "Security Credentials" option.
		Switch to root/IAM user who has permissions on IAM service. Create a Policy to "enable/disable/resync MFA" For all resources and attach to MFA-Task user.
		Switch to MFA-Task user, verify if the MFA-Task user can enable/disable/sync MFA after the policy is attached.
------------------------------------------------------------------------------------------------------------------------
