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
| **_name_** | _This is the human-readable name of the queue_ | _string_ | **_Required_** |
| **_visibility\_timeout\_seconds_** | _The visibility timeout for the queue_ | _number_ | **_Optional (Default - 30)_** |
| **_message\_retention\_seconds_** | _The number of seconds Amazon SQS retains a message_ | _number_ | **_Optional (Default - 345600)_** |
| **_max\_message\_size_** | _The limit of how many bytes a message can contain_ | _number_ | **_Optional (Default - 262144)_** |
| **_delay\_seconds_** | _The time in seconds that the delivery_ | _number_ | **_Optional (Default - 0)_** |
| **_receive\_wait\_time\_seconds_** | _The time for which a ReceiveMessage call_ | _number_ | **_Optional (Default - 0)_** |
| **_policy_** | _The JSON policy for the SQS queue_ | _string_ | **_Optional (Default - null)_** |
| **_redrive\_policy_** | _The JSON policy to set up the Dead Letter Queue_ | _string_ | **_Optional (Default - null)_** |
| **_fifo\_queue_** | _Boolean designating a FIFO queue_ | _bool_ | **_Optional (Default - false)_** |
| **_content\_based\_deduplication_** | _Enables content-based deduplication for FIFO queues_ | _bool_ | **_Optional (Default - false)_** |
| **_kms_master\_key\_id_** | _The ID of an AWS-managed customer master key_ | _string_ | **_Optional (Default - null)_** |
| **_kms\_data\_key\_reuse\_period\_seconds_** | _The length of time, in seconds_ | _number_ | **_Optional (Default - 300)_** |
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