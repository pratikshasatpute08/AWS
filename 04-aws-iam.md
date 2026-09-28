# AWS Learning Journey — Day 4: IAM (Identity and Access Management)

**IAM** is the AWS service that controls **who can do what** in your AWS account. It's the security gatekeeper of AWS — deciding who gets in, and what they're allowed to touch once they're in.

Think of AWS as a big office building. **IAM is the security desk + ID badge system** — it decides who can enter the building, which floors they can access, and which rooms they can open.

---

## Why IAM Exists

Without IAM, anyone with your AWS login could do **anything** — delete servers, access sensitive data, spin up expensive resources. IAM lets you:
- Create **separate identities** for different people/services
- Give each identity **only the permissions it actually needs** (this is called the **Principle of Least Privilege**)

**Real-world example:**
Imagine a company with 50 employees using one shared AWS account login. If a junior developer accidentally deletes a production database, there's no way to know who did it, and nothing stopped them. With IAM, each employee gets **their own identity** with **only the permissions relevant to their job** — a junior developer might only get read-access to logs, not delete-access to databases.

---

## The 4 Core Building Blocks of IAM

| Component | What it is | Simple Analogy |
|---|---|---|
| **User** | An individual identity (a person or app) | An employee's ID badge |
| **Group** | A collection of users with shared permissions | A department (e.g., "Developers", "Finance") |
| **Role** | A temporary identity that can be "assumed" by users/services | A visitor's temporary access pass |
| **Policy** | A document defining exact permissions (allow/deny) | The list of doors a badge can open |

---

### 1️⃣ IAM User

A **User** represents one person (or application) that needs to interact with AWS — logging into the console, or using the CLI/API.

**Example:** You create an IAM User for your teammate "Priya" so she can log in and manage EC2 instances — without sharing your root account password.

⚠️ **Best practice:** Never use the **root account** (the original account you signed up with) for daily work — it has unlimited power. Create IAM Users instead, and lock the root account away.

---

### 2️⃣ IAM Group

A **Group** is just a bunch of Users bundled together so you can assign permissions **once** instead of repeating it for every person.

**Example:** You create a group called "Developers" and attach a policy allowing EC2 + S3 access. Now, every new developer you add to this group **automatically inherits** those permissions — no need to configure each person individually.

---

### 3️⃣ IAM Role

A **Role** is like a temporary identity — instead of permanently belonging to a user, it can be "assumed" when needed, and permissions expire after use.

**Why it's powerful:** Roles are mainly used so **AWS services can talk to each other securely**, without hardcoding passwords/keys anywhere.

**Real-world example:**
Imagine an EC2 instance (a virtual server) needs to read files from an S3 bucket. Instead of storing an access key inside the server's code (risky if leaked), you attach an **IAM Role** to the EC2 instance. AWS automatically gives it **temporary credentials** behind the scenes — if someone steals the server, they don't get a permanent password, since the credentials keep rotating and are tied only to that role.

---

### 4️⃣ IAM Policy

A **Policy** is a **JSON document** that explicitly defines what actions are **allowed or denied**, and on which AWS resources.

**Example Policy (in plain English):**
> "Allow this user to read objects from the S3 bucket called `company-photos`, but deny them from deleting anything."

```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::company-photos/*"
}
```

This policy can then be attached to a **User**, **Group**, or **Role**.

---

## 🔑 Putting It All Together — A Real Scenario

Imagine a company called "PixelStore" using AWS:

1. **IAM Group "Developers"** — has a policy allowing full EC2 + S3 access
2. **IAM User "Rohan"** (a developer) — added to the "Developers" group → automatically gets EC2 + S3 access
3. **IAM Role "EC2-S3-ReadAccess"** — attached to an EC2 server so it can automatically read from an S3 bucket, without any hardcoded password
4. **IAM Policy** — explicitly says: "Allow reading from S3 bucket `product-images`, but deny deleting anything"

This way:
- Rohan can do his job without touching production billing settings
- The EC2 server can access S3 securely without embedded secrets
- If Rohan leaves the company, you just remove his IAM User — nothing else breaks

---

## 🛡️ IAM Best Practices (commonly asked in interviews too)

| Practice | Why |
|---|---|
| **Never use root account for daily tasks** | Root has unlimited power — huge risk if compromised |
| **Enable MFA (Multi-Factor Authentication)** | Adds a second layer of security beyond just a password |
| **Follow Principle of Least Privilege** | Only give the minimum permissions needed — nothing more |
| **Use Roles instead of hardcoding credentials** | Avoids leaked passwords/keys in code |
| **Use Groups instead of assigning policies per user** | Easier to manage permissions at scale |

---

## 🧠 Day 4 Recap

- **IAM** = controls who can do what in your AWS account
- **User** = one person's ID badge
- **Group** = a department sharing the same badge permissions
- **Role** = a temporary visitor pass, mainly used by AWS services
- **Policy** = the actual rulebook (JSON) defining what a badge/pass can or cannot open
- Always use **MFA**, avoid the **root account**, and follow **least privilege**

---

*Next up: S3 (Simple Storage Service) — buckets, objects, and storage classes.*
