Apache Ansible Role — Automated Apache Web Server Deployment
===========================================================

What this project provides
- Role: `roles/apache` which:
  - Installs the correct Apache package depending on the target OS (Debian/RedHat families)
  - Deploys multiple VirtualHosts from a list using a template and loops
  - Creates document roots and a simple index.html for each vhost
  - Uses handlers to restart Apache only when configuration changes
  - Uses OS-specific tasks (enabling site on Debian, placing conf files in right location)
- Playbook: `site.yml`
- Example inventory: `inventory/hosts.ini`
- Default variables and example vhost list in `roles/apache/defaults/main.yml`
- Template: `roles/apache/templates/vhost.j2`

How to run
1. Adjust `inventory/hosts.ini` to point to your servers.
2. Optionally edit `roles/apache/defaults/main.yml` to change vhosts.
3. Run:
   ansible-playbook -i inventory/hosts.ini site.yml

Notes on idempotency and behavior
- Uses `ansible.builtin.package`, `ansible.builtin.template`, `ansible.builtin.file`, and `ansible.builtin.service`.
- On Debian, the playbook runs `a2ensite` to enable sites and reloads the service via handler.
- On RedHat-like systems, config files are placed into `/etc/httpd/conf.d/` and the service is managed as `httpd`.

Example vhosts
- Provided in defaults: example.com and test.example.com (change to your real domains).

Files included
- site.yml
- inventory/hosts.ini
- roles/apache/{tasks,handlers,defaults,templates,meta}

