# Asus Zenfone wireless file transfer automatic downloader
Asus zenfone automatic download scripts to download full folders from "wireless file transfer" without the need to zip them.

## How does this work
The script uses the json representation returned by the "wireless file transfer" protocol to download each of the files listed in the defined folder one by one.
Only unix tools are used, this script is not tested nor developed to work on windows systems

## Required tools
* sed
* jq
* curl
* xargs
* wget

### Ubuntu/Debian installation
```bash
apt install sed jq curl xargs wget
```

### Mac OS
```bash
brew install jq gnu-sed wget 
```

## Automatic download script
```bash
curl -s http://[YOUR LOCAL WIRELESS FILE TRANSFER DEVICE]/file/[PATH OF THE FOLDER]/ | jq '.result' | jq 'map(.name)' | tail -n +2 | head -n -1 | sed -e sed -e 's/  "//g' -e 's/"//g' -e 's/,//g' -e 's/^/http:\/\/[YOUR LOCAL WIRELESS FILE TRANSFER DEVICE]\/file\/[PATH OF THE FOLDER]\//g' | xargs wget
```

In order for the script to correctly work you have to substitute:
* `[YOUR LOCAL WIRELESS FILE TRANSFER DEVICE]` with the ip:port pair given from your device, like the following example `192.168.1.2:55432`
* `[PATH OF THE FOLDER]` with the path of the folder you want to download, like the following example `Memoria%20interna/DCIM/Camera`, remember to url encode all special characters in folder names
