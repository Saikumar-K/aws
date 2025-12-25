
---

## 1. Purpose

This document explains how to **detect and notify whenever AdministratorAccess is granted to any IAM user, group, or role**, in alignment with **AWS Least Privilege security principles**.

The solution ensures:

* 🔔 Immediate notification
* 🛡️ Security visibility for high-risk access
* 📜 Audit-ready monitoring
* ⚙️ Fully AWS-native implementation

---

## 2. Task Name

**Notify When IAM User Gets Administrator Access** ✅

---

## 3. Why This Control Is Critical

Granting `AdministratorAccess`:

* Bypasses least-privilege design
* Allows unrestricted AWS account access
* Represents a **high-severity security event**

⚠️ AWS **does not provide alerts by default** — this must be explicitly configured.

---

## 4. Architecture Overview

```
IAM Policy Change
   ↓
CloudTrail (Management Events)
   ↓
EventBridge Rule (Detect Admin Policy)
   ↓
SNS Topic
   ↓
Email Notification
```

---

## 5. AWS Services Used

* **AWS Identity and Access Management**
* **AWS CloudTrail**
* **Amazon EventBridge**
* **Amazon SNS**

---

## 6. Prerequisites

Before implementation, ensure:

* AWS account with admin permissions
* Valid email address for alerts
* CloudTrail **Trail** enabled (not just Event History)

---

## 7. Practical Implementation Steps

---

## 🔹 Step 1: Create CloudTrail Trail (Mandatory)

### Observation

* **Event History was present**
* **No Trails existed**

📌 **Important:** Event History alone is **not sufficient** for automation or EventBridge rules.

### Action

Path:

```
CloudTrail → Trails → Create trail
```

Configuration:

* Trail name: `org-security-trail`
* Apply to all regions: ✅ Yes
* Management events: ✅ Enabled
* Read & Write events: ✅ Enabled
* Destination: New S3 bucket (default)

<img width="1881" height="522" alt="Screenshot 2025-12-25 150418" src="https://github.com/user-attachments/assets/4f6a25b1-5b67-4e56-abdd-f07e49e01f0f" />
<img width="1893" height="568" alt="Screenshot 2025-12-25 150459" src="https://github.com/user-attachments/assets/6adbc909-4ffd-478b-a61f-6130b253c103" />
*Screenshot attached*

> CloudTrail trail showing “Logging: ON”

---

## 🔹 Step 2: Create SNS Topic for Alerts

Path:

```
SNS → Topics → Create topic
```

Configuration:

* Type: Standard
* Name: `iam-admin-access-alerts`

Add **Email subscription** and confirm it.
<img width="1773" height="481" alt="Screenshot 2025-12-25 143213" src="https://github.com/user-attachments/assets/53fcd128-fa12-4ab3-b26c-2023a11d00c3" />
<img width="1615" height="605" alt="Screenshot 2025-12-25 143338" src="https://github.com/user-attachments/assets/d9fb4d3f-9ed3-4a1a-a412-f6a33fc56875" />
<img width="1442" height="288" alt="Screenshot 2025-12-25 143431" src="https://github.com/user-attachments/assets/91801b72-3698-4096-b45a-482f2eb6ddce" />
<img width="1333" height="547" alt="Screenshot 2025-12-25 143621" src="https://github.com/user-attachments/assets/88dfc19d-8d0c-45a3-a9b7-46df86492af4" />
<img width="875" height="480" alt="Screenshot 2025-12-25 143609" src="https://github.com/user-attachments/assets/c9925bb0-74b1-44c3-85fd-5fc98929f807" />
subscription confirmed
<img width="1591" height="753" alt="Screenshot 2025-12-25 143642" src="https://github.com/user-attachments/assets/74b87324-f65a-48d0-8b03-0cbd14bd6f98" />
📸 *Screenshots attached*

> SNS topic with confirmed email subscription

---

## 🔹 Step 3: Create EventBridge Rule (Core Logic)

Path:

```
EventBridge → Rules → Create rule
```

Rule Details:

* Name: `detect-administrator-access-grant`
* Event bus: `default`

### Event Pattern (Critical)

```json
{
  "source": ["aws.iam"],
  "detail-type": ["AWS API Call via CloudTrail"],
  "detail": {
    "eventSource": ["iam.amazonaws.com"],
    "eventName": [
      "AttachUserPolicy",
      "AttachGroupPolicy",
      "AttachRolePolicy"
    ],
    "requestParameters": {
      "policyArn": [
        "arn:aws:iam::aws:policy/AdministratorAccess"
      ]
    }
  }
}
```
<img width="1882" height="844" alt="Screenshot 2025-12-25 145123" src="https://github.com/user-attachments/assets/c8caf7cb-5ddb-4880-a7e7-01e48bcfe997" />
CustomeEvent
<img width="1868" height="747" alt="Screenshot 2025-12-25 144706" src="https://github.com/user-attachments/assets/cda48ca7-cf3b-41e8-bbf2-be99c0e6648c" />
Target to SNS
<img width="1816" height="707" alt="Screenshot 2025-12-25 144946" src="https://github.com/user-attachments/assets/40fe3cab-ac92-4366-811e-461615d4830e" />
FinalCheck: Eventbridge Rule Enabled
<img width="1818" height="590" alt="Screenshot 2025-12-25 145219" src="https://github.com/user-attachments/assets/2e30da4a-ecf5-44bc-9d8e-245b09906683" />
*Screenshot attached*

> EventBridge rule with custom event pattern

---

## 🔹 Step 4: Configure Target (SNS)

Target:

* Service: SNS
* Topic: `iam-admin-access-alerts`

Ensure rule status is **Enabled**.

> EventBridge target configuration

---

## 🔹 Step 5: Test the Setup

### Test Action

```
IAM → Users → <Test-user-access-alert>
→ Add permissions
→ Attach policies
→ AdministratorAccess
```
<img width="1864" height="771" alt="Screenshot 2025-12-25 151015" src="https://github.com/user-attachments/assets/f0fb6fd5-b187-4206-b733-384697fb050d" />
<img width="1596" height="811" alt="Screenshot 2025-12-25 151041" src="https://github.com/user-attachments/assets/60ac5a1c-7166-4927-b14f-a79bbbc0696e" />

### Result

* ✅ Email notification received
* ✅ Alert triggered immediately

<img width="1754" height="686" alt="Screenshot 2025-12-25 151143" src="https://github.com/user-attachments/assets/8d327632-c4a6-4111-a7e5-b812bb7d3ac5" />
📸 *Screenshot attached confirming the Notification received*
> Email alert showing AdministratorAccess attachment

---

## 8. Sample Alert Meaning

> 🚨 **Security Alert: Administrator Access Granted**
> Policy: AdministratorAccess
> Target: IAM User / Group / Role
> Action: AttachPolicy
> Time: Timestamp

---

## 9. ⚠️ Key Learning Points (Very Important)

### 🔴 Critical Realization

> **Event History alone does NOT trigger EventBridge rules.
> A CloudTrail Trail is mandatory.**

### Key Learnings

* ✅ CloudTrail **Trail** is required for automation
* ❌ Event History is only for manual viewing
* ✅ EventBridge listens to **CloudTrail events**
* ✅ AdministratorAccess detection works in near real-time
* ⚠️ Inline policies granting `*:*` need separate rules

---

## 10. Least Privilege Alignment

This solution:

* Enforces security visibility
* Detects high-risk access grants
* Supports SOC & audit requirements
* Requires no additional permissions

---

## 11. Conclusion

This implementation successfully enables **real-time notification whenever AdministratorAccess is granted** in AWS.

It is:

* ✅ Secure
* ✅ Scalable
* ✅ Audit-ready
* ✅ AWS-recommended

---

## 🧠 Quick Memory Tips (Easy Recall)

> **“No Trail → No Alerts.”**
> **“CloudTrail logs it, EventBridge catches it, SNS alerts it.”**

---
