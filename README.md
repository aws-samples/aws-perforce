## Building Perforce Helix Core on the AWS Cloud

These AWS CloudFormation templates included with this sample deploy Perforce Helix Core on the AWS Cloud.

Perforce is a proprietary version control system that features fast synchronized operation. It’s used mainly in development environments and is particularly popular in the game industry.

Perforce and AWS also offer a free tier, Perforce Helix Core Studio Pack for AWS, which allows customers to start running Perforce on AWS. 

The templates automate either of the following:

* Deploy a single Perforce master server into a single availability zone of a new VPC
* Deploy Perforce master server and replica server for redundancy into different availability zones of a new VPC

You can also use the AWS CloudFormation templates as a starting point for your own implementation.

![Perforce-servers-architecture](/images/Perforce-servers-architecture.png)

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

The AWS CloudFormation templates download and setup Perforce Helix Core on EC2 instances during the process.
Helix Core is a proprietary software and is subject to the terms and conditions of Perforce. Please refer to EULA in the following page for details.
[Perforce Terms of Use](https://www.perforce.com/terms-use)


## Deployment
1. Sign in to the AWS console and click on Launch Stack below. This launches a CloudFormation stack in your AWS account. By default, the stack is launched in the us-west-2 (Oregon) region. If you want to launch it in a different region, change the region from the pull-down menu in the upper right corner of the management console.

[![Launch Stack](/images/launchstack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/template?stackName=AWSPerforceTest&templateURL=https://gametech-cfn-templates-public.s3.amazonaws.com/aws-perforce/templates/PerforceTemplateMain.yaml) 

2. On the Specify template page, keep the default setting for the template URL, and then choose Next.

3. On the Specify stack details page, change the stack name if needed. By default, the stack name is "AWSperforceTest". Review the parameters for the template. Especially provide the following items for the parameters that require input. For all other parameters, review the default settings and customize them as necessary. When you finish reviewing and customizing the parameters, choose Next.

* In VPC Network Configuration, Permitted IP range is configured to restrict access to the Perforce Server based on the source IPs. The default settings allow all IP addresses (0.0.0.0/0), but allowing only limited IP addresses is recommended for security reasons.

* Perforce Server Configuration allows you to specify the EC2 instance type of the Perforce Server. By default, c5.4xlarge is recommended for use in the production environment. However, it is not always appropriate to use for testing purposes, so choose [t3.nano] or [t3.micro] for tests, which have lower hourly rates. Please note that the t3 family is intended for use in the test environment and should not be used in the production environment.

* Select the SSH Key you use to log in to the instance from Key Pair Name. If you have not created an SSH key in advance, create a key pair in your preferred region.

* If you scroll down the Parameters screen, you will see the EBS volume configuration you want to set to the server, but do nothing and leave it as the default. However, some parameters have larger volume sizes by default, so you may set smaller sizes if you prefer to save costs. (For testing purposes, for example, 500GiB, the lowest volume size of st1 should be sufficient for Depot, and 8 GiB of storage should be sufficient for the others. )

* The setting “Enable Replica” is asking if you want to create a Perforce Replica Server. The default value is set to “No”, allowing to build only a Perforce Master Server. If you also need to build a Replica server, change this setting from the pull-down to “Yes”. (The additional procedure is requred to complete the replica setup. )

4. Click on Next to navigate to the “Configure stack options” page. No additional configuration is required here. (Add tags if necessary. )

5. Click on Next to navigate to review page. Scroll down to the bottom, and you will see check boxes in the “Capabilities” section. Check them all. Ensure to check all the check boxes. Click on “Create Stack”, and then the building process starts. It will take about 5-10 minutes to complete. When CREATE_COMPLETE is displayed, the building process is complete.
