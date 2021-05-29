# EncryptedEmailFromPi
Send Encrypted GPG email from a Rasbperry Pi
This is something that is for my own personal use.  If you use it and it works for you, let me know.  

This assumes that your Raspberry Pi can already send out emails.
In this instance postfix and mailutils are already installed and working.  
To install that follow the instructions at [here](https://medium.com/codingtown/send-mail-using-postfix-server-bbb08331d39d).

In this example a Raspberry Pi 3B is being used

To determine version of the raspberry Pi
```shell
cat /proc/cpuinfo | grep Model
```

Run update and upgrade
```shell
sudo apt-get update
sudo apt-get upgrade -y
```

Verify that gpg is installed
```shell
sudo apt-get install gpg -y
```
If emails are going to be sent using root then always be in as root, if not skip this step
```shell
sudo su
```

Fill out name and email address.  Use the configuration for the email address that's already configured to send using.  
When done click O for okey

Generate a revocation certificate
```shell
gpg --output ~/revocation.crt --gen-revoke your_email@address.com
```

Change permissions of the revocation certificate
```shell
chmod 600 ~/revocation.crt
```

Import another users public key
```shell
gpg --import name_of_pub_key_file
```

Sign the imported key
```shell
gpg --sign-key email@example.com (emailaddress of public key)
```

Press Y then enter to confirm

Export signed key
```shell
gpg --output ~/signed.key --export --armor email@example.com
```

To export public key
```shell
gpg --output ~/mygpg.key --armor --export your_email@address.com
```

To send encrypted email example
```shell
cat filename.txt | gpg -ear "<destination@emailaddress.com>" | mail -a "Subject: Monthly Maintenance" -a "X-Custom-Header: yes" "destination@mailaddress.com"
```

I do not claim to know anything.  The information contained in this I gathered from...<br>
https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages
