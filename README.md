你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# terraform_cashier

[![Go Report Card](https://goreportcard.com/badge/github.com/Bjorn248/terraform_cashier)](https://goreportcard.com/report/github.com/Bjorn248/terraform_cashier)
[![Build Status](https://travis-ci.org/BjornTwitchBot/terraform_cashier.svg?branch=master)](https://travis-ci.org/BjornTwitchBot/terraform_cashier)
[![codecov](https://codecov.io/gh/BjornTwitchBot/terraform_cashier/branch/master/graph/badge.svg)](https://codecov.io/gh/BjornTwitchBot/terraform_cashier)

This uses [https://github.com/Bjorn248/graphql_aws_pricing_api](https://github.com/Bjorn248/graphql_aws_pricing_api) to get pricing data

Designed to analyze terraform template files and return a cost estimate of running the infrastructure, assuming AWS is the target cloud. Perhaps other clouds can be supported going forward?

**NOTE**: This only calculates the cost of EC2 and RDS resources right now. To add support for more resources, open a PR or leave a comment. I'm always looking for feedback.

This is very much in a prototype state right now. Any advice or assistance is appreciated.

## Plan File
This relies on terraform plan files generated using `terraform plan -out=<filename>`.
It is recommended that you plan against an empty state so that all of your resources
are present in the plan file.

### Empty/Blank state plan
If you are using remote state, you will need to disable this. I accomplish this by renaming the file that defines my remote state, appending the extension `.off`. Then, I have to run `terraform init` again to initialize a blank local state. Then I can generate a plan that contains all my resources using the following command `terraform plan -out=<filename> -refresh=false`.

## Environment Variables
Variable Name | Description
------------ | -------------
AWS_REGION | The Region for which you want to create a price estimation (e.g. `us-east-1`)
TERRAFORM_PLANFILE | Where cashier should find your terraform plan output.
RUNNING_HOURS | (Optional) The number of running hours normally used in a month for your resources, on average. Defaults to 730 assuming 24/7 operation.
PRINT_VERSION | (Optional) If `true` will print current version of cashier and exit

## Installation and usage
Simply download the latest release from the releases page here: [https://github.com/Bjorn248/terraform_cashier/releases](https://github.com/Bjorn248/terraform_cashier/releases)
Make sure that the binary is set executable
Set your environment variables appropriately
```
export TERRAFORM_PLANFILE="./terraform.plan"
export AWS_REGION="us-west-1"
```
And then run the `cashier` binary

If you wish to see the current version of cashier, use the following environment variable
```
PRINT_VERSION=true
```


## Local Development
This project uses [https://github.com/kardianos/govendor](https://github.com/kardianos/govendor) for dependency management.
Be sure to install all required dependencies to build this locally using `govendor sync`.
