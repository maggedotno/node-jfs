Jotta File System (JFS) client in nodejs 
==============
This will eventually be a client for backup up local files to JottaCloud a fast, reliable and cheap cloud storage solution based in Norway. It's written in NodeJS and should work on most all OS and even devices like NAS. As Jotta hsa not released any official API or documentation this client is entierly created by examining the requests the official client does then figuring out how to recreate them.      

Install
--------------
Install nodejs and npm (node package manager).
Download the code, easiest is to use git and simply clone this repository.

    git clone https://github.com/paaland/node-jfs 

Then download the required dependencies:

    npm install 

Configure
--------------
Create the file config.json and insert your username and password:

    {
        "username": "yourusername",
        "password": "yourpassword" 
    }

Syntax
-------------
**Listing account info and devices:**

    node jsf --account

**Listing content**

    node jsf --ls Device/MountPoint/Folder

**Downloading a file**

    node jsf --get Device/MountPoint/Folder/File

**Upload a file**

    node jsf --put Device/MountPoint/Folder --file LocalFile.ext

Note that for now the destination folder must already exist.