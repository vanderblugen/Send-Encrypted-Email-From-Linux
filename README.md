# EncryptedEmailFromPi
Send Encrypted GPG email from a Rasbperry Pi

This assumes that your Raspberry Pi can already send out emails.
In this instance postfix and mailutils are already installed and working.  
To install that follow the instructions at [here](https://medium.com/codingtown/send-mail-using-postfix-server-bbb08331d39d).

In this example a Raspberry Pi 3B is being used

To determine version of the raspberry Pi
```shell
cat /proc/cpuinfo | grep Model
```

First create a GPG key for the email address 














The information contained in this I gathered from multiple locations...<br>
https://www.linuxbabe.com/security/a-practical-guide-to-gpg-part-1-generate-your-keypair
