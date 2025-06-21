# aws-kms-encryption-lab
Hands-on lab with AWS KMS, S3, EC2, EBS, and CloudTrail to encrypt data at rest.

# AWS KMS Encryption Lab

This repository documents my hands-on experience completing **Lab 5.1: Encrypting Data at Rest by Using AWS KMS** through AWS Academy. The lab focused on securing data using AWS Key Management Service (KMS) with **Amazon S3**, **Amazon EC2**, **Amazon EBS**, and **AWS CloudTrail**.

---

## 🔐 Lab Goals

- ✅ Create a **customer managed AWS KMS key**
- ✅ Encrypt an object in an S3 bucket using **SSE-KMS**
- ✅ Attempt **public vs signed access** to encrypted S3 objects
- ✅ Monitor **KMS API activity via AWS CloudTrail**
- ✅ Encrypt the **root volume of an EC2 instance**
- ✅ Simulate a **KMS key disablement** and observe how it affects access to encrypted data

---

## 🛠️ What I Did

### 1. Created a Symmetric KMS Key
Created a **256-bit symmetric customer managed key** called `MyKMSKey` and granted access to the `voclabs` role.

### 2. Encrypted an Object in S3
Uploaded a file (`clock.png`) to an S3 bucket and applied **SSE-KMS encryption** using `MyKMSKey`. Verified encryption status in object metadata.

### 3. Tested Access Control
- 🔒 **Public access failed** due to encryption requirements.
- 🔐 **Signed access (via AWS Console)** succeeded, demonstrating how credentials and AWS Signature Version 4 are required for KMS decryption.

### 4. Monitored Key Usage with CloudTrail
Viewed:
- `GenerateDataKey` event when S3 requested encryption
- `Decrypt` event when accessing the object
- `DisableKey` and `CreateGrant` events during EBS volume testing

### 5. Encrypted EC2 Root Volume
- Stopped the EC2 instance (`LabInstance`)
- Took a snapshot of the **unencrypted root volume**
- Created a **new encrypted EBS volume** from the snapshot
- Detached the old volume, attached the new one as `/dev/xvda`

### 6. Disabled & Re-enabled the KMS Key
- Disabled `MyKMSKey`:
  - EC2 instance **could not start**
  - Encrypted S3 object became **inaccessible**
- Re-enabled the key:
  - EC2 instance started normally
  - S3 object access restored

---

## 📘 Key Concepts Learned

| Concept                          | Summary                                                                 |
|----------------------------------|-------------------------------------------------------------------------|
| **SSE-KMS**                      | Server-side encryption with AWS KMS. Stronger control than SSE-S3.     |
| **Customer Managed Key (CMK)**   | Gives you full control of permissions, lifecycle, and monitoring.       |
| **CloudTrail + KMS Integration** | Critical for auditing encryption, decryption, and key management events.|
| **EC2 Root Volume Encryption**   | Possible via snapshot + reattach flow with KMS-encrypted volumes.       |
| **KMS Key Disablement**          | Completely blocks access to encrypted resources until re-enabled.       |

---

## 💡 Skills Demonstrated

- AWS KMS key creation & permission management
- Server-side encryption (SSE-KMS) on S3 objects
- Root volume replacement on EC2 instances
- AWS CloudTrail event filtering & analysis
- Security troubleshooting & validation

---

## 📸 Screenshots: AWS KMS Encryption Lab Walkthrough

Below is a step-by-step visual record of the AWS KMS Encryption Lab I completed, showing the key stages of setting up and applying encryption on S3, EC2, EBS, and CloudTrail.

### Step 1: 
![Step 1](screenshots/Lab%20Pic%20(1).png)

### Step 2:
![Step 2](screenshots/Lab%20Pic%20(2).png)

### Step 3: 
![Step 3](screenshots/Lab%20Pic%20(3).png)

### Step 4:
![Step 4](screenshots/Lab%20Pic%20(4).png)

### Step 5:
![Step 5](screenshots/Lab%20Pic%20(5).png)

### Step 6: 
![Step 6](screenshots/Lab%20Pic%20(6).png)

### Step 7:
![Step 7](screenshots/Lab%20Pic%20(7).png)

### Step 8:
![Step 8](screenshots/Lab%20Pic%20(8).png)

### Step 9:
![Step 9](screenshots/Lab%20Pic%20(9).png)

### Step 10:
![Step 10](screenshots/Lab%20Pic%20(10).png)

### Step 11:
![Step 11](screenshots/Lab%20Pic%20(11).png)

### Step 12:
![Step 12](screenshots/Lab%20Pic%20(12).png)
