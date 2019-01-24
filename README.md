# "homebridge-sony-audio-control" Plugin
With this plugin you can create HomeKit services to control a Sony STR-DN1080 Audio Video Receiver or HT-ST5000 Soundbar..

The code for this plugin has originally been forked from [Http Speaker for Homebridge](https://github.com/Supereg/homebridge-http-speaker) authored by Andreas Bauer.

## Compatibility notice
This plugin utilizes Sony's [Audio Control API](https://developer.sony.com/develop/audio-control-api/). It has only been tested with a Sony STR-DN1080 Audio Video Receiver and HT-ST5000 Soundbar, but it may work with other Sony devices that support the API.

The plugin supports powertoggling, volume control including muting, setting sound modes stereo and Dolby Surround and switching configured external inputs.

The plugin doesn't support auto discovery using UPNP. This is by design as the receiver stops responding on port 52323 after being put in standby once (at least that is the case with the european version per firmware version M41.R.0442), which is necessary to support auto discovery.

## Installation
First of all you should already have installed `Homebridge` on your device. Follow the instructions over at the
[HomeBridge Repo](https://github.com/nfarina/homebridge).

To install the `homebridge-sony-audio-control` plugin simply run `sudo npm install -g homebridge-sony-audio-control`.

### Configuration
Below is an example configuration that has to amended to your existing Homebridge-configuration.

You have to edit "ip" to correspond with the IP-address of your receiver.

Set "name" to what you prefer to refer to the device as using Homekit or Siri.

"accessory" is used by homebridge to initialize the plugin correctly, so do NOT edit this setting.

For every external input you want to enable, you have to add a new input object with a "name" and "uri". Again "name" can be set to what you prefer to refer to the input as using Homekit or Siri, while "uri" have to correspond to the Device Resource URI per [Device URI](https://developer.sony.com/develop/audio-control-api/api-references/device-uri).  

    "accessories": [
        {
            "accessory": "receiver",
            "name": "Receiver",
            "ip": "10.0.0.138",
            "inputs": [
              {
                "name": "Apple TV",
                "uri": "extInput:video?port=2"
              },
              {
                "name": "TV",
                "uri": "extInput:sat-catv"
              },
              {
                "name": "Blu-ray",
                "uri": "extInput:bd-dvd"
              },
              {
                "name": "Xbox One",
                "uri": "extInput:game"
              },
              {
                "name": "Bluesound",
                "uri": "extInput:tv"
              },
              {
                "name": "Vinyl",
                "uri": "extInput:sacd-cd"
              }
            ]
        }
    ]


HT-ST5000:
    "accessories": [
        {
            "accessory": "receiver",
            "name": "Receiver",
            "ip": "192.168.x.x",
            "inputs": [
              {
                "name": "TV",
                "uri": "extInput:tv"
              },
              {
                "name": "Apple TV",
                "uri": "extInput:hdmi?port=1"
              },
              {
                "name": "HDMI2",
                "uri": "extInput:hdmi?port=2"
              }
            ]
        }
    ],
