<p align="center">
  <img src="https://github.com/terraform-aws-modules/terraform-aws-rds/blob/main/examples/intel-enhanced-mysql/logo-classicblue-800px.png?raw=true" alt="Intel Logo" width="250"/>
</p>

## Intel Enhanced Optimizations Example for RDS MySQL

This example showcases an Intel Enhanced Optimizations Example for RDS MySQL. The example includes: 

- Intel Xeon Instance Selection
- Intel Xeon MySQL Optimizations using parameter groups


## Intel Xeon Instances

We recommend  Intel Xeon 3rd Generation Scalable processors (code-named Ice Lake) instances
#### General Purpose: db.m6i.large, db.m6i.xlarge, db.m6i.2xlarge, db.m6i.4xlarge, db.m6i.8xlarge, db.m6i.12xlarge, db.m6i.16xlarge, db.m6i.24xlarge, db.m6i.32xlarge
#### Memory Optimized: db.r6i.large, db.r6i.xlarge, db.r6i.2xlarge, db.r6i.4xlarge, db.r6i.8xlarge, db.r6i.12xlarge, db.r6i.16xlarge, db.r6i.24xlarge, db.r6i.32xlarge
See more:
- https://aws.amazon.com/ec2/instance-types/m6i/
- https://aws.amazon.com/ec2/instance-types/r6i/

```hcl

  # Intel Instance selection
  instance_class       = "db.m6i.large"
```
## Intel Xeon MySQL Optimizations

The MySQL Optimizations were based off [Intel Xeon Tuning Guide](<https://www.intel.com/content/www/us/en/developer/articles/guide/open-source-database-tuning-guide-on-xeon-systems.html>)

We have included a new sub module that brings in all the optimizations from a stand alone module at <https://github.com/intel/terraform-intel-aws-mysql-parameter-group/>. Within the enhanced optimization code we have made a few updates.

## Usage

main.tf updates:

```hcl
################################################################################
# Intel Xeon MySQL Enhanced Parameter Group
################################################################################
# https://github.com/intel/terraform-intel-aws-mysql-parameter-group
# Intel Xeon Tuning Guide https://www.intel.com/content/www/us/en/developer/articles/guide/open-source-database-tuning-guide-on-xeon-systems.html

module "aws-mysql-parameter-group" {
  source  = "intel/aws-mysql-parameter-group/intel"
  version = "2.0.0"
}

... 

  ################################################################################
  # Intel
  ################################################################################
  # Intel based 6i Instances running Intel Xeon 3rd Generation Scalable processors (code-named Ice Lake) are recommended for optimal price/performance
  # General Purpose: db.m6i.large, db.m6i.xlarge, db.m6i.2xlarge, db.m6i.4xlarge, db.m6i.8xlarge, db.m6i.12xlarge, db.m6i.16xlarge, db.m6i.24xlarge, db.m6i.32xlarge
  # Memory Optimized: db.r6i.large, db.r6i.xlarge, db.r6i.2xlarge, db.r6i.4xlarge, db.r6i.8xlarge, db.r6i.12xlarge, db.r6i.16xlarge, db.r6i.24xlarge, db.r6i.32xlarge

  # Intel Instance selection
  instance_class       = "db.m6i.large"
  # Intel parameter group selection
  parameter_group_name = module.aws-mysql-parameter-group.db_parameter_group_name

```

## Usage

To run this example you need to execute:

```bash
terraform init
terraform plan
terraform apply
```

Note that this example may create resources which cost money. Run `terraform destroy` when you don't need these resources.

## Performance Data

<center>

#### [Process up to 1.33x more MySQL database transactions with the 3rd Generation Intel® Xeon® Scalable Processor (Ice Lake) vs. previous generation](https://www.intel.com/content/www/us/en/content-details/753185/book-up-to-1-42x-the-reservations-at-once-with-aws-ec2-m6i-instances-vs-aws-m5n-instances.html)

<p align="center">
  <a href="https://www.intel.com/content/www/us/en/content-details/753185/book-up-to-1-42x-the-reservations-at-once-with-aws-ec2-m6i-instances-vs-aws-m5n-instances.html">
  <img src="https://github.com/intel/terraform-intel-aws-mysql/blob/main/images/aws-mysql-1.png?raw=true" alt="Link" width="600"/>
  </a>
</p>

#

#### [Handle up to 1.32x more MySQL transactions per minute with AWS M6i 3rd Generation Intel® Xeon® Scalable Processor (Ice Lake) vs. previous generation](https://www.intel.com/content/www/us/en/content-details/752377/select-aws-ec2-m6i-instances-and-support-up-to-1-38x-the-ecommerce-transactions-for-mysql-databases-vs-aws-ec2-m5-instances.html)

<p align="center">
  <a href="https://www.intel.com/content/www/us/en/content-details/752377/select-aws-ec2-m6i-instances-and-support-up-to-1-38x-the-ecommerce-transactions-for-mysql-databases-vs-aws-ec2-m5-instances.html">
  <img src="https://github.com/intel/terraform-intel-aws-mysql/blob/main/images/aws-mysql-2.png?raw=true" alt="Link" width="600"/>
  </a>
</p>

#

#### [Get better price per performance($$/per) value by selecting Intel® Xeon® Scalable Processor vs. ARM](https://www.intel.com/content/www/us/en/content-details/765568/increase-mysql-database-transactions-by-1-65x-with-aws-ec2-m5-instances-vs-aws-ec2-m6g-instances.html)

<p align="center">
  <a href="https://www.intel.com/content/www/us/en/content-details/765568/increase-mysql-database-transactions-by-1-65x-with-aws-ec2-m5-instances-vs-aws-ec2-m6g-instances.html">
  <img src="https://github.com/intel/terraform-intel-aws-mysql/blob/main/images/aws-mysql-3.png?raw=true" alt="Link" width="600"/>
  </a>
</p>

#

#### [Process up to 1.18x more MySQL Transactions with AWS EC2 C5 Instances vs. AWS EC2 C5a Instances](https://www.intel.com/content/www/us/en/content-details/756027/process-up-to-1-18x-more-mysql-transactions-with-aws-ec2-c5-instances-vs-aws-ec2-c5a-instances.html)

<p align="center">
  <a href="https://www.intel.com/content/www/us/en/content-details/756027/process-up-to-1-18x-more-mysql-transactions-with-aws-ec2-c5-instances-vs-aws-ec2-c5a-instances.html">
  <img src="https://github.com/intel/terraform-intel-aws-mysql/blob/main/images/aws-mysql-4.png?raw=true" alt="Link" width="600"/>
  </a>
</p>

</center>
