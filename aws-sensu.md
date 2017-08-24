## Notes from monitoring AWS from Sensu Summit

Grafana has a CloudWatch plugin you can use to access the data directly rather than pulling to TSDB
data lags and by default is 5min aggregation.  Not generally very useful for granularity.
They’ve recently added some dashboarding but it’s not very good compared to Grafana

### Good practices/checks to implement:
  * Eric wrote a check all target groups in the region for ALB - https://github.com/sensu-plugins/sensu-plugins-aws/blob/master/bin/check-alb-target-group-health.rb
  * Check for instances that are impaired - https://github.com/sensu-plugins/sensu-plugins-aws/blob/master/bin/check-instance-health.rb
  * Reconfigure autoscale groups via handlers based on metrics - https://github.com/sensu-plugins/sensu-plugins-aws/blob/master/bin/handler-scale-asg-up.rb
  * gather info for billing purposes using billing data in cloudwatch
  * check for detached volumes/untagged instances/etc - https://github.com/sensu-plugins/sensu-plugins-aws/blob/master/bin/check-ec2-cpu_balance.rb
  * Checking for CPU credits is a good practice to avoid unexpected throttling affecting the application when something has gone off the rails.  Cloudwatch check is helpful for this as it can be exposed as a metric

### Building checks:
  * use SDKs but be aware of what version
  * https://github.com/sensu-plugins/sensu-plugins-aws
  * Build with config management tool so devs/ops can add a new ALB/EC2/whatever to a list and then iterate that list to build checks as needed

### Managing your AWS spend via monitoring:
  * anything that doesn’t have a tag is destroyed after 30mins
  * tags are used to do showback/chargeback to keep costs under control
  * can require tags
  * reaping is a good idea

Eric - cleanup in sensu/chef is often needed.  wrote aws-cleaner (https://github.com/eheydrick/aws-cleaner) which looks for termination events in cloudwatch and calls sensu API to remove the node

### Permissions:
checks used to pass keys via commandline (not very secure!), now SDKv2 is somewhat better.  Recommend creating an IAM role with readonly to everything and run sensu on an EC2 instance with this role so it doesn’t need to pass credentials around where they might be exposed.

### Dealing with non-EC2 non-agent monitoring automation:
  * Some people parse Terraform state file to pull info out about what checks you might need v2.0 may have a Terraform provider that will help with this?
