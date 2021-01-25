# WINDOWS SUBSYSTEM FOR LINUX 2 as DEVELOPMENT MACHINE

## Win 10 / Enable WSL and VMP

PowerShell:
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform
```

## Win 10 / Install Kernel Update
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi


## Win / Set WSL 2 as default
PowerShell:
```
wsl --set-default-version 2
```

## Win / Install Windows Package Manager (winget)
```
https://www.microsoft.com/en-us/p/app-installer/9nblggh4nns1?activetab=pivot:overviewtab
```

## Win / Install Linux distro
```
winget install Canonical.Ubuntu
```

## Win / Tune Linux distro configuration

Create `.wslconfig` file on the current user home:

```
notepad "$env:USERPROFILE/.wslconfig"
```

Add:
```
[wsl2]
memory=8GB   # Limits VM memory in WSL 2
processors=4 # Makes the WSL 2 VM use that number of virtual processors
```

See https://docs.microsoft.com/en-us/windows/wsl/wsl-config#wsl-2-settings for all options.


## Win / Install Windows Terminal
```
winget install Microsoft.WindowsTerminal
```

## Win / Optional: Install X11 server
```
winget install marha.VcXsrv
```
Invoke it like this once installed. This equivalent marking "Disable Access Control" during the GUI installer.
```
vcxsrv.exe -ac
```
NOTE: You need to allow public access via Windows Defender ("Allow apps to communicate through Windows Defender Firewall")

## WSL / Passwordless sudo

Open Linux distro with `wsl`, then:

```
echo "$USER  ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/$USER
```

## WSL: Install OhMyBash for a fancy PS1
```
wsl bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

## WSL / Optional: Prepare for X11 on Windows
Add to `~/.bashrc` (provide IP of your Windows host):
```
export DISPLAY=$(ip route | awk '/default via / {print $3; exit}' 2>/dev/null):0
export LIBGL_ALWAYS_INDIRECT=1
```

## WSL / Update
Bash:
```
sudo apt-get update
suod apt-get dist-upgrade
```

## WSL / Setup Tools

Git:
```
git config --global user.email "donhector@gmail.com"
git config --global user.name "donhector"
```

SSH Agent:
```
sudo apt-get install keychain
```

Add to ~/.bashrc
```
# For Loading the SSH key
/usr/bin/keychain --nogui $HOME/.ssh/id_rsa
source $HOME/.keychain/$HOSTNAME-sh
```

## Win / Install Docker Desktop
```
winget install Docker.DockerDesktop
```

Enable `Enable the experimental WSL 2 based engine` on `General` tab if not already enabled.
Enable your WSL distro on `Resources` tab.

### WSL / Verify
Bash:
```
docker info
docker run hello-world
```

## Win / Map Network drive to Linux distro home \\wsl$\Ubuntu

Right click on the \\wsl$\Ubuntu folder and select "Map network drive..."


## Win / Install additional software
```
winget install 7Zip.7Zip
winget install Google.Chrome
winget install Google.BackupAndSync
winget install Lexikos.AutoHotkey
winget install VideoLAN.VLC
winget install Piriform.CCleaner
winget install Notepad++.Notepad++
winget install Valve.Steam
```

## Win / Exclude certain folders from Windows Defender Scanning



## WSL / Install additional DEV tools
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common \
    wget \
    jq

curl -sLS https://dl.get-arkade.dev | sudo sh

