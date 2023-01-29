Objectives

* Create an Amazon SNS notification
* Configure a CloudWatch alarm
* Stress test an EC2 instance
* Confirm that an Amazon SNS email was sent
* Create a CloudWatch dashboard

Pre-create EC2 instance with the below user data
```
#!/bin/bash -ex
yum -y update
amazon-linux-extras install epel -y
yum install stress -y
```
Task 1: Configure Amazon SNS

* In the AWS Management Console, enter SNS in the search bar, and then choose Simple Notification Service.

* On the left, choose the button, choose Topics, and then choose Create topic.

* On the Create topic page in the Details section, configure the following options:

 Type: Choose Standard.
 Name: Enter MyCwAlarm 

* Choose Create topic.

* On the MyCwAlarm details page, choose the Subscriptions tab, and then choose Create subscription.

* On the Create subscription page in the Details section, configure the following options:

 Topic ARN: Leave the default option selected.
 Protocol: From the dropdown list, choose Email.
 Endpoint: Enter a valid email address that you can access.

* Choose Create subscription. 

  In the Details section, the Status should be Pending confirmation. You should have 
  received an AWS Notification - Subscription Confirmation email message at the email 
  address that you provided in the previous step.

* Go back to the AWS Management Console. In the left navigation pane, choose Subscriptions.
 The Status should now be  Confirmed.

Task 2: Create a CloudWatch alarm

View some metrics and logs stored within CloudWatch. You then create a CloudWatch alarm to initiate and send an email to your SNS topic if the Stress Test EC2 instance increases to more than 60 percent CPU utilization.

* In the AWS Management Console, enter Cloudwatch in the search  bar, and then choose it.

* In the left navigation pane, choose the  Metrics dropdown list, and then choose All metrics.

* CloudWatch usually takes 5-10 minutes after the creation of an EC2 instance to start fetching metric details.

* On the Metrics page, choose EC2, and choose Per-Instance Metrics.

* From this page, you can view all the metrics being logged and the specific EC2 instance for the metrics.

* Select the check box with CPUUtilization as the Metric name for the Stress Test EC2 instance.

 select -> Stress Test  -> CPUUtilization

* In the left navigation pane, choose the Alarms dropdown list, and then choose All alarms.

* Choose Create alarm.

* Choose Select metric, choose EC2, and then choose Per-Instance Metrics.

* Select the check box with CPUUtilization as the Metric name for the Stress Test instance name.

* Choose Select metric.

* On the Specify metric and conditions page, configure the following options:
  **Metric**
  Metric name: Enter CPUUtilization
  InstanceId: Leave the default option selected.
  Statistic: Enter Average
  Period: From the dropdown list, choose 1 minute.

 **Conditions**
 Threshold type: Choose Static.
 Whenever CPUUtilization is...: Choose Greater > threshold.
 than... Define the threshold value: Enter 60

* Choose Next.

* On the Configure actions page, configure the following options:

**Notification**
 Alarm state trigger: Choose In alarm.
 Select an SNS topic: Choose Select an existing SNS topic.
 Send a notification to...: Choose the text box, and then choose MyCwAlarm.

* Choose Next, and then configure the following options:

**Name and description**

* Alarm name: Enter LabCPUUtilizationAlarm
* Alarm description - optional: Enter CloudWatch alarm for Stress Test EC2 instance CPUUtilization

* Choose Next

* Review the Preview and create page, and then choose Create alarm.

Task 3: Test the Cloudwatch alarm

The Stress Test EC2 instance and run a command that stresses the CPU load to 100 percent. This increase in CPU utilization activates the CloudWatch alarm, which causes Amazon SNS to send an email notification to the email address associated with the SNS topic.

* Connect the EC2 Instance from Session manager - Connect

In the terminal

* To manually increase the CPU load of the EC2 instance, run the following command:

```
sudo stress --cpu 10 -v --timeout 400s

```
* Run the following command

```
top
```
* Navigate back to the AWS console where you have the CloudWatch Alarms page open.

* Choose LabCPUUtilizationAlarm.

* Monitor the graph while selecting the refresh button every 1 minute until the alarm status is In alarm.

  It takes a few minutes for the alarm status to change to In alarm and for an email to 
   send.
  On the graph, you can see where CPUUtilization has increased above the 60 percent 
   threshold.

* Navigate to your email inbox for the email address that you used to configure the Amazon SNS subscription. You should see a new email notification from AWS Notifications.

Task 4: Create a CloudWatch dashboard
 CloudWatch dashboards to create customized views of the metrics and alarms for your AWS resources.

* Go to the CloudWatch section in the AWS console. In the left navigation pane, choose Dashboards.

* Choose Create dashboard.

* For Dashboard name, enter LabEC2Dashboard and then choose Create dashboard.

* Choose Line.

* Choose Metrics.

* Choose EC2, and then choose Per-Instance Metrics.

* Select the check box with Stress Test for the Instance name and CPUUtilization for the Metric name.

* Choose Create widget.

* Choose Save dashboard.



