---
layout: post
title: "Mac Settings"
date: 2018-07-12
categories: mac
tags: mac
comments: true
last_modified_at: 2022-09-05
---

- Do not remove this line (it will not be displayed)
  {:toc}

# Software that HEP poeple need on mac

1. [Skype](https://www.skype.com/en/)
2. [Zoom](https://cern.zoom.us/download)
3. Download Mac `self service` from CERN: [link](https://devices.docs.cern.ch/devices/mac/MacSelfService/). This will be download in background once you enroll and install proper certificates. Then from self-service one can install following software:
   1. xquartz (needed for visulations, as Mac OSX does not come with an X11 server installed.)
   2. cernbox app
   3. Mattermost app
   4. Joplin (note taking software)
   5. Latex and others
4. Apple app store
   1. xcode
   2. Numbers
   3. Keynote
   4. Pages
   5. Todoist: To-Do List & Task
5. [Sublime text](https://www.sublimetext.com)
   1. package control
   2. sftp
   3. AllAutocomplete: Autocomplete word from all open files.
   4. Terminal : Launch terminal from current file folder
   5. A File Icon: Sublime text file-specific icons for improved visual grepping
   6. BracketHighligher
   7. Expand selection to quotes: plugin to expand selection to surrounding quotes
   8. [AutoDocstring](https://packagecontrol.io/packages/AutoDocstring)
      Plugin for inserting / updating docstrings in Python after analyzing function parameters and the like
   9. [Anaconda](https://packagecontrol.io/packages/Anaconda)
      This turns your Sublime Text into a full featured Python IDE.
6. Visual Studio:

   Some details about problems faced and how to resolve is summarised here: [link]({{ site.baseurl }}{% link _posts/2022-04-03-VSCode.md %})

7. Download Homebrew ([https://brew.sh](https://brew.sh)).

   Just paste below command in mac terminal:

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

8. For efficiently organising literature: [https://www.jabref.org](https://www.jabref.org)
9. [sshpass](https://stackoverflow.com/a/63886356)

   One can install it using below command:

   ```bash
   brew install esolitos/ipa/sshpass
   ```

10. **Youtube video downloader**: youtube-dl

    ```bash
    brew install youtube-dl
    brew install ffmpeg
    ```

    for downloading a youtube video, go on terminal then:

    ```bash
    youtube-dl <youtube video sharing link>
    ```

    Best way to download the playlist is to use the playlist ID. For example, if the youtube link is

    ```
    https://www.youtube.com/watch?v=JdsXVrq5pVQ&list=PL5A5QJkW7MkttflM0JOGJsnxDSY32s092
    ```

    then use the command to download:

    ```bash
    youtube-dl -i PL5A5QJkW7MkttflM0JOGJsnxDSY32s092
    ```

    A script to download many youtube videos in one go is placed here: [link](https://gist.github.com/ram1123/7534f07e6904bb24bfa85bc87e76d2f7)

11. Antivirus for mac: [https://devices.docs.cern.ch/pss/eset/](https://devices.docs.cern.ch/pss/eset/)

# Some other settings

## Mattermost setting

1. How to browse: [https://mattermost.web.cern.ch](https://mattermost.web.cern.ch)

2. How to download: [https://about.mattermost.com/download/](https://about.mattermost.com/download/)

3. Settings to connect the app:

   **Server display name:** CERN

   **Server URL:** `https://mattermost.web.cern.ch`

## HOW TO MAKE A BOOTABLE USB STICK FROM AN ISO FILE ON AN APPLE MAC OS X

Reference: [https://www.lewan.com/blog/2012/02/10/making-a-bootable-usb-stick-on-an-apple-mac-os-x-from-an-iso](https://www.lewan.com/blog/2012/02/10/making-a-bootable-usb-stick-on-an-apple-mac-os-x-from-an-iso)

## ROOT installation using homebrew

```bash
brew install root
```

Reference: [https://root.cern/install/#macos-package-managers](https://root.cern/install/#macos-package-managers)

Also, root can be installed using conda. Check [here](https://root.cern/install/#conda)

### Old instructions

```bash
brew install root
brew info root6
. $(brew --prefix root6)/libexec/thisroot.sh
```

Reference: [https://alexpearce.me/2016/02/root-on-os-x-el-capitan/](https://alexpearce.me/2016/02/root-on-os-x-el-capitan/)

# Prevent SSH from disconnecting

Because of firewall or load-balancer the ssh session drops after being in ideal state for some time. To prevent this, one can configure the session to keepalive, which will prevent the the network device to consider it as ideal.

There are two methods. First method:

```bash
ssh -o "ServerAliveInterval 60" <SERVER_ADDRESS>
```

Second method: If one wants to keep all the ssh session alive then the keepalive information can be passed to the `.ssh/config` file. For this add

```bash
ServerAliveInterval 60
```

this line in file `/etc/ssh/ssh_config` or `~/.ssh/config`.

Reference: [https://superuser.com/questions/699676/how-to-prevent-ssh-from-disconnecting-if-its-been-idle-for-a-while](https://superuser.com/questions/699676/how-to-prevent-ssh-from-disconnecting-if-its-been-idle-for-a-while)

# kerberos setup for lxplus

1. Install "kerberos config file new" from _Mac Self-Service_. It can be found in the category "Configuration" of the _Mac Self-Service_.
2. Create a kerberos token using command: `kinit yourCernAccountName`
3. In file `~/.ssh/config` (if it does not exists create it) add following line:

   ```bash
   #
   Host lxplus.cern.ch aiadm.cern.ch mylinuxbox.cern.ch pcmydepmygroup*.cern.ch

   GSSAPIAuthentication yes
   GSSAPIDelegateCredentials yes
   ```

4. Then login as usual using ssh. It should login without any password.

Reference: [https://devices.docs.cern.ch/devices/mac/AboutKerberosAndSsh/](https://devices.docs.cern.ch/devices/mac/AboutKerberosAndSsh/)
