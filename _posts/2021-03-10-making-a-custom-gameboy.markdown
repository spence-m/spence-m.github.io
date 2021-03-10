---
layout: post
title:  "Making a Gameboy with a Raspberry Pi Zero W and GPi case"
date:   2021-03-10
categories:
 - retro gaming
 - raspberry pi zero
comments: false
---

This custom Gameboy can play all the classics and even has a backlight :)

![Custom gameboy on my desk](/images/gameboy-front.jpeg)

Hardware you’ll need:
* GPi CASE
* Raspberry Pi Zero W (make sure you get the one without the pre-soldered header otherwise it won’t fit inside the cartridge)
* Micro SD Card, I’d recommend at least 8GB
* Micro SD card reader
* 3 x AA battery

Software you’ll need:
* SD card writer, I use [Etcher](https://github.com/balena-io/etcher/releases/download/v1.5.116/balenaEtcher-Setup-1.5.116.exe) on Windows
* An SSH client, I use [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) on Windows

## Assemble your GPi case
Follow the GPi case assembly instructions [here](http://download.retroflag.com/manual/case/GPi_CASE_Manual.pdf) and then proceed to the next step.

## Download RetroPie
**Make sure to download the Raspberry Pi 0/1 version**

[Download](https://retropie.org.uk/download/)

## Download GPi case patch
[Download](http://download.retroflag.com/Products/GPi_Case/GPi_Case_patch.zip)

## Flash SD card
1. Insert your SD card into your computer
2. Open Etcher
3. Select `Flash from file`
4. Select the Retropie img.gz that you downloaded in step 2
5. Select `Select target`
6. Select your Micro SD card
7. Finally, select `Flash!`

Once your SD card has been flashed it will be ejected. Re-insert your SD card reader into your computer to mount it as mass storage for the next step.

## Configure WiFi
WiFi will allow you to easily drag-and-drop ROMs from your computer to your Gameboy.

1. Open your SD card in file File Explorer, it was named BOOT for me
2. In the root folder create a file called wifikeyfile.txt and add the following information into the file:
```
ssid="NETWORK_NAME"
psk="NETWORK_PASSWORD"
```
3. Replace `NETWORK_NAME` and `NETWORK_PASSWORD` with your home network name and WiFi password

## Add patch
1. Unzip `GPi_Case_patch.zip`. You’ll find a folder called `GPi_Case_patch` and a `readme.txt`
2. Copy the `GPi_Case_patch` to the root of your SD card
4. Go inside the `GPi_Case_patch` folder on your SD card and run `install_patch.bat`
5. Safely eject your SD card, insert it into your gameboy cartridge, insert your batteries, and switch that bad boy on

## Set up controls
1. Once booted you'll be prompted to configure each button on your case. Retropie supports a plethora of systems so skip the buttons you don't need by holding down any button

**Tip: I configure the two rear buttons to left and right shoulder so I can also play Gameboy Advance games**

## Enable WiFi
1. Select `WiFi` on the configuration menu
2. You’ll be asked whether you want to launch raspi-config to set your country, select `Yes`
3. Press the down arrow several times until you get to `Localisation`
4. Press the right arrow to highlight `Select`
5. Press `(B)`
6. Select `WLAN country` in the same way you did with localisation
7. Now select your country from the list in the same way
8. Once you’ve set your WLAN country you can select `Finish`
9. You’ll be asked whether you want to reboot, select `Yes`
10. Once rebooted, select `(A)` to go into configuration
11. Select `WiFi` again
12. Select `3. Import WiFi credentials from…` -- if your credentials were successfully imported you should see that your IP address has been populated
13. Select `Exit` to go back to the configuration menu

## Enable SSH
We enable SSH so we can change the default password for the pi and also install the safe shutdown script remotely.

On the configuration menu:
1. Select `raspi-config`
2. Select `interface options`
3. Select `P2 SSH`
4. You’ll be shown a warning, select `Yes`
5. Select `Ok`
6. Select `Finish`

## Configure security
We should change the default password on your Raspberry Pi just to be safe.

1. Select `WiFi` on the configuration menu so you can view the Gameboy's IP address
2. Open PuTTY on your PC
3. Set the Host Name as the IP shown on your Gameboy
4. Click Open
5. Accept the warning
6. Login as the user: `pi`
7. Enter the password: `raspberry`
8. Once you’re in type: `passwd`
Follow the onscreen instructions to update your password

## Install safe shutdown patch
Run:
```
wget -O - "https://raw.githubusercontent.com/RetroFlag/retroflag-picase/master/install_gpi.sh" | sudo bash
```

Once the script has finished installing your SSH session will end and your Gameboy will reboot.

## Disable SSH
We don't really need SSH enabled now we have installed the safe shutdown script.

1. Once the Gameboy has rebooted go to the configuration menu
2. Select `raspi-config`
3. Select `interface options`
5. Select `SSH`
6. Select `No`
7. Select `Ok`
8. Select `Finish`

## Enable safe shutdown
1. Press `Start`
2. Select `Quit`
3. Select `Shutdown System`
4. Select `Yes` to confirm
5. Flick the power switch off and pop the batteries out once the device is off
6. Switch the safe shutdown switch to ON. This switch is located underneath where the batteries go

This will now safely shutdown the device when you flick the power switch instead of having to go to the configuration menu to shutdown safely each time.

## Install ROMs
1. Switch your Gameboy back on
2. Go to `\\retropie\roms` in the File Explorer on your PC and you’ll be greeted with folders for all the different systems that Retropie supports. The ones you’ll be mostly interested in are `gb`, `gba`, and `gbc`. These stand for gameboy, gameboy advance, and gameboy color
3. Drop your ROMs into the correct device folders
4. Reboot

Phew, we made it! :) Now go play Mother 3