---

## Notify Replication Failures in AWS S3

---

## 1. Purpose

This document describes the **end-to-end procedure to notify S3 replication failures** using **S3 Event Notifications with SNS and SQS**, including the **critical prerequisite** required for failure events to be published.

The goal is to **receive alerts when an object fails to replicate from a source S3 bucket to a destination bucket**.

---

## 2. Task Name

**Notify the Replication Failures in AWS S3**

---

## 3. Architecture Overview

**Flow Summary:**

```
S3 Source Bucket
   ↓ (Replication Failure)
S3 Replication Rule (Metrics Enabled)
   ↓
S3 Event Notification (Failed to replicate)
   ↓
SNS Topic
   ↓
SQS Queue + Email Subscription
```

This setup ensures **near real-time, object-level notification** when replication fails.

---

## 4. Resources Created

### Step 1: Resource Setup

The following AWS resources were created:

| Resource Type                 | Name                                     |
| ----------------------------- | ---------------------------------------- |
| Source S3 Bucket              | `my-source-bucket-replication-test`      |
| Destination S3 Bucket         | `my-destination-bucket-replication-test` |
| SNS Topic (Event Destination) | `my-topic-test-replication`              |
| SQS Queue (Subscribed to SNS) | `my-queue-test-replication`              |
| Email Subscription            | Configured on SNS topic                  |

📌 **Note:** SNS was configured as the event destination, with both **SQS** and **Email** subscriptions for notification delivery.
<img width="911" height="203" alt="image" src="https://github.com/user-attachments/assets/068ba3f2-b603-4600-a0be-f96a42e8dc9d" />
<img width="938" height="221" alt="image" src="https://github.com/user-attachments/assets/b6c88c94-ba42-4c8e-ab54-7ee2e73125aa" />
<img width="634" height="275" alt="image" src="https://github.com/user-attachments/assets/d39f07fd-cd0c-4ff1-8162-0c82ed98e527" />
<img width="941" height="355" alt="image" src="https://github.com/user-attachments/assets/ecf45d9a-9579-4a61-93da-3b42a1ae2943" />

---

## 5. Replication Rule Configuration

### Step 2: Create Replication Rule

A replication rule was created on the **source bucket** with the following details:

| Setting               | Value                                    |
| --------------------- | ---------------------------------------- |
| Replication Rule Name | `testing-replication`                    |
| Source Bucket         | `my-source-bucket-replication-test`      |
| Destination Bucket    | `my-destination-bucket-replication-test` |
| Status                | Enabled                                  |

### 🔴 **Important Configuration (Mandatory)**

Under **Additional replication options**:

* ☑ **Replication metrics — ENABLED**

📌 **This is a critical requirement for replication failure events to be published.**

<img width="1847" height="710" alt="Screenshot 2025-12-24 012638" src="https://github.com/user-attachments/assets/9510cdb3-62e8-42c2-a7c6-f7eef65739e2" />
*Screenshot attached — Replication rule with metrics enabled*

---

## 6. Failure Simulation (Testing Scenario)

### Step 3: Force Replication Failure

To intentionally trigger a replication failure for testing:

* The **IAM role associated with the replication rule** was modified
* Required permissions were removed from the role’s **Access Policy**
* This caused replication attempts to **fail permanently**

📌 This approach is safe and commonly used for testing alert mechanisms.

---

## 7. Triggering the Failure Event

### Step 4: Upload Test Object

* A file was uploaded to the **source bucket**
* The object matched the replication rule
* Replication attempted and **failed due to IAM permission issues**

---

## 8. Notification Verification

### Step 5: Validate Notifications

Once replication failed:

* ✅ **S3 published a “Replication – Failed to replicate” event**
* ✅ Event was sent to **SNS topic**
* ✅ Notifications were received in:

  * **SQS queue**
  * **Email subscription**

<img width="1920" height="1080" alt="Screenshot (90)" src="https://github.com/user-attachments/assets/6bc650da-ab87-4d3b-b459-1a8b1011cd68" />
<img width="847" height="268" alt="image" src="https://github.com/user-attachments/assets/71ce4cf0-d400-4604-861f-838ae37adf5b" />
 *Screenshot attached — SQS message and email notification*

---

## 9. Event Details (Example)

A typical replication failure event contains:

* Source bucket name
* Destination bucket name
* Object key
* Failure reason (e.g., `AccessDenied`)
* Event type: `Replication:Failed`

This provides **object-level visibility** into replication issues.

---

## 10. ⚠️ Important Realization (Critical Learning)

> **Replication failure notifications are published only when “Replication metrics” are enabled in the replication rule.**

### Key Insight

* Even if:

  * Event notifications are configured correctly
  * “Replication events – Failed to replicate” is selected
  * SNS and subscriptions are properly set
* ❌ **No events will be published unless replication metrics are enabled**

### Summary Rule

> **No replication metrics → No replication failure events**

This dependency is **not obvious in the console** but is mandatory for failure notifications.

---

## 11. Key Benefits of This Approach

* ✅ Near real-time, object-level failure alerts
* ✅ No polling or manual checks required
* ✅ Integrates cleanly with SQS, email, or automation
* ✅ Scalable and AWS-native
* ✅ Suitable for production monitoring

---

## 12. Conclusion

This implementation successfully enables **replication failure notifications for AWS S3** by combining:

* S3 Replication (with metrics enabled)
* S3 Event Notifications
* SNS for message distribution
* SQS and Email for alert consumption

This setup is **production-ready, auditable, and aligned with AWS best practices**.

---

### 🧠 Quick Memory Tip

> **“Metrics first, events next.”**

---
