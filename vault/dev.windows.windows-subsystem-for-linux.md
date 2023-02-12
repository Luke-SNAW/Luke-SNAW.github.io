---
id: sljkvoig4nmdb1gpa89znah
title: Windows Subsystem for Linux
desc: ''
updated: 1666074671516
created: 1666074627296
---

> https://learn.microsoft.com/ko-kr/windows/wsl/install

## [Update WSL kernel](https://pureinfotech.com/install-windows-subsystem-linux-2-windows-10/)

To update the WSL kernel to the latest version, use these steps:

1. Open **Start**.
2. Search for **Command Prompt**, right-click the top result, and select the **Run as administrator** option.
3. Type the following command to *update the WSL kernel* and press **Enter**:

```shell
wsl --update
```

https://learn.microsoft.com/ko-kr/windows/wsl/install-manual#step-3---enable-virtual-machine-feature

## [Set default version](https://pureinfotech.com/upgrade-wsl2-wsl1-windows-10/)

Type the following command to set Windows Subsystem for Linux 2 your default architecture for new distros you’ll install and press **Enter**:

```shell
wsl --set-default-version 2
```

Type the following command to get a list of all the distros installed on your device and press **Enter**:

```shell
wsl -l -v
```

Type the following command to convert the distro from WSL 1 to WSL 2 and press **Enter**:

```shell
wsl --set-version DISTRO-NAME 2
```

## [How to reset WSL2 Linux distro on Windows 10](https://pureinfotech.com/reset-wsl2-linux-distro-windows-10/)

## Trouble-shooting

### [WSL: VSCode server install fails on Ubuntu](https://github.com/microsoft/vscode-remote-release/issues/1856)

> **consider to run only node in WSL, the others in windows.**
> git setting, vs code expansions needs to be redundant.

Running Windows 10, WSL with Ubuntu 19.10.

The VSCode server install fails when untaring the server: `'/bin/gzip: 10: Syntax error: "(" unexpected'`

WSL log:

```shell
[2019-11-09 01:04:18.721] Starting server: /home/mellowd/.vscode-server/bin/86405ea23e3937316009fc27c9361deee66ffbf5/server.sh --port=0 --fileWatcherPolling=0
[2019-11-09 01:04:18.721] /bin/gzip: 10: Syntax error: "(" unexpected
[2019-11-09 01:04:18.721] tar: Child returned status 2
[2019-11-09 01:04:18.721] tar: Error is not recoverable: exiting now
[2019-11-09 01:04:18.721] /bin/gzip: 10: Syntax error: "(" unexpected
[2019-11-09 01:04:18.721] tar: Child returned status 2
[2019-11-09 01:04:18.721] tar: Error is not recoverable: exiting now
[2019-11-09 01:04:18.721] ERROR: Unpacking failed: Files expected: 0, is 1
[2019-11-09 01:04:18.721] /mnt/c/Users/mellowd/.vscode/extensions/ms-vscode-remote.remote-wsl-0.40.2/scripts/wslServer.sh: 60: /home/mellowd/.vscode-server/bin/86405ea23e3937316009fc27c9361deee66ffbf5/server.sh: not found
[2019-11-09 01:04:18.721] VS Code Server for WSL closed unexpectedly.
```

https://github.com/microsoft/WSL/issues/4461#issuecomment-1132360882

> I am also affected by this bug again in Ubuntu 22.04. Weirdly enough, the rest of the binaries work fine. Only gzip seems to fail.

use this command may help

```shell
echo -en '\\x10' | sudo dd of=/usr/bin/gzip count=1 bs=1 conv=notrunc seek=$((0x189))
```
