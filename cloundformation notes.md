A template is a JSON or YAML text file that contains the configuration information about the AWS resources you want to create in the stack. For this walkthrough, the sample template includes six top-level sections: AWSTemplateFormatVersion, Description, Parameters, Mappings, Resources, and Outputs; however, only the Resources section is required.

RESOURCES: The Resources section contains the definitions of the AWS resources you want to create with the template.

PARAMETERS: You use the Parameters section to declare values that can be passed to the template when you create the stack. A parameter is an effective way to specify sensitive information, such as user names and passwords, that you don't want to store in the template itself.

MAPPINGS: In the template, you'll also find a Mappings section. You use mappings to declare conditional values that are evaluated in a similar manner as a lookup table statement. The template uses mappings to select the correct Amazon machine image (AMI) for the region and the architecture type for the instance type.



cloudformation init is desired state

"sources" : {
  "/var/www/html" : "http://wordpress.org/latest.tar.gz"
}
cfn-init will download from url, put it into /var/www/html. no need to worry aobut tar extraction etc.

for ASG, you can either use existing EC2 instnace or use launch configuration.

Type: "AWS::AutoScaling::AutoScalingGroup"
Properties:
  AvailabilityZones:
    - String
  Cooldown: String
  DesiredCapacity: String
  HealthCheckGracePeriod: Integer
  HealthCheckType: String
  InstanceId: String
  LaunchConfigurationName: String
  LifecycleHookSpecificationList:
    - LifecycleHookSpecification
  LoadBalancerNames:
    - String
  MaxSize: String
  MetricsCollection:
    - MetricsCollection
  MinSize: String
  NotificationConfigurations:
    - NotificationConfiguration
  PlacementGroup: String
  Tags:
    - TagProperty
  TargetGroupARNs:
    - String
  TerminationPolicies:
    - String
  VPCZoneIdentifier:
    - String


cfn-signal

cfn-signal --success|-s signal.to.send \
        --access-key access.key \
        --credential-file|-f credential.file \
        --exit-code|-e exit.code \
        --http-proxy HTTP.proxy \
        --https-proxy HTTPS.proxy \
        --id|-i unique.id \
        --region AWS.region \
        --resource resource.logical.ID \
        --role IAM.role.name \
        --secret-key secret.key \
        --stack stack.name.or.stack.ID \
        --url AWS CloudFormation.endpoint
