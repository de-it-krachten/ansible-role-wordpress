[![CI](https://github.com/de-it-krachten/ansible-role-wordpress/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-wordpress/actions?query=workflow%3ACI)


# ansible-role-wordpress

<basic role description>


## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- RockyLinux 8
- OracleLinux 8
- AlmaLinux 8
- Debian 11 (Bullseye)
- Ubuntu 20.04 LTS

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Wordpress configuration location
wordpress_conf_dir: /var/www/wordpress

# Wordpress code location
wordpress_path: /var/www/wordpress

# Wordpress tmp path
wordpress_tmp_path: /tmp/wordpress

# Wordpress owner
wordpress_user: "{{ webserver_user | default('wordpress') }}"

# Wordpress group
wordpress_group: "{{ webserver_group | default('wordpress') }}"

# Wordpress database name
wordpress_db_name: wordpress

# Wordpress database user
wordpress_db_user: wordpress

# Wordpress database password
wordpress_db_pwd: wordpress
</pre></code>


### vars/family-RedHat.yml
<pre><code>

</pre></code>

### vars/default.yml
<pre><code>

</pre></code>

### vars/family-Debian.yml
<pre><code>

</pre></code>



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'wordpress'
  hosts: all
  become: "{{ molecule['converge']['become'] | default('yes') }}"
  vars:
    openssl_fqdn: www.example.com
    apache_fqdn: server.example.com
    apache_ssl_key: "{{ openssl_server_key }}"
    apache_ssl_crt: "{{ openssl_server_crt }}"
    apache_ssl_chain: "{{ openssl_server_crt }}"
    apache_vhosts: "[{'vhost': 'www.example.com', 'template': 'vhost.conf.j2', 'listen': '*', 'port': '443', 'ssl': True, 'ssl_key': '{{ openssl_server_key }}', 'ssl_crt': '{{ openssl_server_crt }}', 'ssl_chain': '{{ openssl_server_crt }}', 'owner': '{{ apache_user }}', 'group': '{{ apache_group }}'}]"
    mariadb_user: root
    mariadb_pwd: root
    mariadb_db_host: localhost
    mariadb_db_name: wordpress
    mariadb_db_user: wordpress
    mariadb_db_pwd: wordpress
    mariadb_socket_authentication: False
    wordpress_path: /var/www/www.example.com/public_html
    wordpress_conf_dir: /var/www/www.example.com/public_html
    wordpress_db_host: localhost
    wordpress_db_name: wordpress
    wordpress_db_user: wordpress
    wordpress_db_pwd: wordpress
  pre_tasks:
    - name: Create 'remote_tmp'
      file:
        path: /root/.ansible/tmp
        state: directory
        mode: "0700"
  roles:
    - openssl
    - apache
    - php
    - mariadb
  tasks:
    - name: Include role 'wordpress'
      include_role:
        name: wordpress
</pre></code>
