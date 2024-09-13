# Phantom Fighter Source Code

This is the source code for the Commodore Amiga game "Phantom Fighter" released commercially in 1988. It was my first commercial game. I found a floppy from Aug 1988 with the source code but no graphics files. I coded this when I was 19 years old and it's sorely lacking in comments. It's a combination of lattice C and 68000 assembler. 
The code was executed natively by booting from a floppy, no bootstrap. It uses a boot library and floppy driver written by Brian Kelly who worked at Emerald Software at the same time as me. This boot library was called KOS (Kel's operating system).

## Whats missing

I found a floppy containing this code when rummaging through stuff at my parents house. The game is not complete. It's missing header files and libraries and the graphics. The graphics could possibly be recovered from a game disk which I also have but haven't done yet. I will try to recover the graphics and add them to this repository.

The code is organized around an event scheduler which executes every frame. The scheduler is a linked list of events which are executed in order of their time. The scheduler is updated every frame and events are added and removed from the scheduler as needed. The scheduler is the main loop of the game. I will try to comment the code and improve explaining how it works
over time. Meanwhile, I guess it's an interesting piece of history for those interested in the Amiga and game development in the late 80s.
