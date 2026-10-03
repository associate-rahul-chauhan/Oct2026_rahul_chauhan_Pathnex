# ☁️ How to Connect an AWS EC2 Instance to Your Local Machine Using SSH

## 1. Login to AWS

First, log in to your **AWS account**.

If you are using a new account, check the current **AWS Free Tier** terms and limits before launching resources, because AWS pricing and Free Tier offers can change over time.

---

# 2. Launch an EC2 Instance

Go to:

```text
AWS Console
   ↓
Services
   ↓
EC2
   ↓
Launch Instance
```

### Select an Operating System

For learning purposes, select:

```text
Amazon Linux
```

---

# 3. Create a Key Pair

During instance creation, AWS asks you to select or create a **Key Pair**.

Create a new key pair.

For example:

```text
Key pair name:
pathnex_ec2_security_key
```

AWS will provide a private key file:

```text
pathnex_ec2_security_key.pem
```

### Important ⚠️

Save the `.pem` file safely on your **local computer**.

Do not share this file with anyone.

The private key is required to authenticate yourself when connecting to the EC2 instance.

---

# 4. Configure the Instance

For learning purposes, you can initially use the default settings where appropriate.

Then click:

```text
Launch Instance
```

AWS will create your EC2 instance.

🎉 **Your first EC2 instance is now running!**

---

# 5. Find the Public IP

Go to:

```text
EC2
 ↓
Instances
 ↓
Select your instance
```

Find:

```text
Public IPv4 address
```

For example:

```text
54.252.251.146
```

This is the IP address you can use to connect to the instance from your local machine, assuming the network/security configuration allows it.

---

# 6. Move the `.pem` File to Your SSH Directory

On your local Linux/WSL environment, the standard SSH directory is:

```text
~/.ssh
```

First create it if necessary:

```bash
mkdir -p ~/.ssh
```

Then copy your `.pem` file into it:

```bash
cp /mnt/c/Users/<WindowsUser>/Downloads/pathnex_ec2_security_key.pem ~/.ssh/
```

For example, in WSL:

```bash
cp /mnt/c/Users/INILPTP089/Downloads/pathnex_ec2_security_key.pem ~/.ssh/
```

Verify:

```bash
ls -l ~/.ssh
```

---

# 7. Set the Correct Permission on the Key

SSH requires the private key to be protected.

Run:

```bash
chmod 400 ~/.ssh/pathnex_ec2_security_key.pem
```

`400` means:

```text
Owner → read
Group → no permission
Others → no permission
```

---

# 8. Connect to EC2 Using SSH

For an Amazon Linux EC2 instance, the default username is commonly:

```text
ec2-user
```

The SSH command is:

```bash
ssh -i ~/.ssh/pathnex_ec2_security_key.pem ec2-user@<PUBLIC_IP>
```

Example:

```bash
ssh -i ~/.ssh/pathnex_ec2_security_key.pem ec2-user@54.252.251.146
```

### Break down the command

```text
ssh
 ↓
Connect using SSH

-i
 ↓
Specify the private key

~/.ssh/pathnex_ec2_security_key.pem
 ↓
Your private key

ec2-user
 ↓
Username on the EC2 server

@
 ↓
at

54.252.251.146
 ↓
EC2 public IP
```

---

# 9. First Connection

The first time you connect, SSH may ask:

```text
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Enter:

```bash
yes
```

If authentication succeeds, you'll see a shell similar to:

```text
[ec2-user@ip-172-31-47-224 ~]$
```

🎉 You are now connected to your EC2 instance.

---

# 10. If You Get `Permission Denied`

If you see something like:

```text
Permission denied (publickey)
```

first check:

### Check the key permission

```bash
ls -l ~/.ssh/pathnex_ec2_security_key.pem
```

If needed:

```bash
chmod 400 ~/.ssh/pathnex_ec2_security_key.pem
```

### Check the username

For Amazon Linux:

```text
ec2-user
```

For Ubuntu, it is commonly:

```text
ubuntu
```

So don't automatically use `ec2-user` for every Linux AMI.

---

# 11. If You Get `Connection Timed Out`

If you get:

```text
Connection timed out
```

this usually points to a **network/security configuration problem**, rather than an incorrect private key.

Go to:

```text
AWS Console
 ↓
EC2
 ↓
Instances
 ↓
Your Instance
 ↓
Security
 ↓
Security Group
 ↓
Inbound Rules
```

Make sure there is an inbound rule allowing:

```text
Type: SSH
Protocol: TCP
Port: 22
Source: My IP
```

Using **My IP** is generally preferable to opening SSH to:

```text
0.0.0.0/0
```

because `0.0.0.0/0` allows connections from anywhere on the Internet.

---

# 🔐 Complete Flow

The complete process is:

```text
AWS Account
     ↓
Launch EC2
     ↓
Select Amazon Linux
     ↓
Create Key Pair
     ↓
Download .pem
     ↓
Save .pem on Local Machine
     ↓
Copy .pem to ~/.ssh
     ↓
chmod 400 key.pem
     ↓
Get EC2 Public IP
     ↓
Configure Security Group
     ↓
SSH
     ↓
ec2-user@PUBLIC_IP
     ↓
EC2 Instance
```

### ⭐ Final command to remember

```bash
ssh -i ~/.ssh/<key-name>.pem ec2-user@<public-ip>
```

For example:

```bash
ssh -i ~/.ssh/pathnex_ec2_security_key.pem ec2-user@54.252.251.146
```

**Key concept:**

```text
.pem file       → proves you have the private key
ec2-user        → user account on EC2
Public IP       → tells SSH which EC2 machine to connect to
Security Group  → controls whether network traffic can reach port 22
SSH             → secure protocol used to connect
```
