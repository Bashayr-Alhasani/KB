---
title: "Access Linux Machines from Windows"
date: 2020-9-29T11:02:05+06:00
weight: 4
draft: false
---

Bluvalt Linux Servers are accessible only through Keypair. This document will help you to understand, how to access a linux machine from Microsoft Windows clients using a Keypair.

# Assumptions

- You have subscribed to Bluvalt Cloud. If not, Get a subscription from [here](https://cloud.bluvalt.com/#/register)
- You have setup your vDC. If you dont know how to, these [Videos](https://kb.bluvalt.com/kb/tools) will help.
- Create a Keypair and save to your Computer

# Download Putty & Puttygen

- Download the Files from [Here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). You can download Portable Execution file.

# Create PPK file from PEM

- Open puttygen
- Under Type of key to generate, choose **RSA**.
  ![](https://kb.bluvalt.com/uploads/puttygen-key-type.png)
  _If you're using an older version of PuTTYgen, choose SSH-2 RSA._
- Choose Load. By default, PuTTYgen displays only files with the extension .ppk. To locate your .pem file, select the option to display files of all types.
  ![](https://kb.bluvalt.com/uploads/puttygen-load-key.png)
- Choose Save private key to save the key in the format that PuTTY can use. PuTTYgen displays a warning about saving the key without a passphrase. Choose Yes.

```
A passphrase on a private key is an extra layer of protection, so even if your private key is discovered, it cannot be used without the passphrase. The downside to using a passphrase is that it makes automation harder because human intervention is needed to log on to an instance, or copy files to an instance.
```

- Specify the same name for the key that you used for the key pair (for example, my-key-pair). PuTTY automatically adds the .ppk file extension.

- Your private key is now in the correct format for use with PuTTY. You can now connect to your instance using PuTTY's SSH client.

# Access the VM using Putty

- Open Putty
  ![](https://kb.bluvalt.com/uploads/01_Putty_config.png)
- Write the Floating IP of the virtual server in to `Hostname Field`
- Click on the `+` sign on the Left pane associated to `SSH`
  ![](https://kb.bluvalt.com/uploads/putty-auth-config.png)
  `Choose the converted PPK file`
- If this is the first time you have connected to this instance, PuTTY displays a security alert dialog box that asks whether you trust the host you are connecting to.
- (Optional) Verify that the fingerprint in the security alert dialog box matches the fingerprint that you previously obtained in step 1. If these fingerprints don't match, someone might be attempting a "man-in-the-middle" attack. If they match, continue to the next step.
- Choose Yes. A window opens and asks for the user name. For default username, refer this [Link](https://kb.bluvalt.com/kb/linux-server-credentials).
- Once you enter the user name you can see the console.

```
If you specified a passphrase when you converted your private key to PuTTY's format, you must provide that passphrase when you log in to the instance.
```
