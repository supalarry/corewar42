# corewar42
```
Corewar is a game where players fight within a virtual space to stay live the longest.
Players can overwrite virtual space and can duplicate processes with which to execute commands.
```
![alt text](https://imgur.com/BSXVUlI.png)

This project consists of two parts:

**Assembler** - Assembler translates assembly code into machine code. The players that fight in this game are written in        assembly. Because the environment where they fight only understands machine code, they need to be translated.

**Virtual Machine** - This is virtual arena where player executables fight. From the executable, it extracts infotmation        about players and places their commands on virtual battlefield. Then, each player receives a process called **carriage**.      The purpose is carriage is to execute function is has stepped on. In the image above, carriages are coloured squares that      have stepped on some command. The winner who reports 'live' command last, wins.
