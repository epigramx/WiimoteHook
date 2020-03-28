# WiimoteHook: Nintendo Wii Remote driver with MotionPlus, Rumble and Nunchuk support

![3 images](https://i.imgur.com/ZyIqZMe.png)

## What this is:
WiimoteHook is software for the Nintendo Wii Remote that has native support for MotionPlus-based motion, the Nunchuk, Rumble, Mouse emulation from Gyroscope data, and XInput output. It can be used in a standalone fashion as an XInput, DS4 or mouse emulation layer but when combined with Cemuhook's motion API it provides 6-axes based motion on Cemu games from gyroscope and accelerometer data to the emulated GamePad or emulated Wii Remote.

When driving a vanilla Wii Remote without MotionPlus hardware, the software retains basic 3-axes motion via Accelerometer data, which can be useful on games that use it as a "Wii Wheel", like Mario Kart 8.

Various additional options are provided by the software like multiple and custom orientations, DS4 hardware emulation, Rumble custom settings, multiple(unlimited) Wiimotes, and more.

![mk8 motion settings](https://i.imgur.com/Bzid6IC.png)

## How to use it / Requirements:
Step 1: **Get the latest WiimoteHook zip from the end of this post** and **extract the full folder to a location** including its subfolders. To extract the folder if you don't have a third-party tool for the job, just right click the .zip and select "Extract All.." or copy & paste the folder to another location after you open the .zip with explorer.

Step 2: **Install the emulated gamepads driver** included in the WiimoteHook folder by running InstallEmulatedGamepadsDriver(run as admin).bat (right click->run as admin). This is not strictly required but **it allows WiimoteHook to produce the Rumble effect and a convenient XInput device** for Cemu's Input menu. The feature called "Also use for buttons/axes" of Cemuhook is also supported alternatively. **Win 7** machines also need for the XInput feature(ignore these URLs for Win8, 8.1 or 10): the _[xbox360 driver](https://www.microsoft.com/accessories/en-us/products/gaming/xbox-360-controller-for-windows/52a-00004#techspecs-connect)_, and [_this security update_](https://www.microsoft.com/en-us/download/details.aspx?id=46148). An alternative method is to install that driver from _[here](https://github.com/ViGEm/ViGEmBus/releases)_.

Step 3: **Run WiimoteHook.exe** to automatically pair with or connect to a Wiimote, deal with its incoming data and launch the motion server and xinput output. Let it run in the background. In case it is required, a .NET 4.5.2 installation link is included in the zip. When WiimoteHook first runs, and provided the controller is properly paired and connected to windows, the Wiimote should be detected by the application (next pic).

![console proper](https://i.imgur.com/mveWWxk.gif)

Note: When WiimoteHook first runs and if it doesn't detect a device it will offer to **automatically pair Wiimotes with Windows** by pressing "B" and then pressing the red button on the Wiimotes (next pic); this needs standard Bluetooth support (if you're in the market for an adapter, special ones aren't required; a generic CSR 4.0 works well); If the pairing process fails (possibly because of an unsupported bluetooth stack) you can manually pair the device with standard windows tools.  In order to manually pair the device on Windows 10 **and avoid the PIN question** you might need to “Add” it as a device in “Devices and Printers” and click Next when asked for a Pin, without entering a pin. While **Windows 7 or older** installations can pair with the new Remote Plus devices, they require the [_Toshiba bluetooth stack_](https://extranet.toshiba-tro.de/en-us/supportquality/bluetoothinfopage/news/downloadtoshiba.aspx) to properly communicate with them.

Note: **DolphinBar also works if set to mode 4** and since it always exposes 4 devices, it's normal for the software to detect bogus ones at launch before a real one is detected. If a DolphinBar doesn't work at first, it's reported **reconnecting** it to another USB port helps.  

Note: To **reconnect** a paired remote after it's disconnected press "A" so that it's detected by the PC and it's reported "connected" in Windows. This is normal behavior for various gaming controllers. They power off to save power after disconnections and they need to wake up by a user action.

![console bt](https://i.imgur.com/vnJVgcj.gif)

Step 4: **Optionally, configure the application with the settings editor** (or leave it at the defaults for a start). Various niche options not described in this thread are in the .config file; the config editor can open with "S" from the console.

![settings editor](https://i.imgur.com/Ldff3Mf.png)

The software also features a tray icon which can be used to open the configuration, toggle the visibility of the console and exit the application (double-clicking it also toggles the visibility of the console).

![tray icon](https://i.imgur.com/njjJj06.png)

Step 5: **Test motion with PadTest** found [_here_](https://files.sshnuke.net/PadTest_1011.zip) (next pic). To do that use the Port set for WiimoteHook (26760 by default), click “Start”, then **double-click a detected controller** . **To test Rumble and XInput support** run XInputTest found _[here](http://drive.google.com/uc?export=download&id=1Fwx29nOnQ1wSRR6zC6vTDAwmwlhZHw7r)_. If you had used another motion server in the past that had a custom remote IP in cemuhook's ini you will need to either edit that setting or remove it.

![PadTest](https://i.imgur.com/TM07H8X.gif)

Note 1: The **Orientation for motion** can be changed by pressing "O"/"M" in the console or permanently in the settings editor. Preset orientations include Aiming (default), WiiWheel, Upright, Classic and there's also Manual which depends on the config. To similarly change the orientation of the D-pad buttons press "D" or edit the default in the settings editor.

Note 2: **MotionPlus** hardware is autocalibrated a few seconds after launch and also manually with "C". The Remote should be on a standstill during calibration. Also a motion client (Cemu or Padtest) expects the remote to be physically at the orientation preferred when they start (pressing "A" on the Remote itself resets the view on Padtest).

Step 6: **Have Cemuhook** in Cemu.exe’s directory. Use the latest version from [_here_](https://sshnuke.net/cemuhook). This step is not strictly required for all features, but it allows Cemu to receive motion data and non-XInput button data.

**Note: Cemu 1.18.0 supports Cemuhook's API natively so Cemuhook is not required to be installed from that version onwards (note that the same version also supports motion for the emulated Wii Remote).**

Step 7: Launch Cemu.exe, **select a motion source** now detected in the Options->Gamepad motion source menu (next pic). If you elect to not use XInput's binds, you can select “Also use for buttons/axes” (you can reconfigure buttons for that feature in the settings editor). "By Slot" or "By MAC" only affects behavior if there are multiple remotes; by selecting a remote by MAC it will be remembered as the motion source regardless of order of detection (Cemu and Cemuhook currently only support one motion source).

![cemuhook motion settings in cemu](https://i.imgur.com/OmJ9hb4.png)

Step 8: Choose GamePad as controller 1, and also select "Controller #" under XInput and set up the buttons (or leave them be if you use the "Also use for buttons/axes" feature).

Note: Cemu 1.18.0 added motion support on the emulated Wii Remote itself.

Note: Cemu 1.11.5 onwards added emulated wiimotes but for some games it's mainly for booting and not playing them yet, and Cemuhook does not support motion servers for it.

![cemu input options](https://i.imgur.com/NmMsEuF.png)

Note: **Shaking** a Nunchuk or a Remote corresponds to certain buttons. This behavior can be configured or removed in the settings editor.

Step 9: Load a game

## Caveats/Notes:
1. Bluetooth pairing can be ..an adventure on Windows. WiimoteHook now has a built-in pairing method but if that fails (possibly because of an unsupported bluetooth stack) you can try standard windows tools for pairing and in some cases physically reconnecting an adapter, rebooting or removing a pairing might help. While Windows 7 or older installations can pair with the new Remote Plus devices, they require the [_Toshiba bluetooth stack_](https://extranet.toshiba-tro.de/en-us/supportquality/bluetoothinfopage/news/downloadtoshiba.aspx) to properly communicate with them; Windows 10's default method asks for a pin, but you can avoid that problem by "adding" it in "devices and printers" and click next when asked for a pin without entering one.

2. DolphinBar works on mode 4 + it's normal to always return 4 devices and few of them to be detected as bogus + reconnecting it to another usb port often helps.

3. Linux is partly supported now that we've added raw Bluetooth HID support in Wine (originally inspired for this software). Details/Instructions are _[here](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=1857&viewfull=1#post1857)_.

## Known bugs or limitations:
1. Cemu 1.11.5 onwards includes emulated wiimotes in input settings but for some games it's mainly for booting and not playing them yet, and Cemuhook does not support motion for it. Update: Cemu 1.18.0 added support for motion with the emulated Wii Remote too.

2. Multiple(unlimited) Wiimotes are supported, however motion only works for the first Cemu GamePad chosen as the first controller (this is a Cemu and Cemuhook limitation).

3. Static MotionPlus calibration data are not fully reverse engineered. If your MotionPlus gets inverted axes you can switch that with the settings editor.

## Changelog:
up to 20180616/080042/beta:
- [Configuration editor, tray icon, and hide/show the console features](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=2679&viewfull=1#post2679)
- [Mouse emulation from MotionPlus gyroscope data
](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=2642&viewfull=1#post2642)

up to 20180601/150417/alpha:
- [Attempt to better distinguish old VS new MotionPlus hardware based on static calibration data](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=2572&viewfull=1#post2572)
- [Considerably better connectivity related to status reports](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=2554&viewfull=1#post2554)
- Better logging in .log.txt

<details>
  <summary>All Changelogs</summary>

up to 20180311/153427/alpha:
- [Attempt to a fix for base calibration data and a logging feature](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=1981&viewfull=1#post1981)
- [Wine-Linux support
](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=1857&viewfull=1#post1857)
- [Bug fix towards smoother connections, migration to x86 and a printing fix
](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=1851#post1851) 
- [Now any IP is possible for the motion server in the .config for easier access to it from remote computers or via a virtual machine on linux.](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=1812&viewfull=1#post1812)
- [Rumbling should work properly again for multiple wiimotes and the text of console should no longer be garbled for multiple wiimotes
](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-MotionPlus-Rumble-and-Nunchuk-support?p=1682&viewfull=1#post1682)
- [XInput/DS4 output improvements](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=1475&viewfull=1#post1475)
- [WiimoteHook now supports Shaking](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=1430&viewfull=1#post1430)
- [The nunchuk should no longer be unable to provide an accelerometer-based motion source if set that way in the .config](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=1414&viewfull=1#post1414)
- [DolphinBar should no longer crash with its invalid extra devices, multiple wiimotes should be supported by default, and handling of invalid devices should be better in general. As a bonus consequence, Pressing O or D in console should no longer crash the application when using a DolphinBar](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=1396&viewfull=1#post1396)

up to 20180119/174337/alpha:
- [The discrete MotionPlus extension should now work properly at Nunchuk passthrough mode.](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=1381&viewfull=1#post1381)
- [Attempt to support MotionPlus on 0x0306 ID devices better
](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=1362&viewfull=1#post1362)
- [Solution related to MAC address being returned from the Wiimote but in an invalid format
](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=1174&viewfull=1#post1174)
- [Emulated analog stick with MotionPlus data](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=1003&viewfull=1#post1003) (disabled by default, optional setting in the .config)
- [The true cause of the recent crashes has been identified and fixed](https://forum.cemu.info/showthread.php/140?p=928#post928)

up to 20171201/114212/alpha:
- [MotionPlus Support. In addition, the new Remote Plus devices no longer require the Toshiba stack](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=870&viewfull=1#post870)
- [The Analog Stick of some Nunchuks now works again
](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=875&viewfull=1#post875)

up to 20171120/064127/alpha:
- Better DS4 emulation support (with it, rumble works on software/games that directly support a DS4, use the XInput device for rumble on Cemu. The DS4 device is disabled by default; it can be enabled in the .config)
- [The Analog Stick of the Nunchuk is now correctly calibrated](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=747&viewfull=1#post747)
- [Automatic pairing of Wiimotes](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wii-Remote-with-Motion-Rumble-and-Nunchuk-support?p=739&viewfull=1#post739)
- [Better multi-Wiimote support](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wiimote-Cemu-support-Wii-Wheel-for-Mario-Kart-8-edition?p=726&viewfull=1#post726) (motion only works on the first Cemu GamePad (it's a Cemu and Cemuhook limitation)
- [Nunchuk support](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wiimote-Cemu-support-Wii-Wheel-for-Mario-Kart-8-edition?p=680&viewfull=1#post680) (and Hot-plugging Extension support)
- [Rumble max time bug fixed](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wiimote-Cemu-support-Wii-Wheel-for-Mario-Kart-8-edition?p=717&viewfull=1#post717) and its defaults changed

Native XInput support
- [Rumble code (PWM)](https://forum.cemu.info/showthread.php/140-WiimoteHook-Nintendo-Wiimote-Cemu-support-Wii-Wheel-for-Mario-Kart-8-edition?p=713&viewfull=1#post713)
- Wacky Analog Stick emulation with IR camera; it's disabled by default.

0.1alpha:
- Initial release - "Wii Wheel for Mario Kart 8 edition":
- Basic accelerometer and buttons support.
- Mainly useful for Mario Kart 8

</details>


## Crowdfunding:
If you use this software consider a [contribution](https://tinyurl.com/y8x23xao); further crowdfunding/donation info and options are included in a relevant .txt file in the .zip.

## Downloads:
**Latest release**: [WiimoteHook_20180616_080042_beta.zip](http://drive.google.com/uc?export=download&id=123Lq-uX2lwL2Y42iiYi6fUJVwTawiHU9)
