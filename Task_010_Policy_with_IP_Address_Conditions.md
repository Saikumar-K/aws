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

---

	task10.1 Created a policy "AmazonS3FullAccessFromMyIpCustomPolicy" 
	to allow AmazonS3FullAccess, but restrict it to a specific IP address or network.
		Used my own network IP address: i.e; x.x.x.x/32. ==> "183.83.164.73"
			( get my network IP by visiting websites i.e;
			http://checkip.amazonaws.com/ or https://whatismyipaddress.com/)
		Added condition to the policy to allow access only when the request originates from this IP address.

<img width="947" height="448" alt="image" src="https://github.com/user-attachments/assets/aab64bd4-8f25-473e-9c01-ae18ca1f46a9" />

<img width="944" height="160" alt="image" src="https://github.com/user-attachments/assets/fe00a8fe-b32f-46aa-96d6-a71307646a29" />

---

	task10.2 Attached the policy to an IAM user "S3UserWithMyIpOnly" and tested as below:
		Log in from a different IP address and attempt to access S3.
		Log in from the allowed IP and perform S3 actions.

<img width="970" height="387" alt="image" src="https://github.com/user-attachments/assets/54da74b5-0c40-4f4b-a941-3c4014d22f1b" />

Verified that ==>Log in from the allowed IP and perform S3 actions is done without any restrictions.
<img width="937" height="305" alt="image" src="https://github.com/user-attachments/assets/37e8ebfb-6601-471b-8363-f0c63c0de37a" />

Verified that ==>Log in from the different IP and when tried to perform S3 actions , getting the access permission issue.
<img width="943" height="304" alt="image" src="https://github.com/user-attachments/assets/2e7087e1-f531-4f64-b8b9-b995bdedd85e" />


