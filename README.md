![Logo](DHLogoColorWhiteBack240.png) 

# Deep Harmony

## A Roon Extension for Logitech Harmony

### Version: 2.5.0

[//]: # (TOC Begin)
* [Introduction  ](#introduction)
* [Main Features](#main-features)
* [Distribution Formats and Compatibility](#distribution-formats-and-compatibility)
	* [Compatibility](#compatibility)
* [Upgrade from Deep Harmony 1.x](#upgrade-from-deep-harmony-1.x)
* [Installation](#installation)
	* [Docker Image](#docker-image)
	* [Console applpications](#console-applpications)
* [Setup](#setup)
	* [Introduction](#introduction)
	* [Extension Settings](#extension-settings)
	* [Roon Audio Device Settings](#roon-audio-device-settings)
	* [Harmony Remote Setup](#harmony-remote-setup)
	* [Options Section](#options-section)
	* [Tools Section](#tools-section)
* [Troubleshooting](#troubleshooting)
* [Change History](#change-history)
	* [2.5.0](#)
	* [2.1.6](#)
	* [2.1.5](#)
	* [2.1.4](#)
	* [2.1.3](#)
	* [2.1.2](#)
	* [2.1.1](#)
	* [2.1.0](#)
	* [2.0.2](#)
	* [2.0.1](#)
	* [2.0.0](#)
	* [1.1.0](#)
	* [1.0.0 (beta)](#beta)
* [FAQ](#faq)
* [Acknowledgements](#acknowledgements)
* [Donating and some Background](#donating-and-some-background)

[//]: # (TOC End)

___

## Introduction  

**Deep Harmony** is an extension for the Roon media system from Roon Labs LLC that provides integration with Logitech's Harmony Hub remote control system to provide activity detection and selection by and for Roon and provide volume/mute control from with the Roon UI. Additionally it includes a media device emulator that allows for transport control and other functions from a Harmony Hub remote control over WiFi.

## Main Features

* Supports multiple Harmony hubs

* Supports multiple harmony zones

* Associate Harmony activities with Roon zones for transport and other control

* Volume step up/down and mute/unmute from within Roon UI

* Volume control of Roon Ready devices and DACs in device volume mode and some other extensions

* Select/standby activity from within Roon UI

* Auto stop linked zone when Harmony selects another activity or powers off

* Transport control of Roon from your Harmony remote

  * Play/Pause, Stop

  * Skip forward/backward

  * Next/previous track

  * Shuffle toggle

  * Loop mode cycle

  * Auto-Radio toggle

* Up to 10 internet radio services or playlists can be assigned to Harmony remote number keys

## Distribution Formats and Compatibility

The extension is available as a docker image and as a _bare bones_ console application. The console applications are a by-product of the build process and at this stage do not feature installers. They do however come with a very simple script to keep them running. 

* Docker Images for
  * linux-x64
  * linux-armv7
* _Bare bones_ console apps for
  * linux-x64
  * linux-armv7
  * windows-x64
  * macos-x64

### Compatibility

* Docker Images tested on

  * QNAP TS 251+ NAS with Container Station (linux-x64)
  * Docker on Raspberry PI 3B+ (linux-armv7)
  * User feedback suggests no issues on Synology NAS 
  
* Console apps tested on

  * Windows 10 (windows-x64)
  * Mac OSX High Sierra (macos-x64)
  * QNAP TS251+ NAS (linux-x64)
  * Raspberry PI 3B+ Rasbian (linux-armv7)

## Upgrade from Deep Harmony 1.x

Deep Harmony 2 is very different to Deep Harmony 1 with a completely new remote control that enables a bunhc of new feature now and in the future. The current remote emulator from v1 cannot be used with v2, so should be removed from Harmony. I do not anticpate that the remote device will change again in futurre versions. I anticpate it will take around 5-10 minutes to remote the old remote, pair the new remote and customize buttons again. I hope you will agree that the new features are worth the inconvenience of having to setup a remote all over again.

Deep Harmony v1 was only available as a docker image for Linux-x64. The v1 docker container should simply be deleted, followed by removal of the old remote emulator from Harmony, then follow the instructions below for setting up Deep Harmony v2.

## Installation

### Docker Image

#### Assets

* docker images - https://store.docker.com/community/images/khazul/roon-extension-deep-harmony

Docker images are provided for linux hosts (x64 and ARMv7) only at this time. They will not run correctly on Docker for Windows or Docker for MacOS due to the way the virtual networking works on the included virtual linux host with the result that the network service discovery method used by Roon and Harmony will not work.

#### QNAP Container Station

Locate the docker image &#39;roon-extension-deep-harmony&#39; via docker. In Container-Station on a QNAP NAS, ensure the docker-hub tab is selected then enter 'khazul' into the search box from the 'Create' menu. This should list the image. When the list of versions appears, then select the highest tagged **amd64** version rather than latest as it seems container station will pull the wrong (v1.x) version.

For command line use, the docker pull command is shown here on the right.

Create a container with network mode set to _host_. This is most important as otherwise neither Roon nor Harmony will discover this extension. Note, bridge mode may be usable as well.

Start the container.

Further information on QNAP Container Station can be found at:
[https://www.qnap.com/hu-hu/how-to/tutorial/article/how-to-use-container-station/](https://www.qnap.com/hu-hu/how-to/tutorial/article/how-to-use-container-station/)

#### Synology

I have no access to a Synology NAS. You can find a Synology KB on the subject at:
[https://www.synology.com/en-uk/knowledgebase/DSM/help/Docker/docker_container](https://www.synology.com/en-uk/knowledgebase/DSM/help/Docker/docker_container)

#### Linux (x64 and Armv7 on Raspberry PI 3/3B+)

At a shell prompt, type:
`docker run --detach --restart unless-stopped --network host khazul/roon-extension-deep-harmony`

For those new to docker, there is beginners guide at [https://docker-curriculum.com/](https://docker-curriculum.com/) which is a useful read particularly for command line use of docker.

### Console applications

#### Assets

* console apps - https://github.com/Khazul/roon-extension-deep-harmony-release/releases

The console applications are provided as zip files for the various supported target platforms:

* **windows-x64** For recent 64 bit Windows (Tested on Windows 10).
* **macos-x64** For recent 64 bit MacOS (Tested on OSX 10.13).
* **linux-x64** For recent 64 bit Linux (Tested on Debian 9.5, QNAP QTS 4.3.4).
* **linux-armv7** For recent 32 bit ARMv7 Linux (Tested on Debian 9.5, Rasbian 4.14 on Raspberry PI 3B+).

Make sure you download the correct version for your OS.

#### Linux and MacOS

Unpack the zip file. Inside you will find two files:

* `roon-extension-deep-harmony`
* `run.sh`

Open a command prompt and change directory to where you unpacked these files.
At the command prompt, type `./run.sh`. The supplied script is a very simple script to keep the extension executable running. Note that while you can directly run the executable, the script is required as part of the self-update service. 

#### Windows

Unpack the zip file. Inside you will find two files:

* `roon-extension-deep-harmony.exe`
* `run.bat`

Open a command prompt and change directory to where you unpacked these files.
At the command prompt, type `run.bat`. The supplied script is a very simple script to keep the extension executable running. Note that while you can directly run the executable, the script is required as part of the self-update service. 

## Setup

Once the extension is running, you should see it in the Extensions section of Roon's settings with an Enable button. Click on this button to enable the extension. Note, you can also click on the extension name _Deep Harmony_ web link to get to this documentation.

### Introduction

Deep-Harmony can support multiple Harmony hubs and can provide a separate remote control device for each hub (one per hub). Each hub with remote device has its own favourites list as well. 

Roon user profiles are not currently supported, but are on the road map, so your favourite playlists may need to be shared playlists for now if you have multiple user profile setup in Roon.

It is now also possible to setup multiple activities for use with Roon in a single hub. You can choose which activities have source and/or volume control available for them. For example, one activity may use both volume and source control of a Hi-Fi amp while another activity associated with another Roon zone may only have a source control as perhaps another extension provides direct AVR volume control integration.

### Extension Settings

Extension settings are organised into 3 sections:

* Select which Harmony Hubs to use with Roon.
* Detailed setup of each hub, activities and remote use.
* Tools for software updates, remote pairing assistance (if you have multiple Harmony hubs) and diagnostics.

Within the detailed setup of each hub you can select the activities to use with Roon via source and volume controls, whether to use a remote and select which Playlists and/or Internet Radio services to assign to up to ten quick access favourites that can be access from the number buttons on the Harmony remote.

#### About remote control device IDs

Each hub will require the setup of a unique remote control device if you want to use your Harmony remote to control transport, favourites etc. In order to ensure that each remote control is unique, then each must be assigned a unique identifier. In the menus related to setting up a remote, this identifier is shown as a number from 1 to 9. The identifer ensures that commands from button presses on a remote paired with a hub are directed to the correct Roon zone according to the current activity selected for each hub within Harmony.

#### Enable your Harmony hub

Upon opening settings, there will be one drop-down menu per Harmony hub showing the name of each hub and the subtitle _Use this hub with Roon?_. Select _Yes_ from the drop-down menu to enable the hub. As you enable a hub, a new expandable section (with a _**+**_ and the hub name) will appear.

_Note: When you first start the Deep-Harmony extension and open settings quickly, it is possible that it may not have discovered any Harmony hubs yet and you will see the message **No Harmony hubs discovered** Press Cancel and try again in a few seconds._

Click on _**+ Hub 'Harmony' Settings**_ (where _Harmony_ will be replaced with the name of your hub). This will open up settings for the hub.
At the top of the section with be a drop-drop from which you can create a remote control device for the hub to enable control of Roon's transport and other functions from your Harmony remote. For the first hub, use the ID _**1**_ and for the second, if you have additional hubs, use the ID _**2**_ and so on. Once these are setup and paired with Harmony (described under _Harmony Remote Setup_ below), then they must not be changed.

Next are listed the activities available on the hub as _**+** Activity 'Name of activity'_. Click on the _**+**_ to open up the settings for an activity you wish to associate with Roon. Associating an Harmony activity is required in order to create a _Source_ and/or _Volume_ control for Roon. Select _Yes_ from the drop-down menu to create the required control.

Assuming a remote ID was setup above, then there is also a drop-menu menu labelled _Remote control zone_. Select the Roon zone that will be controlled by the Harmony remote when this activity is current in Harmony.

Next repeat the above for any other Harmony hubs you may have that you wish to use with Roon and then click _Save_. 

At this point, Roon device controls for Source selection and Volume control and Harmony remote devices are created, however they will not do anything until the Source and Volume controls are associated with zones in Roon and the remote control device is paired with it respective Harmony hub.

### Roon Audio Device Settings

In the Roon controller UI, click on the zone icon at the bottom right (second icon from right).

In the list that pops up, click on the speaker icon for the zone you selected when setting up the extension.

Now click on the right-most cog-wheels like icon to open zone settings.

At the bottom of this dialog, click on Device Setup.

In the Volume Control drop down, you should now see a new entry named as _Deep Harmony:_ followed by the name of your Harmony hub and the activity you selected. Select this to enable integrated volume control via Harmony.

At the bottom of this dialog (you may need to scroll down), you should see a heading labelled _External Source Controls_ and _Add

External Source Control_. If there is already another device listed, then click the X to the right of it to remove.

Click on _Add External Source Control_ and select the device named _Deep Harmony:_ followed by your selected hub name and activity name.

Click on Save.

This is the main Roon setup complete.

### Harmony Remote Setup

Deep Harmony includes an emulator of a Roku TV device that serves purely as a control bridge between Harmony and the the Deep Harmony Roon extension. You will need to add the device to Harmony, then add it to your chosen activity and finally customise the buttons for the activity. 

The process for pairing remote devices with hubs depends on how many hubs + remote device you have setup. If you have only a single Harmony hub, then it is straight forward and the same as pairing any other device with Harmony. However, if you have multiple Harmony hubs then the process is a little more complex as it appears that if Harmony can see several new devices on WiFi, then it appears too be a matter of chance as to which one of those device it will detect and ask you to pair and there is no means to select the correct one. To deal with this scenario, this extension has a multi-hub pairing mode that will enable one remote device at a time to simplify pairing of the correct remote with the correct Harmony hub.

#### Adding the Remote Devices to multiple hubs

If you have have multiple Harmony hubs and have associated multiple remotes above, then re-open settings and expand the tools section. At the top of this section will be a drop down menu labelled _Remote pairing_. In the drop down menu are options for _All enabled_ and for each remote device you have configured, there will be an option to enable only that device and disable all others.
_Note: this Remote pairing drop-down is only available when you have multiple Harmony hubs configured._

To pair a single remote, select the option for the remote ID number you wish to pair, click _Save_ and then proceed as described below in for pairing a single remote. When you need to pair the next remote, open settings again, expand tools and change the Remote pairing to that of the next hub and remote pair you want to pair.

Finally, once all remotes have been paired with their respective Harmony hubs, open up settings a final time and choose _All enabled_ from the _Remote pairing_ drop-down and click _Save_.

#### Adding the Remote Device to a single hub

First of all, open your Harmony app on your mobile phone and select the _Devices_ tab.

Scroll to bottom of the list as required until the _Edit Devices_ button is visible and tap on _Edit Devices_.

At the bottom of screen that appears, there should be a button labelled _+ Device_; tap this.

At this point, if you do not have room for an additional device, Harmony may complain and you will need to remove another device.

The next screen that appears will be a menu with _SCAN FOR WI-FI DEVICES_ at the bottom; select this menu item.

Harmony should now scan your network. This may take a minute or so.

When the scan is complete, Harmony should find a _TCL 4k Roku TV_ device. Ensure the device is ticked and tap on Next, then proceed through the following screens until the device is added. In case you already have a real TCL Roku TV, then tap on the _(i)_ on the right; the device name should appear as _Deep Harmony N_ where N is the ID number you selected. The ID number can also be seen at the end of the displayed serial number. You should check this carefully to make sure it is as expected before proceeding when setting up multiple hubs. If it is not the ID that is expected, then check the Remote pairing as described above for adding multiple remote devices.

Before you add the device to an activity you should disable the power control on the device. 

Ensure devices are in edit mode by tapping _Edit Devices_ if required. Select the TCL TV device.

Scroll to the bottom and tap power settings, then select _NO POWER BUTTONS ON MY ORIGINAL REMOTE_. It may be useful to also rename the device to something like _'Roon Control'_.

Once the device is saved, try using the device in Harmony from your phone application just to make sure that it is controlling the expected zone/activity before spending time customising Harmony activities and remote buttons.

#### Activity Customisation

Now that you have added your device, disabled its power and renamed it you are now ready to create or change a Harmony activity. If you create an activity from scratch, then because Harmony think this is a TV, then it will insist on you creating an activity type of Watch Netflix, or Watch Roku etc. However, if you re-run an existing audio activity it did not do that.

For this reason, then I find it easier to first setup a music related activity without the Roon Controller, and then re-run the activity adding in the Roon controller.
  
When adding the device, Harmony may ask you which device you use to stream music. Select the Roon Control.

Once you have added the Roon Control to an activity, then I suggest you map the remote buttons as follows:

| Roon Action       | Harmony Button  | Roku Command   | Usage / Notes                            |
|-------------------|-----------------|----------------|------------------------------------------|
| Play/Pause        | Play            | Play           | Harmony appears to treat both play and pause as play for Roku devices |
| Play/Pause        | Pause           | Play           |                                          |
| Stop              | Stop            | PowerOff       | Make sure power control for the Roku emulator device is disabled |
| Skip back / Previous Track | Reverse | Reverse           | Skip backward 30 seconds / hold for replay/previous track |
| Skip forward / Next Track | Forward  | FastForward           | Skip forward 30 seconds / hold for next track |
| Volume Up         | Volume Up       | VolumeUp      | Optional - for controlling devices via Roon |
| Volume Down       | Volume Down     | VolumeDown    | Optional - for controlling devices via Roon |
| Volume Mute       | Volume Mute     | Mute    | Optional - for controlling devices via Roon |
| Rewind            | Reverse         | InputAV      | Optional - for separate short/long press with Previous / Rewind |
| Forward           | Forward         | InputUSB      | Optional - for separate short/long press with Next / Forward |
| Shuffle toggle    | Red             | InputHDMI1    | Toggle On/Off                            |
| Loop cycle        | Green           | InputHDMI2    | Cycles Off/Once/Repeat                   |
| Auto-radio toggle | Yellow          | InputHDMI3    | Toggle on/off                            |
|                   | Blue            | InputHDMI4    | Future planned feature                   |
|                   | 1               | 1              | Favourite 1                              |
|                   | 2               | 2              | Favourite 2                              |
|                   | 3               | 3              | Favourite 3                              |
|                   | 4               | 4              | Favourite 4                              |
|                   | 5               | 5              | Favourite 5                              |
|                   | 6               | 6              | Favourite 6                              |
|                   | 7               | 7              | Favourite 7                              |
|                   | 8               | 8              | Favourite 8                              |
|                   | 9               | 9              | Favourite 9                              |
|                   | 0               | 0              | Favourite 0                              |
|                   | -               | -              | Future planned feature                   |
|                   | E               | Backspace      | Future planned feature                   |
|                   | Exit            | Home           | Future planned feature                   |
|                   | Up              | Up             | Future planned feature                   |
|                   | Down            | Down           | Future planned feature                   |
|                   | Left            | Left           | Future planned feature                   |
|                   | Right           | Right          | Future planned feature                   |
|                   | OK              | OK             | Future planned feature                   |
|                   | Back            | Back           | Future planned feature                   |
|                   | Channel Up      | ChannelUp      | Future planned feature                   |
|                   | Channel Down    | ChannelDown    | Future planned feature                   |
|                   | Guide           | Search         | Future planned feature                   |
|                   | Info            | Info           | Future planned feature                   | 
|                   |                 | InstantReplay |                                          |
|                   |                 | InputTuner    |                                          |

_Some buttons are not needed right now, for example all of the browsing related buttons and some have no labels at all... yet! For some of these buttons, there are planned future feature that will make use of them as Deep Harmony continues to be developed._ 

Once this is complete, then test all the buttons and ensure they are to your liking and edit if necessary.

### Options Section

#### Skip/Seek track function

* **Dual function** - Harmony remote is assumed to have _Reverse_ and _FastForward_ assigned to the seek/skip track buttons. Short presses will seek +/- 30 seconds and long presses will function as previous or next track.  

* **Dual buttons** - then Harmony remote is assumed to have _Reverse_ and _FastForward_ assigned to short press and _InputAV_ and _InputUSB_ assigned to long press (as indicated as optional in the table above). Short press will seek +/-m 30 seconds and long press will skip to previous or next track. This tends to function better than the _Dual function_ option.  

* **Reversed dual buttons** - then Harmony remote is assumed to have _Reverse_ and _FastForward_ assigned to short press and _InputAV_ and _InputUSB_ assigned to long press (as indicated as optional in the table above). Short press will skip to previous or next track and long press will seek +/-m 30 seconds (i.e. the reverse of the above).  

#### Volume Linked to current activity

* **Yes** - volume and mute controls can only change the volume of the current Harmony activity.  

* **No** - volume and mute controls are independent of the current Harmony activity and thus remain active even when the activity is not selected.  

#### Unmute linked to volume change

* **Yes** - when muted and volume is changed, then mute status is assumed to be reset to off. This is the behavior of many AVRs and integrated amplifiers.  

* **No** - then when muted and volume is changes, the mute status remains unchanged. This setting is for use when a device needs to be explicitly unmuted.  

### Tools Section

In addition to the remote Pairing help for multiple hubs as described above the tools section also provide support for software updates and diagnostics.

#### Software updates

Deep Harmony will periodically check for new software updates. When an update is available, then the status message next to the extension will indicate the new version available. This can be found in Roon UI by selecting _Settings_ from the main Roon menu and then selecting _Extensions_. Normally the status will simply indicate _OK_ to show that it is configured and operating normally. If the availability of an update is indicated, then you can update your software version as follows:

1. Open settings for the extension by clicking on the _Settings_ button.
2. Expand the _**+** Tools_ section.
3. Find the drop down labelled _Update now_.
4. Select the required version from the drop down menu.
5. Click _Save_.

The extension will now download and unpack the update in the background and then exit once this is complete which should be in under a minute. When running the extension in docker and when using the run scripts, then the extension will install the update and restart automatically with the new version.

#### Reset Configuration

This allow full or partial reset of the extension configuration. It will not however effect Roon extension pairing, nor will you loose the remote of a remote with Harmony as this is ties to the selected remote identifier.

**Yes - erase all settings** will remove all settings period. In general you should never need to do this. After doing this, you can still recover a remote pairing by selecting the remote identifier that was used before for the hub. There is no need to re-pair and setup the remote again with Harmony.

**Yes - Roon pairing** will remove the Roon pairing token only. All Deep Harmony settings are preserved. Following use of this you should also remove the extension from Roon completely by clicking on _View_ in settings and then clicking _Remove_ next to the extension.

**Yes - activities only** will remove all settings associated with activities (source and volume controls and control zone). Enabled hubs, associated remote identifiers and all hub based favourites will be preserved.

#### Logging

To facilitate diagnosing any issues you may encounter the extension includes an extensive loggings system along with a web server to give easy access to those logs from another computer. As the Roon settings system does not appear have any means of clicking on a link within the settings UI, the link for accessing long is presented in a text box labelled _Logs (Copy the URL)_. If you click on this text, then it should be highlighted and you should be able to copy it and paste it into the address bar of a web browser such as Chrome or Edge. The should result in downloading a zip file containing recent logs.

## Troubleshooting

| Issue | Resolution |
|----------|----------|
| Harmony remote appears to be controlling the wrong hub or zone | The remote device was added to the wrong Harmony hub. It will need to be removed and setup again. |
| Roon unable to discover the extension | Docker container was not started in _host_ or _bridge_ network modes and thus is hidden on a docker virtual network |
| Harmony unable to discover the Roku emulator | as above. |
| UI Controller sometimes exits when saving settings. | I have no idea of the cause. It could be Roon, it could be this extension. Just restart the Roon UI controller. I know the Roon settings UI can be a bit fragile and is particular sensitive to imperfections in an extension. |
| No X next to source device name | If you have a long Harmony hub name and/or activity name, then the X next to the external source control name is hidden so you cannot remove it. Use load defaults to reset the audio device settings. You will have to re-apply your chosen MQA, DSD and other settings. |

## Change History

### 2.5.0

#### Changes

* Harmony xmpp protocol stack replaced with new websocket stack to support Harmony firmware 4.15.206 onwards
* Re-wrote harmony hub discovery
* Update node.js to 12.7
* Update docker images to debian-slim 10.0

### 2.2.0

#### Changes

* Attempt workaround for Roon apparently starting a source switch twice.
* New config option to restart extension at a set time if memory use threshold exceeded.
* Update node.js to 10.13
* Update docker images to debian-slim 9.6

### 2.1.5

#### Changes

* Added heap usage debugging to logs.
* Some very minor speculative fixes.

### 2.1.4

#### Changes

* Fixed issues with applying settings that could sometimes result in all controls being removed (causing _Add Source Control_ to not appear).
* Attempt to block bad SSDP responses that could result in undefined hub (underlying cause unknown).
* Added settings cleaner during startup to remove known invalid keys (including undefined hub).

### 2.1.3

#### Changes

* Fixed corrupt extension status web link.
* Add ToC to readme.

### 2.1.2

#### Changes

* Update to latest Roon SDK (1.2.1) modules to pick up bug-fix.
* Add Roon pairing reset option.

### 2.1.1

#### Changes

* Update to latest Roon SDK (1.2) modules.

### 2.1.0

#### New Features

* Allow use of Harmony remote volume and mute to control other Roon DACs device level and other extension volume/mute controls.
* Options section to tweak behaviour of volume and mute controls and skip/seek controls.
* Volume and mute can now function independently of the current Harmony activity as they are now linked to physical device rather than the selected activity. This means Harmony volume controls can still function even though the required activity is not selected.

#### Improvements

* Better handling of Harmony IP address changes (for eg due to router or hub reboot).

#### Fixes

* When multiple source or volume controls are used, sometimes they would attach to the wrong zone following a restart of either Roon core or this extension. (Fix requires change to Roon SDK).

### 2.0.2

#### Fixes

* Force explicit conversion of EOLs in unix and dos scripts in build due to editors converting them

* Switch ARM build tags to correct arm docker tag

### 2.0.1

#### Fixes

* Promise rejection warning when opening settings and no playlists have been setup preventing opening of settings view
* Initial state of debug switches not reflecting in dropdowns

### 2.0.0

#### New Features

* Now supports multiple Harmony Hubs.
* Now supports multiple Roon zones allowing for each zone to be associated with a Harmony hub+activity as needed.
* New Roku emulator to provide many more buttons.
* Supports a separate Roku emulator per Harmony hub. 
* Quick access to up to 10 favourite playlists or internet radio services from Harmony remote.

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

## Donating and some Background

A number of people have asked about donating to support this project and I was a bit taken aback that people would actually wish to donate, but after giving it some thought, it occurs that accepting donations may allow development to pursue directions that would otherwise be inaccessible for practical _freeware_ purposes. So to that end I have set up an account with Liberapay and a donate button may be found at the bottom. Thank you everyone for your ongoing support.

Some of the ideas I am interesting in pursuing are:

* Expanding the level of control to include a device UI with remote control browse, control of Roon zones other than that which you are listening to and other related features.

* Some level of integration with Amazon Alexa and maybe Google Home. We use Amazon Alexa at home currently with a Spot and an Echo. I am interested in seeing if the Spot (and Show) can reasonably be used to display now playing information and provide basic voice and touch based media control.

___

[![Liberapay](https://liberapay.com/assets/widgets/donate.svg)](https://liberapay.com/Khazul/donate)  
[![PayPal](https://www.paypalobjects.com/webstatic/mktg/Logo/pp-logo-100px.png)](https://paypal.me/khazul)  
