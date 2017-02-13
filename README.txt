The OSSC does not output audio over HDMI or DVI-D, respectively. This add on captures the analoge audio you feed over the SCART or audio 3.5mm stereo jack. The audio signal is digitalize and put into the IT6613E over the I2S audio interface.
This repository provides the hardware design for the modification. The installation requires installation effort which depends on the OSSC version number you have.

Firmware
========
The IT6613E has to be programmed appropriately to insert audio to the digital video output. In the 'original' firmware audio is not taken into account. Therefore the firmware of the OSSC has to be updated.
Up to the OSSC firmware version v0.73 you can grab the current firmware in this repository. With v0.74 the source code part needed for the audio modification was integrated to the official GitHub branch by marqs85. The builds can be grabbed from the official source: https://www.niksula.hut.fi/~mhiienka/ossc/fw/. Additionally, I provide a mirror here.


PCB Production
==============
Choose the service you would ever like. I have uploaded the design to OSHPark, too.
VERY IMPORTANT: The substrate thickness has to be as thin as possible.
The PCB for v1.3 is design to sit between lifted pins of the IT6613 (the HDMI transmitter) and OSSC-PCB (just look at the installation pictures to get an idea ;)). With v1.5 the OSSC comes with jumpers which are connected to the appropriate pins of the IT6613E. The add-on sits on top of the jumpers (don't forget to open them). 
I have produced the PCBs with OSHPark and have chosen 0.8mm thickness. The PCB must not be thicker.
Link to PCB at OSHPark:
- https://oshpark.com/shared_projects/rmFBAKyo (for v1.3)
- https://oshpark.com/shared_projects/vKUEgBSy (for v1.5)
- https://oshpark.com/shared_projects/WeKdeoGP (for v1.5 with wired connection to the SCART)

Part list of the DIY-Audio PCB
==============================
running number ------ footprint(s) --------- device/part --------- package ----- mouser ordering key
     01         |  U1                 |  PCM1808               |  TSSOP14     |  595-PCM1808PWR
     02         |  U2                 |  74LVC1G34             |  SOT23-5     |  595-SN74LVC1G34DCKR
     03         |  U3                 |  MK2705SLF             |  SOIC8       |  972-MK2705SLF
     04         |  FB1, FB2           |  Ferrit Beat           |  SMD0603     |  81-BLM18PG471SN1D
     05         |  C1                 |  tantal-cap. 47uF/16V  |  SMD case C  |  74-293D476X9016C2TE3
     06         |  R11, R12           |  res. >2.2 kOhm        |  SMD0603     |  71-CRCW06034K99FKEAH (e.g. 4.99k)
     07         |  C11, C13, C15      |  tantal-cap. 10uF/6.3V |  SMD case A  |  74-TR3A106M6R3C1500
     08         |  C12, C14, C16, C21 | cap. 0.1uF/50V         |  SMD0603     |  77-VJ0603V104MXACBC
     09         |  C17, C18, C31      | tantal-cap. 1uF/16V    |  SMD case A  |  74-293D105X9016A2TE3
     10         |  R19, R20           | res. ***               |  SMD0603     |  see description below
     11         |  C19, C20           | cap. ***               |  SMD0603     |  see description below
     12         |  R31                | res. 33 Ohm            |  SMD0603     |  71-CRCW060333R0FKEAH
     13         |  C32, C33           | cap. 0.01uF/50V        |  SMD0603     |  77-VJ0603Y103KXACBC

RC-filtering of the Audio
=========================
The RC filters (R19,C19) and (R20,C20) mainly bandlimits the noise. The filter also avoids aliasing effects if the bandwith of the audio signal increases.
The PCM1808 samples the audio signal with 96kHz. This means that the cut-off frequency of the filters have to be 96kHz or below. The firmware will also allows you to further downsample the datastream to 48kHz. If you want to use that I recommend you to set the filter to 48kHz or below to avoid aliasing.
The cut-off frequency f_c of a simple RC low pass filter is determined by f_c = 1/(2*pi*R*C).
here is my choice which gives a cut-off frequency of 47.938kHz.
     10         |  R19, R20  |  res. 3.32 kOhm   |  SMD0603  |  71-CRCW0603-3.32K-E3  
     11         |  C19, C20  |  cap. 1000pF/50V  |  SMD0603  |  77-VJ0603Y102KXACBC



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