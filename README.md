# Dark-and-Darker-Linux
Compilation of all known methods to run Dark and Darker on Linux, listed roughly from easiest to hardest. Accordingly, I will go into less detail on the less user-friendly methods since those will primarily be reserved for those who understand wine/linux well and want to avoid things like Steam, Lutris, and Flatpak.

# Known issues (These will apply to all methods)
1. Launcher will not remember sign-in credentials. You have to enter them each time.
2. Launcher does not close propertly using the x button or closing from the task bar (this happens sometimes in windows as well). You will need to stop from lutris/steam or use `flatpak kill com.darkanddarker.DaD` to make sure it's closed.
3. Installer progress bar overlays all text on top of itself, looking like a jumbled mess. It is still working even though it looks wrong.
4. Mouse will leave your in-game window periodically if the blacksmith launcher is behind it. Simply move or minimize blacksmith after launch to prevent this.
5. Sometimes on launch of Dark and Darker nothing is clickable. Alt-tab to fix this.

# Lutris (prereqs: Lutris)
Simply run this installer https://lutris.net/games/dark-and-darker/ using Lutris. I do not keep this script up-to-date, but it works at time of writing.

# Dark and Darker flatpak (prereqs: flatpak)
I created and maintain a flatpak repo here https://github.com/nmlynch94/com.darkanddarker.DaD along with a one-liner to install it. It will create an application shortcut on your desktop. Follow the instructions in the README.

# Steam Proton (prereqs: protontricks, steam)
1. Download the [Blacksmith Installer](https://www.darkanddarker.com/)
2. In Steam, choose Games -> Add Non-Steam Game to My Library
3. Choose Browse, and select the blacksmith installer.exe
4. Right Click -> properties and add double quotes around the "target" path
5. Under Compatibility, choose Proton Experimental
6. Launch and install blacksmith. Close the sign-in window before logging in.
7. Run protontricks and choose the prefix for you shortcut
8. Install wininet and urlmon. This may take awhile and, if you run protontricks outside the cli, it will appear to be doing nothing for awhile.
9. Perform the voip fix DLL override in the final section using protontricks to access winecfg.

# Wine (prereqs: wine-ge, winetricks)
1. Download the latest wine-ge
2. Download the [Blacksmith Installer](https://www.darkanddarker.com/)
3. Run blacksmith installer with wine. Close the window before signing in.
4. Use winetricks to install wininet and urlmon to the prefix
9. Perform the voip fix DLL override in the final section using winecfg.

# VOIP Fix
1. open winecfg for your prefix using winetricks or protontricks
2. on Applications, click "Add Application"
3. Navigate to Program Files/IRONMACE/Dark and Darker and choose DungeonCrawler.exe
4. Highlight the new application you just created as shown in the first screenshot, and then click the libraries tab
5. Add the overrides as shown in the second screenshot

![image](https://github.com/nmlynch94/Dark-and-Darker-Linux/assets/40608755/384596b5-047f-4fde-a54b-4c8b3db61857)

![image](https://github.com/nmlynch94/Dark-and-Darker-Linux/assets/40608755/f029353a-9858-43d0-8d42-bfaac9773d7c)
