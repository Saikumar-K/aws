
---

## 1. Purpose

This document explains the **end-to-end steps to create Amazon S3 buckets and configure replication** from a source bucket to a destination bucket.

The objective is to **automatically copy objects uploaded to the source bucket into the destination bucket**, validating the replication setup.

---

## 2. Task Name

**Task 13: S3 Bucket Creation and Replication**

---

## 3. Service Overview

* **Amazon S3** provides object storage with built-in support for **replication**, enabling automatic, asynchronous copying of objects between buckets.

---

## 4. Prerequisites

Before starting, ensure:

* AWS account with S3 permissions
* Buckets created in the same or different regions (both supported)
* IAM role available for S3 replication
* **Versioning enabled** on both source and destination buckets

---

## 5. Practical Implementation Steps

---

## 🔹 Practical Step 1: Create S3 Buckets

The following S3 buckets were created:

| Bucket Type        | Bucket Name                              |
| ------------------ | ---------------------------------------- |
| Source Bucket      | `my-source-bucket-replication-test`      |
| Destination Bucket | `my-destination-bucket-replication-test` |

📌 Buckets were created successfully and are accessible from the S3 console.
<img width="428" height="236" alt="image" src="https://github.com/user-attachments/assets/ae6b283e-6131-4257-b7a0-42a782ac7e57" />
 *Screenshot attached — Source and destination buckets created*

---

## 🔹 Practical Step 2: Enable Versioning and Configure Replication

### Enable Versioning (Mandatory)

Versioning was enabled on **both buckets**:

```
S3 → Bucket → Properties → Bucket Versioning → Enable
```

📌 **Note:**
Replication **will not work** unless versioning is enabled on **both the source and destination buckets**.

---

### Create Replication Rule

A replication rule was created on the **source bucket**:

| Setting               | Value                                    |
| --------------------- | ---------------------------------------- |
| Replication Rule Name | `testing-replication`                    |
| Source Bucket         | `my-source-bucket-replication-test`      |
| Destination Bucket    | `my-destination-bucket-replication-test` |
| Rule Status           | Enabled                                  |

Path:

```
Source Bucket → Management → Replication rules
```

<img width="1362" height="866" alt="Screenshot 2025-12-25 124001" src="https://github.com/user-attachments/assets/211cd608-0aea-4a25-9582-e75ada11c4cf" />
 *Screenshot attached — Replication rule configuration*

---

## 🔹 Practical Step 3: Replication Verification

To verify the replication setup:

1. Uploaded objects to the **source bucket**
2. Objects were **automatically replicated** to the destination bucket
3. Replication completed successfully without errors

### Verification Result

| Action                               | Result                 |
| ------------------------------------ | ---------------------- |
| Upload object to source bucket       | ✅ Success              |
| Object appears in destination bucket | ✅ Automatically copied |

<img width="823" height="296" alt="Screenshot 2025-12-25 124314" src="https://github.com/user-attachments/assets/ba525bdb-712d-4305-8f5a-cdf293d2aedb" />
<img width="1767" height="627" alt="Screenshot 2025-12-25 124339" src="https://github.com/user-attachments/assets/fd6b3368-f580-4a1e-808d-4c8c8897d623" />
 *Screenshot attached — Object present in both source and destination buckets*

---

## 6. Key Observations (Quick Notes)

* ✅ Replication works **only on versioned buckets**
* ✅ Replication is **asynchronous**
* ✅ Existing objects are not replicated unless explicitly enabled
* ✅ New uploads are automatically replicated
* ✅ Replication is managed from the **source bucket only**

---

## 7. Common Mistakes to Avoid

| Mistake                            | Impact                      |
| ---------------------------------- | --------------------------- |
| Versioning not enabled             | Replication fails           |
| Rule created on destination bucket | Invalid                     |
| IAM role missing permissions       | Replication failure         |
| Expecting instant replication      | Replication is asynchronous |

---

## 8. Conclusion

This task successfully demonstrated **Amazon S3 bucket creation and replication**, ensuring that objects uploaded to the source bucket are **automatically copied to the destination bucket**.

The setup follows **AWS best practices** and serves as a strong foundation for:

* Backup strategies
* Cross-region disaster recovery
* Data redundancy solutions

---

## 🧠 Quick Memory Tip

> **“No versioning → no replication.”**

---
