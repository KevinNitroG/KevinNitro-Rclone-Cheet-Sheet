---
description: Guide for Mounting Remotes using Rclone for Windows
cover: .gitbook/assets/wallpaperflare.com_wallpaper.jpg
coverY: 0
---

# Rclone mount Windows

This is my trick to use rclone mount command. If it isn't efficient and you have another efficent, easy way, feel free to create an issue or create a pull request 🥰

***

## 1️⃣ SOME REQUIREMENTS

### INSTALL SILENTCMD

#### What is it? 🤔

* It helps to run commands silently, not open the cmd window

#### Installation ⚙️

1. Go to [SilentCMD repo](https://github.com/stbrenner/SilentCMD)
2. **Download** from [Release page](https://github.com/stbrenner/SilentCMD/releases/latest), **extract** and **put** it in a folder

### SET ENV FOR RCLONE & SILENT CMD

You should also **set** **environment** **path** for Rclone to make it easier to use 😪

***

## &#x20;2️⃣ CREATE A BATCH SCRIPT 📜

> The directory where the batch script locates doesn't matter, you can create it in any directory

1. Create a batch file _(Ex: Mount.bat)_
2.  Edit it _(Ex: Notepad)_ and put the below script inside the batch file

    {% code title="Mount.bat" overflow="wrap" lineNumbers="true" fullWidth="false" %}
    ```batch
    set rclone_command=replace_your_rclone_command_here

    set website_to_ping=google.com

    :CHECK_CONNECTION
    ping %website_to_ping% -n 1 > nul
    if %errorlevel% neq 0 (
        timeout /t 5 > nul
        goto CHECK_CONNECTION
    )

    start SilentCMD %rclone_command%

    timeout /t 2

    taskkill /f /im SilentCMD.exe
    ```
    {% endcode %}
3.  **Replace your command** in the script above 👆

    > Ex of my rclone mount script:

    <pre class="language-batch" data-overflow="wrap"><code class="lang-batch"><strong>rclone mount CombineNeccessary: Z: --cache-dir "D:\Program Files\Rclone Cache" --vfs-cache-mode full --network-mode --volname "Cloud Storages" --no-modtime --no-checksum --buffer-size=512M --vfs-cache-max-age 72h
    </strong></code></pre>

    See more about rclone command to use it as your demand 😪
4. Copy the **full path** of the script above for the below step

{% hint style="warning" %}
In step 3, if you don't set env for **SilentCMD** & **Rclone,** you will have to replace the full path of the .**exe** file of those programs
{% endhint %}

<details>

<summary>Click here to see the explanation of the script above</summary>

* First, it will ping to `google.com`, if it fails, it will retry to ping until it successes
* After pinging successfully, it will start **SilentCMD** to run **Rclone mount command**
* After 2 seconds waiting, it will terminate _(End task)_ all the **SilentCMD** itself

With **SilentCMD**, **Rclone** doesn't run under any terminal, cmd,... So after terminating **SilentCMD**, **Rclone** still works 😤

</details>

***

## 4️⃣ SET UP RUNNING MOUNT SCRIPT 🏃‍♂️

1. Right-click anywhere to open **Context Menu** --> **New** --> **Shortcut**
2. **Type the location of the item:** `SilentCMD "the_full_path_of_batch_script"` --> Next
3. **Type a name for this shortcut:** Anything you want _(Ex: Rclone mount)_

{% hint style="warning" %}
In step 2, if you don't set env for **SilentCMD**, you have to enter the full path of **.exe** of **SilentCMD**
{% endhint %}

### Addition:

#### _Change icon for shortcut:_

1. Open its **properties** _(<mark style="color:purple;">`Alt + Enter`</mark>)_
2. **Click on** `Change icon...`: Browse to the icon file\
   You can use **rclone.exe**'s icon

***

## 5️⃣ RUN RCLONE MOUNT AT STARTUP 🪟

### Easiest way:

1. Windows + R: `shell:startup`
2. **Copy** & **Paste** the shortcut you created from the previous step

### More controlable way:

Use task schedule which I'm not good at using it 🥴

## 6️⃣ MAKE THE SHORTCUT BE VISIBLE IN PROGRAM LIST + START MENU

1. <mark style="color:purple;">Windows + R</mark>: `shell:Common Programs`
2. **Copy** & **Paste** the shortcut you created from the previous step

And now you can search for the shortcut in search bar 🔎
