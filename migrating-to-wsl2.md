# Migrating from WSL1 to WSl2

## Steps
1. [Install/Enable WSL2](./migrating-to-wsl2.md/#installenable-wsl2)
2. [Install new Ubuntu Distro](./migrating-to-wsl2.md/#Install-new-Ubuntu-Distro)
3. [Configure Software for the new VM](./migrating-to-wsl2.md/#Configure-Software-for-the-new-VM)
4. [Migrate data to new Distro](./migrating-to-wsl2.md/#Migrate-data-to-new-Distro)
5. [Change file/folder permissions](./migrating-to-wsl2.md/#change-filefolder-permissions)

### Install/Enable WSL2
To install WSL1 you previously ran the following command in Powershell: 
```Powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

To continue onto the more stable and robust WSL2 we run the following commands in Powershell to enable virtualization: 

```Powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

**Once Virtualization is enabled, we'll want to run/install he Linux Kernal Update package found [here](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).**

WSL2 should now be configured. Now we want to instruct newly installed Distros to utilize WSL2 instead by running the following Powershell command: 

```Powershell
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
```

### Install new Ubuntu Distro
Distro is shorthand for *distribution*. The preference for this course is the Ubuntu Distribution. There are three versions listed in the Microsoft Store. It doesn't matter which one we use but the preference would be *Ubuntu* or *Ubunutu 20.04*. 

1. Open the Microsoft Store
2. Search for "Ubuntu"
3. Install either "Ubuntu" or "Ubuntu 20.04", whichever one you **do not** have installed as WSL1. 

### Configure Software for the new VM
1. Open the new distribution. 
2. Input Username and Password ((These credentials do not need to be the same as the previous Distribution or Windows)) 
3. Install [Node.js](./nodejs-setup.md)
4. Install [Python](./python-setup.md)

### Migrate data to new Distro
Because this is a new distribution, it contains none of the data we've created previously in the WSL1 instance. We can migrate the data using Windows Explorer. 

1. Open both the old and new Ubuntu installations
2. Open Windows File Explorer and navigate to `\\wsl$`
3. There should be two folders, one for each distribution. Open each one in a separate window so we can drag-and-drop files between distributions.
4. Open the home directory in each distribution followed by the username directory. 
5. Drag and drop any files that are wanting to be kept. 

### Change file/folder permissions
By transferring files across distributions, we lose access to read and write files in the new distribution. To fix this we can take ownership of those files be running the following command in the new distribution where files were transferred to. 
  
```bash
chown -R $USER DIRECTORY
```

Where `DIRECTORY` is any folders with files you wish to take ownership of. 


> instalation of WSL2 sourced from [here](https://docs.microsoft.com/en-us/windows/wsl/install-manual)