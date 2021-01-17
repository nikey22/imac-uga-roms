# imac-uga-roms
A collection of modified vbios ROMs that include a working efi which enables bootscreen and native brightness control on MXM based video cards. This is tested on the iMac 2011 based computers. These ROM does not require a 3rd party bootloader like OpenCore to emulate bootscreens/brightness.

**Compatible machines**
- iMac 27-Inch "Core i5" 2.7 (Mid-2011)	2.7 GHz Core i5 (I5-2500S)	Mid-2011	A1312 (EMC 2429)	iMac12,2
- iMac 27-Inch "Core i5" 3.1 (Mid-2011)	3.1 GHz Core i5 (I5-2400)	Mid-2011	A1312 (EMC 2429)	iMac12,2
- iMac 27-Inch "Core i7" 3.4 (Mid-2011)	3.4 GHz Core i7 (I7-2600)	Mid-2011	A1312 (EMC 2429)	iMac12,2

**Pre-installation Requirements**
- Modification of the MXM-B 2 pipe or 3 pipe heatsink to allow clearance of the 2 inductors on nvidia cards
- Nvidia based MXM-B Kepler based GPUs 
- Backup original vbios rom by using the Linux USB grml.org:

  `ssh root@your.ip`
  `./nvflash_linux --save /root/original.rom`
  `scp root@your.ip:/root/original.com`

**Post-installation Requirements** 
 (Brightness Control Stepping):
- Turn computer on, hold down Command(⌘)-R
- Choose Utilities > Terminal
- Enter:`csrutil disable`
- Reboot
- Download and open [Kext Utility v2.6.6](http://cvad-mac.narod.ru/index/0-4)
- Navigate to S/L/E (System/Library/Extensions)
- Copy "AppleBacklight.kext" to Desktop
- Edit: AppleBacklight.kext/Contents/Info.plist
- Scroll down to: `IOKitPersonalities > AppleIntelPanelA > ApplePanels`
- There you find several Apple LCD profiles.
- For the iMac 2011 27" machine locate: 
```<key>F10Ta007</key>
<data>
ABEABgALABQAHAAnADMAPwBOAFwAZwBzAIEAkQClAL8A2wD/
</data>
```
- Change the <data> section to: `ABEAAgA3AF8AigCzAOsBJAFnAakB1AIJAlQCogL4A00DlgRpBGk=`
- Drag your modded kext into Kext Utility, allow it correct permissions
- Applebacklight.kext.bak folder will be created
- Reboot

The above data pattern will allow for a wider span of steppings for the brightness control and utilizes more of the capacity of the HD3000. If you have a different machine, your panel ID can be found by going to:

`System Preferences > Displays > Color > Open Profile > mmod`

warning: please remember this is a WSON based card. You will be unable to recover from a bad flash with a regular clip.
