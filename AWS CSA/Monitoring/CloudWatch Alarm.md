Alarms are used to trigger notifications for any metric. Options like sampling, percentage, max, min...

Alarm States: OK, INSUFFICIENT_DATA, ALARM

For example, you can set an alarm that triggers when CPU util is >95%. Then, you can trigger a reboot of the EC2 instance and an auto scaling action. You can also send a notification to your email.
#### CloudWatch Alarm Targets
- EC2 instances: Stop, terminate, reboot, recover
- Auto Scaling: Trigger auto scaling action of EC2
- SNS: Send notification to SNS (which then you can use for anything)

### Composite Alarms
Normally, alarms are on single metric. If you want multiple metrics, you should use composite alarm, which monitors multiple metrics. You can use AND and OR conditions