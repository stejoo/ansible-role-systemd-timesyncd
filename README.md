Ansible role systemd-timesyncd
==============================

Ansible role to configure systemd-timesyncd on a Linux system.

Requirements
------------

- a Linux system using systemd as init
- recommended: no other Network Time Protocol software running

Role Variables
--------------

The following variables can be set to your preference:

| variable                          | default value                                                              | description                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------------|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `timesyncd_fallback_servers`      | `['0.pool.ntp.org', '1.pool.ntp.org', '2.pool.ntp.org', '3.pool.ntp.org']` | List of NTP server host names or IP addresses to be used as the fallback NTP servers. NTP servers obtained from `systemd-networkd.service` take precedence over this setting, as do any servers set by the `timesyncd_ntp_servers` variable. This way `systemd-timesyncd` will try a NTP server provided by the local network (over DHCP for example), or one configured in `timesyncd_ntp_servers`, before falling back to this list of NTP servers or a hard-coded one. |
| `timesyncd_ntp_servers`           | `[]`                                                                       | List of NTP server host names or IP addresses. `systemd-timesyncd` appends this list with any NTP servers acquired from `systemd-networkd.service` and tries them all.                                                                                                                                                                                                                                                                                                    |
| `timesyncd_root_distance_max_sec` | 5                                                                          | Maximum acceptable root distance. Takes a time value (in seconds).                                                                                                                                                                                                                                                                                                                                                                                                        |
| `timesyncd_poll_interval_min_sec` | 32                                                                         | Minimum interval in seconds to contact a NTP server (again). Must not be smaller than 16 seconds.                                                                                                                                                                                                                                                                                                                                                                         |
| `timesyncd_poll_interval_max_sec` | 2048                                                                       | Maximum interval to synchronize with NTP server (again). Must be larger than `poll_interval_min_sec`.                                                                                                                                                                                                                                                                                                                                                                     |

Be aware of version dependent behavior:
- `fallback_servers` is available from systemd v216 and up
- `root_distance_max_sec`, `poll_interval_min_sec` and `poll_interval_max_sec` are usable with systemd v236 and up

Table generated with: <https://www.tablesgenerator.com/markdown_tables>


Dependencies
------------

None, this role has no dependency on another role.

Example Playbook
----------------

    - hosts: all
      vars:
        timesyncd:
          ntp_servers:
            - 0.europe.pool.ntp.org
            - 1.europe.pool.ntp.org
            - 2.europe.pool.ntp.org
            - 3.europe.pool.ntp.org
      roles:
         - stejoo.systemd-timesyncd

Tasks
-----

  - Configure `systemd-timesyncd`
  - Enable and start the `systemd-timesyncd.service`

License
-------

BSD

Author(s)
---------

- Laurent Goussard (author of [debian-timesyncd](<https://github.com/cowops/debian-timesyncd>))
- Stefan Joosten
