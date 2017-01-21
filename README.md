# Ansible Role: PulseAudio

An Ansible role that installs PulseAudio as a system-wide-daemon on Fedora.

Running PulseAudio in system mode is usually [a bad idea](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/WhatIsWrongWithSystemWide/),
but there are use cases where it makes sense to run it this way.

## Requirements

For configuring the firewall the service `firewalld` has to run and the package `python-firewall` needs to be installed.

## Role Variables

Available variables are listed below, along with default values:

    pulseaudio_network: no
    pulseaudio_avahi: no

    pulseaudio_firewall_zones: []

### Network

Networking can be enabled with setting the variable `pulseaudio_network` to `true`.
If you also want auto-discovery using avahi, set `pulseaudio_avahi` to `true`.
Enabling avahi implicitly enables networking as well.

### Firewall

The variable `pulseaudio_firewall_zones` can be used to declare firewall zones in which pulseaudio should be accessible.
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
