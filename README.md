[![CI](https://github.com/de-it-krachten/ansible-role-wordpress/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-wordpress/actions?query=workflow%3ACI)


# ansible-role-wordpress

<basic role description>



## Dependencies

#### Roles
None

#### Collections
- community.general
- ansible.posix
- community.crypto

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS

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




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'wordpress'
  hosts: all
  become: "yes"
  vars:
    openssl_fqdn: server.example.com
    apache_fqdn: server.example.com
    apache_ssl_key: "{{ openssl_server_key }}"
    apache_ssl_crt: "{{ openssl_server_crt }}"
    apache_ssl_chain: "{{ openssl_server_crt }}"
    mariadb_user: root
    mariadb_pwd: root
    mariadb_db_host: localhost
    mariadb_db_name: wordpress
    mariadb_db_user: wordpress
    mariadb_db_pwd: wordpress
    mariadb_socket_authentication: False
    wordpress_path: /var/www/html
    wordpress_conf_dir: /var/www/html
    wordpress_db_host: localhost
    wordpress_db_name: wordpress
    wordpress_db_user: wordpress
    wordpress_db_pwd: wordpress
  roles:
    - deitkrachten.showinfo
    - deitkrachten.openssl
    - deitkrachten.apache
    - deitkrachten.php
    - deitkrachten.mariadb
  tasks:
    - name: Include role 'wordpress'
      ansible.builtin.include_role:
        name: wordpress
</pre></code>
