# corewar42
```
Corewar is a game where players fight within a virtual space to stay live the longest.
Players can overwrite virtual space and can duplicate processes with which to execute commands.
```
![alt text](https://imgur.com/BSXVUlI.png)

## Overview

This project consists of four main parts:

**Assembler** - Assembler translates assembly code into machine code. The players that fight in this game are written in        assembly. Because the environment where they fight only understands machine code, they need to be translated.

**Virtual Machine** - This is virtual arena where player executables fight. From the executable, it extracts infotmation        about players and places their commands on virtual battlefield. Then, each player receives a process called **carriage**.      The purpose is carriage is to execute function is has stepped on. In the image above, carriages are coloured squares that      have stepped on some command. The winner who reports 'live' command last, wins. Our virtual machine also has a visualizer to see how the games goes.

If it is hard to understand the point of the game, then that's expected. At the start of the assignement we were just given properly working assembler, virtual machine and example players and needed to figure out the rules of the game ourselves. It took quite a time to wrap our heads around it too.

**Champion** - This is player written in assembly language with a purpose to stay alive long as possible and battle other players.

**Visualizer** - As shown in the picture above, visualizer shows the current state of the game.

A more detailed guide can be seen at my teammate's wiki page - https://github.com/k-off/Corewar/wiki

## Project folder structure
```
corewar42
├── asmf [all files for assembler]
├── dasmf [all files for disassembler]
├── includes [header files for the project]
├── libs [files for libraries
├── test [files for testing our project]
├── test_vm [files for testing virtual machine]
├── vm [all files for assembler]
LavanderMan.s [our champion written in assembly]
Makefile [compiles the project]
author [my and my teammate's usernames]
```

## Installation

Clone repository and then go into the created directory and run the following command:

```
make
```

## Usage

### `assembler`

```
Usage: ./asm (champion.s)
    champion.s   — convert from assembly to bytecode
```

### `disassembler`

```
Usage: ./dasm (champion.cor)
    champion.cor — convert from bytecode to assembly
```

### `corewar`

```
Usage: ./corewar [-a (-dump) <num> [-v] [-n <num>] <champion.cor> <...>
    -a          : Print output from "aff" (Default is off)
    -dump <num> : Dump memory (64 octets per line) after <num> cycles and exit
    -v          : Run visualizer
    -n    <num> : Set <num> of the next player
    -L          : Print all the reports 'alive' to the standard output
```

### `visualizer`

```
    up/down arrows    : switch between players
    left/right arrows : switch between processes of selected player
    space             : pause/continue execution
    <                 : go to previous cycle and pause the game
    >, tab            : go to next cycle and pause the game
    To change the history depth(amount of previous cycles available to visualizer), modify the HIST_DEPTH in the visual.h
```

### `tester`

There is a simple tester included in the repo.

To run it:

```
    cd test
    sh test.sh -all
```

It will check makefile, Norminette (complinace with the internal 42 coding standards), assembler, disassembler and the vm against the outputs and behaviour of the reference files `original_asm` and `original_corewar` from the directory `test`.

** Important **

If you don't have the norminette script installed on your machine, you may want to delete or comment out lines 27-34 from the file `test.sh`.


## Assembler
Assembly language used to write players has been developed specifically for this exercise. Like real assembly language, programmer can load number into a register, do addition and substraction etc.

Each player needs to include it's name, comment about it and then operations. Below is an example:
```
.name 		"turtle"
.comment	"TURTLE FFS U LAMA"

entry:
	sti			r1, %:zork, %1
	sti			r1, %:ardef, %1
	sti			r1, %:avdef, %1
	sti			r1, %:entry_l1, %1
	ld			%0, r16
	fork		        %:zork

entry_l1:
	live		%42
	ld			%439025904, r2
	ld			%0, r16
	fork		        %:avdef
...
...
...
```
In total, there are 16 different operations that can be used. Furthermore, it is allowed to use labels, like in the example 'entry' and 'entry_l1'. Labels are like pointers pointing to specific instruction. We can see that in the very first operation 'r1, %:zork, %1', '%;zork' refers to label found further in code. This is translated into a distance in bytes aka how far is that operation from current one.

The assembler also validates the input. For example, if for a specific operation incorrect amount of arguments, or incorrect type was used, or not existing registry is used then an error is thrown.

The assembler takes this file and outputs executable file. To translate file, you must use it as input for the assembler:

```
./asm < player
```

The output of the whole file above is:

```
0000000 00 ea 83 f3 74 75 72 74 6c 65 00 00 00 00 00 00
0000010 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
*
0000080 00 00 00 00 00 00 00 00 00 00 01 8a 54 55 52 54
0000090 4c 45 20 46 46 53 20 55 20 4c 41 4d 41 00 00 00
00000a0 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
*
0000890 0b 68 01 00 df 00 01 0b 68 01 00 35 00 01 0b 68
00008a0 01 00 d9 00 01 0b 68 01 00 11 00 01 02 90 00 00
00008b0 00 00 10 0c 00 bc 01 00 00 00 2a 02 90 1a 2b 00
00008c0 f0 02 02 90 00 00 00 00 10 0c 00 ae 01 00 00 00
00008d0 2a 03 70 02 fe 70 03 70 02 fe 70 03 70 02 fe 70
00008e0 03 70 02 fe 70 03 70 02 fe 70 03 70 02 fe 70 03
00008f0 70 02 fe 70 03 70 02 fe 70 03 70 02 fe 70 03 70
0000900 02 fe 70 03 70 02 fe 70 03 70 02 fe 70 03 70 02
0000910 fe 70 03 70 02 fe 70 03 70 02 fe 70 03 70 02 fe
0000920 70 03 70 02 fe 70 03 70 02 fe 70 03 70 02 fe 70
0000930 03 70 02 fe 70 03 70 02 fe 70 03 70 02 fe 70 03
0000940 70 02 fe 70 03 70 02 fe 70 03 70 02 fe 70 03 70
0000950 02 fe 70 03 70 02 fe 70 03 70 02 fe 70 03 70 02
0000960 fe 70 03 70 02 fe 70 03 70 02 fe 70 09 ff 60 01
0000970 00 00 00 2a 09 ff fb 01 00 00 00 2a 03 70 02 01
0000980 90 03 70 02 01 90 03 70 02 01 90 03 70 02 01 90
0000990 03 70 02 01 90 03 70 02 01 90 03 70 02 01 90 03
00009a0 70 02 01 90 03 70 02 01 90 03 70 02 01 90 03 70
00009b0 02 01 90 03 70 02 01 90 03 70 02 01 90 03 70 02
00009c0 01 90 03 70 02 01 90 03 70 02 01 90 03 70 02 01
00009d0 90 03 70 02 01 90 03 70 02 01 90 03 70 02 01 90
00009e0 03 70 02 01 90 03 70 02 01 90 03 70 02 01 90 03
00009f0 70 02 01 90 03 70 02 01 90 03 70 02 01 90 03 70
0000a00 02 01 90 03 70 02 01 90 03 70 02 01 90 03 70 02
0000a10 01 90 03 70 02 01 90 09 ff 60
0000a1a
```

## Virtual Machine
Virtual machine receives executables from all players and then places them in memory.
Then each player receives a 'carriage'. Carriage is a process that executes command it is standing on.
Below you can see the whole gameplay speeded up
