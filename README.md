Osquery config update
=========

This role can be used to update a osquery config, e. g. early in the
startup process before the actual services runs.

[![CI](https://github.com/Rheinwerk/ansible-role-update_osquery_config/actions/workflows/ci.yml/badge.svg)](https://github.com/Rheinwerk/ansible-role-update_osquery_config/workflows/ci.yml)

Notice that it will not start the service and expects the program to be
installed already.

Requirements
------------

The target machine must have osquery installed.

Role Variables
--------------

| Variable | Default |
|---|---|
| `_osquery_config` | the JSON written to `/etc/osquery/osquery.conf`: a `schedule` with the snapshot queries `instance_info` (EC2 instance, kernel, uptime and OS facts) and `software_versions` (`deb_packages`), both every 12 hours |

Set `_osquery_config` to replace the whole configuration; see `defaults/main.yml` for the
default. Until v0.1.0 the role took one `_osquery` dict with the key `config` instead.

Dependencies
------------

None.


Example Playbook
----------------

    - hosts: servers
      vars:
        _osquery_config:
          schedule:
            software_versions:
              query: 'SELECT * from deb_packages;'
              interval: 3600
              snapshot: true
      roles:
         - { role: update_osquery_config, tags: [ 'osquery' ] }

License
-------

Please see LICENSE.

Author Information
------------------

Original author is [Michael Schmitz](https://github.com/eifelmicha) as member of the [Rheinwerk](https://github.com/Rheinwerk) project.
