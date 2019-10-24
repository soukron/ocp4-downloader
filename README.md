# OpenShift 4 downloader
## Description
This script will allow you to download some products related with OpenShift 4.

It will create `$HOME/bin` directory if not exists and will download the selected products on it using a naming convention which includes the version, so you will be able to use any version at any time.

It will also use symlinks to choose the downloaded version but it won't (for now) allow you to manage the symlinks. You will need to edit them manually in order to use different versions.

## Disclaimer
While this script will allow you to download product related with OpenShift 4 from their public locations, please be aware that you'd better review the official documentation of each product. I will do my best in keeping the public URLs updated but if the official documentations refers to another location, you may be out of support if you use this ones.

## Usage
~~~
Usage: ocp4-downloader [--force] [--version <ver>] [--all|--client|--oc|--install|installer|--crc|--odo]
  --all               downloads all products
  --client|--oc       downloads OpenShift CLI (oc / kubectl)
  --crc               downloads CodeReady Containers (crc)
  --force             deletes any existing file matching the version
  --help|-h           shows this message
  --install|installer downloads OpenShift Installer (openshift-install)
  --odo               downloads OpenShift CLI for Developers (odo)
  --version <ver>     select the version to download for all components. Default: latest
~~~

## Examples
- Download latest OpenShift Client tools:
  ~~~
  $ ocp4-downloader --client 
  -> Requested to download only some products: openshift-client.
  -> Requested to download latest version of each requested component.

  [openshift-client] Downloading version 4.2.0 to disk (~30MB)...
  [openshift-client] Extracting... 
  [openshift-client] openshift-client 4.2.0 successfully installed!!
  
  $ ls -l $(which oc)
  lrwxrwxrwx 1 sgarcia sgarcia 29 Oct 24 04:24 /home/sgarcia/bin/oc -> openshift-client-linux-4.2.0
  ~~~

- Download version 4.1.20 of OpenShift Installer and OpenShift Client tools:
  ~~~
  $ ocp4-downloader --client --install --version 4.1.20
  -> Requested to download only some products: openshift-client openshift-install.
  -> Requested to download 4.1.20 version of each requested component.

  [openshift-install] Downloading version 4.1.20 to disk (~70MB)...
  [openshift-client] Downloading version 4.1.20 to disk (~30MB)...
  [openshift-client] Extracting... 
  [openshift-client] openshift-client 4.1.20 successfully installed!!
  [openshift-install] Extracting... 
  [openshift-install] openshift-install 4.1.20 successfully installed!!

  $ ls -l $(which openshift-install oc)
  lrwxrwxrwx 1 sgarcia sgarcia 29 Oct 24 04:28 /home/sgarcia/bin/oc -> openshift-client-linux-4.1.20
  lrwxrwxrwx 1 sgarcia sgarcia 30 Oct 24 04:29 /home/sgarcia/bin/openshift-install -> openshift-install-linux-4.1.20
  ~~~
  
- Download latest version of all products:
  ~~~
  $ ./ocp4-downloader --all
  -> Requested to download all products: openshift-client openshift-install crc odo.
  -> Requested to download latest version of each requested component.

  [odo] Downloading version latest to disk (~25MB)...
  [crc] Version 1.0.0 is already present. Skipping installation.
  [openshift-install] Downloading version 4.2.0 to disk (~70MB)...
  [openshift-client] Version 4.2.0 is already present. Skipping installation.
  [odo] Extracting...
  [odo] odo 1.0.0 successfully installed!!
  [openshift-install] Extracting... 
  [openshift-install] openshift-install 4.2.0 successfully installed!!
  ~~~

## Todo
- Manage symlinks from the tool itself to switch between versions

## Contact
Reach me in [Twitter] or email in soukron _at_ gmbros.net

## License
Nothing to be licensed, but just in case, everything in this repo is licensed under GNU GPLv3 license. You can read the document [here].

[Twitter]:http://twitter.com/soukron
[here]:http://gnu.org/licenses/gpl.html

