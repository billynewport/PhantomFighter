# Phantom Fighter Source Code

This is the source code for the Commodore Amiga game "Phantom Fighter" released commercially in 1988. It was my first commercial game. I found a floppy from Aug 1988 with the source code but no graphics files. I coded this when I was 19 years old and it's sorely lacking in comments. It's a combination of lattice C and 68000 assembler. 
The code was executed natively by booting from a floppy, no bootstrap. It uses a boot library and floppy driver written by Brian Kelly who worked at Emerald Software at the same time as me. This boot library was called KOS (Kel's operating system).

## Whats missing

I found a floppy containing this code when rummaging through stuff at my parents house. The game is not complete. It's missing header files and libraries and the graphics. The graphics could possibly be recovered from a game disk which I also have but haven't done yet. I will try to recover the graphics and add them to this repository.

The code is organized around an event scheduler which executes every frame. The scheduler is a linked list of events which are executed in order of their time. The scheduler is updated every frame and events are added and removed from the scheduler as needed. The scheduler is the main loop of the game. I will try to comment the code and improve explaining how it works
over time. Meanwhile, I guess it's an interesting piece of history for those interested in the Amiga and game development in the late 80s.

## History

I joined Emerald Software in March 1988 to do my work experience at the company. I was hired by Mike Murphy and Mike Dixon was the Managing Director of Emerald Software. Dave Martin was the financial backer along with the IDA, which is the Irish Government. Dave Martin had a UK based games company called Martech Software. This was a 6 month job after which I returned to finish my Degree at Waterford Institute of Technology in Waterford Ireland. It was called Waterford Regional Technical College (WRTC) at the time. I started work there evaluating a CAPCOM coin op conversion for Tiger Road to home computers but ultimately ended up coding Phantom Fighter. The artist was Paul McLaughlin. Paul stayed in video games after Emerald Software failed and became a key figure in UK video games through his work at BullFrog.

Initially, we obtained what I think were some of the first Amiga 1000 computers in Europe. We used them with 2 floppy drives and later small external hard drives (maybe 5MB in size). We had the full hardware and software manual sets. We mostly used the hardware manuals as we decided to run the games natively with no operating system. We booted straight in to the game using a home grown operating system KOS (Kel's operating system) written by Brian Kelly.

## Graphics inspiration

Paul was responsible for the graphics. He was intriguted with the Alien movies and wanted an organic feel.

## Game Hardware overview

The game was designed around the dual playfield graphics mode on the Amiga. This provided 2 independent 320x200 8 color view fields, one on top of the other. Each can be scrolled independently. I used hardware sprites for player bullets and ships were rendered on the screen using the blitter. The blitter was used in a clever way. Normally, each bitplane for each playfield (there are 3 per playfield, hence 8 colors) is allocated in memory and then the hardware is setup to point at the 3 bitplanes memory for each playfield. We rendered the ships and graphics on the top playfield. Usually, this means we would need a blitter operation per bitplane to render a software sprite. Brian Kelly came up with the idea of interlacing the playfield bitplanes. Usually, you tell the hardware the bitplane starts at address X and each scan line is 40 bytes long. Instead, we interlaced the 3 bitplanes. This first we have 40 bytes for line 0 of bitplane 0, then the next 40 bytes is the line 0 for bitplane 1 and the next 40 bytes is line 0 for bitplane 2. We need to tell the hardware still the start in memory of line 0 for each bitplane like before but we tell it the skip to the next line is 120 bytes instead of 40. The Amiga hardware happily showed the bitplanes correctly. But, it also allowed us to use a single blitter operation to do all 3 bitplanes. I also interlaced the software sprites similarly in memory.

The game used the Copper chip to interact with the video hardware registers. This included setting up the dual playfield as described above, the hardware sprites and switching the video mode towards the bottom of the screen allowing a score board to be displayed. The dual playfield was only at the top portion of the screen, the playable area. The score board showed how many lifes were left, the score and so on. This was a straight 16 color playfield.
