# Disclaimer
I am in no way affiliated with IRONMACE and running the launcher through linux is unsupported by them as they clearly state in their faq on their website. Use at your own risk.

These instructions are a result of all of all the work from Tepri's Discord https://discord.gg/ggu2yMSVjt. This is the best place for questions/support if you need it.

# Dark-and-Darker-Linux
Compilation of all known methods to run Dark and Darker on Linux, listed roughly from easiest to hardest. Accordingly, I will go into less detail on the less user-friendly methods since those will primarily be reserved for those who understand wine/linux well and want to avoid things like Steam, Lutris, and Flatpak.

Discord started by Tepri is the best place to get support if you need it: https://discord.gg/ggu2yMSVjt. This repo is based on the work done by everyone there, just putting it in a more visible location.

# Known issues (These will apply to all methods)
1. Launcher will not remember sign-in credentials. You have to enter them each time.
2. Launcher does not close propertly using the x button or closing from the task bar (this happens sometimes in windows as well). You will need to stop from lutris/steam or use `flatpak kill com.darkanddarker.DaD` to make sure it's closed.
3. Installer progress bar overlays all text on top of itself, looking like a jumbled mess. It is still working even though it looks wrong.
4. Mouse will leave your in-game window periodically if the blacksmith launcher is behind it. Simply move or minimize blacksmith after launch to prevent this.
5. Sometimes on launch of Dark and Darker nothing is clickable. Alt-tab to fix this.

# Lutris (prereqs: Lutris)
Simply run this installer https://lutris.net/games/dark-and-darker/ using Lutris. I do not keep this script up-to-date, but it works at time of writing.

# Dark and Darker flatpak (prereqs: flatpak)
I created and maintain a flatpak repo here https://github.com/nmlynch94/com.darkanddarker.DaD along with a one-liner to install it. It will create an application shortcut in your desktop environment. Follow the instructions in the README.

# Steam Proton (prereqs: protontricks, steam, protonrup-qt)
1. Download the [Blacksmith Installer](https://www.darkanddarker.com/)
2. Install the latest proton-ge from protonup-qt and reboot steam.
3. In Steam, choose Games -> Add Non-Steam Game to My Library
4. Choose Browse, and select the blacksmith installer.exe
5. Right Click -> properties and add double quotes around the "target" path
6. Under Compatibility, choose Proton GE
7. Launch and install blacksmith. Close the sign-in window before logging in.
8. Run protontricks and choose the prefix for you shortcut
9. Install wininet, vcrun2022, and urlmon. This may take awhile and, if you run protontricks outside the cli, it will appear to be doing nothing for awhile.
10. Perform the voip fix DLL override in the final section using protontricks to access winecfg.
11. Change the target to BlacksmithBootstrap.exe inside your steam prefix at "<prefix>"/drive_c/Program Files/IRONMACE/Blacksmith/". Add double quotes around the target path again.
12. Launch!

# Wine (prereqs: wine-ge, winetricks)
1. Download the latest wine-ge
2. Download the [Blacksmith Installer](https://www.darkanddarker.com/)
3. Run blacksmith installer with wine. Close the window before signing in.
4. Use winetricks to install wininet and urlmon to the prefix
9. Perform the voip fix DLL override in the final section using winecfg.
10. Run BlacksmithBootstrap.exe inside your prefix.

# Steam Deck
All of the steps shown above will work as written on a steam deck. The flatpak version is probably the fewest steps to get up and running. The only note is that it currently does not work in Gaming Mode, so, you will need to play in Desktop Mode.

# Apple Silicon Macs (NOTE: at time of writing, this is broken due to a Rosetta 2 bug. Upgrading to the 14.4 developer preview build is required to make this work. Otherwise, you need to wait until it's in the stable release)
1. brew install --cask whisky (1.2.0 as of writing this)
2. open -a /Applications/Whisky.app
3. Make a new Bottle eg ‘Dark and Darker’
4. Click 'Winetricks..' button and input wininet urlmon vcrun2019
5. Check that Windows 10 / 18362 are still listed in Config, if not, Open Wine Configuration and change from XP to Windows
6. Enable the 'ESYNC' toggle in Config (leave DXVK off, we use GPTK for dx12) (you can mess with vsync later in AppData GameUserSettings.ini)
7. Download latest 'Blacksmith Installer.exe' from darkanddarker.com, and copy it to the Bottle’s drive_c
8. Click 'Run..' and run 'Blacksmith Installer.exe'
9. Login should work because of vcrun2019, then click Install, which should work because of wininet urlmon
10. In the top-left of the launcher, click Game → Launch Options → -dx12 and then click 'X' to close
11. Click Play, wait a while on black screen (compiling shaders?)
12. In-game, change settings to Medium and FXAA, then Quit
13. Perform VOIP fix
14. Click Play

# VOIP Fix
To make the blacksmith launcher function properly, we had to install wininet and urlmon. This fixes the launcher, which is great, but it breaks VOIP in game. This means, Blacksmith.exe needs the native urlmon and wininet, while DungeonCrawler.exe needs the builtin urlmon and wininet. Luckily, wine provides the ability to override per-executable using application profiles.

1. open winecfg for your prefix using winetricks or protontricks
2. on Applications, click "Add Application"
3. Navigate to Program Files/IRONMACE/Dark and Darker and choose DungeonCrawler.exe
4. Highlight the new application you just created as shown in the first screenshot, and then click the libraries tab
5. Add the overrides as shown in the second screenshot

![image](https://github.com/nmlynch94/Dark-and-Darker-Linux/assets/40608755/384596b5-047f-4fde-a54b-4c8b3db61857)

![image](https://github.com/nmlynch94/Dark-and-Darker-Linux/assets/40608755/f029353a-9858-43d0-8d42-bfaac9773d7c)
