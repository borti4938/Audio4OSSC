PCB-Installation on a v1.5-A3a Audio PCB  
========================================  
  
Before you start, check the following points:  
- Your OSSC is pre-assembled?  
  -> If yes, you have to desolder the SCART connector first.  
- Bought a a v1.3-DIY/DVI OSSC?  
  -> If yes, please consider additional notes.  
  
The pictures assumes that you have OSSC board and SCART connector.  
Now you can start :)  
  
01 - cut three wires between each pair of solder joints marked with I2S, WS and SCK  
     -> Note for v1.3: You don't have these jumpers. Lift pins 9, 10 and 11 of the IT6613E.  
02 - demonstration of point 1 on a v1.5-DVI board  
03 - cut off the plastic around pin 2, 4 and 6 of the SCART connector  
04 - solder the SCART plug into place and solder the audio PCB onto the SCART connector (remind to check jumper assignment at next to the IT6613E during soldering the first leg)  
05 - solder the three top solder joints on the OSSC PCB (I2S, WS and SCK) to the audio PCB  
     -> make sure that you don't reconnect the jumpers to GND with your solder  
     -> Note for v1.3: Solder lose wires to the lifted pins. Be carefull to not harm the pins!  
06 - connect the wires for 5V, 3.3V and 27MHz  
07 - 5V and 3.3V can be get from U5  
08 - 27MHz from the crystal oscillator (pin between U7 and U9)  
