https://www.tikalk.com/java/AWSCloudformation/

Debugging

The hard part is how do you know what went wrong with your script?

Cloud formation itself writes a log file on the machine in the /var/log directory. But it does not write the output from the user data file.

To do this you need to do it yourself. There are some options that you can find at ec2-user-data-output. The solution is used in the end is:

#!/bin/bash -ex
exec > >(tee /var/log/user-data.log|logger -t user-data -s 2>/dev/console) 2>&1
# Echoes all commands before executing.
set -o verbose
