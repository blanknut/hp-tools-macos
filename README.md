# Running HP vintage computing tools on macOS
If you are - like me - interested in vintage computing, you may use different tools like emulators etc. for your hobby activities. Many of those tools are created for the Windows operating system. As a longtime user of Apple computers, I wondered how to run them directly on my MacBook. There are several options like:
1. Install Windows on a second partition using [Boot Camp](https://support.apple.com/de-ch/guide/bootcamp-assistant/).
2. Use commercial tools like [Parallels](https://www.parallels.com/) or [CrossOver](https://www.codeweavers.com/crossover/).
3. Run Windows using [VirtualBox](https://www.virtualbox.org/).

Option 1 is very awkward, you need to reboot to switch between macOS and Windows. Option 2 is better, no need to reboot, just run both operating systems in parallel. However, for Parallels you still need a valid Windows license. CrossOver uses a different approach and does _not_ need a Windows license. Both applications do not come for free. VirtualBox is free software but you need a Windows license, too.

Well, for more serious use cases, I might be willing to spend some money and get support etc. But for hobby activities I was looking for a cheap or even free solution. Therefore, I gave [Wine](https://www.winehq.org/) a try.

## Installation of Wine
Installation of Wine (the stable version) on macOS is super easy using [Homebrew](https://brew.sh/) (if you do not have Homebrew yet, get it, it's a must have). Open a terminal and enter the following commands:
```
brew tap homebrew/cask-versions
brew install --cask --no-quarantine wine-stable
```
For more details and instructions about uninstalling Wine, please refer to [this page](https://wiki.winehq.org/MacOS).

## Installation of V41
[V41](https://hp.giesselink.com/v41.htm) is an emulator for the Hewlett Packard Series 40 calculators like HP-41C, HP-41CV and HP-41CX. First, download the VS2005 Runtime package and run it. Then, download the V41 installer package (currently named V41R9K) and execute it, too. You will notice that installation under Wine on macOS is as smooth as on a real Windows system.

On my MacBook, I've installed V41 into the folder ~/Windows/V41. To run it from a terminal window, I have to type:
```
cd Windows/V41
wine V41.exe
```

Note that you have to change to the V41 installation directory before starting the emulator, otherwise it does not find some true type fonts (I did not futher investigate this issue).

## Creating a shortcut for V41
Of course, it would be even more convenient if you have a shortcut to start V41. That's easy, too, just follow these instructions:
1. Start Automator.
2. Choose 'Application' (Programm in German).
3. Search for the 'shell' action.
4. Choose the shell you're using on your computer.
5. Enter the shell script as listed below.
6. Save the shortcut.

This is my Automator shell script to start V41. You have to adjust the paths to your needs:
```
export WINEPREFIX="$HOME/.wine"
export DYLD_FALLBACK_LIBRARY_PATH=/usr/X11/lib
export FREETYPE_PROPERTIES="truetype:interpreter-version=35"
cd ~/Windows/V41
wine V41.exe
```

One additional detail to adjust is the icon of the shortcut. This is also possible:
1. Navigate to the V41 installation directory.
2. Copy the file 'Medium.bmp' (or 'Small.bmp' or 'Tiny.bmp' if you prefer) to the clipboard.
3. Navigate to the V41 shortcut file and select it.
4. Press Command+I to show the properties.
5. In the upper left corner of the properties window, select the current icon (showing the Automator robot) and press Command+V.

## Install the HP-85 Emulator
The [HP Series 80 emulator](https://www.kaser.com/hp85.html) written by Everett Kaser is one of my favorite tools. It also runs fine under Wine and the installation is done in the same way as for V41.

## What about DOS programs?
If you want to run DOS programs on your macOS computer, you might want to give [DOSBox](https://www.dosbox.com) a try. But this is another story and I will not cover it here.
