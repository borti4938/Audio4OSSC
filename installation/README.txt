This read me is a part-copy of the main-readme.

PCB-Installation
=================
(see pictures; assumes that at least the SCART connector has been desoldered for v1.3 and v1.5 without wired connection to the SCART)
01 - v1.3 - bend up pins 9, 10 and 11 of the IT6613 (v1.3 only!!!) (and eventually pin 5 - see External MCLK)
   - v1.5 - cut three wires between each pair of solder joints marked with I2S, WS and SCK (v1.5 only) (eventually lift pin 5 of the IT6613E - see External MCLK)
02 - make a placement check (might look different between v1.3 and v1.5)
03 - cut off the plastic around pin 2, 4 and 6 of the SCART connector (not needed if you have the version with wired connection to the SCART, e.g. if you bought your board from VGP)
04 - solder the IT6613 into place (if not done yet) and approximately fix the audio pcb into place (v1.5 does not sit under the  pins)
05 - solder the SCART plug into place and solder the audio PCB onto the SCART connector (remind to check the pin / jumper assignment at the IT6613 during soldering the first leg)
   - v1.5: make sure that you don't reconnect the jumpers to GND with your solder
   - v1.5 with wired connection to SCART: solder three pins to the SCART plug which replaces the 'fork' (L <-> pin 6, GND <-> pin 4, R <-> pin 2)
06 - v1.3 - solder pin 9, 10 and 11 of the IT6613 onto the audio PCB (v1.3 only)
   - v1.5 - solder the three top solder joints on the OSSC PCB (I2S, WS and SCK) to the DIY audio PCB (v1.5 only)
07 - connect the wires
08 - 5V and 3.3V can be get from U5
09 - 27MHz from the crystal oscillator (pin between U7 and U9)
10 - Pin 5 of the IT6613E lifted and connected to R31 (top pad) (only if you want to use the external MCLK)


External MCLK (read update, too)
================================
The IT6613E derives the system clock for audio processing (audio master clock, MCLK) from the I2S input (I2S0, WS and SCK) by default. It is also possible to feed the MCLK into the IT6613E using pin 5 and setting appropriate register bits.
If you have problems with the internally derived MCLK of the IT6613E, you have to use the external MCLK. Problems mean that you might have audio dropouts or you simply hear nothing! Then you have to use the external MCLK.
Next to setting the option in the OSSC menu you might have to modify your OSSC a bit.
- older audio boards v1.5-A3x, v1.3-A3, and before: lift pin 5 of the IT6613E and connect the pin with R31 (top pad; see picture 10) 
- newer audio boards v1.3-A4: designed to lift pin 5 before installation. Nothing more to done.
- newer audio boards v1.5-A4x: lift pin 5 and connect the pin with the pad 'MCLK' on the audio add-on board

Update:
marqs has found out that the problem was related to a bug of the IT6613E. Setting the output audio mode flag to standard I2S forced the IT6613E to use 16bit word length instead of 24bit as it is. Setting this flag to use '32bit' fixed that and the IT6613E uses 24bit then. See this commit and especially this line here: https://github.com/marqs85/ossc/commit/fac88b348e32807aa04aa2773f0e064f15f79182#diff-fac9ffe1afa8860b748fee26e07f05a0R565
Please report if you observe problems despite that change? Does it makes any difference between using internally generated MCLK or externally provided MCLK?