# sleepyhart Clip Studio Paint bottle
Sleepyhart's Wine Config for running Clip Studio Paint 4.0 in Linux

This only has rough initial testing - so far can open files, get huion tablet working with pressure, manipulate 3D assets and load/save files including some recovery functionality. Clip Studio Store doesn't seem to work so needs bit more tweaking with WebView/Edge. 

(WINE is a translation layer that allows Windows programs to run in Linux, Bottles creates independent containers for WINE programs to run without disrupting the system wide configuration, e.g. WINE you'll use to run games in Steam).

# Installation Instructions

- Download the **sleepyhart_Clip-Studio-Paint.yml** file from this repo and the **Clip Studio Paint** installer for Windows from [the official website](https://www.clipstudio.net/en/dl/)
- Install the flatpak version of [Bottles](https://flathub.org/apps/com.usebottles.bottles) 
- Edit the permissions of Bottles to allow access to devices and files. The easiest GUI way to do this is using [Flatseal](https://flathub.org/apps/com.github.tchx84.Flatseal)
  -  Install and open Flatseal. From the left hand panel select "Bottles" (com.usebottles.bottles). The main panel will have permission toggles we will need to edit.
  - Under "Device" enable **GPU acceleration** (for better graphics performance) and **Input Devices** (for pen pressure passthrough).
  - To allow CSP to access local files, go to "Filesystem" and enable **All user files** to allow access to your "home" directory (/$USER/home)
  - If you want CSP to access folders outside your home directory, add their locations in **Other files** - press the plus folder icon and enter the path to folders in the bar
    - Easiest way to find folder paths is opening them in your file manager (Dolphin, Nautilus etc), right clicking and selecting "Copy Location"
- Before we can make our  need to install our runner and other components in Bottles. Open Bottles and go to **Preferences** (under the three dots menu)
  - In the **Runners** tab, select **Kron4ek** and press the save icon next to the latest version (tested version was *kron4ek-wine-10.12-amd64*)
  - In the **DLL Components** tab, find the latest version of **DXKV** (tested version was *dxvk-2.7*) and click the save icon to install. Scroll down and do the same for the latest version of **VKD3D** (tested was *vkd3d-proton-2.14.1*)
- Close preferences and **create a new bottle** ("+" button in top left)
  - Give the bottle a name - e.g. "Clip Studio Paint" - and select **Custom**
  - Make sure Architecture is set to **64-bit** and Runner is set to the version of **kron4ek** we installed earlier
  - At the bottom click on **Import Configuration**. Nagivate to and select the **sleepyhart_Clip-Studio-Paint.yml** file downloaded from this repo. Click **Create** and wait for Bottle to be created.
- Once created select our new bottle from the list. Go to **Settings** and under "Compatability" set **the Windows Version to Windows 8.1**
- Now we're ready to install CSP - click on **Run Executable**. A file selection popup will appear - navigate to the Windows installer we downloaded earlier **(CSP_4XXw_setup.exe)** and click "Run". Run through the installation wizard like you would in Windows, keeping all settings at default.
- Under "Programs" you should see a link to **ClipStudio** - we need to run Clip Studio to finish set up. Click on the "Run" button (play arrow) to start
  - Clip Studio itself will open though the store will not load properly. If it prompts to download assets, click on allow. Click "Draw" to open CSP
  - You will be prompted with the trial or login prompt as you would in Windows. Either select a trial option or click the button to login/enter your product key to activate. Once clip opens you will get a message about the Operating System not being supported, this can be ignored or you can select to not show again.
- Clip Studio Paint is now installed. We can access it by opening Bottles, then the ClipStudio shortcut and clicking Paint like before. We can also set up shortcuts to make this easier:
  - To add a shortcut to CSP in Bottles directly, click "add shortcuts" and then navigate to the CSP exe file - **"drive_c/
Program Files/CELSYS/CLIP STUDIO 1.5/CLIP STUDIO PAINT/CLIPStudioPaint.exe"**
  - To add a shortcut directly to CSP from your desktop/application list, click on the dots next to the shortcut and select **Add to Desktop**

Some notes and tweaks:
- By default, your Linux filesystem will be accessible from CSP under **Drive Z:** in the open file dialog. If you can't find folders or paths, make sure you granted Bottles permission to these directories in FlatSeal (or last resort allow Bottle access to full filesystem)
- If tablet pressure isn't working, open CSP Preferences, go to "Tablet" and enable **User mouse mode in tablet driver settings**. Generally tablet driver and tablet settings should be sorted first in Linux itself rather than in Bottles or the Windows environment it makes.
