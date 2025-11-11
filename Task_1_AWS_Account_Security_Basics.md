Task 1 → AWS Account Security Basics

	task1.1 Create an AWS Account: Set up a new AWS account.
	task1.2 Enable MFA for the Root User: Protect the root user by enabling Multi-Factor Authentication (MFA). Use a virtual MFA device like Google Authenticator.
	task1.3 Set Account Alias and Custom Password Policy:
				Create an account alias for easier identification (e.g., Avinash-demo).
				Configure a custom password policy:
					Minimum password length: 8 characters.
					Require at least one uppercase letter, one number, and one special character.
					Disallow password reuse for the last 3 passwords.
----------------------------------------------------------------------------------------------------
task1.1 AWS Account created , sign up at AWS Console https://aws.amazon.com/console
task1.2️ To Enable MFA for the Root User
	Logged in as Root User (your email ID used during account creation).
	Go to:
	Profile Icon → Security Credentials → 
	OR
	IAM Service → (Quick Links Section) Security Credentials 
	→ Multi-Factor Authentication (MFA)--> Assign MFA device ->
	Choose Virtual MFA device → scan QR code using Google Authenticator / Authy app.
	Enter the 2 OTPs shown →  Done.
  <img width="897" height="461" alt="image" src="https://github.com/user-attachments/assets/f87dfc06-9b4a-4d63-81e4-a77ae611dd39" />

----------------------------------------------------------------------------------------------------
task1.3.1 Set Account Alias
	This makes login easy (instead of using your 12-digit AWS account ID).
	Go to  IAM → (AWS Account Section) Account Alias
	Example: Sai-demo
	Then your login URL becomes:
	https://Sai-demo.signin.aws.amazon.com/console
	<img width="937" height="395" alt="image" src="https://github.com/user-attachments/assets/585538d4-68e3-46a7-bb17-979b1f30c84c" />

	CLI:
		aws iam create-account-alias --account-alias Sai-demo
		aws iam list-account-aliases

----------------------------------------------------------------------------------------------------
task1.3.2 Configure Custom Password Policy
	Go to  IAM → Account Settings → Password Policy
	Apply:
	Minimum length = 8 characters
	Must include:
	 At least one uppercase
	 At least one number
	 At least one special character
	 Prevent password reuse (last 3 passwords).
	 <img width="947" height="431" alt="image" src="https://github.com/user-attachments/assets/d57efb99-6a50-4a02-8139-f4da50370f8e" />

	 CLI:
		aws iam update-account-password-policy \
		  --minimum-password-length 8 \
		  --require-uppercase-characters \
		  --require-numbers \
		  --require-symbols \
		  --password-reuse-prevention 3
		
		aws iam get-account-password-policy

==========================================================================================================================
