[![CI](https://github.com/de-it-krachten/ansible-role-wordpress/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-wordpress/actions?query=workflow%3ACI)


# ansible-role-wordpress

<basic role description>


## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Wordpress configuration location
wordpress_conf_dir: /var/www/wordpress

# Wordpress code location
wordpress_path: /var/www/wordpress

# Wordpress database name
wordpress_db_name: wordpress

# Wordpress database user
wordpress_db_user: wordpress

# Wordpress database password
wordpress_db_pwd: wordpress
</pre></code>

### vars/default.yml
<pre><code>

</pre></code>



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'wordpress'
  hosts: all
  become: "{{ molecule['converge']['become'] | default('yes') }}"
  vars:
    mariadb_db_name: wordpress
    mariadb_db_user: wordpress
    mariadb_db_pwd: wordpress
    wordpress_db_name: wordpress
    wordpress_db_user: wordpress
    wordpress_db_pwd: wordpress
    php_packages: ['php-curl', 'php-gd', 'php-mbstring', 'php-intl', 'php-soap', 'php-xml', 'php-xmlrpc', 'php-zip']
  pre_tasks:
    - name: Create 'remote_tmp'
      file:
        path: /root/.ansible/tmp
        state: directory
        mode: "0700"
  roles:
    - apache
    - php
    - mariadb
  tasks:
    - name: Include role 'wordpress'
      include_role:
        name: wordpress
</pre></code>
