**Step 1: Choose an Amazon Machine Image (AMI)**

 * Choose the Amazon Linux 2 AMI (at the top), click Select.

**Step 2: Choose an Instance Type**

 * Select  t3.micro
 * Click Next: Configure Instance Details

**Step 3: Configure Instance Details**

* Configure these settings:

*   Network: Lab VPC
*   Subnet: Public Subnet
*   Click Next: Add Storage

**Step 4: Add Storage**

* You will use the default disk size, so no changes are required.

* Click Next: Add Tags

**Step 5: Add Tags**

* Tags allow you to categorize your AWS resources in different ways, such as by purpose, owner, or environment. 

* Click Add Tag then configure:

Key: Name
Value: Web Server
This name will appear on the instance in the EC2 management console.

* Click Next: Configure Security Group

**Step 6: Configure Security Group**

* Configure these settings:

Security group name: Web security group
Select Add rule and configure the rule with the following settings:
 Type: HTTP
 Source: Anywhere-IPv4

**Step 7: Configuring advanced details**

* Expand the Advanced details pane.
* Copy the following commands, and paste them into the User data text box.

```bash
#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Web Server!</h1></html>' > /var/www/html/index.html
```

The script does the following:

Install an Apache web server (httpd)
Configure the web server to automatically start on boot
Activate the Web server
Create a simple web page

**Step 8: Review Instance Launch**

* Click Launch

* In the Key pair (login) pane, select Proceed without a key pair (Not recommended).

* Select  I acknowledge ....
 
* Click Launch Instances

The Web Server will appear in a pending state, which means it is being launched. It will then change to running, which indicates that the instance has started booting.

* Wait for the Instance State to change to running.

 Instance State:  Running
 Status Checks:   2/2 checks passed

**Step 9:Access the Web Server**

* Select the instance by checking the box and selecting the Details tab.

* Copy the Public IPv4 address of your instance to your clipboard.

* Open a new tab in your web browser, paste the IP address you just copied, then press Enter.

* You should see the message Hello From Your Web Server!
