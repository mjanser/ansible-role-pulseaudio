# Ansible Role: PulseAudio

An Ansible role that installs PulseAudio as a system-wide-daemon on Fedora.

Running PulseAudio in system mode is usually [a bad idea](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/WhatIsWrongWithSystemWide/),
but there are use cases where it makes sense to run it this way.

## Requirements

For configuring the firewall the service `firewalld` has to run and the package `python-firewall` needs to be installed.

## Role Variables

Available variables are listed below, along with default values:

    pulseaudio_card_profiles: []
    pulseaudio_sink_formats: []

    pulseaudio_network: no
    pulseaudio_avahi: no

    pulseaudio_firewall_zones: []

### Profiles

With the variable `pulseaudio_card_profiles` you can define the default profiles for each card.
This will be stored in the `default.pa` file.

Each entry in the list must contain the keys `card` as a number and `profile`, for example:

    pulseaudio_card_profiles:
      - card: 1
        profile: output:iec958-stereo

Use the command `pactl list cards` for more information and a list of possible values on your system.

### Sink formats

The supported formats of a sink can be defined with the variable `pulseaudio_sink_formats`.
This configuration will be implemented using a custom systemd service which starts after `pulseaudio`.

Each entry in the list must contain the keys `sink` as a search string and `formats` (separated by semicolon), for example:

    pulseaudio_sink_formats:
      - sink: iec958
        formats: "pcm; ac3-iec61937; dts-iec61937"

Use the command `pactl list sinks` for more information about the available sinks.

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
