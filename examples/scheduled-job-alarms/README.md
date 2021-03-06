**Note**: This public repo contains the documentation for the private GitHub repo <https://github.com/gruntwork-io/module-aws-monitoring>.
We publish the documentation publicly so it turns up in online searches, but to see the source code, you must be a Gruntwork customer.
If you're already a Gruntwork customer, the original source for this file is at: <https://github.com/gruntwork-io/module-aws-monitoring/blob/master/examples/scheduled-job-alarms/README.md>.
If you're not a customer, contact us at <info@gruntwork.io> or <http://www.gruntwork.io> for info on how to get access!

# Scheduled Job Alarms

This is an example of how to create an alarm that goes off if a scheduled job (e.g. a cron job) fails to run, using the
following modules:

* [scheduled-job-alarms](/modules/alarms/scheduled-job-alarms): This module creates an alarm that goes off if a
  specified metric drops below a specified threshold over a specified time period. This is most useful for detecting if
  a scheduled job (e.g. a cron job) failed.

## Quick start

To try these templates out you must have Terraform installed (minimum version: `0.6.11`):

1. Open `vars.tf`, set the environment variables specified at the top of the file, and fill in any other variables that
   don't have a default.
1. Run `terraform get`.
1. Run `terraform plan`.
1. If the plan looks good, run `terraform apply`.

## How do I get notifications from these alarms?

This example configures the CloudWatch alarms to send notifications to an [SNS](https://aws.amazon.com/sns/) topic
whenever the state of the alarm changes. You can subscribe to this topic to receive notifications via email and/or
SMS:

1. When you run `terraform apply`, or, later, if you run `terraform output`, the name and ARN of this topic will be
   outputted to the console.
2. Login to the [SNS console](https://console.aws.amazon.com/sns/v2/home).
3. Click the "Topics" link in the menu on the left.
4. Find the topic with the name and ARN from step 1 in the list and click the checkbox next to it.
5. Click the "Actions" button and select "Subscribe to Topic".
6. Choose "Email" or "SMS Message" as the protocol, enter your email or phone number, and click "Create Subscription".
7. AWS will email or message you to confirm the subscription. Be sure to confirm it, or you won't receive any
   notifications, and the alarm will report its status as `INSUFFICIENT_DATA`!