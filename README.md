# DrexelWeiss_x2

This is my Drexel & Weiss integration into Home Assistant leveraging Node-RED to handle the input/output from/to the USB / Serial interface directly plugged in to my raspberry pi.

Thanks to ikewestbrook from the home assistant community for the initial Node-RED implementation, that I based my work on.

I did not try to re-integrate the files into an empty HASS installation, so no guarantee this will work right out of the box. But I am happy to share whatever would be missing ;)

## Python Script Setup

This repository also includes Python scripts for processing TID data. To set up the Python environment:

```bash
# Create a virtual environment (recommended)
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

**Note:** The `requirements.txt` file pins `urllib3` to version 1.26.x to ensure compatibility with LibreSSL 2.8.3. This prevents the "NotOpenSSLWarning" that occurs with urllib3 v2.0+ which requires OpenSSL 1.1.1+.

## Home Assistant Integration

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

## Troubleshooting

### urllib3 OpenSSL Warning

If you encounter the following warning:
```
NotOpenSSLWarning: urllib3 v2 only supports OpenSSL 1.1.1+, currently the 'ssl' module is compiled with 'LibreSSL 2.8.3'
```

**Recommended Solution (Best for Security):** Upgrade your Python installation or system OpenSSL library to a version that includes OpenSSL 1.1.1+. This allows you to use urllib3 v2.6+ which includes important security fixes.

For macOS users:
- Install Python from python.org instead of using the system Python
- Or use Homebrew: `brew install python@3.9` (or later stable version)
- Or upgrade macOS to a newer version

**Alternative Solution (Quick Fix):** The `requirements.txt` file pins urllib3 to version 1.26.x for compatibility with LibreSSL 2.8.3. Install dependencies using:
```bash
pip install -r requirements.txt
```

If you already have urllib3 v2 installed, you can downgrade it:
```bash
pip install 'urllib3<2.0'
```

**Note:** urllib3 1.26.x has known security vulnerabilities that are fixed in v2.6+. Use this workaround only if you cannot upgrade your SSL library, and be aware of the security implications.
