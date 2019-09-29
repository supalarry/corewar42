# corewar42

Corewar is an algorythmic project at Codam (42).
The purpose of this project is to recode the programming game “Core War”.

Corewar is a game where players fight within a virtual space to stay live the longest.
Players can overwrite virtual space and can duplicate processes with which to execute commands.
Below is an image of our project:

![alt text](https://imgur.com/BSXVUlI.png)

## Overview

This project consists of:

**Assembler** - Assembler translates assembly code into machine code. The players that fight in this game are written in        assembly. Because the environment where they fight only understands machine code, they need to be translated.

**Disassembler** - Disassembler turns executable code back into human readable assembly code.

**Virtual Machine** - This is virtual arena where player executables fight. From the executable, it extracts information        about players and places their commands on virtual battlefield. Then, each player receives a process called **carriage**.      The purpose is carriage is to execute function is has stepped on. In the image above, carriages are coloured squares that      have stepped on some command. The winner who reports 'live' command last, wins. Our virtual machine also has a visualizer to see how the games goes.

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
├── libs [files for libraries]
├── test [files for testing our project]
├── test_vm [files for testing virtual machine]
├── vm [all files for virtual machine]
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

