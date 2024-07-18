# Setting Up Cloud Storage and Cloud SQL in Google Cloud Platform

## Task 1 - Deploy a web server VM instance
In the Google Cloud console, on the Navigation menu (Navigation menu icon), click Compute Engine > VM instances.

Click Create Instance.
![pic1- creating vm instances](https://github.com/user-attachments/assets/60b99e06-c8fc-4174-974f-fdf742dd3cd2)

On the Create an Instance page, for Name, type bloghost

For Region and Zone, select the region and zone assigned by Qwiklabs.

For Machine type, accept the default.

For Boot disk, if the Image shown is not Debian GNU/Linux 11 (bullseye), click Change and select Debian GNU/Linux 11 (bullseye).
![pic 2 - bootdisk modify](https://github.com/user-attachments/assets/b6f963bb-a0c8-4629-a407-6a88ed96d52b)

Leave the defaults for Identity and API access unmodified.

For Firewall, click Allow HTTP traffic.

Click Advanced options to open that section of the dialog.

Click Management to open that section of the dialog.

Scroll down to the Automation section, and enter the following script as the value for Startup script:

```
apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart
```
![pic3 - startup script](https://github.com/user-attachments/assets/7ac67fc9-e168-4061-a153-7706aaeb8525)


```Note: Be sure to supply that script as the value of the Startup script field. If you accidentally put it into another field, it won't be executed when the VM instance starts.
Leave the remaining settings as their defaults, and click Create.```

```Note: Instance can take about two minutes to launch and be fully available for use.
On the VM instances page, copy the bloghost VM instance's internal and external IP addresses to a text editor for use later in this lab.```
