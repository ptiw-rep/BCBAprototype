# Blockchain derived authentication mechanism

### Problems to overcome :
 1. Secure Authentication
 2. Data/Information mutability
 3. Anything that comes from user as an input is vulnerable 
 4. MITM, Spoofing and Phishing Attacks
 5. How to get an confirmation of login
 6. Movement of data outside the entities
 7. Vulnerable databases cause more damage than user data exploitation

## Signup  :

1. It requires a user identifier and the user description ( for digital signature ). For user identifier the proposed solution is a combination of name, MAC address, and a live time physical authentication such as fingerprint or retina scan. a combination of these is used to generate a unique ID here called as user_identifier along with the description of the device used.

2. As soon as the SignUp Entity ( say signup manager ) gets the confirmation for these two, a block in the mainchain is allocated with the following generated information :
	1.  the new user’s block address
	2.  the new user’s block private key
	3.  the new user’s block public key
	4.  the relevant transaction id 
	5.  the new user’s RSA public key
	6.  the new user’s RSA private key

3. The following are automatically published to the user metadata stream ( a metadata of users without mapping ) :
	1.  new user’s identifier
	2.  new user’s description
	3.  new user’s chain address
	4.  new user’s chain public key
	5.  new user’s RSA public key

**The newly created user’s chain private key and RSA private key are not published to any data stream or any metadata.**

## Procedure :
 1. Login Request :
	 1. Access **Provider** RSA Public key and encrypt **User** Chain Address using it. Send this encrypted address to **Provider**.
	 2. **Provider** decrypts this message using its RSA Private Key and gets the **User** chain address. Using this retrieve RSA public key of **User**.
	
 2.  Digital Signature : 
		1. Hashing Timestamp and Identity description ( signature ) using message digest and encrypt it using **User** RSA public key and send it back to the **User** ( lets call this sent data encrypted *hash value*).
	 2. Decryption of this encrypted *hash value* using **User** RSA private key, we get the *hash value*.
	 3. Encrypt the *hash value* obtained using **User** chain private key (i.e equivalent of digital signature), encrypting it with **Provider** RSA public key and sending it to **Provider**.
	 4. **Provider** decrypts this with **Provider** RSA private key.

 3. Verification :
	 1. Verification of digital signature by **User** chain public key. 
	 2. Verification of timestamp can be done using a buffer time period i.e. this whole process is valid only for a fixed period of time from start to finish.
	 3. If all the verification criteria is fulfilled, the user can be granted access to resources.
