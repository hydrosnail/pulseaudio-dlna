# About #

This is pulseaudio-dlna-portable, which is a fork of _pulseaudio-dlna_. I recommend that anyone that is interested in using pulseaudio-dlna use the official version, which is likely to be better maintained and more up to date.  The purpose of this fork is to maintain a simple, primarily portable version of pulseaudio-dlna that is easy to install on Arch Linux, and possibly other distros.

Why a fork?  Because the original application is being developed to include better system integration, and support for running as a SystemD daemon.  These features, while beneficial for most, are not necessary if the app is to remain portable.  

## License ##

    pulseaudio-dlna-portable is licensed under GPLv3.

    pulseaudio-dlna-portable is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    pulseaudio-dlna-portable is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with pulseaudio-dlna-portable.  If not, see <http://www.gnu.org/licenses/>.

### Portable Installation in Arch Linux ###

Coming

### Using ###

Start pulseaudio-dlna-portable from the local installation via:

    bin/pulseaudio-dlna

_pulseaudio-dlna_ should detect the ip address your computer is reachable within
your local area network. If the detected ip address is not correct or there
were no ips found, you still can specifiy them yourself via the host
option (```--host <your-ip>```)

Right after startup it should start searching for UPNP devices in your LAN and
add new PulseAudio sinks.

After 5 seconds the progress is complete and you can select your UPNP renderers
from the default audio control.

Note that pulseaudio-dlna-portable has to run all the time while you are listening to
your music.

Also note that _pulseaudio-dlna_ won't search for additional UPNP devices after
startup. It just does this once and (for me) there is no need in continuously
doing that. So if you added a new UPNP device to your network, restart
_pulseaudio-dlna_.

### CLI ###

    Usage:
        pulseaudio-dlna [--host <host>] [--port <port>] [--encoder <encoder>] [--filter-device=<filter-device>] [--renderer-urls <urls>] [--debug]
        pulseaudio-dlna [-h | --help | --version]

    Options:
           --host=<host>                       Set the server ip.
        -p --port=<port>                       Set the server port [default: 8080].
        -e --encoder=<encoder>                 Set the audio encoder [default: lame].
                                               Possible encoders are:
                                                 - lame  MPEG Audio Layer III (MP3)
                                                 - ogg   Ogg Vorbis
                                                 - flac  Free Lossless Audio Codec (FLAC)
                                                 - wav   Waveform Audio File Format (WAV)
                                                 - opus  Opus Interactive Audio Codec (OPUS)
        --filter-device=<filter-device>        Set a name filter for devices which should be added.
                                               Devices which get discovered, but won't match the
                                               filter text will be skipped.
        --renderer-urls=<urls>                 Set the renderer urls yourself. no discovery will commence.
        --debug                                enables detailed debug messages.
        -v --version                           Show the version.
        -h --help                              Show the help.

Samples:
- `pulseaudio-dlna` will start 
_pulseaudio-dlna_ on port _8080_ and stream your PulseAudio streams encoded
with _mp3_.
- `pulseaudio-dlna --encoder ogg` will start 
_pulseaudio-dlna_ on port _8080_ and stream your PulseAudio streams encoded
with _Ogg Vorbis_.
- `pulseaudio-dlna --port 10291 --encoder flac` will start 
_pulseaudio-dlna_ on port _10291_ and stream your PulseAudio streams encoded
with _FLAC_.
- `pulseaudio-dlna --filter-device 'Nexus 5,TV'` will just use devices named
_Nexus 5_ or _TV_ even when more devices got discovered.
- `pulseaudio-dlna --renderer-urls http://192.168.1.7:7676/smp_10_`
won't discover upnp devices by itself. Instead it will search for upnp renderers
at the specified locations. You can specify multiple locations via urls
seperated by comma (_,_). Most users won't ever need this option, but since
UDP multicast packages won't work (most times) over VPN connections this is
very useful if you ever plan to stream to a UPNP device over VPN.

## Tested devices ##

_pulseaudio-dlna_ was successfully tested on the follwing devices / applications:

- D-Link DCH-M225/E
- [Cocy UPNP media renderer](https://github.com/mnlipp/CoCy)
- BubbleUPnP (Android App)
- Samsung Smart TV LED60 (UE60F6300)
- Samsung Smart TV LED40 (UE40ES6100)
- Xbmc / Kodi
- Philips Streamium NP2500 Network Player
- Yamaha RX-475 (AV Receiver)
- Majik DSM
- [Pi MusicBox](http://www.woutervanwijk.nl/pimusicbox/)
- [Raumfeld Speaker M](http://raumfeld.com)
- Pioneer VSX-824 (AV Receiver)
- Pioneer A4 XW-SMA4-K (Wireless Speaker System)
- [ROCKI] (http://www.myrocki.com/)
- Sony STR-DN1050 (AV Receiver)

## Supported encoders ##

_pulseaudio-dlna_ supports the following encoders:

- __lame__  MPEG Audio Layer III (MP3)
- __ogg__   Ogg Vorbis
- __flac__  Free Lossless Audio Codec (FLAC)
- __wav__   Waveform Audio File Format (WAV)
- __opus__  Opus Interactive Audio Codec (OPUS)
