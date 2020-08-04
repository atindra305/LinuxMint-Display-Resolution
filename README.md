# LinuxMint-Permanent-Display-Resolution
Set the linux mint display setting for monitor

# [Temporary Fix](https://github.com/atindra305/LinuxMint-Permanent-Display-Resolution/blob/master/resolution) 
1. Open Terminal
2. Type xrandr

            $ xrandr
            Screen 0: minimum 320 x 200, current 2560 x 1024, maximum 8192 x 8192
            LVDS-1 connected 1280x800+0+0 (normal left inverted right x axis y axis) 331mm x 207mm
               1280x800      60.00*+  59.99    59.97    59.81    59.91  
               1280x720      60.00    59.99    59.86    59.74  
               1024x768      60.04    60.00  
               960x720       60.00  
               928x696       60.05  
               896x672       60.01  
               1024x576      59.95    59.96    59.90    59.82  
               960x600       59.93    60.00  
               960x540       59.96    59.99    59.63    59.82  
               800x600       60.00    60.32    56.25  
               840x525       60.01    59.88  
               864x486       59.92    59.57  
               800x512       60.17  
               700x525       59.98  
               800x450       59.95    59.82  
               640x512       60.02  
               720x450       59.89  
               700x450       59.96    59.88  
               640x480       60.00    59.94  
               720x405       59.51    58.99  
               684x384       59.88    59.85  
               680x384       59.80    59.96  
               640x400       59.88    59.98  
               576x432       60.06  
               640x360       59.86    59.83    59.84    59.32  
               512x384       60.00  
               512x288       60.00    59.92  
               480x270       59.63    59.82  
               400x300       60.32    56.34  
               432x243       59.92    59.57  
               320x240       60.05  
               360x202       59.51    59.13  
               320x180       59.84    59.32  
            VGA-1 connected primary 1280x1024+1280+0 (normal left inverted right x axis y axis) 0mm x 0mm
               1024x768      60.00  
               800x600       60.32    56.25  
               848x480       60.00  
               640x480       59.94  
            SVIDEO-1 unknown connection (normal left inverted right x axis y axis)
               848x480       59.94 +
               640x480       59.94 +
               1024x768      59.94  
               800x600       59.94  
               
3. Type the display resolution which you want:

            $ cvt 1280 1024 60
            # 1280x1024 59.89 Hz (CVT 1.31M4) hsync: 63.67 kHz; pclk: 109.00 MHz
            Modeline "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync

4. Type the following next commands:

      Format: $ xrandr --newmode <After Modeline>
  
            $ xrandr --newmode "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync
            
5. Now, just type xrandr. This will give you something like 

            Screen 0: minimum 320 x 200, current 1280 x 1024, maximum 1920 x 2048
            VGA-1 connected primary 1280x1024+0+0 (normal left inverted right x axis y axis) 0mm x 0mm
               1024x768       60.0  
               800x600        60.3     56.2  
               848x480        60.0  
               640x480        59.9  
               1280x1024_60.00   59.9* 
               
6. The connected screen name is what you need - on my system, it's VGA-1.
    
    1. This will add the mode to the dropdown when you go into the display settings
    
            $ xrandr --addmode VGA-1 1280x1024_60.00
            
    2. This should change your resolution within a split second to your desired setting
    
            $ xrandr --output VGA-1 --mode "1280x1024_60.00"

# [Permanant Fix](https://github.com/atindra305/XFCE-Display-Resolution/blob/master/SetResolution.sh)
1. Create a bash file to automate the above changes.

2. Open a text editor and type the following commands (as above ones):

            #! /bin/bash
            xrandr --newmode "1280x1024_60.00"  109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync
            xrandr --addmode VGA-1 1280x1024_60.00
            xrandr --output VGA-1 --mode "1280x1024_60.00"

3. Save the file on 'Desktop' as 'SetResolution.sh'.

4. Right-click on the icon for SetResolution.sh, and choose "Properties".

5. Select the "Permissions" tab.

6. Click on the checkbox to allow executing file as program, and then click "Close".

You should now be able to double-click this file and instantly change your resolution whenever you boot into your system.

# Automate from Start of System

1. Add a link to this file into your Startup Applications
