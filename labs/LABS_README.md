

### ansible
usage of dynamic inventory - Get inventory hosts from AWS ec2 using `amazon.aws.aws_ec2` plugin
NOTE: need to specify correct ssh user (different for ubuntu AMI and amz AMI)

amsible cmd:
```sh
ansible -i labs/ansible/inventory.aws_ec2.yaml -m ping -u ec2-user all
```

`ec2.yaml` - CloudFormation prerequisite stack, creates two ec2 instances with custom SG


### s3-replication