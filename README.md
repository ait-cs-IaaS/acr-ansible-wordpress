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

| Variable name          | Type   | Default                 | Description                                                           |
| ---------------------- | ------ | ----------------------- | --------------------------------------------------------------------- |
| wp_sys_user            | string | 'www-data'              | User owning the wordpress files on server                             |
| wp_sys_usergroup       | string | 'www-data'              | Usergroup owning the wordpress files on server                        |
| wp_cli_dir             | string | '/usr/local/bin/wp-cli' | Path to the wp-cli installation                                       |
| libapache2_mod_version | string | 'libapache2-mod-php7.0' | Passed to apach2 role. Use php7.2 for compatibility with Ubuntu 18.04 |

### Apache Config

| Variable name           | Type   | Default                 | Description                                                                |
| ----------------------- | ------ | ----------------------- | -------------------------------------------------------------------------- |
| wp_apache_hostname      | string | 'team_site'             | vhost name and foldername in /var/www                                      |
| wp_apache_alias         | string | 'www.team_site.com'     | vhost alias                                                                |
| wp_apache_ssl           | bool   | False                   | Activate HTTPS for this wordpress instance                                 |
| wp_apache_ssl_cert      | path   | 'ssl-cert-snakeoil.pem' | The source path of the ssl certificate file                                |
| wp_apache_ssl_key       | path   | 'ssl-cert-snakeoil.key' | The source path of the ssl certificates key file                           |
| wp_apache_ssl_copycerts | bool   | False                   | Flag to control if certificate and key should be copied to the target host |
| wp_apache_ssl_cert_path | path   | '/etc/ssl/certs'        | The base directory for certificates on the host                            |
| wp_apache_ssl_key_path  | path   | '/etc/ssl/private'      | The base directory for certificate keys on the host                        |

### Wordpress
These variables contain the admin user credentials, the Site Title, Tagline etc.

| Variable name     | Type   | Default                             | Description                                         |
| ----------------- | ------ | ----------------------------------- | --------------------------------------------------- |
| wp_version        | string | 'latest'                            | Wordpress version to be installed (format: 'x.x.x') |
| wp_admin_name     | string | 'admin'                             | Adminuser for e.g. wp-admin                         |
| wp_admin_email    | string | 'admin@localhost.localdomain'       | Admin contact email address                         |
| wp_admin_password | string | 'secret'                            | Password for admin login                            |
| wp_title          | string | 'Team Site'                         | Title of wordpress page                             |
| wp_tagline        | string | 'Informationsplatform'              | Subtitle of wordpress page                          |
| wp_host           | string | (N/A)                               | Address for wp-installation                         |
| wp_path           | string | '/var/www/{{ wp_apache_hostname }}' | Installation path to wordpress                      |


### wp-config
Variables required for the wp-config file.

| Variable name       | Type   | Default                       |
| ------------------- | ------ | ----------------------------- |
| wp_mysqldb_user     | string | 'wordpress_user'              |
| wp_mysqldb_password | string | 'secret'                      |
| wp_mysqldb_dbname   | string | 'wordpress_db'                |
| wp_mysqldb_host     | string | 'localhost'                   |
| wp_mysqldb_charset  | string | 'utf8'                        |
| wp_mysqldb_collate  | string | (N/A)                         |
| wp_auth_key         | string | 'put your unique phrase here' |
| wp_secure_auth_key  | string | 'put your unique phrase here' |
| wp_logged_in_key    | string | 'put your unique phrase here' |
| wp_nonce_key        | string | 'put your unique phrase here' |
| wp_auth_salt        | string | 'put your unique phrase here' |
| wp_secure_auth_salt | string | 'put your unique phrase here' |
| wp_logged_in_salt   | string | 'put your unique phrase here' |
| wp_nonce_salt       | string | 'put your unique phrase here' |
| wp_table_prefix     | string | 'wp_'                         |
| wp_debug            | string | 'false'                       |


### Wordpress Content
These variables contain the content of the wordpress instance.

| Variable name                              | Type    | Default     | Description                                                                |
| ------------------------------------------ | ------- | ----------- | -------------------------------------------------------------------------- |
| wp_remove_samples                          | boolean | yes         | If set to 'yes' the default example content of wordpress is removed        |
| **wp_themes**                              | list    |             | Wordpress themes to install                                                |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name            | string  | 'fblogging' | Theme name                                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .activate        | boolean | true        | If set it is activated after installation                                  |
| **wp_plugins**                             | list    |             | Wordpress plugins to install                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name            | string  | (N/A)       | Plugin name                                                                |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .activate        | boolean | true        | If set it is activated after installation                                  |
| **wp_users**                               | list    |             | Users to create                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name            | string  | (N/A)       | User login                                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .displayname     | string  | (N/A)       | User displayname                                                           |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .email           | string  | (N/A)       | User email                                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .password        | string  | (N/A)       | User password                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .role            | string  | (N/A)       | User role                                                                  |
| **wp_users_update**                        | list    |             | Users to update                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .id_id           | string  | (N/A)       | Identify by ID *or*                                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .id_name         | string  | (N/A)       | Identify by name *or*                                                      |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .id_email        | string  | (N/A)       | Identify by email                                                          |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .new_displayname | string  | (N/A)       | Updated displayname                                                        |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .new_email       | string  | (N/A)       | Updated email                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .new_password    | string  | (N/A)       | Updated password                                                           |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .new_role        | string  | (N/A)       | Updated role                                                               |
| **wp_categories**                          | list    |             | Wordpress categories to create                                             |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name            | string  | (N/A)       | Category name                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .description     | string  | (N/A)       | Category description                                                       |
| **wp_posts**                               | list    |             | Posts to create                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .title           | string  | (N/A)       | Post title                                                                 |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .author          | string  | (N/A)       | User name or Id                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .category        | string  | (N/A)       | Category name                                                              |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .date            | string  | (N/A)       | Post date in format: 'yyyy-dd-mm hh:mm'                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .content         | string  | (N/A)       | Content                                                                    |
| **wp_options**                             | list    |             | Posts to create                                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .option_name     | string  | (N/A)       | wp-option to be updated (see below a list of by default available options) |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .option_value    | string  | (N/A)       | value to be updated to                                                     |


#### wp-option list

| Option_name                  | Option_name                     | Option_name                  | Option_name                   |
| ---------------------------- | ------------------------------- | ---------------------------- | ----------------------------- |
| active_plugins               | default_ping_status             | page_for_posts               | timezone_string               |
| admin_email                  | default_pingback_flag           | page_on_front                | uninstall_plugins             |
| auto_core_update_failed      | default_post_format             | permalink_structure          | upload_path                   |
| auto_core_update_notified    | default_role                    | ping_sites                   | upload_url_path               |
| avatar_default               | finished_splitting_shared_terms | posts_per_page               | uploads_use_yearmonth_folders |
| avatar_rating                | fresh_site                      | posts_per_rss                | use_balanceTags               |
| blacklist_keys               | gmt_offset                      | recently_edited              | use_smilies                   |
| blog_charset                 | hack_file                       | recovery_keys                | use_trackback                 |
| blog_public                  | home                            | require_name_email           | users_can_register            |
| blogdescription              | html_type                       | rewrite_rules                | widget_archives               |
| blogname                     | image_default_align             | rss_use_excerpt              | widget_calendar               |
| category_base                | image_default_link_type         | show_avatars                 | widget_categories             |
| category_children            | image_default_size              | show_comments_cookies_opt_in | widget_custom_html            |
| close_comments_days_old      | initial_db_version              | show_on_front                | widget_media_audio            |
| close_comments_for_old_posts | large_size_h                    | sidebars_widgets             | widget_media_gallery          |
| comment_max_links            | large_size_w                    | site_icon                    | widget_media_image            |
| comment_moderation           | link_manager_enabled            | siteurl                      | widget_media_video            |
| comment_order                | links_updated_date_format       | start_of_week                | widget_meta                   |
| comment_registration         | mailserver_login                | sticky_posts                 | widget_nav_menu               |
| comment_whitelist            | mailserver_pass                 | stylesheet                   | widget_pages                  |
| comments_notify              | mailserver_port                 | tag_base                     | widget_recent-comments        |
| comments_per_page            | mailserver_url                  | template                     | widget_recent-posts           |
| cron                         | medium_large_size_h             | theme_mods_fblogging         | widget_rss                    |
| current_theme                | medium_large_size_w             | theme_mods_twentynineteen    | widget_search                 |
| date_format                  | medium_size_h                   | theme_switched               | widget_tag_cloud              |
| db_version                   | medium_size_w                   | thread_comments              | widget_text                   |
| default_category             | moderation_keys                 | thread_comments_depth        | wp_page_for_privacy_policy    |
| default_comment_status       | moderation_notify               | thumbnail_crop               | wp_user_roles                 |
| default_comments_page        | nonce_key                       | thumbnail_size_h             |                               |
| default_email_category       | nonce_salt                      | thumbnail_size_w             |                               |
| default_link_category        | page_comments                   | time_format                  |                               |



Dependencies
------------

This role utilizes two roles from [sct-cyberrange](https://git-service.ait.ac.at/sct-cyberrange/ansible-roles/):
- [apache2](https://git-service.ait.ac.at/sct-cyberrange/ansible-roles/apache2.git)
- [mariadb](https://git-service.ait.ac.at/sct-cyberrange/ansible-roles/mariadb.git)


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

MIT


Author Information
------------------

This role was created in 2019 by Lenhard Reuter