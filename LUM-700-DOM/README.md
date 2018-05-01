# Luma Camera Documentation

**Please Note:** This documentation was written and tested to work with an older firmware version. The newer Luma cameras ship with firmware that makes you set a username & password on first boot versus the hardcoded `admin/admin` credentials outlined here. When resetting theese cameras, you may be able to set a custom password, but I am not sure if this is true or not. 

## Specifications:

**Model Number:** LUM-700-DOM-IPH-WH

**Resolution:**

| Resolution | Max FPS |
|------------|---------|
| 2688x1520  | 20      |
| 1920x1080  | 30      |
| 1280x720   | 30      |

**Power:** IEEE 802.11af POE (48V)

**SD Card Slot:** Up to 128GB

## Resetting the Camera:
Before using the camera with a custom NVR, you will need to reset it to the factory defaults.

### Tools Needed:
* Hex 3.0 Bit
* Phillips Head 2.0 Bit

### Step 1: Remove Outer Casing Screws
![Camera](images/camera_normal.jpg)
![Camera Screws](images/camera_cover_removed_2.jpg)
![Camera Lid Detached](images/camera_cover_removed_1.jpg)

### Step 2: Remove Plastic Lens Assembly Cover
![Remove Plastic Cover By Pinching Sides](images/remove_plastic_cover.jpg)
![Camera Lid and Plastic Cover Removed](images/camera_cover_removed_3.jpg)

### Step 3: Locate, Then Press and Hold Reset Button for 15 Seconds.
![Close Up on User Area of Mainboard. Reset Switch, SD Card Slot, and other connectors pictured](images/reset_switch.jpg)

## Setting Up a DHCP Server:

To configure the camera, you have to set up a DHCP server so it can get an IP. The range it uses is `192.168.123.3-192.168.123.254`. Your computer should be configured with a static IP of `192.168.123.1` and the router configured with a static IP of `192.168.123.2`.

**Subnet:** `192.168.123.0/24`

**Start Address:** `192.168.123.3`

**End Address:** `192.168.123.254`

**Router:** `192.168.123.2`

**DNS:** Personal Preference. I use `8.8.8.8` and `8.8.4.4`

**Workstation IP:** `192.168.123.1`

## Powering the Camera:

The Luma LUM-700-DOM-IPH-WH uses the IEEE 802.11af POE standard. Any switch or POE injector that supports this and the wattage/voltage the camera supports should be able to power it via POE. The camera and Switch/POE Injector should negotiate and the camera should recieve power.

## Finding the Cameras IP Address:

After you have set up the DHCP Server, you can check the DHCP leases to see if the camera has obtained an IP address yet. If you don't see the IP Pop up, you can use `nmap` to search for the camera via this command: `nmap -v 192.168.123.0/24`.

By default, the camera has a few ports open:

|PORT|STATE|SERVICE|
|----|-----|-------|
|22/tcp|filtered|ssh|
|80/tcp|open|http|
|554/tcp|open|rtsp|
|8000/tcp|open|http-alt|
|8200/tcp|open|trivnet1|

**From here on out, your camera's IP address will be referred to as `CAM_IP`.**

Point your browser towards `http://CAM_IP/` and you should see a login page like the following:
![LUMA Default Login Page](images/screenshots/login.png)

The default credentials for this camera are as follows:

|USERNAME|PASSWORD|
|--------|--------|
|admin|admin|

*Note: On newer firmware versions, the camera will prompt you to create a password, and will not have hardcoded credentials.*

## Changing the Cameras IP Address & Other Settings:

When you log in, you will see this if you aren't on safari with the Luma plugin: 

![LUMA Homepage](images/screenshots/interface.png)

Click the gears on the right sidebar.

![Gears Icon](images/screenshots/gears.png)

This will bring you to the main settings page.

![Settings Page](images/screenshots/settings_mainpage.png)

Using the left sidebar, navigate to "Basic Network Settings"

![Basic Network Settings Tab](images/screenshots/network_tab.png)

Under this menu, you can change the cameras IP address, and ports for different services.

![Network Settings Menu 1](images/screenshots/network_settings.png)

## Using The Cameras RTSP Stream:

The default RTSP port on the camera is 554. The url is formatted like this: `rtsp://CAM_IP/Streaming/channels/101`

If you have set custom credentials on your camera, you can use this format: `rtsp://username:password@192.168.1.20/Streaming/channels/101`
