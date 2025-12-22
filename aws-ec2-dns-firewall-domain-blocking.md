

## Blocking Specific Websites in an AWS EC2 Instance Using DNS Firewall

---

## 1. Objective

The objective of this document is to **block access to specific websites (`yahoo.com` and `wikipedia.org`) from an EC2 Linux instance**, while **allowing access to all other websites**, using **AWS DNS Firewall** at the VPC level.

This solution ensures:

* **Centralized control** (no OS-level or instance-level changes)
* **Scalable and reusable** policy enforcement
* **Network-level security enforcement** using AWS-managed services

---

## 2. Scope

* **Target Resource**: Amazon EC2 (Linux)
* **Network Layer**: Amazon VPC
* **Blocking Mechanism**: DNS-based filtering
* **Blocked Domains**:

  * `yahoo.com`
  * `wikipedia.org`
* **Allowed**: All other internet domains

---

## 3. Prerequisites

Before proceeding, ensure the following:

* An **AWS account** with permissions for:

  * VPC
  * Route 53 Resolver
* A **running EC2 Linux instance** inside a VPC
* EC2 instance has:

  * Internet access (via Internet Gateway or NAT Gateway)
  * DNS resolution enabled at the VPC level
* Basic Linux command-line access (SSH)

---

## 4. Architecture Overview

### High-Level Flow

1. EC2 instance sends a DNS request
2. DNS request is intercepted by **Route 53 Resolver DNS Firewall**
3. Firewall checks the **Domain List**
4. If the domain matches:

   * Request is **blocked**
5. If no match:

   * Request is **allowed**

📌 **Important**: This works at the DNS level — no IP addresses are required.

---

## 5. Verification – Before Changes

### Step 1: Validate Internet Access

SSH into the EC2 instance and run:

```bash
wget https://yahoo.com
wget https://wikipedia.org
wget https://google.com
```

### Expected Result (Before Changes)

* ✅ All websites are accessible
* No connection failures

📸 **Screenshot Placeholder**

> Insert screenshot showing successful `wget` output for all websites

---

## 6. Create Domain List

### Step 2: Create a DNS Firewall Domain List

You can perform this step from either:

* **VPC Console**
* **Route 53 Console**

#### Actions:

1. Open **AWS Console**
2. Navigate to:

   * **VPC → DNS Firewall**
   * or **Route 53 → Resolver → DNS Firewall**
3. Select **Domain Lists**
4. Click **Create domain list**
5. Enter:

   * **Name**: `blocked-domains-list`
6. Add domains:

   ```text
   yahoo.com
   wikipedia.org
   ```
7. Save the domain list

📸 **Screenshot Placeholder**

> Insert screenshot of domain list creation with domains added

---

## 7. Create DNS Firewall Rule Group

### Step 3: Create a Rule Group and Add Rules

#### Actions:

1. Navigate to **DNS Firewall → Rule groups**
2. Click **Create rule group**
3. Enter:

   * **Rule group name**: `block-selected-domains`
4. Add a rule:

   * **Domain list**: `blocked-domains-list`
   * **Action**: `BLOCK`
   * **Block response**: `NXDOMAIN` (recommended)
   * **Priority**: `1`
5. Create the rule group

📸 **Screenshot Placeholder**

> Insert screenshot showing rule configuration and action set to BLOCK

---

## 8. Associate Rule Group with VPC

### Step 4: Attach Rule Group to VPC

#### Actions:

1. Open the created **Rule Group**
2. Choose **Associate with VPC**
3. Select:

   * Target VPC where EC2 instance is running
4. Confirm association

📸 **Screenshot Placeholder**

> Insert screenshot of VPC association screen

---

## 9. Verification – After Changes

### Step 5: Test DNS Blocking

From the same EC2 Linux instance, run:

```bash
wget https://yahoo.com
wget https://wikipedia.org
wget https://google.com
```

### Expected Result (After Changes)

| Website       | Result    |
| ------------- | --------- |
| yahoo.com     | ❌ Blocked |
| wikipedia.org | ❌ Blocked |
| google.com    | ✅ Allowed |

* Blocked domains will show **DNS resolution failure**
* Allowed domains will work normally

📸 **Screenshot Placeholder**

> Insert screenshot showing `wget` failure for blocked domains and success for allowed domain

---

## 10. Key Advantages of This Approach

* ✅ No EC2 configuration changes required
* ✅ Works across **all instances** in the VPC
* ✅ Domain-based filtering (no IP dependency)
* ✅ Centralized and auditable security control
* ✅ Easy to extend by adding more domains

---

## 11. Limitations & Notes

* DNS Firewall blocks **only DNS-based access**
* If applications use **hardcoded IPs**, DNS Firewall will not block them
* HTTPS SNI is not inspected — DNS-based filtering only
* Ensure VPC has **DNS Resolution & DNS Hostnames enabled**

---

## 12. Conclusion

Using **AWS DNS Firewall**, we successfully enforced **domain-level outbound access control** for EC2 instances by blocking `yahoo.com` and `wikipedia.org` while allowing all other websites.

This solution is **secure, scalable, AWS-native, and production-ready**, making it the recommended standard for enterprise environments.

---

