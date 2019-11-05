# OpenShift 4 downloader
## Description
This script will allow you to download some products related with OpenShift 4.

It will create `$HOME/bin` directory if not exists and will download the selected products on it using a naming convention which includes the version, so you will be able to use any version at any time.

It will also use symlinks to choose the downloaded version and will let you manage the symlinks easily.

## Disclaimer
While this script will allow you to download product related with OpenShift 4 from their public locations, please be aware that you'd better review the official documentation of each product. I will do my best in keeping the public URLs updated but if the official documentations refers to another location, you may be out of support if you use this ones.

## Usage
~~~
Usage: ocp4-downloader [--force] [--version <ver>] [--all|--client|--install|installer|--crc|--odo] [--set]
  --all               downloads all products
  --client|--oc       downloads OpenShift CLI (oc / kubectl)
  --crc               downloads CodeReady Containers (crc)
  --force             deletes any existing file matching the version
  --help|-h           shows this message
  --install|installer downloads OpenShift Installer (openshift-install)
  --odo               downloads OpenShift CLI for Developers (odo)
  --set               updates the symlink to whatever set in --version parameter
  --version <ver>     select the version to download for all components. Default: latest
~~~

## Examples
- Download latest OpenShift Client tools:
  ~~~
  $ ocp4-downloader --client 
  [main] Requested to download only some products: openshift-client.
  [main] Requested to download latest version of each requested component.

  [openshift-client] Downloading openshift-client-linux-4.2.0.tar.gz to disk, please be patient...
  [openshift-client] Extracting...
  [openshift-client] openshift-client-linux-4.2.0 successfully installed!!

  $ file $(which oc)
  /home/sgarcia/bin/oc: symbolic link to `openshift-client-linux-4.2.0'
  ~~~

- Download version 4.1.20 of OpenShift Installer and OpenShift Client tools:
  ~~~
  $ ocp4-downloader --client --install --version 4.1.20
  [main] Requested to download only some products: openshift-client openshift-install.
  [main] Requested to download 4.1.20 version of each requested component.

  [openshift-install] Downloading openshift-install-linux-4.1.20.tar.gz to disk, please be patient...
  [openshift-client] Downloading openshift-client-linux-4.1.20.tar.gz to disk, please be patient...
  [openshift-client] Extracting...
  [openshift-client] openshift-client-linux-4.1.20 successfully installed!!
  [openshift-install] Extracting...
  [openshift-install] openshift-install-linux-4.1.20 successfully installed!!

  $ file $(which oc openshift-install)
  /home/sgarcia/bin/oc: symbolic link to `openshift-client-linux-4.1.20'
  /home/sgarcia/bin/openshift-install: symbolic link to `openshift-install-linux-4.1.20'
  ~~~
  
- Change back the default version of openshift-client to 4.2.0:
  ~~~
  $ file $(which oc)
  /home/sgarcia/bin/oc: symbolic link to `openshift-client-linux-4.1.20'

  $ ocp4-downloader --client --set --version 4.2.0
  [main] Requested to download only some products: openshift-client.
  [main] Requested to download 4.2.0 version of each requested component.

  [openshift-client] File openshift-client-linux-4.2.0 is present.
  [openshift-client] openshift-client-linux-4.2.0 successfully set as default!!

  $ file $(which oc)
  /home/sgarcia/bin/oc: symbolic link to `openshift-client-linux-4.2.0'
  ~~~

- Install latest version if all products:
  ~~~
  $ ocp4-downloader --all
  [main] Requested to download all products: openshift-client openshift-install crc odo.
  [main] Requested to download latest version of each requested component.

  [odo] Downloading odo-linux-amd64.tar.gz to disk, please be patient...
  [crc] Downloading crc-linux-amd64.tar.xz to disk, please be patient...
  [openshift-client] Downloading openshift-client-linux-4.2.0.tar.gz to disk, please be patient...
  [openshift-install] Downloading openshift-install-linux-4.2.0.tar.gz to disk, please be patient...
  [odo] Extracting...
  [odo] odo-linux-1.0.0 successfully installed!!
  [openshift-install] Extracting...
  [openshift-install] openshift-install-linux-4.2.0 successfully installed!!
  [openshift-client] Extracting...
  [openshift-client] openshift-client-linux-4.2.0 successfully installed!!
  [crc] Extracting...
  [crc] crc-linux-1.0.0 successfully installed!!
  ~~~

## Todo
- List existing versions
- Delete existing version

## Contact
Reach me in [Twitter] or email in soukron _at_ gmbros.net

## License
Nothing to be licensed, but just in case, everything in this repo is licensed under GNU GPLv3 license. You can read the document [here].

[Twitter]:http://twitter.com/soukron
[here]:http://gnu.org/licenses/gpl.html

