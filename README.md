# DrexelWeiss_x2

This is my Drexel & Weiss integration into Home Assistant leveraging Node-RED to handle the input/output from/to the USB / Serial interface directly plugged in to my raspberry pi.

Thanks to ikewestbrook from the home assistant community for the initial Node-RED implementation, that I based my work on.

I did not try to re-integrate the files into an empty HASS installation, so no guarantee this will work right out of the box. But I am happy to share whatever would be missing ;)

The helpers and sensors are included as a package in my configuration.yaml, by adding the following at the beginning:

homeassistant:
  packages: !include_dir_named packages
  
The scripts and automations are in saparate directories under config/scripts and config/automations, respectively and added with:

automation: !include_dir_merge_list automations/

script: !include_dir_merge_named scripts/

Note: I moved my other scripts.yaml and my automations.yaml in those directories as well so that they load as well
