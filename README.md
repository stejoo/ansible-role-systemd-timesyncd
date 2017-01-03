Debian-timesyncd
================

Network Time Synchronization

Requirements
------------

This role requires systemd running on a debian compliant system such as ubuntu.

Role Variables
--------------

timesyncd:
    servers:
        - 0.debian.pool.ntp.org
        - 1.debian.pool.ntp.org
        - 2.debian.pool.ntp.org
        - 3.debian.pool.ntp.org

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: loranger.debian-timesyncd, timesyncd.servers: 0.debian.pool.ntp.org }

Tasks
-----

  - Install [ntp](http://www.ntp.org/)
  - Setup with [french ntp pool](http://www.pool.ntp.org/fr/)

License
-------

BSD
