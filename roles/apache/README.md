Role: apache
===========
Purpose: Install and configure Apache with multiple virtual hosts.

Variables:
- apache_vhosts (list): Each item must include name, port, docroot, index_content (optional)
- apache_server_admin (string): default contact

Behavior:
- Uses ansible_facts['os_family'] to choose package and service names.
- On Debian, runs a2ensite to enable the site; on RedHat-like systems places conf into /etc/httpd/conf.d/.
- Triggers `Restart Apache` handler when templates change.
