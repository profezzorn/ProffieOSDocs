These commands are usually used for deeper diagnostics beyond typical use.  
For more typical use case commands, see [Serial Monitor Commands](serial-monitor-commands.md).  
# WARNING - While most of these are harmless, some of these are powerful and should only be used if you're familiar with how they work. 


##  scanid

Have the board deactivate all current blades, check the BladeID and pick a BladeConfig [] array based on the new detected BladeID.

## id

Show the blade ID. 

## dacbuf

Print the current contents of the dac buffer.

## list_named_style

List all available named styles.

## describe_named_style <style>

Show what arguments a style requires.

## amp on/off

Turn amplifier on or off.

## booster on/off

Turn 5V booster on or off.

## make_default_console

Make this connection the default connection (if using something other than Arduino Serial monitor, like a TTL->USB interface)


## malloc

Show how much dynamic memory is allocated.

##  whatison

Shows all the wav players, whether they are currently on or off, and what is loaded into each of them.

# **BLADES:**

### **SimpleBlade:**     
## blade on/off
Turn simple blade on off.
## state
Displays if SimpleBlade is on or off.
<br/>  
The following requires ENABLE_FASTLED defined:    
## blade on/off
Turn apa102 blade on off.  
<br/>
The following requires ENABLE_WS2811 defined:   
## blade on/off
Turn ws2811 blade on off. 
<br/> 
The following requires ENABLE_DEVELOPER_COMMANDS defined:    
## state
Displays if WS2811 is on or off
<br/>
<br/>
*NOTE* - The following commands only work if  
`#define DISABLE_DIAGNOSTIC_COMMANDS` in _NOT_ active in the config.h file. 

## monitor <topic>

Toggle extra debug printouts. Topic is one of: swings, gyro, samples, touch, battery, pwm, clash, temp, strokes, serial, fusion, variation

## volumes

Prints volumes of sounds currently occupying wav players.

## buffered

Prints buffering of sounds currently occupying wav players.

## get_ble_config

Show BLE PIN

## top

Prints statistics about how often things are running and how much cpu they are using. If something is slow, start by running this command a few times and see if something sticks out at you.

<br/>
<br/>
*NOTE* - The following commands only work if  
`#define ENABLE_DEVELOPER_COMMANDS` _IS_ active in the config.h file. 

## say _ARG_
Test error messages. See following ARGs list:  
    - bfd "Error in font directory"  
    - bof "Font directory not found"  
    - ftl "Font directory too long"  
    - sd "SD card not found"  
    - bb "Error in blade array"  
    - bp "Error in preset array"  
    - lb "Low battery"  
## talkie <hexdata>
Play talkie from hex string. rate = 25.

## talkie_slow
rate = 25  

## talkie12
rate = 12   

## talkie15
rate = 15  

