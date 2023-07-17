# KEVIN NITRO RCLONE CHEAT SHEET

These are my personal rclone tips, commands,... not a document for rclone or sth 😪

# SILENTCMD

## What is it?

It helps to run command silently, not shows out any log

- Go to [SilentCMD repo][SilentCMD repo]
- Download, put it in a folder
- Set environment for SilentCMD

# RCLONE COMMANDS

## ARG

```
--transfers 8
--auto-confirm
--drive-server-side-across-configs
--config
-v
```

## COPY, MOVE, SYNC

```
rclone copy "Source" "Destination"
```

so on with move, sync

## MOUNT

### For Windows:

- You'd rather use [SilentCMD](#silentcmd)
- Create a batch file _(Ex: mount.bat)_
- Fill in this script

```mount.bat
@echo off

set website_to_ping=google.com

:CHECK_CONNECTION
ping %website_to_ping% -n 1 > nul
if %errorlevel% neq 0 (
    echo Connection to google.com failed. Retrying in 5 seconds...
    timeout /t 5 > nul
    goto CHECK_CONNECTION
)

echo Connection to google.com successful. Continue with script execution.

start SilentCMD rclone mount [replace you command here!!!!]

start SilentCMD taskkill /f /im SilentCMD.exe /DELAY:2
```

Rclone mount command: _(My personal command)_

```rclone mount command
rclone mount CombineNeccessary: Z: --cache-dir "D:\Program Files\Rclone Cache" --vfs-cache-mode full --network-mode --volname "Cloud Storages" --no-modtime --no-checksum --buffer-size=512M --vfs-cache-max-age 72h
```

> This script will first ping to `google.com` to test does your machine has internet connection or not. If it is successful, then it will start `SilentCMD` to mount your remotes

<!-- Foot hyperlink -->

[SilentCMD repo]: https://github.com/stbrenner/SilentCMD
