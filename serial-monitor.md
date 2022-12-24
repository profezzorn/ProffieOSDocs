The Serial Monitor is a simple tool for talking to ProffieOS.
ProffieOS will print out messages when something is happening, and you can enter commands to try things out.

To start the Serial Monitor, go to connect your board to the computer and start up Arduino.
Now go check Tools->Port and select the right port. For Proffieboard it might say "butterfly" next to it.

If the port doesn't show up, see this page: [Where's my Port?](troubleshooting/wheres-my-port.md)

Once the right port is selected, start the serial monitor by selecting it from the Tools menu.
If everything works, you should see some messages from ProffieOS, such as "Welcome to ProffieOS".
The first time you use the Serial Monitor, you will need to select the correct line endings in the bottom right corner. The correct line ending is "newline".

You should now be able to type commands. For a list of typically used entries, 
see [Serial Monitor Commands](serial-monitor-commands.md).  
For additional available commands, see [Serial Monitor Additional Commands](serial-monitor-additional-commands.md).

