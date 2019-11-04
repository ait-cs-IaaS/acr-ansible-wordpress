wordpress
=========

This role installs and configures wordpress and adds content defined in the vars file. 

Requirements
------------

This role utilizes two roles from [sct-cyberrange](https://git-service.ait.ac.at/sct-cyberrange/ansible-roles/). These two requirements are defined in the **requirements.yml** file and can be installed via:

```console
$ ansible-galaxy install -r requirements.yml
```

Role Variables
--------------

There are four sections of variables:
- Misc
- Wordpress
- wp-config
- Wordpress Content 

## Misc

| Variable name                   | Type    | Default | Description                                             |
| ------------------------------- | ------- | ------- | ------------------------------------------------------- |
| wp_sys_user | string | www-data | User owning the wordpress files on server |
| wp_sys_usergroup | string | www-data | Usergroup owning the wordpress files on server |
| wp_cli_dir | string | /usr/local/bin/wp-cli | Path to the wp-cli installation |
| libapache2-mod-version | string | libapache2-mod-php7.0 | Passed to apach2 role. Use php7.2 for compatibility with Ubuntu 18.04 |


Dependencies
------------

This role utilizes two roles from [sct-cyberrange](https://git-service.ait.ac.at/sct-cyberrange/ansible-roles/):
- [apache2](git@git-service.ait.ac.at:sct-cyberrange/ansible-roles/apache2.git)
- [mariadb](git@git-service.ait.ac.at:sct-cyberrange/ansible-roles/mariadb.git)


Example Playbook
----------------

```yaml
- hosts: 
  - wordpress

  vars:
    ansible_become: yes
    ansible_become_pass: <password>

  roles:  
    - wordpress
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
