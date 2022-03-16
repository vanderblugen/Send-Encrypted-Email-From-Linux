# Send-Encrypted-Email-From-Linux
This is a basic walkthru on how to configure a Raspberry Pi, or other linux based system, to sned encrypted GPG Emails
This is something that is for my own personal use.  If you use it and it works for you, let me know.  

#This assumes that your Linux system can already send out emails from the command line
    - when setting up this, postfix was already installed and working.  Instructions are [here](https://medium.com/codingtown/send-mail-using-postfix-server-bbb08331d39d).

In this example a Raspberry Pi 3B is being used

If using a raspberry Pi, here's how to check the version
```shell
cat /proc/cpuinfo | grep Model
```

## Run update and upgrade
```shell
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get dist-upgrade -y
```

## Verify that gpg is installed
```shell
sudo apt-get install gpg -y
```
### If emails are going to be sent using root then always be in as root, if not skip this step
```shell
sudo su
```

Fill out name and email address.  Use the configuration for the email address that's already configured to send using.  
When done click O for okey

## Generate a key
This generates a key for the email address you provide without a passphrase
```shell
gpg --batch --passphrase '' --quick-gen-key your-email@address.com default default
```

## Import another users public key
```shell
gpg --import name_of_pub_key_file
```

## Sign the imported key
```shell
gpg --sign-key email@example.com
```
Press Y then enter to confirm

## Export signed key
```shell
gpg --output ~/signed.key --export --armor your_email@address.com
```

## To export public key
```shell
gpg --output ~/mygpg.key --armor --export your_email@address.com
```

# To send encrypted email example
```shell
cat filename.txt | gpg -ear "<destination@emailaddress.com>" | mail -a "Subject: Test Email" -a "X-Custom-Header: yes" "destination@mailaddress.com"
```

I do not claim to know anything.  The information contained in this I gathered from...<br>
https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages
