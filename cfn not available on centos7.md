I did pretty much the same things you outlined first...but found, I think, a much easier method.

This method is also great for multi-instance use as it creates your own RPM from their source rpm.
1. On any CentOS 7 machine, install rpm-build and if you want redhat-rpm-config (you may want to follow this doc: http://wiki.centos.org/HowTos/SetupRpmBuildEnvironment and might want to create the mockbuild user that the rpm looks for)

2. Either wget and install or just "rpm -ivh https://s3.amazonaws.com/cloudformation-examples/aws-cfn-bootstrap-latest.src.rpm" This will place a .spec file inside ~/rpmbuild/SPECS/aws-cfn-bootstrap.spec.

3. cd into or execute this with the whole path, "rpmbuild -ba aws-cfn-boostrap.spec"

4. This will create an rpm usable on any CentOS 7 instance

5. To install the rpm there are two dependencies, pystache and python-daemon both available in EPEL (yum -y install epel-release) so you can either install those then install the aws-cfn-bootstrap-1.4-0.el7.centos.noarch.rpm or simply do a "yum -y install aws-cfn-bootstrap-1.4-0.el7.centos.noarch.rpm" and it will grab the dependencies for you.

If you drop the rpm into an S3 bucket you can easily call this out in the UserData section of your CloudFormation script. You may need to adjust the permissions for this file.

The first couple lines of my UserData section look like this:
"UserData": {"Fn::Base64": {"Fn::Join": ["", [
"#!/bin/bash\n",
"yum -y install epel-release\n",
"yum -y install https://s3buckethere/aws-cfn-bootstrap-1.4-0.el7.centos.noarch.rpm\n",
"/opt/aws/bin/cfn-init -s ", {"Ref": "AWS::StackId"}, " -r EC2Instance --region ", {"Ref": "AWS::Region"}, "\n",

Hope that was helpful! I agree that the documentation on this is less than stellar!

Also, on CentOS 6 this rpm works https://s3.amazonaws.com/cloudformation-examples/aws-cfn-bootstrap-latest.amzn1.noarch.rpm but it uses Python 2.6 and CentOS 7 uses native Python 2.7 so that creates a problem. Also a problem with Cent6 is the marketplace AMI does not come pre-packaged with cloud-init.
