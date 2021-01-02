# imac-uga-roms
A collection of modified vbios ROMs for PC based MXM video cards for iMac 2011 based computers. This ROM does not require a 3rd party bootloader like OpenCore. A color-pixel bug is still present. I am working on it. 

**Pre-installation Requirements**
- CH341a Programmer with Pomona clip


**Post-installation Requirements** 
 (Brightness Control Stepping):
- Turn computer on, hold down Command(⌘)-R
- Choose Utilities > Terminal
- Enter:`csrutil disable`
- Reboot
- Download and open 'Kext Utility v2.6.6'
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

The above data pattern will allow for a wider span of steppings for the brightness control and utilizes more of the capacity of the HD3000. If you have a different machine, your panel ID can be found by going to `System Preferences > Displays > Color > Open Profile > mmod`

warning: please remember this is a WSON based card. You will be unable to recover from a bad flash with a regular clip.
