# ansible_ssl_expiry_check

This Ansible playbook creates a new user on the remote server and setups the scripts and cron jobs that check for a expiring SSL certificate. If a certificate expiration period is less than **30** days notifications will be sent to a Slack channel.

## Configure the Ansible playbook

You must define `slack_webhook` and `domains` as both variables are required.

Optionally configurable variables
* **ssl_port** - standard is 443,
* **ssl_expiry_days_check** - the script starts warning if certificate is expiring in less than this period,
* **cron_period_check** - how often the cron job should be run.

Example ``ansible_ssl_check.yml`` playbook .

````
---
- hosts: server_name
  roles:
    - user_group_directories
    - rvm
    - whenever
  vars:
    slack_webhook: "https://hooks.slack.com/services/xxxxxxx/xxxxxxx/xxxxxxxx"
    domains:
      - github.com
      - gitlab.com
````
If you want to test things out then change `ssl_expiry_days_check` to something high like **300**.

## Run the playbook

* Add the server to Ansible's inventory file and then run the command below.

````
ansible-playbook -i hosts ansible_ssl_check.yml
````
This command presumes the hosts inventory file is in the current directory.
