# tec-VIDEO-BG
TEC-1 Video system by Benn Grimmett


from FB;

Ben Grimmett?Australian Vintage Computer Group
Visual Storyteller · 13 hrs · 
 
I spent last night working 
	on coding my TEC SD/PS2/Serial/video card 
	and its coming along great. 

Video and SD interface was confirmed working 
and a complete SD and FAT32 library will easily fit in the 2kbytes of EPROM. 

The limitations 
	of the 2K SRAM, port and address mirroring 
	and lack of SRAM /OE control 
	has inspired V1.3 of my video card.

This new revision has 
	128kbytes of SRAM onboard 
	with a mapper which has 2kbyte granularity 
	and can place any 2kbytes of the 128k in any 2kbyte bank. 
	It can also map in and out the EPROM 
	and the Video RAM address space. 
		All through the Expansion port plus a few control lines.

The idea is the EPROM can 
	bootstrap a ROM file from the SD card, 
	and launch it from any address location. 

Combined with 
	a PS2 keyboard interface 
	and a very capable video controller 

the TEC can now join the ranks 
	of TRS-80's, 
	Microbees, 
	Amstrads 
	and Sinclairs 
	running Microsoft Basic, CPM as well as a graphical assembler/disassembler 
	which I feel is a natural progression of the TEC computer.

Still a lot of work ahead 
but once the new PCB's arrive 
	I'll port over Basic as well 
	as add a command line interface to the monitor ROM. 

To some its an abomination 
	but it certainly gives new life to your TEC computer!. 
	Fully assembled boards will be available once hardware is confirmed. 
	Approx $50. 
	Source will be available as well as documentation of all ports and address space.


Ben Grimmett Reinoud de Lange 
	it'll really benefit from the xtal mod board 
	though it could technically run at the original clock speeds too. 
	Just very very slowly
Reinoud de Lange Ben Grimmett 
	and this xtal mod board replaces the 4049?
Ben Grimmett 
	Yes, drop in replacement
Reinoud de Lange 
	and this xtal mod board, is it difficult to build?
Ben Grimmett Reinoud de Lange 
	it's surface mount and will need hot air, ir, or an oven
Ben Grimmett 
	But I sell them pre built
Reinoud de Lange 
	you should set up a webshop and wiki for the TEC-1 and peripherals...
Ben Grimmett Reinoud de Lange 
	yes I will. 
	I have started to list and document the various boards I've made
  
  ============
  
Latest revisions have just arrived. 
The TEC video card now includes a 
PS2 keyboard port, 
micro SD socket 
and serial port.

 
================

My TEC Video Card:

A work in progress. 
	The latest FPGA configuration file is HERE

The address and port 
	breakdown is as follows:

Base Address of Expansion socket = 0x1000
Mode Register = Port3
Scroll Register = Port4

When in Mode0: - Video RAM Access
Scroll Register = xPssssss
x=dont care
P=Page
s=Scroll Offset
32x32 Character visible screen area located at 0x1000-0x13FF
32x32 Character off screen area located at 0x1400-17FF
1 Page = 32x64 Characters.

When in Mode1: - Character RAM Access
2kbytes Character RAM are mapped to 0x1000-0x17FF
Charaters are drawn as:
0bxxxxxxxx ;Byte 0
0bxxxxxxxx ;Byte 1
0bxxxxxxxx ;Byte 2
0bxxxxxxxx ;Byte 3
0bxxxxxxxx ;Byte 4
0bxxxxxxxx ;Byte 5
0bxxxxxxxx ;Byte 6
0bxxxxxxxx ;Byte 7

When in Mode2: - Spirte Attribute Access
5 Sprites available
0x1000 - Sprite1 X location
0x1001 - Sprite1 Y location
0x1002 - Sprite2 X location
0x1003 - Sprite2 Y location
Down to.....
0x1010 - Sprite9 X location
0x1011 - Sprite9 Y location
0x1012 - Sprite10 X location
0x1013 - Sprite10 Y location

0x1014 - Sprite1 Tile Pointer
0x1015 - Sprite2 Tile Pointer
Down to.....
0x101D - Sprite10 Tile Pointer

When in Mode3: - Sprite RAM Access
0x1000 - 0x1007 Sprite1 Character Data (Tiles)
Down to.....
0x13F0 - 0x13FF Sprite 128 Character Data

Each sprite can use any one of 128 sprite tiles. 
	This is handy for turning them off (selecting a blank tile) 
	or animation (changing the tile without re-writing new tile data) 
	as well as multiplexing tiles to draw more than 10 sprites on screen at once.

Sprites not valid in location 0,0

When power is first applied, 
	ChrRAM is pre-loaded with the default DOS ASCII character set 
	and Vram loaded with a messages on page 0. 

==================

