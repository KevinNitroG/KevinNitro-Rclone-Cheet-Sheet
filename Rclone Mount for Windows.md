# RCLONE MOUNT FOR WINDOWS

This is my trick to use rclone mount command. If it isn't efficient and you have another easier way, just feel free to create an issue or create a pull reguest. 🥰

## INSTALL SILENTCMD

## What is it? 🤔

It helps to run command silently, not shows out any log

## 1️⃣ Installation ⚙️

1. Go to [SilentCMD repo][SilentCMD repo]
2. Download, put it in a folder
3. Set environment for SilentCMD
   > Or you can put SilentCMD in the same Directory of Rclone, Rclone config file...

## 2️⃣ Create a batch script 📜

> The directory where the batch script locates doesn't matter, you can create it in any directory

1. Create a batch file _(Ex: Mount.bat)_
2. Put the script inside the batch file

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

<Details>
<Summary>
Click here to see the explanation of the script above
</Summary>

- First, it will ping to `google.com`, if it fails, it will retry to ping until it successes.
- After pinging successfully, it will start SilentCMD to run Rclone mount command and terminate _(End task)_ the SilentCMD
- With SilentCMD, Rclone doesn't run under any terminal, cmd,... So after terminating SilentCMD, Rclone still works 😤

</Details>

3.  Replace your command in the script above 👆

    > Ex of my rclone mount script:

    ```rclone mount command
    rclone mount CombineNeccessary: Z: --cache-dir "D:\Program Files\Rclone Cache" --vfs-cache-mode full --network-mode --volname "Cloud Storages" --no-modtime --no-checksum --buffer-size=512M --vfs-cache-max-age 72h
    ```

    See more about rclone command to use it as your demmand 😪

## 4️⃣ RUN THE RCLONE MOUNT SCRIPT 🏃‍♂️

In order to make the rclone run most silently, you have to do some trick here

1. Create a shortcut for the script _(Right click, send to, desktop,...)_
2. Right click, properties it, set these values:
   - `Run`: `Minimized`
   - `Change icon...`: Locate to `.exe` or icon file to make the shortcut more beautiful :v

> This will make the script run minimized

## 5️⃣ RUN RCLONE MOUNT AT STARTUP 🪟

### Easiest way:

1. Windows + R: `shell:startup`
2. Copy & Paste the shortcut you created from the previous step

### More controlable way:

Use task schedule which I'm not good at using it 🥴

   <!-- Foot hyperlink -->

[SilentCMD repo]: https://github.com/stbrenner/SilentCMD
