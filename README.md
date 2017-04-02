# terraform_cashier

[![Go Report Card](https://goreportcard.com/badge/github.com/Bjorn248/terraform_cashier)](https://goreportcard.com/report/github.com/Bjorn248/terraform_cashier)

Designed to analyze terraform template files and return a cost estimate of running the infrastructure, assuming AWS is the target cloud. Perhaps other clouds can be supported going forward?

This is very much in a prototype state right now. Any advice or assistance is appreciated.

## Environment Variables
Variable Name | Description
------------ | -------------
AWS_REGION | The Region for which you want to create a price estimation (e.g. `us-east-1`)
GLOB_PATTERN | (Optional) Where cashier should find your terraform files (e.g. `*.tf`) Defaults to `*.tf`
