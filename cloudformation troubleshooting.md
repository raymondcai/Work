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
