# Settiong up CloudWatch Agent

## Create an EC2 Role

Create an EC2 role with the following policies

```
CloudWatchAgentServerPolicy
AmazonSSMFullAccess 
```

## Install Agent

* wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
* sudo rpm -U ./amazon-cloudwatch-agent.rpm
* sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
* Accept all defaults, until default metrics .. pick advanced.
* sudo mkdir -p /usr/share/collectd/
* sudo touch /usr/share/collectd/types.db

## Load Config and start agent

* sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c ssm:AmazonCloudWatch-linux -s
