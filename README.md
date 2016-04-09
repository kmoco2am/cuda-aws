# cuda-aws

* Create new `env.sh` with proper EC2 information (`env.sh.template` can be used for easier setup)

:warning: This script creates `g2.large` machine in EC2 which is paid!

```
source env.sh
vagrant up
vagrant reload # to restart the box after provisioning
```
