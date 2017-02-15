External MCLK (read update, too)
================================
  
Update:
marqs has found out that the problem was related to a bug of the IT6613E. Setting the output audio mode flag to standard I2S forced the IT6613E to use 16bit word length instead of 24bit as it is. Setting this flag to use '32bit' fixed that and the IT6613E uses 24bit then. See this commit and especially this line here: https://github.com/marqs85/ossc/commit/fac88b348e32807aa04aa2773f0e064f15f79182#diff-fac9ffe1afa8860b748fee26e07f05a0R565
Please report if you observe problems despite that change? Does it makes any difference between using internally generated MCLK or externally provided MCLK?  

old text:  
The IT6613E derives the system clock for audio processing (audio master clock, MCLK) from the I2S input (I2S0, WS and SCK) by default. It is also possible to feed the MCLK into the IT6613E using pin 5 and setting appropriate register bits.
If you have problems with the internally derived MCLK of the IT6613E, you have to use the external MCLK. Problems mean that you might have audio dropouts or you simply hear nothing! Then you have to use the external MCLK.
  
Firmware  
========  
Due to the latest update, the external master clock is not supported by official firmware. A simple hardware modification does not change anything. However, this repository provides firmware build to use the external clock. ONLY use that firmware along with the hardware modification described here.  
The firmware has the ext. mclk enabled! This cannot be changed in the menu.  
  
Hardware Modification
=====================
  
Next to using the inofficial firmware you have to modify your OSSC a bit.
- older audio boards v1.5-A3x, v1.3-A3, and before: lift pin 5 of the IT6613E and connect the pin with R31 (top pad; see picture 10) 
- newer audio boards v1.3-A4: designed to lift pin 5 before installation. Nothing more to done.
- newer audio boards v1.5-A4x: lift pin 5 and connect the pin with the pad 'MCLK' on the audio add-on board

Pictures  
========  
  
10 - Pin 5 of the IT6613E lifted and connected to R31 (top pad) (only if you want to use the external MCLK)  
