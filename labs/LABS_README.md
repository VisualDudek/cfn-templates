

### ansible
deploy CloudFormation stack:
```sh
rain deploy labs/ansible/ec2{-xx}.yaml
```

usage of dynamic inventory - Get inventory hosts from AWS ec2 using `amazon.aws.aws_ec2` plugin
NOTE: need to specify correct ssh user (different for ubuntu AMI and amz AMI) manually or use ec2 tags

ansible inline cmd:
```sh
ansible -i labs/ansible/inventory.aws_ec2.yaml -m ping -u ec2-user all
```

`ec2.yaml` - CloudFormation prerequisite stack, creates two ec2 instances with custom SG, provide correct key pair name and make sure that exist in your region.

Versions:
`ec2-01.yaml` - using imported key pair, `Type: AWS::EC2::KeyPair`. Provide your pub key.

`ec2-02.yaml` - Add `login_name` tag `{ubuntu|ec2-user}`


`play_02.yaml` - playbook with ping task, utilize dynamic SSH User from ec2 tags

run playbook:
```sh
ansible-playbook -i labs/ansible/inventory.aws_ec2.yaml labs/ansible/play_02.yaml -v
```

get dynamic inventory info:
```sh
ansible-inventory -i labs/ansible/inventory.aws_ec2.yaml --list
```

`invnetory.aws_ec2.yaml` - file must end with `aws_ec2.{yml|yaml}`. Provide correct region


### interface
Overall, this template excerpt sets up a simple infrastructure for a Lambda function that requires access to an SSM parameter. The `Metadata` section provides a user-friendly interface for setting the `DatabaseUsername` parameter, and the `Parameters` section defines the parameter itself. The `Resources` section defines the SSM parameter and IAM role needed for the Lambda function to access the parameter.


### s3-replication
This CloudFormation template creates two S3 buckets and an IAM role. The first bucket, `SourceBucket`, is configured with versioning and replication to the second bucket, `DestinationBucket`. The replication is defined by a replication rule that replicates all objects in the bucket. The IAM role, `ReplicationRole`, is used by the replication configuration to grant permissions to replicate objects between the two buckets. Additionally, the policy for the `ReplicationRole` is defined in a separate resource, `BucketBackupPolicy`.

Overall, this template sets up a simple replication configuration between two S3 buckets and creates the necessary IAM role and policy to enable the replication.