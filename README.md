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


```
Note: Be sure to supply that script as the value of the Startup script field. If you accidentally put it into another field, it won't be executed when the VM instance starts.
Leave the remaining settings as their defaults, and click Create.```

```
Note: Instance can take about two minutes to launch and be fully available for use.
On the VM instances page, copy the bloghost VM instance's internal and external IP addresses to a text editor for use later in this lab.```

## Task 2 - Create a Cloud Storage bucket using the gcloud storage command line

All Cloud Storage bucket names must be globally unique. To ensure that your bucket name is unique, these instructions will guide you to give your bucket the same name as your Google Cloud project ID, which is also globally unique.

Cloud Storage buckets can be associated with either a region or a multi-region location: US, EU, or ASIA. In this activity, you associate your bucket with the multi-region closest to the region and zone that Qwiklabs or your instructor assigned you to.

On the Google Cloud console, on the top right toolbar, click the Activate Cloud Shell Activate Cloud Shell icon. If a dialog box appears, click Continue.

For convenience, enter your chosen location into an environment variable called LOCATION. Enter one of these commands:

```export LOCATION=US```

Or

```export LOCATION=EU```

Or

```export LOCATION=ASIA```

In Cloud Shell, the DEVSHELL_PROJECT_ID environment variable contains your project ID. Enter this command to make a bucket named after your project ID:
```gcloud storage buckets create -l $LOCATION gs://$DEVSHELL_PROJECT_ID```
![t3 - p4 - activating cloud shell](https://github.com/user-attachments/assets/fd6c66f0-1f04-4f36-88d8-39b121c443d0)


If prompted, click Authorize to continue.
![t3 - p5 - authorizing](https://github.com/user-attachments/assets/742e0c3c-1d05-48ce-a876-eb1243540c5a)


Retrieve a banner image from a publicly accessible Cloud Storage location:
```gcloud storage cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png```
Copied!
Copy the banner image to your newly created Cloud Storage bucket:
```gcloud storage cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png```
Copied!
Modify the Access Control List of the object you just created so that it's readable by everyone:
```gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png```
![t3 - p4 - last step](https://github.com/user-attachments/assets/37081780-940d-4865-a53a-667186865c1a)
