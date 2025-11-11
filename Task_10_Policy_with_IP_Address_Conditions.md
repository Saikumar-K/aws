Task 10 → Policy with IP Address Conditions

	task10.1 Create a policy to allow AmazonS3FullAccess, but restrict it to a specific IP address or network.
		Use your own network IP address: i.e; x.x.x.x/32. 
			(You can get your network IP by visiting websites i.e;
			http://checkip.amazonaws.com/ or https://whatismyipaddress.com/)
		Add a condition to the policy to allow access only when the request originates from this IP address.

	task10.2 Attach the policy to an IAM user and test:
		Log in from a different IP address and attempt to access S3.
		Log in from the allowed IP and perform S3 actions.
------------------------------------------------------------------------------------------------------------------------
