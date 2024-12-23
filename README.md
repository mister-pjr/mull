# mull
Multi User Lunar Lander 11 - Only for RSX-11M+

After getting my PiDP-11 up and running, I settled on RSX-11 as the OS to delve deeper.
After some "delving" I wondered what to do with it... Some kind of multi-user game seemed a good option.
I settled on a 2-user version of the lunar lander game in glorious 24x80 "graphics", not knowing if someone had done it before. 

BP2 or Basic Plus 2 was the choosen language: easy to learn and prototype, some nifty capabilities and it's a compiled language.

Technically, the game has 3 components: a server (MULLSRV) that does almost all the calculations, a client (MULLCLI) doing the display and accepting commands, 
and finally a common area module (MULLCOM), where are all the common variables between clients and server reside. 
Both the server and client require two additional files (COMDEF.B2S and COMCODE.B2S) that are included at compile time.

Finally, Johnny Bilquist help was fundamental in helping me understand how to use a common area to share variables.

So each player has to run the client program (RUN MULLCLI) at a terminal window and one of them has also to launch the server (RUN MULLSRV) from another terminal.
Obviously both need access to MULLCLI... and before everything starts, someone has to load the common area (INS MULLCOM).

# Installation
First we need to compile client and server:

BP2 MULLCLI

BP2 MULLSRV

Now we need to build the executable task with the commands:

TKB @MULLCLI

TKB @MULLSRV

BUT... first we need to slightly the CMD files used by the task builder. The line RESCOM = SY:MULLCOM/RW must be added as the last line to MULLCLI.CMD and MULLSRV.CMD
Now we can run the TKB commands above.

To finish we need to assemble and build the common area module:

MAC MULLCOM=MULLCOM

TKB MULLCOM/-HD/PI,MULLCOM,MULLCOM=MULLCOM

This common module has to be "inserted" into memory before calling either the server or client, or else you'll get an error.
To do that you need to be a privileged user (like SYSTEM):

INS MULLCOM

The module will remain in memory until it is specifically removed with REM MULLCO/REG or the PDP reboots.
That's all...

# Operation
First launch the server:

RUN MULLSRV

It will start by asking for initial values for altitude, starting speed, fuel allowance and max admissible speed when touching the ground.
Pressing Return will accept the presented defaults.
The server will now wait until both players join in.

Each player should execute in their terminals:

RUN MULLCLI

After both players have entered the game starts. First the game layout is displayed along with a random terrain contour. 
The landing pad is denoted by 8 underscores (_). Trying to land anywhere else (the "mountains") will get you killed.

