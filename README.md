# Setting Up a Local Mail Server on Ubuntu with Postfix, Dovecot, and Mutt

This guide provides step-by-step instructions to set up a mail server on Ubuntu using **Postfix** as the SMTP server, **Dovecot** as the IMAP/POP3 server, and **Mutt** as the email client. The setup allows sending and receiving emails locally.

---

## Prerequisites
- A machine running Ubuntu (preferably 22.04 LTS or later).
- Root or sudo privileges.

---

## Step 1: Update System Packages
Update and upgrade your system to ensure you have the latest versions of all packages.
```bash
sudo apt update
sudo apt upgrade -y

##Step 2: Install Required Packages
Install Postfix, Dovecot, and Mutt.

```bash
sudo apt install postfix dovecot-core dovecot-imapd mutt -y

##Step 3: Configure Postfix (SMTP Server)
Open the Postfix configuration file:

```bash
sudo nano /etc/postfix/main.cf
Update the following parameters in main.cf:

```bash
myhostname = localhost
mydomain = localdomain
myorigin = $mydomain
inet_interfaces = all
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
home_mailbox = Maildir/
Restart Postfix to apply changes:

```bash
sudo systemctl restart postfix


##Step 4: Configure Dovecot (IMAP/POP3 Server)
Open the Dovecot configuration file:


```bash
sudo nano /etc/dovecot/dovecot.conf

Enable the IMAP protocol. Update the file to include:

plaintext
Copy code
protocols = imap
mail_location = maildir:~/Maildir
Open the authentication configuration file:

bash
Copy code
sudo nano /etc/dovecot/conf.d/10-auth.conf
Uncomment and set disable_plaintext_auth to no:

plaintext
Copy code
disable_plaintext_auth = no
Restart Dovecot to apply changes:

bash
Copy code
sudo systemctl restart dovecot
