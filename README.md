# Deep Harmony

### A Roon Extension for Logitech Harmony

### Version: 2.0.0

# Introduction  

**Deep Harmony** is an extension for the Roon media system from Roon Labs LLC that provides integration with Logitech's Harmony Hub remote control system to provide activity detection and selection by and for Roon and provide volume/mute control from with the Roon UI. Additionally it includes a media device emulator that allows for transport control and other functions from a Harmony Hub remote control over WiFi.

# Features

* Supports multiple Harmony hubs

* Supports multiple harmony zones

* Associate Harmony activities with Roon zones for transport and other control

* Volume step up/down and mute/unmute from within Roon UI

* Select/standby activity from within Roon UI

* Auto stop linked zone when Harmony selects another activity or powers off

* Transport control of Roon from your Harmony remote

  * Play/Pause, Stop

  * Skip forward/backward

  * Next/previous track

  * Shuffle toggle

  * Loop mode cycle

  * Auto-Radio toggle

* Upto 10 internet radio services or playlists can be assigned to Harmony remote number keys

# What's New

This release was originally intended to be a few fixes and addition of auto update and a few minor tidy ups under the hood. However one thing led to another and eventually it made more sense to start on future plans now as it became clear that some of the under the hood improvements were going to need a rather more major rework. So, instead of the intended 1.0.1 release, here it is; 2.0 and allmost everything has changed.

## New Features ##
* Now supports multiple Harmony Hubs.
* Now supports multiple Roon zones allowing for each zone to be associated with a Harmony hub+activity as needed.
* New Roku emulator to provide many more buttons.
* Supports a separate Roku emulator per Harmony hub. 
* Quick access to upto 10 favourite playlists or internet radio services from Harmony remote.
* Proper rolling and trimmed log capture system with embedded web server for easy access to recent logs as a zip file.
* Simple software update system to download and install new versions as they become available. This is controlled from settings.

## Other improvements ##
* Roku emulator button assignments are a more natural fit with Harmony.
* Significantly reduced docker image size (Just under 800MB reduced to around 115MB on x64 and around 95MB on ArmV7).
* Web based access to logs and user controllable logging levels.
* Docker images for two platforms (linux-x64, linux-armv7) including multi-platform tagged docker image.
* Basic console applications for 4 platforms: linux-x64, linux-armv7, windows-x64, macos-x64.

# Distribution Formats

The extension is available as a docker image and as a _bare bones_ console application. The console applications are a by-product of the build process and at this stage do not feature installers. They do however come with a very simple script to keep them running. 

* Docker Images for 
  * linux-x64
  * linux-armv7
* _Bare bones_ console apps for
  * linux-x64
  * linux-armv7
  * windows-x64
  * macos-x64

## Compatibility

* Docker Images tested on

  * QNAP TS 251+ NAS with Container Station (linux-x64)
  * Docker on Raspberry PI 3B+ (linux-armv7)
  * User feedback suggests no issues on Synology NAS 
  
* Console apps tested on

  * Windows 10 (windows-x64)
  * Mac OSX High Sierra (macos-x64)
  * QNAP TS251+ NAS (linux-x64)
  * Raspberry PI 3B+ Rasbian (linux-armv7)

# Upgrade from Deep Harmony 1.x

Deep Harmony 2 is very different to Deep Harmony 1 with a completely new remote control that enables a bunhc of new feature now and in the future. The current remote emulator from v1 cannot be used with v2, so should be removed from Harmony. I do not anticpate that the remote device will change again in futurre versions. I anticpate it will take around 5-10 minutes to remote the old remote, pair the new remote and customize buttons again. I hope you will agree that the new features are worth the inconvenience of having to setup a remote all over again.

Deep Harmony v1 was only available as a docker image for Linux-x64. The v1 docker container should simply be deleted, followed by removal of the old remote emulator from Harmony, then follow the instructions below for setting up Deep Harmony v2.

# Installation

## Docker Image

### Assets

* docker images - https://store.docker.com/community/images/khazul/roon-extension-deep-harmony

Docker images are provided for linux hosts (x64 and ARMv7) only at this time. They will not run correctly on Docker for Windows or Docker for MacOS due to the way the virtual networking works on the included virtual linux host with the result that the network service discovery method used by Roon and Harmony will not work.

### QNAP Container Station

Locate the docker image &#39;roon-extension-deep-harmony&#39; via docker. In Container-Station on a QNAP NAS, enter 'khazul' into the search box from the 'Create' menu. This should list the image. For command line use, the docker pull command is shown here on the right.

Create a container with network mode set to _host_. This is most important as otherwise neither Roon nor Harmony will discover this extension. Note, bridge mode may be usable as well.

Start the container.

Further information on QNAP Container Station can be found at:
[https://www.qnap.com/hu-hu/how-to/tutorial/article/how-to-use-container-station/](https://www.qnap.com/hu-hu/how-to/tutorial/article/how-to-use-container-station/)

### Synology 

I have no access to a Synology NAS. You can find a Synology KB on the subject at:
[https://www.synology.com/en-uk/knowledgebase/DSM/help/Docker/docker_container](https://www.synology.com/en-uk/knowledgebase/DSM/help/Docker/docker_container)

### Linux (x64 and Armv7 on Raspberry PI 3/3B+)
At a shell prompt, type:
`docker run --detach --restart unless-stopped --network host khazul/roon-extension-deep-harmony`

For those new to docker, there is beginners guide at [https://docker-curriculum.com/](https://docker-curriculum.com/) which is a useful read particularly for command line use of docker.

## Console applpications

### Assets

* console apps - https://github.com/Khazul/roon-extension-deep-harmony-release/releases

The console applications are provided as zip files for the various supported target platforms:
* **windows-x64** For recent 64 bit Windows (Tested on Windows 10).
* **macos-x64** For recent 64 bit MacOS (Tested on OSX 10.13).
* **linux-x64** For recent 64 bit Linux (Tested on Debian 9.5, QNAP QTS 4.3.4).
* **linux-armv7** For recent 32 bit ARMv7 Linux (Tested on Debian 9.5, Rasbian 4.14 on Raspberry PI 3B+).

Make sure you download the correct version for your OS.

### Linux and MacOS

Unpack the zip file. Inside you will find two files:
* `roon-extension-deep-harmony`
* `run.sh`

Open a command prompt and change directoory to where you unpacked these files.
At the command prompt, type `./run.sh`. The supplied script is a very simple script to keep the extension executable running. Note that while you can directly run the executable, the script is required as part of the self-update service. 

### Windows

Unpack the zip file. Inside you will find two files:
* `roon-extension-deep-harmony.exe`
* `run.bat`

Open a command prompt and change directoory to where you unpacked these files.
At the command prompt, type `run.bat`. The supplied script is a very simple script to keep the extension executable running. Note that while you can directly run the executable, the script is required as part of the self-update service. 

# Setup

Once the extension is running, you should see it in the Extensions, section of Roon's settings with an Enable button. Click on this button to enable the extension.

## Introduction

Deep-Harmony can support multiple Harmony hubs and can provide a separate remote control device for each hub (one per hub). Each hub with remote device has its own favourites list as well. 

Roon user profiles are not currrently supported, but are on the roadmap, so your favourite playlists may need to be shared playlists for now if you have multiple user profile setup in Roon.

It is now also possible to setup multiple activities for use with Roon in a single hub. You can choose which activities have source and/or volume control available for them. For example, one activity may use both volume and source control of a Hi-Fi amp while another activity associated with another Roon zone may only have a source control as perhpas another extension provides direct AVR volume control integration.

## Extension Settings

Extension settings are organised into 3 sections:
* Select which Harmony Hubs to use with Roon.
* Detailed setup of each hub, activities and remote use.
* Tools for software updates, remote pairing assistance (if you have multiple Harmony hubs) and diagnostics.

Within the detailed setup of each hub you can select the activities to use with Roon via source and volume controls, whether to use a remote and select which Playlists and/or Internet Radio services to assign to upto ten quick access favourites that can be access from the number buttons on the Harmony remote.

### About remote control device IDs

Each hub will require the setup of a unique remote control device if you want to use your Harmony remote to control transport, favourites etc. In order to ensure that each remote control is unique, then each must be assigned a unique identifier. In the menus related to setting up a remote, this identifier is shown as a number from 1 to 9. The identifer ensures that commands from button presses on a remote paired with a hub are directed to the correct Roon zone according to the current activity selected for each hub within Harmony.

### Enable your Harmony hub

Upon opening settings, there will be one drop-down menu per Harmony hub showing the name of each hub and the subtitle _Use this hub with Roon?_. Select _Yes_ from the drop-down menu to enable the hub. As you enable a hub, a new expandable section (with a _**+**_ and the hub name) will appear.

_Note: When you first start the Deep-Harmony extension and open settings quickly, it is possible that it may not have discovered any Harmony hubs yet and you will see the message **No Harmony hubs discovered** Press Cancel and try again in a few seconds._

Click on _**+ Hub 'Harmony' Settings**_ (where _Harmony_ will be replaced with the name of your hub). This will open up settings for the hub.
At the top of the section with be a drop-drop from which you can create a remote control device for the hub to enable control of Roon's transport and other functions from your Harmony remote. For the first hub, use the ID _**1**_ and for the second, if you have additional hubs, use the ID _**2**_ and so on. Once these are setup and paired with Harmony (described under _Harmony Remote Setup_ below), then they must not be changed.

Next are listed the activities available on the hub as _**+** Activity 'Name of activity'_. Click on the _**+**_ to open up the settings for an activity you wish to associate with Roon. Associating an Harmony activity is required in order to create a _Source_ and/or _Volume_ control for Roon. Select _Yes_ from the drop-down menu to create the required control.

Assuming a remote ID was setup above, then there is also a drop-menu menu labelled _Remote control zone_. Select the Roon zone that will be controlled by the Harmony remote when this activity is current in Harmony.

Next repeat the above for any other Harmony hubs you may have that you wish to use with Roon and then click _Save_. 

At this point, Roon device controls for Source selection and Volume control and Harmony remote devices are created, however they will not do anything until the Source and Volume controls are associated with zones in Roon and the remote control device is paired with it respective Harmony hub.

## Roon Audio Device Settings

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

## Harmony Remote Setup

Deep Harmony includes an emulator of a Roku TV device that serves purely as a control bridge between Harmony and the the Deep Harmony Roon extension. You will need to add the device to Harmony, then add it to your chosen activity and finally customise the buttons for the activity. 

The process for pairing remote devices with hubs depends on how many hubs + remote device you have setup. If you have only a single Harmony hub, then it is straight forward and the same as pairing any other device with Harmony. However, if you have multiple Harmony hubs then the process is a little more complex as it appears that if Harmony can see several new devices on WiFi, then it appears too be a matter of chance as to which one of thoose device it will detect and ask you to pair and there is no means to select the correct one. To deal with this scenario, this extension has a multi-hub pairing mode that will enable one remote device at a time to simplify pairing of the correct remote with the correct Harmony hub.

### Adding the Remote Devices to mutiple hubs

If you have have multiple Harmony hubs and have associated multiple remotes above, then re-open settings and expand the tools section. At the top of this section will be a drop down menu labelled _Remoote pairing_. In the drop down menu are options for _All enabled_ and for each remote device you have configured, there will be an option to enable only that device and disable all others. 
_Note: this Remote pairing drop-down is only available when you have multiple Harmony hubs configured._

To pair a single remote, select the option for the remote ID number you wish to pair, click _Save_ and then proceed as described below in for pairing a single remote. When you need to pair the next remote, open settings again, expand tools and change the Remote pairing to that of the next hub and remote pair you want to pair.

Finally, once all remotes have been paired withg their respective Hrmony hubs, open up settings a final time and choose _All enabled_ from the _Remote pairing_ drop-down and click _Save_.

### Adding the Remote Device to a single hub

First of all, open your Harmony app on your mobile phone and select the _Devices_ tab.

Scroll to bottom of the list as required until the _Edit Devices_ button is visible and tap on _Edit Devices_.

At the bottom of screen that appears, there should be a button labelled _+ Device_; tap this.

At this point, if you do not have room for an additional device, Harmony may complain and you will need to remove another device.

The next screen that appears will be a menu with _SCAN FOR WI-FI DEVICES_ at the bottom; select this menu item.

Harmony should now scan your network. This may take a minute or so.

When the scan is complete, Harmony should find a _TCL 4k Roku TV_ device. Ensure the device is ticked and tap on Next, then proceed through the following screens until the device is added. In case you already have a real TCL Roku TV, then tap on the _(i)_ on the right; the device name should appear as _Deep Harmony N_ where N is the ID number youo selected. The ID number can also be seen at the end of the displayed serial number. You should check this carefully to make sure it is as expected before proceeding when setting up mutiple hubs. If it is not the ID that is expected, then check the Remote pairing as described above for adding multiple remote devices.

Before you add the device to an activity you should disable the power control on the device. 

Ensure devices are in edit mode by tapping _Edit Devices_ if reuqired. Select the TCL TV device.

Scroll to the bottom and tap power settings, then select _NO POWER BUTTONS ON MY ORIGINAL REMOTE_. It may be useful to also rename the device to something like _'Roon Control'_.

Once the device is saved, try using the device in Harmony from your phone application just to make sure that it is controlling the expected zone/activity before spending time customising Harmony activities and remote buttons.

### Activity Customisation

Now that you have added your device, disabled its power and renamed it you are now ready to create or change a Harmony activity. If you create an activity from scratch, then because Harmony think this is a TV, then it will insist on you creating an activity type of Watch Netflix, or Watch Roku etc. However, if you re-run an existing audio activity it did not do that.

For this reason, then I find it easier to first setup a music related activity without the Roon Controller, and then re-run the activity adding in the Roon controller.
  
When adding the device, Harmony may ask you which device you use to stream music. Select the Roon Control.

Once you have added the Roon Control to an activity, then I suggest you map the remote buttons as follows:

| Roon Action       | Harmony Button  | Roku Command   | Usage / Notes                            |
|-------------------|-----------------|----------------|------------------------------------------|
| Play/Pause        | Play            | Play           | Harmony appears to treat both play and pause as play for Roku devices |
| Play/Pause        | Pause           | Play           |                                          |
| Stop              | Stop            | PowerOff       | Make sure power control for the Roku emulator device is disabled |
| Skip back / Previous Track | Reverse | Rev           | Skip backward 30 seconds / hold for replay/previous track |
| Skip forward / Next Track | Forward  | Fwd           | Skip forward 30 seconds / hold for next track |
| Shuffle toggle    | Red             | Input HDMI1    | Toggle On/Off                            |
| Loop cycle        | Green           | Input HDMI2    | Cycles Off/Once/Repeat                   |
| Auto-radio toggle | Yellow          | Input HDMI3    | Toggle on/off                            |
|                   | Blue            | Input HDMI4    | Future planned feature                   |
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
|                   | -               | Backspace      | Future planned feature                   |
|                   | Exit            | Home           | Future planned feature                   |
|                   | Up              | Up             | Future planned feature                   |
|                   | Down            | Down           | Future planned feature                   |
|                   | Left            | Left           | Future planned feature                   |
|                   | Right           | Right          | Future planned feature                   |
|                   | OK              | Select         | Future planned feature                   |
|                   | Back            | Back           | Future planned feature                   |
|                   | Channel Up      | Page Up        | Future planned feature                   |
|                   | Channel Down    | Page Down      | Future planned feature                   |
|                   | Guide           | Search         | Future planned feature                   |
|                   | Info            | Info           | Future planned feature                   | 
|                   |                 | Instant Replay |                                          |
|                   |                 | Input AV1      |                                          |
|                   |                 | Input Tuner    |                                          |
|                   |                 | Input USB      |                                          |

_Some buttons are not needed right now, for example all of the browsing related buttons and some have no labels at all... yet! For some of these buttons, there are planned future feature that will make use of them as Deep Harmony continues to be developed._ 

Once this is complete, then test all the buttons and ensure they are to your liking and edit if necessary.

These mappings can be changed in the Roon settings.

Note: while there are a number of other currently unused buttons, future planned features are likely to use them which is why the channel up/down, browse and input related Roku buttons have been left alone.

## Tools Section

In additoin to the remote Pairing help for multiple hubs as described above the tools section also provide support for software updates and diagnostics.

### Software updates

Deep Harmony will periodically check for new sofware updates. When an update is available, then the status message next to the extension will indicate the new version available. This can be found in Roon UI by selecting _Settings_ from the main Roon menu and then selecting _Extensions_. Normally the status will simply indicate _OK_ to show that it is configurred and operating normally. If the availability of an update is indicated, then you can update your software version as follows:

1. Open settings for the extension by clicking on the _Settings_ button.
2. Expand the _**+** Tools_ section.
3. Find the drop down labelled _Update now_.
4. Select the requiured version from the drop down menu.
5. Click _Save_.

The extension will now download and unpack the update in the background and then exit once this is complete which should be in under a minute. When running the extenion in docker and when using the run scripts, then the extension will install the update and restart automatically with the new version.

### Diagnostics

To facilitate diagnosing any issues you may encounter the extenion includes an extensive loggings system along with a web server to give easy access to those logs from another computer. As the Roon settings system does not appear have any means of clicking on a link within the settings UI, the link for accessing long is presented in a text box labelled _Logs (Copy the URL)_. If you click on this text, then it should be highlighthed and you should be able to copy it and paste it into the address bar of a web browser such as Chrome or Edge. The should result in downloading a zip file containing recent logs.

There is also a section labelled _Logging switches_. Upon expanding this section there are many drops down for enabling or disabling logging of various components with in the extension. In general, you should probbaly leave these alone unless directed otherwise. The default setting here are chosen as a useful compromise to capture most likely issues without resulting in excessive CPU use due to log capture.

# Troubleshooting

| Issue | Resolution |
|----------|----------|
| Harmony remote appears to be controlling the wrong hub or zone | The remote device was added to the wrong Harmony hub. It will need to be removed and setup again. |
| Roon unable to discover the extension | Docker container was not started in _host_ or _bridge_ network modes and thus is hidden on a docker virtual network |
| Harmony unable to discover the Roku emulator | as above. |
| UI Controller sometimes exits when saving settings. | I have no idea of the cause. It could be Roon, it could be this extension. Just restart the Roon UI controller. I know the Roon settings UI can be a bit fragile and is particular sensitive to imperfections in an extension. |
| No X next to source device name | If you have a long Harmony hub name and/or activity name, then the X next to the external source control name is hidden so you cannot remove it. Use load defaults to reset the audio device settings. You will have to re-apply your chosen MQA, DSD and other settings. |

# Change History

## 2.0.0

### New Features
* Now supports multiple Harmony Hubs.
* Now supports multiple Roon zones allowing for each zone to be associated with a Harmony hub+activity as needed.
* New Roku emulator to provide many more buttons.
* Supports a separate Roku emulator per Harmony hub. 
* Quick access to upto 10 favourite playlists or internet radio services from Harmony remote.

## 1.1.0

### Fixes
 * Keyboard (Ctrl+M) mute not working in Roon UI
 * Improved device name not change when activity changed. (This _may_ also be a Roon Core issue).
 * Reduce calls to Roon and Harmony when settings dialog opened (may help those who have experienced issues with this).

### New Features
 * Rolling log capture and embedded web server for easy log access
 * Auto-update system to automatically download and make-ready new updates

### Improvements
 * Significantly reduced docker image size
 * Add ARMv7 docker image for Raspberry PI 3/3B+
 * Add basic console apps for Linux-x64, Linux-Armv7, Windows-x64 and MacOS-x64

### Changes
 * New Roon Device emulator _TCL Roku TV_ to provide many more buttons along with new suggested Harmony remote setup

### Known Issues
 * Occasionally the UI controller may stall or crash when changing settings or when changing source or volume devices. This _may_ be a Roon UI issue.
 * When changing Hub name, Activity name or changing the activity associated with a zone, while the source device will change in volume control pop-up, the devices names will not change in audio device settings. This _may_ be a Roon Core issue.

## 1.0.0 (beta)
 * Initial release

### New features
 * Roon Source Control linked to Harmony
 * Roon Volume Control linked to Harmony
 * Transport play/pause/stop/rew/fwd/next/previous from Harmony remote
 * Zone shuffle, loop and auto-radio control from Harmony remote

### Known Issues
 * Occasionally the UI controller may stall or crash when changing settings or when changing source or volume devices.
 * When changing Hub name, Activity name or changing the activity associated with a zone, while the source device will change in volume control pop-up, the devices names will not change in audio device settings.
  
# FAQ
**Why only Linux Docker and Why only Linux Docker host?**

Currently it is not possible to run MacOS inside a container. As for windows, then it is simply a case of not having looked into doing a windows build yet.

**Why cant I run the Linux-x64 image under Docker for Windows or Docker for Mac OS?**

The Linux docker host runs in a virtual machine on Docker for Windows and Docker for Mac with a virtual network bridge to your Windows or Mac host's network. The virtual network is a seprate network and so the service discovery methods used by Roon and Harmony cannot fully see your main home network and thuus cannot find the Roon extension. As a stop-gap, console apps for Windows and Mac OS have been made available however they are not packaged within installers nor registered as a service on Windows (or a daemon on OSX) nor have any means of keeping themselves running over any kind of failure.

# Acknowledgements

These are node modules used that have a significant part to play. Thanks are due to their authors for making them available.

* node-roonapi and related modules by Roon Labs LLC ([https://roonlabs.com/](https://roonlabs.com/))

  [https://github.com/RoonLabs/node-roon-api](https://github.com/RoonLabs/node-roon-api)

* npm-pkg

  [https://www.npmjs.com/package/pkg](https://www.npmjs.com/package/pkg)

* harmonyhubjs-client

  [https://github.com/swissmanu/harmonyhubjs-client](https://github.com/swissmanu/harmonyhubjs-client)

* harmonyhubjs-discover

  [https://github.com/swissmanu/harmonyhubjs-discover](https://github.com/swissmanu/harmonyhubjs-discover)

* node-xmpp-client

  [https://github.com/chris-rock/node-xmpp-client](https://github.com/chris-rock/node-xmpp-client)

* node-ssdp

  [https://github.com/diversario/node-ssdp](https://github.com/diversario/node-ssdp)


# Donating and some Background

A number of people have asked about donating to support this project and I was a bit taken aback that people would actually wish to donate, but after giving it some thought, it occurs that accepting donations may allow development to pursue directions that would otherwise be inaccessable for practical _freeware_ purposes. So to that end I have set up an account with Liberapay and a donate buttonm may be found at the bottom. Thank you everyone for your ongoing support.

Some of the ideas I am interesting in persuing are:

* Expanding the level of control to include a device UI with remote control browse, control of Roon zones other than that which you are listenign to and other related features.

* Some level of integration with Amazon Alexa and maybe Google Home. We use Amazon Alexa at home currently with a Spot and an Echo. I am interested in seeing of the Spot (and Show) can reasonably be used to display now playing information and provide basic voice and touch based media control.

This project started as the first stage of a home dash-board to integrate media control, lighting (Philips Hue for example), perhaps heating (for eg, Tado, Nest etc) and security (Ring, Nest etc). In time I still plan on looking at ways in which all of these system can be brought together. 

I also work for a tiny company in the UK that produces software for mobile devices for use at home and at school to help to make the internet and safer and more productive place for your children as well as to encourage more restrained use of media devices in the home to allow for better focus on family life and personal development of your children. 

There is quite alot of crossover between with I do at work and the personal interests I pursue for myself. We have all seen the fancy future promitional video of the future automated homes and perfect integrated families etc. In my own tiny way I try to make some of this a reality that we can all have while my employer attempts to positively tackle some of the resulting social fall out from our modern always-on connected world.

I wish more product companies were as enlightened as Roon Labs in the support they provide for community based extension of their product. While Roon (to my mind) has an excellent core architecture it is the possibility of extension and the extensions that many people in our community have created that sealed the deal for me and have made it the core of our music experience at home for my wife and myself. Finally we have a system with the richness of a PC based player, but that is standalone like a hardware player and like a the best hardware players can have a decent family friendly remote control and is muti-room and supports the sound quality aspirations of music and audio enthusiasts. Long may it continue!

[![Liberapay](https://liberapay.com/assets/widgets/donate.svg)](https://liberapay.com/Khazul/donate)
