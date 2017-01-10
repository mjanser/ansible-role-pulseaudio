# Ansible Role: PulseAudio

An Ansible role that installs PulseAudio as a system-wide-daemon on Fedora.

Running PulseAudio in system mode is usually [a bad idea](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/WhatIsWrongWithSystemWide/),
but there are use cases where it makes sense to run it this way.

## Requirements

For configuring the firewall the service `firewalld` has to run and the package `python-firewall` needs to be installed.

## Role Variables

Available variables are listed below, along with default values:

    kodi_type: service # service, desktop
    kodi_user: kodi
    kodi_user_create: yes

    kodi_pvr_addons: []

    kodi_database_password: secret

    kodi_watched_list_database: false
    kodi_watched_list_database_backup: ~

    kodi_firewall_zones: []

### Firewall

The variable `kodi_firewall_zones` can be used to declare firewall zones in which kodi should be accessible.
This means the ports `8080/tcp` and `9777/udp` will be opened.

Currently only `firewalld` is supported which is default on Fedora.

## Dependencies

None

## Example Playbook

    - hosts: all
      roles:
        - { role: mjanser.pulseaudio }

## License

MIT
