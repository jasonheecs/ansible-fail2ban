Ansible Role: Fail2ban for Ubuntu
=========
Installs and configures [Fail2ban](https://www.fail2ban.org/) for Debian/Ubuntu and RHEL/CentOS machines

Requirements
------------
No special requirements, but do note that this role requires root access, so either run it in a playbook with a global become: true, or invoke the role in your playbook like:

```
- hosts: all
  roles:
    - role: jasonheecs.fail2ban
      become: true
```


Installation
------------
`ansible-galaxy install jasonheecs.fail2ban`


Role Variables
--------------
Available variables are listed below, along with default values (see defaults/main.yml):
```
fail2ban_loglevel: INFO
fail2ban_logtarget: /var/log/fail2ban.log
fail2ban_socket: /var/run/fail2ban/fail2ban.sock

fail2ban_ignoreip: 127.0.0.1/8
fail2ban_bantime: 600
fail2ban_maxretry: 6

fail2ban_backend: polling

fail2ban_destemail: root@localhost
fail2ban_banaction: iptables-multiport
fail2ban_mta: sendmail
fail2ban_protocol: tcp
fail2ban_chain: INPUT

fail2ban_action: action_

fail2ban_services:
  - name: ssh
    port: ssh
    filter: sshd
    logpath: /var/log/auth.log
```

Dependencies
------------
Ansible version >= 2.18

Example Playbook
----------------

```
- hosts: all
  become: yes
  roles:
    - { role: jasonheecs.fail2ban }
```   

Testing
-------
Testing is done via Molecule. Refer to the [molecule](molecule/default/) folder and [Github CI](https://github.com/jasonheecs/ansible-fail2ban/actions/workflows/ci.yml).

License
-------
MIT

Author Information
------------------
[Jason Hee](https://jasonhee.com)
