# MineSweeper Hacking Documentation

## What is Minesweeper?
From Wikipedia:
>Minesweeper is a logic puzzle video game genre generally played on personal computers. The game features a grid of clickable squares, with hidden "mines" scattered throughout the board. The objective is to clear the board without detonating any mines, with help from clues about the number of neighboring mines in each field. 

![image](https://user-images.githubusercontent.com/5856107/223177684-78a9b037-4ea8-4fd2-ab2b-4871f28007c0.png)

The objective of this document is to make a log of things that I've changed/hacked in the binary of the windows minesweeper.
<br />
<br />
<br />

## Contents / Changes In Binary

1. Flags Already Set In Mines Places From Startup
2. Question Marks Already Set In Mines Places From Startup
3. Make Mine Counter Do Not Decrement When Added a Flag in Field

<br />

## Important Informations before modifying MineSweeper

THIS IS NOT A TUTORIAL: this is my log from the learning of the workshop Begin RE (where you can find a link in Study Resources)

The address where it stores the randomized data in memory (such as Mines or Empty Spaces) is at **Hex Dump: 0x01005360**\
From there you can check where is a mine or not.
<br />
<br />

### 1. Flags Already Set In Mines Places From Startup

Objective : In the beggining of the game, the places where the mines is hidden, change the sprite to a Flag

1. Open `Ollydbg` on your machine
2. Open `Minesweeper.exe` in `Ollydbg > File > Open`, or pressing F3
3. Minesweeper will start paused, to show the game and continue the code to running press Play button or F9
4. To generate flags in mine places, we need to change the CPU command at `0x010036FA` to be  
`XOR BYTE PTR DS:[EAX],81` , because currently it is adding the hexadecimal `80` to a `0F` field making it `8F` (bomb).  
To change it to `8E` (flag) we will need to change it to a `XOR 81` to `8F` resulting in `8E` (flag)
5. Go to address `0x010036FA`, press Space and change the command to `XOR BYTE PTR DS:[EAX],81`.
6. Press play to make the minesweeper.exe start running
7. The flags should be appearing in the place of the mines
<br />
<br />

### 2. Question Marks Already Set In Mines Places From Startup

Objective : In the beggining of the game, the places where the mines is hidden, change the sprite to a Question Mark

1. Open `Ollydbg` on your machine
2. Open `Minesweeper.exe` in `Ollydbg > File > Open`, or pressing F3
3. Minesweeper will start paused, to show the game and continue the code to running press Play button or F9
4. To generate Questions in mine places, we need to change the CPU command at `0x010036FA` to be  
`XOR BYTE PTR DS:[EAX],82` , because currently it is adding the hexadecimal `80` to a `0F` field making it `8F` (bomb).  
To change it to `8D` (Question) we will need to change it to a `XOR 82` to `8F` resulting in `8D` (Question)
5. Go to address `0x010036FA`, press Space and change the command to `XOR BYTE PTR DS:[EAX],82`.
6. Press play to make the minesweeper.exe start running
7. The question marks should be appearing in the place of the mines
<br />
<br />

### 3. Make Mine Counter Do Not Decrement When Added a Flag in Field


<br />
<br />

## Tools

IDA (Free) : https://www.hex-rays.com/ida-pro/ \
OllyDebugger : https://www.ollydbg.de/
<br />
<br />

## Study Resources

Reverse Engineering For Beginners : https://www.begin.re/
