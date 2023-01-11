# Sndio PulseAudio module

A module for PulseAudio to support playing to sndio servers.

This is liberated from the OpenBSD PulseAudio port:
http://cvsweb.openbsd.org/cgi-bin/cvsweb/ports/audio/pulseaudio/files/

This module supports playback only.

## Installation on Debian

First install the dependencies:

```bash
$ sudo apt install pulseaudio pulsemixer build-essential libpulse-dev libtool libltdl-dev libsndio-dev
```

Reboot the computer,

```bash
$ sudo reboot
```

Then get the latest release of the repo,

```bash
$ wget 'https://github.com/OpenBSDGuy/pulseaudio-module-sndio/archive/refs/tags/v14.tar.gz' && tar -xvzf v14.tar.gz && cd pulseaudio-module-sndio-14
```

Compile the code,

```bash
$ make && sudo make install
```

Then load the sndio module and set the server,

```bash
$ pactl load-module module-sndio device="snd@100.64.1.2/0" record=false playback=true
```

Make it permanent by adding the following line to the `/etc/pulse/default.pa` file,

```bash
load-module module-sndio device="snd@100.64.1.2/0" record=false playback=true
```

The IP must point to the IP address of the VMM host machine in NAT set up (Networking option-2 on [FAQ16](https://www.openbsd.org/faq/faq16.html#VMMnet), which in this case is the OpenBSD machine.

~~## Setup~~

~~Load it via `/etc/pulse/default.pa` (Linux) or `/usr/local/etc/pulse/default.pa` (FreeBSD):~~
~~```~~
~~load-module module-sndio device=snd@thor/0~~
~~```~~

~~It's best to disable the `suspend-on-idle` module, so comment or remove the following line from `default.pa`:~~
~~```~~
~~load-module module-suspend-on-idle~~
~~```~~

~~Also set the default sink if you want:~~
~~```~~
~~set-default-sink sndio-sink~~
~~```~~
