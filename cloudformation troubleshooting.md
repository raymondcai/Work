2017-12-01 22:22:02,176 [ERROR] Error encountered during build of config: File specified with non-absolute path: commands
Traceback (most recent call last):
  File "/usr/lib/python2.7/dist-packages/cfnbootstrap/construction.py", line 542, in run_config
    CloudFormationCarpenter(config, self._auth_config).build(worklog)
  File "/usr/lib/python2.7/dist-packages/cfnbootstrap/construction.py", line 251, in build
    changes['files'] = FileTool().apply(self._config.files, self._auth_config)
  File "/usr/lib/python2.7/dist-packages/cfnbootstrap/file_tool.py", line 99, in apply
    raise ToolError('File specified with non-absolute path: %s' % filename)
ToolError: File specified with non-absolute path: commands
2017-12-01 22:22:02,176 [ERROR] -----------------------BUILD FAILED!------------------------
2017-12-01 22:22:02,179 [ERROR] Unhandled exception during build: File specified with non-absolute path: commands


"VpcId" : {
  "Type" : "AWS::EC2::VPC::Id",
  "Description" : "VpcId of your existing Virtual Private Cloud (VPC)",
  "ConstraintDescription" : "must be the VPC Id of an existing Virtual Private Cloud."
},

"Subnets" : {
  "Type" : "List<AWS::EC2::Subnet::Id>",
  "Description" : "The list of SubnetIds in your Virtual Private Cloud (VPC)",
  "ConstraintDescription" : "must be a list of at least two existing subnets associated with at least two different availability zones. They should be residing in the selected Virtual Private Cloud."
},
