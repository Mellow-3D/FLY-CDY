## Issues

There is a known issue with the bootloader that is shipped with the Fly-CDY board.  
It will manifest itself in the board being unable to boot if the E1 UART connector is in place.  
There are 2 methods that can be employed to fix this issue.  

### Method 1

Rather then installing the jumper for UART mode as described above, install it as shown in the image below.  

![cdy_jumper_fix](https://github.com/FLYmaker/FLY-CDY/blob/master/Bootloader/fly_cdy_fix.jpg)

Then include the following line in the board.txt file.  
```
stepper.TmcUartPins = { 1.4, 1.10, 1.16, 4.28, 0.21, 0.10, NoPin }
```  

### Method 2

This involves updating the bootloader on the Fly-CDY and required a [USB TTL device](https://www.amazon.co.uk/dp/B00AFRXKFU/ref=cm_sw_em_r_mt_dp_2D8VTXSMW5DWXBT7F9GN).  

Ensure the power is disconnected from your Fly-CDY, although ideally, this should be done with nothing else connected to the board (especially high drain items such as a screen).  
Connect the USB TTL to the Fly-CDY.  

|TTL|CDY|
|:---|:---|
|+5V|+5V|
|GND|GND|
|RX|TX|
|TX|RX|

![cdy_jumper_fix2](https://github.com/FLYmaker/FLY-CDY/blob/master/Bootloader/fly_cdy_fix2.jpg)

Download and install [Flash Magic](https://www.flashmagictool.com/download.html&d=10.90/FlashMagic.exe).  
Download and install the updated bootloader from here.  
Launch flash magic. 

![flash_magic](https://github.com/FLYmaker/FLY-CDY/blob/master/Bootloader/flash_magic.png)

As shown above, instep 1 select LPC1769 in the first box, the COM port should be the COM port of your Fly-CDY board and set the baudrate to 38400.  
In step 2, make sure "Erase all..." is unticked and "Erase blocks..." is ticked.  
In step 3, browse and select the new bootloader image you downloaded from above.  
In step 4, make sure "Verify..." is ticked and "Patch" and "Fill unused" are unticked.  

Hold both the reset and boot buttons on the Fly-CDY. Release the reset button and then the boot button.  
Press Start on Flash Magic.  

Once the flashing has been completed, the UART connection can be used as normal.