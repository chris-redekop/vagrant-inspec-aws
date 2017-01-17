# vagrant-inspec-aws

## Steps required before `vagrant up`:
1. copy **ssh/config.sample** to **ssh/config**
1. copy your GitHub SSH keys to **ssh/** _and make sure **ssh/config** references them_
1. copy **etc/aws-vars.sample** to **etc/aws-vars** _and set your API keys_

## Steps required after `vagrant up`:
1. `$ vagrant ssh`
1. `$ inspec exec inspec-aws`
