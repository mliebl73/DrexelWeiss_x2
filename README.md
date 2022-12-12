# DrexelWeiss_x2

This is my Drexel & Weiss integration into Home Assistant leveraging Node-RED to handle the input/output from/to the USB / Serial interface directly plugged in to my raspberry pi.

Thanks to ikewestbrook from the home assistant community for the initial Node-RED implementation, that I based my work on.

I did not try to re-integrate the files into an empty HASS installation, so no guarantee this will work right out of the box. But I am happy to share whatever would be missing ;)

Packages used for Node-Red are node-red-contrib-home-assistant-websocket and the node-red-node-serialport.

The helpers and sensors are included as a package in my configuration.yaml, by adding the following at the beginning:

homeassistant:
  packages: !include_dir_named packages
  
The scripts and automations are in saparate directories under config/scripts and config/automations (maintaining the UI based automations with the second line), respectively and added with:

automation manual: !include_dir_merge_list automations/
automation ui: !include automations.yaml

script: !include_dir_merge_named scripts/

Note: I moved my other scripts.yaml and my automations.yaml in those directories as well so that they load as well


<img width="1048" alt="Screenshot 2022-11-06 at 22 58 54" src="https://user-images.githubusercontent.com/84347442/200252545-c423ac29-3d78-4b81-be75-b6889710dcb7.png">

![Screenshot 2022-11-06 at 23 24 22](https://user-images.githubusercontent.com/84347442/200252579-3aa1069a-507f-4a61-97d5-2d8e225c6033.png)
