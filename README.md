# mull
Multi User Lunar Lander 11 - Only for RSX-11M+

After getting my PiDP-11 up and running, I settled on RSX-11 as the OS to delve deeper.
After some "delving" I wondered what to do with it... Some kind of multi-user game seemed a good option.
I settled on a 2-user version of the lunar lander game in glorious 24x80 "graphics", not knowing if someone had done it before.

BP2 or Basic Plus 2 was the choosen language: easy to learn and prototype and with some nifty capabilities.
Technically, the game has 3 components: a server (MULLSRV) that does almost all the calculations, a client (MULLCLI) doing the display and accepting commands, 
and finally a common area module (MULLCOM), where are all the common variables between clients and server reside.
Johnny Bilquist help was fundamental in understanding how to use a common area to share variables.

So each player has to run the client program (RUN MULLCLI) at a terminal window and one of them has also to launch the server (RUN MULLSRV) from another terminal.
Obviously both need access to MULLCLI... and before everything starts, someone has to load the common area (INS MULLCOM).

