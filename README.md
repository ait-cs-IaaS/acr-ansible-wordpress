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

### Misc

| Variable name                   | Type    | Default | Description                                             |
| ------------------------------- | ------- | ------- | ------------------------------------------------------- |
| wp_sys_user | string | 'www-data' | User owning the wordpress files on server |
| wp_sys_usergroup | string | 'www-data' | Usergroup owning the wordpress files on server |
| wp_cli_dir | string | '/usr/local/bin/wp-cli' | Path to the wp-cli installation |
| libapache2_mod_version | string | 'libapache2-mod-php7.0' | Passed to apach2 role. Use php7.2 for compatibility with Ubuntu 18.04 |


### Wordpress
These variables contain the admin user credentials, the Site Title, Tagline etc.

| Variable name                   | Type    | Default | Description                                             |
| ------------------------------- | ------- | ------- | ------------------------------------------------------- |
| wp_admin_name | string | 'admin' | Adminuser for e.g. wp-admin |
| wp_admin_email | string | 'admin@localhost.localdomain' | Admin contact email address |
| wp_admin_password | string | 'secret' | Password for admin login |
| wp_title | string | 'Team Site' | Title of wordpress page |
| wp_tagline | string | 'Informationsplatform' | Subtitle of wordpress page |
| wp_host | string | 'localhost' | wp-database location |
| wp_host_ip | string | (N/A) | IP address for wp-installation |
| wp_apache_hostname | string | 'team_site' | vhost name and foldername in /var/www |
| wp_apache_alias | string | 'www.team_site.com' | vhost alias |
| wp_path | string | '/var/www/{{ wp_apache_hostname }}' | Installation path to wordpress |


### wp-config
Variables required for the wp-config file.

| Variable name                   | Type    | Default | 
| ------------------------------- | ------- | ------- | 
| wp_mysqldb_user | string | 'wordpress_user' | 
| wp_mysqldb_password | string | 'secret' | 
| wp_mysqldb_dbname | string | 'wordpress_db' | 
| wp_mysqldb_host | string | 'localhost' | 
| wp_mysqldb_charset | string | 'utf8' | 
| wp_mysqldb_collate | string | (N/A) | 
| wp_auth_key | string | 'put your unique phrase here' | 
| wp_secure_auth_key | string | 'put your unique phrase here' | 
| wp_logged_in_key | string | 'put your unique phrase here' | 
| wp_nonce_key | string | 'put your unique phrase here' | 
| wp_auth_salt | string | 'put your unique phrase here' | 
| wp_secure_auth_salt | string | 'put your unique phrase here' | 
| wp_logged_in_salt | string | 'put your unique phrase here' | 
| wp_nonce_salt | string | 'put your unique phrase here' | 
| wp_table_prefix | string | 'wp_' | 
| wp_debug | string | 'false' | 


### Wordpress Content
These variables contain the content of the wordpress instance.

| Variable name                   | Type    | Default | Description                                             |
| ------------------------------- | ------- | ------- | ------------------------------------------------------- |
| wp_remove_samples | boolean | yes | If set to 'yes' the default example content of wordpress is removed |
| **wp_themes** | list |  | Wordpress themes to install |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name | string | 'fblogging' | Theme name | 
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .activate | boolean | true | If set it is activated after installation |
| **wp_plugins** | list |  | Wordpress plugins to install |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name | string | (N/A) | Plugin name | 
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .activate | boolean | true | If set it is activated after installation |
| **wp_users** | list |  | Users to create |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name | string | (N/A) | User login | 
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .displayname | string | (N/A) | User displayname |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .email | string | (N/A) | User email |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .password | string | (N/A) | User password |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .role | string | (N/A) | User role |
| **wp_users_update** | list |  | Users to update |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .id_id | string | (N/A) | Identify by ID *or* | 
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .id_name | string | (N/A) | Identify by name *or* |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .id_email | string | (N/A) | Identify by email |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .new_displayname | string | (N/A) | Updated displayname |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .new_email | string | (N/A) | Updated email |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .new_password | string | (N/A) | Updated password |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .new_role | string | (N/A) | Updated role |
| **wp_categories** | list |  | Wordpress categories to create |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name | string | (N/A) | Category name | 
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .description | string | (N/A) | Category description |
| **wp_posts** | list |  | Posts to create |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .title | string | (N/A) | Post title | 
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .author | string | (N/A) | User name or Id |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .category | string | (N/A) | Category name |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .date | string | (N/A) | Post date in format: 'yyyy-dd-mm hh:mm' |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .content | string | (N/A) | Content |



Dependencies
------------

This role utilizes two roles from [sct-cyberrange](https://git-service.ait.ac.at/sct-cyberrange/ansible-roles/):
- Role [apache2](git@git-service.ait.ac.at:sct-cyberrange/ansible-roles/apache2.git)
- Role [mariadb](git@git-service.ait.ac.at:sct-cyberrange/ansible-roles/mariadb.git)


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
