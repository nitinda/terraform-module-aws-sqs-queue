# _Terraform Module: terraform-module-aws-sqs-queue_
_Terraform module for **AWS SQS Queue**_

## _General_

_This module can be used to deploy a_ _**SQS Queue** on **AWS** Cloud Provider......_


---

## _Prerequisites_

_This module needs **Terraform 0.12.20** or newer._
_You can download the latest Terraform version from_ [_here_](https://www.terraform.io/downloads.html).



---

## _Features Branches_

_Below we are able to check the resources that are being created as part of this module call:_

- _**SQS Queue**_


---

## _Usage_

## _Using this repo_

_To use this module, add the following call to your code:_

* **_Example Usage_**

```tf
module "sqs_queue" {
  source = "git::https://github.com/nitinda/terraform-module-aws-sqs-queue.git?ref=master"

  providers = {
    aws = aws.services
  }

  # Tags
  tags = {
    Project      = "POC"
    Owner        = "Platform Team"
    Environment  = "prod"
    BusinessUnit = "Platform Team"
    ManagedBy    = "Terraform"
    Application  = "RDS Cluster Parameter Group"
  }

  # SQS Queue
  name                      = "terraform-example-queue"
  delay_seconds             = 90
  max_message_size          = 2048
  message_retention_seconds = 86400
  receive_wait_time_seconds = 10
  redrive_policy            = jsonencode({
    deadLetterTargetArn = aws_sqs_queue.terraform_queue_deadletter.arn
    maxReceiveCount     = 4
  })
}
```

* **_Example : FIFO queue_**

```tf
module "sqs_queue" {
  source = "git::https://github.com/nitinda/terraform-module-aws-sqs-queue.git?ref=master"

  providers = {
    aws = aws.services
  }

  # Tags
  tags = {
    Project      = "POC"
    Owner        = "Platform Team"
    Environment  = "prod"
    BusinessUnit = "Platform Team"
    ManagedBy    = "Terraform"
    Application  = "RDS Cluster Parameter Group"
  }

  # SQS Queue
  name                        = "terraform-example-queue.fifo"
  fifo_queue                  = true
  content_based_deduplication = true
}
```

- **_Example : Server-side encryption (SSE)_**

```tf
module "sqs_queue" {
  source = "git::https://github.com/nitinda/terraform-module-aws-sqs-queue.git?ref=master"

  providers = {
    aws = aws.services
  }

  # Tags
  tags = {
    Project      = "POC"
    Owner        = "Platform Team"
    Environment  = "prod"
    BusinessUnit = "Platform Team"
    ManagedBy    = "Terraform"
    Application  = "RDS Cluster Parameter Group"
  }

  # SQS Queue
  name                              = "terraform-example-queue"
  kms_master_key_id                 = "alias/aws/sqs"
  kms_data_key_reuse_period_seconds = 300
}
```

---

## _Inputs_

_The variables required in order for the module to be successfully called from the deployment repository are the following:_

|**_Variable_** | **_Description_** | **_Type_** | **_Argument Comments_** |
|:----|:----|-----:|:---:|
| **_tags_** | _Resource tags_ | _map(string)_ | **_Required_** |


---


## _Outputs_

### _General_

_This module has the following outputs:_

* **_id_**
* **_arn_**


### _Usage_

_In order for the variables to be accessed at module level please use the syntax below:_

```tf
module.<module_name>.<output_variable_name>
```


_The output variable is able to be accessed through terraform state file using the syntax below:_

```tf
data.terraform_remote_state.<layer_name>.<output_variable_name>
```

---



## _Authors_

_Module maintained by Module maintained by the -_ **_Nitin Das_**