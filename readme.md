JottaCloud File System (JFS) client in nodejs 
==============
This will eventually be a client for backup up local files to JottaCloud a fast, reliable and cheap cloud storage solution based in Norway. It's written in NodeJS and should work on most all OS and even devices like NAS. As Jotta has not released any official API or documentation this client is entirely created by examining the requests the official client does then figuring out how to recreate them.      

Requirements
--------------
    NodeJS (required), https://nodejs.org
    git (optional, but recomended), https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
    
Install
--------------
Install nodejs and npm (node package manager).
Download the code, easiest is to use git and simply clone this repository.

    git clone https://github.com/paaland/node-jfs 

Then download the required dependencies:

    npm install 

Update
-------------
To update if you used git simply do a git pull from within the node-jfs folder you previously cloned.

    git pull

Configure
--------------
Create the file config.json and insert your username and password:

    {
        "username": "yourusername",
        "password": "yourpassword" 
    }

Syntax
-------------
**Listing content**

    node jfs.js --ls [Device/MountPoint/Folder]

    --ls                            list all devices (if you have more than one)
    --ls device                     list all mount points on device
    --ls device/mountpoint          list all folders and files in mount point
    --ls device/mountpoint/folder   list all folders and files in folder

**Downloading a file**

    node jfs.js --get Device/MountPoint/Folder/File

**Upload a single file**

    node jfs.js --put Device/MountPoint/Folder --file LocalFile.ext

Note that for now the device (first part of path) must already exist.

**Upload a folder**

    node jfs.js --put Device/MountPoint/Folder --folder LocalPath --ignore .tmp --ignore temp 

This will scan all files (and folders) in LocalPath and upload any new or changed files. Ignoring any files containing ignore strings in name.

Example

    node jfs.js --put MyComputer/Backup/Pictures --folder "c:\Users\paaland\Documents\My Pictures" --ignore .tmp --ignore temp --ignore .thumb 2> Backup.%date%.errors.log

This will backup all content in c:\Users\paaland\Documents\My Pictures (except any files that has .tmp temp or .thump as part of their name) to Jotta device MyComputer, mount point Backup and folder Pictures.
Any errors will be logged to Backup.08.02.2017.errors.log (date is example).

Devices and mount points
=============
The first part of the path is called a device. Whether you can have multiple devices depends on your account type. Unlimited accounts can have an unlimited number of devices.
The device "Jotta" is reserved for the Jotta functionality. Under Jotta you will find "Sync", "Backup" and "Archive" which are reserved mount points.

    Jotta/Sync    -> This is where your sync folder resides
    Jotta/Backup  -> This is the mount point for backup of devices
    Jotta/Archive -> This is the mount point for archived files

Limitations
==============
* Note that JottaCloud is officially only for Windows. This means that file names and paths are not case sensitive. 
So README and readme will be the same file.
* To download files or list files in folders that has a space either encapsulate in quotes or use a + character 
("device/Home Videos" or device/Home+Videos)
* When uploading folders the client will calculate the MD5 hash for the file and query JottaCloud before uploading the file. Only new or changed files are uploaded.
* This client cannot create new devices. You have to use an existing device when uploading to JottaCloud (first part of destination URL).

API documentation
==============
This client has been made partially by observing what the official client does (by setting up a proxy) and the following "documentation":
http://forum.jotta.no/jotta/topics/api_http
