# Ansible Logrotate
[![CI](https://github.com/supertarto/ansible-logrotate/workflows/CI/badge.svg?event=push)](https://github.com/supertarto/ansible-logrotate/actions?query=workflow%3ACI)

Install and configure logrotate with Ansible

## Requirements
None

## Tested plateform
* Debian 10 (Buster)

## Role variables
The path of your custom scripts.
```yml
logrotate_conf_dir: "/etc/logrotate.d/"
```
List of scripts to remove. For example, /etc/logrotate.d/rsyslog
```yml
logrotate_scripts_to_remove: []
```
This variable is used to configure custom scripts. 
 - **name**: Define the name of the file
 - **paths**: List of paths for the log rotation
 - **options**: List of directives to apply. Optionnal
 - **scripts**: Dictionnary of script to apply. Optionnal 
```yml
logrotate_scripts: []
# Exemple
#  - name: mail
#    paths:
#      - "/var/log/mail/mail.info"
#      - "/var/log/mail/mail.warn"
#      - "/var/log/mail/mail.err"
#    options:
#      - "rotate 52"
#      - "weekly"
#      - compress
#    scripts:
#      postrotate: invoke-rc.d rsyslog rotate > /dev/null
```

## Examples
```yml
hosts: all
roles:
    - role: supertarto.logrotate

vars:
    - name: mail
      paths:
        - "/var/log/mail/mail.info"
        - "/var/log/mail/mail.warn"
        - "/var/log/mail/mail.err"
      options:
        - "rotate 52"
        - "weekly"
        - "compress"
      scripts:
        postrotate: invoke-rc.d rsyslog rotate > /dev/null
```
## Installation
```
ansible-galaxy install supertarto.logrotate
```
## License
GPL V3.0
