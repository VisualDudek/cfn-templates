

## TODO
1. ~~find json -> yaml converter~~
2. Try `rain`
3. From aws workshop check following:
    - github pr template
    - github issue template
    - github workflows
    - makefile
    - pre-commit-comfig
    - docs/LOCAL_DEVELOPMENT.md

## Discussion

All top-lvl objects in yaml template are optional.
Structure of template

Metadata -> `AWS::CloudFormation::Interface` defines how parameters are grouped and sorted in the AWD CloudFormation console.
NOTE: only console uses Interface metadata key. CLI and API calls don't use this key. 

**Parameters** define in `Parameters` block and use via `!Ref` -> intrinsic function (other e.g. `!Join`, `!Sub`)
Can acces public parameters stored in SSM parameter store or store priv parameters.

list parameters stored in SSM Parameter Store:
```sh
aws ssm describe-parameters
```

**Intrinsic functions**

*Fn::Ref* - 

*Fn::Join* - manipulate strings, usecase -> tags


## Convert templates between JSON and YAML
**NOTICE** Template Flip is now *depricated.*
Use [rain](https://github.com/aws-cloudformation/rain) instead.
`rain fmt` can convert between JSON and YAML

`rain` - development workflow tool for working with AWS CloudFormation
Place binary into `/usr/local/bin/`
```bash
sudo cp rain /usr/local/bin/
```

```bash
rain info
rain deploy s3.yaml
rain cat s3
rain ls
rain ls -a s3
```

## `cfn-lint`
[github](https://github.com/aws-cloudformation/cfn-lint)

NOTE: VSCode do not read `.cfnlintrc.yaml` config file. It works form cli but not in problems window.

run in debug mode from CLI:
```bash
cfn-lint -D templates/s3.yaml
```

## Serverless Rules
Serverless Rules are a compilation of rules to validate infrastructure-as-code template against recommended practices. This currently provides a module for cfn-lint and a plugin for tflint.
[link](https://awslabs.github.io/serverless-rules/)


## VSCode CloudFormation Linter
[link](https://marketplace.visualstudio.com/items?itemName=kddejong.vscode-cfn-lint)


