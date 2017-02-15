PCB-Installation of a v1.3-A3 Audio PCB  
=======================================  
  
Before you start, check the following points:  
- Your v1.3-DVI/DIY OSSC is pre-assembled?  
  -> If yes, you have to desolder the SCART connector first and lift pins 9, 10 and 11 of the IT6613E IC.  
- Have a v1.5-DVI/DIY OSSC and the v1.3-A3 add on board?  
  -> If yes, stay here.  
- Bought a a v1.5-DIY/DVI OSSC?  
  -> If yes, you are in the wrong folder.  
  
The pictures assumes that you have spare IT6613E, OSSC board and SCART connector. Now you can start :)  
  
01 - bend up pins 9, 10 and 11 of the IT6613 (v1.3 only!!!) (and eventually pin 5 - see External MCLK; not supported by official firmware)  
02 - make a placement check  
03 - cut off the plastic around pin 2, 4 and 6 of the SCART connector (not needed if you have the version with wired connection to the SCART, e.g. if you bought your board from VGP)  
04 - solder the IT6613 into place (if not done yet) and approximately fix the audio pcb into place  
05 - solder the SCART plug into place and solder the audio PCB onto the SCART connector (remind to check the pin assignment at the IT6613 during soldering the first leg)  
06 - solder pin 9, 10 and 11 of the IT6613 onto the audio PCB  
07 - connect the wires for 5V, 3.3V and 27MHz  
08 - 5V and 3.3V can be get from U5  
09 - 27MHz from the crystal oscillator (pin between U7 and U9)  
