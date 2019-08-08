### 1.1.0

#### Fixes

* Keyboard (Ctrl+M) mute not working in Roon UI
* Improved device name not change when activity changed. (This _may_ also be a Roon Core issue).
* Reduce calls to Roon and Harmony when settings dialog opened (may help those who have experienced issues with this).

#### New Features

* Rolling log capture and embedded web server for easy log access
* Auto-update system to automatically download and make-ready new updates

#### Improvements

* Significantly reduced docker image size
* Add ARMv7 docker image for Raspberry PI 3/3B+
* Add basic console apps for Linux-x64, Linux-Armv7, Windows-x64 and MacOS-x64

#### Changes

* New Roon Device emulator _TCL Roku TV_ to provide many more buttons along with new suggested Harmony remote setup

#### Known Issues

* Occasionally the UI controller may stall or crash when changing settings or when changing source or volume devices. This _may_ be a Roon UI issue.
* When changing Hub name, Activity name or changing the activity associated with a zone, while the source device will change in volume control pop-up, the devices names will not change in audio device settings. This _may_ be a Roon Core issue.

### 1.0.0 (beta)

* Initial release

#### New features

* Roon Source Control linked to Harmony
* Roon Volume Control linked to Harmony
* Transport play/pause/stop/rew/fwd/next/previous from Harmony remote
* Zone shuffle, loop and auto-radio control from Harmony remote

#### Known Issues

* Occasionally the UI controller may stall or crash when changing settings or when changing source or volume devices.
* When changing Hub name, Activity name or changing the activity associated with a zone, while the source device will change in volume control pop-up, the devices names will not change in audio device settings.
  
## FAQ

**Why only Linux Docker and Why only Linux Docker host?**

Currently it is not possible to run MacOS inside a container. As for windows, then it is simply a case of not having looked into doing a windows build yet.

**Why cant I run the Linux-x64 image under Docker for Windows or Docker for Mac OS?**

The Linux docker host runs in a virtual machine on Docker for Windows and Docker for Mac with a virtual network bridge to your Windows or Mac host's network. The virtual network is a separate network and so the service discovery methods used by Roon and Harmony cannot fully see your main home network and thus cannot find the Roon extension. As a stop-gap, console apps for Windows and Mac OS have been made available however they are not packaged within installers nor registered as a service on Windows (or a daemon on OSX) nor have any means of keeping themselves running over any kind of failure.

## Acknowledgements

These are node modules used that have a significant part to play. Thanks are due to their authors for making them available.

* node-roon-api and related modules by Roon Labs LLC ([https://roonlabs.com/](https://roonlabs.com/))

  [https://github.com/RoonLabs/node-roon-api](https://github.com/RoonLabs/node-roon-api)
