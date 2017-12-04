cloud-init is the tool that started as part of the Ubuntu AWS AMIs that allow the interpretation of the EC2 user-data component of the instance meta-data. Amazon Linux adopted this tool as well and built it into their AMI.

cfn-init is part of a different toolset called CloudFormation Helper Scripts created by AWS for Amazon Linux that can read an additional section named Metadata in your CloudFormation template.

So, Ubuntu and Amazon Linux AMIs both have the cloud-init tools preinstalled to access the user-data, but only Amazon Linux has the CloudFormation Helper Scripts preinstalled e.g. cfn-init to access the CloudFormation Metadata.
