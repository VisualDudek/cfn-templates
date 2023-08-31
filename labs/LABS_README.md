

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


### s3-replication