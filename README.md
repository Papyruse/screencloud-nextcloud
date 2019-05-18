# ScreenCloud - NextCloud

A NextCloud service plugin for ScreenCloud

## Installation

* Go to: **Preferences** -> **Online Services** -> **More services**
* Select: **Install from URL** and paste the following address:

```
https://github.com/Papyruse/screencloud-nextcloud/archive/master.zip
```

* Or go to: **Preferences** -> **Online Services** -> **More Services**
* Select: **Mirror: Other** and paste the following address:

```
https://github.com/Papyruse/screencloud-nextcloud/raw/master/plugin-list.xml
```

Tested and working with Nextcloud 15.0.2, ScreenCloud 1.3.0 from Debian 9.0 repo on Ubuntu 18.10.

PS: In "Server URL" use "https://nextcloud.domain.com", not the WebDAV url.

To install ScreenCloud from Debian 9.0 repo:

Add the Screencloud repo:

```
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/home:/olav-st/Debian_9.0/ /' >> /etc/apt/sources.list.d/screencloud.list"
```

Update your software sources and install Screencloud’s Debian app:

```
sudo apt-get update && sudo apt-get install screencloud
```

Download the repo key:

```
cd /tmp
```
```
wget http://download.opensuse.org/repositories/home:olav-st/Debian_9.0/Release.key
```

Add the repo key:

```
sudo apt-key add - < Release.key
```

Guide source: https://www.omgubuntu.co.uk/2016/06/force-install-screencloud-ubuntu-16-04


# Screenshots

Plugin installed:

![screenshot installed](https://raw.githubusercontent.com/Papyruse/screencloud-nextcloud/master/Screenshot%20at%2017_56_41.png?raw=true "Plugin installed")

Plugin settings:

![screenshot settings](https://raw.githubusercontent.com/Papyruse/screencloud-nextcloud/master/Screenshot%20at%2018_06_39.png?raw=true "Plugin settings")

Images uploaded:

![screenshot uploaded](https://raw.githubusercontent.com/Papyruse/screencloud-nextcloud/master/Screenshot%20at%2018_14_08.png?raw=true "Images uploaded")


## Extras

At this time, Nextcloud don't permit to share uploaded files with their name + extension to the link itself, feature needed sometime for services like chat, forum preview, etc..

With the Public Path feature from the plugin and a little web server configuration, you can bypass this limitation like below :


```
# Create a virtual website folder
mkdir -p /var/www/screenshots/johndoe

# Symlink you real upload account folder to this one
ls -s /var/www/nextcloud/data/johndoe/files/screenshots /var/www/screenshots/johndoe

# Create a new vhost (like apache)
vi /etc/apache2/sites-available/screenshots.domain.tld.conf

# Add primary directives and this code block

DocumentRoot /var/www/screenshots/
<Directory /var/www/screenshots/>
        Options FollowSymlinks
        AllowOverride None
        Require all granted
</Directory>

# Activate new website
a2enmod screenshots.domain.tld.conf

# Reload web server
systemctl reload apache2
```

Then access to your uploads with the new URL : https://screenshots.domain.tld/johndoe/snap_xxx.png


## Info

Forked and customized from https://github.com/p3lim/screencloud-webdav, thank to the author.

