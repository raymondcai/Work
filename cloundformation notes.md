A template is a JSON or YAML text file that contains the configuration information about the AWS resources you want to create in the stack. For this walkthrough, the sample template includes six top-level sections: AWSTemplateFormatVersion, Description, Parameters, Mappings, Resources, and Outputs; however, only the Resources section is required.

RESOURCES: The Resources section contains the definitions of the AWS resources you want to create with the template.

PARAMETERS: You use the Parameters section to declare values that can be passed to the template when you create the stack. A parameter is an effective way to specify sensitive information, such as user names and passwords, that you don't want to store in the template itself.

MAPPINGS: In the template, you'll also find a Mappings section. You use mappings to declare conditional values that are evaluated in a similar manner as a lookup table statement. The template uses mappings to select the correct Amazon machine image (AMI) for the region and the architecture type for the instance type.



cloudformation init is desired state, similar to cloud-init, it is declarative.

"sources" : {
  "/var/www/html" : "http://wordpress.org/latest.tar.gz"
}
  download from url, put it into /var/www/html. no need to worry aobut tar extraction etc.



Need to pay attention to metadata under cloudformation init and ec2 user-data.

"Properties": {
        "ImageId" : { "Fn::FindInMap" : [ "AWSRegionArch2AMI", { "Ref" : "AWS::Region" },
                          { "Fn::FindInMap" : [ "AWSInstanceType2Arch", { "Ref" : "InstanceType" }, "Arch" ] } ] },
        "InstanceType"   : { "Ref" : "InstanceType" },
        "SecurityGroups" : [ {"Ref" : "WebServerSecurityGroup"} ],
        "KeyName"        : { "Ref" : "KeyName" },
        "UserData" : { "Fn::Base64" : { "Fn::Join" : ["", [
                       "#!/bin/bash -xe\n",
                       "yum update -y aws-cfn-bootstrap\n",

                       "/opt/aws/bin/cfn-init -v ",
                       "         --stack ", { "Ref" : "AWS::StackName" },
                       "         --resource WebServer ",
                       "         --configsets wordpress_install ",
                       "         --region ", { "Ref" : "AWS::Region" }, "\n",

                       "/opt/aws/bin/cfn-signal -e $? ",
                       "         --stack ", { "Ref" : "AWS::StackName" },
                       "         --resource WebServer ",
                       "         --region ", { "Ref" : "AWS::Region" }, "\n"
        ]]}}
      },


  "mode"  : "000400", first 3 digis are for symlink, last 3 are permission.
