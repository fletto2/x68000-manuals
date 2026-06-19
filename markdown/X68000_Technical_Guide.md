# X68000 Technical Guide

*English translation from the Japanese original*

"PERSONAL WORKSTATION
X68000

Technical Data Book

Supervised by Sharp Corporation TV Business Division
Edited by ASCII Publishing Technical Writing Section

ASCII Publishing"

*(Blank page in the original.)*

*(Blank page in the original.)*

*(Blank page in the original.)*

**PERSONAL WORKSTATION**
**X68000**
**Technical Data Book**

**Supervised by Sharp Corporation Television Business Division**
**Compiled by ASCII Publishing Department Tech Write Section**

**ASCII Publishing Department** 

"PERSONAL WORKSTATION ZX58000"

**Introduction**

This document is a data book that collects technical information mainly related to the hardware of the Sharp personal workstation X68000.

Since its release in 1986, the X68000 has attracted the attention of the media with its sophisticated specifications and unique features. In particular, by using the MPU 68000, the X68000 was able to directly manipulate 1M byte of main RAM, standardize the unique sprite function, bit-map mode with a resolution of 768 x 512 dots (with 65,536 colors in dot units), high-level graphic functions, FM sound source LSI, sound synthesis LSI, and various other features, making it an ideal machine for software development.

We hope that the hardware information in this document will be useful for both amateur enthusiasts and professional programmers in developing software for the X68000.

While we strive to ensure the accuracy of the content in this document, please let us know if there are any errors or concerns. If you intend to use this information, please conduct sufficient evaluations beforehand.

For any questions regarding the contents of this document, please send a postcard to Ascii Publishing’s editorial department. We can only respond to questions via mail.

Table of Contents

Chapter 1 Overview of the System  1
```
1 Features of the System  1
2 Specifications  3
3 Block Diagram  7
4 Memory Map  8
```

Chapter 2 Screen Control  9
1 Text Screen Configuration  11
```
  1-1 Display Screen Configuration  11
  1-2 Text VRAM Memory Map  11
  1-3 Text Screen Address Allocation  12
  1-4 Text Palette Address  13
```
2 Graphic Screen Configuration  14
```
  2-1 Display Screen Configuration  14
  2-2 Graphic VRAM Memory Map  14
  2-3 Graphic Screen Address Allocation  17
  2-4 Graphic Palette Address  21
```
3 Text Screen and Graphic Screen Control (CRTC)  23
```
  3-1 CRTC Connection and Internal Registers  24
  3-2 Details of the CRTC Registers  27
  3-3 CRTC Special Feature Details (Text)  33
  3-4 CRTC Special Feature Details (Graphic)  34
```
4 Sprite  35
```
  4-1 Features of Sprites  35
  4-2 Sprite Control Register Address Map  37
  4-3 Details of Sprite Control Registers  40
  4-4 Background Control Register and Screen Mode Register  42
```

Table of Contents

4-5   PCG Area ................................................................. 47
4-6   Details of Text Area (1) ................................................ 49
4-7   Details of Text Area (2) ................................................ 50
4-8   How to Access CPU ................................................... 51

5   Video Controller ........................................................ 55
5-1   Address Map of Video Controller Registers ................. 56
5-2   Details of Video Controller Registers ......................... 57
5-3   Special Mode Details ............................................... 65

6   CGROM ........................................................................ 74
6-1   CGROM Specifications .............................................. 74
6-2   Address Map of CGROM .......................................... 75
6-3   Configuration of CGROM Address ........................... 76

7   Superimpose & Overscan ........................................ 80

Chapter 3   Sound Functions ...................................... 83
1   FM Sound Source ........................................................ 84
1-1   Characteristics .......................................................... 84
1-2   Block Diagram of FM Sound Source ........................ 84
1-3   FM Sound Source Registers Configuration ............. 85
1-4   Address Map of FM Sound Source Registers .......... 86
1-5   Channels & Slots ...................................................... 87
1-6   Details of FM Sound Source Registers .................... 87
1-7   Method for Correcting the System Clock 
       at 4MHz ................................................................. 111

2   PSG Sound Source .................................................... 114
2-1   Characteristics ........................................................ 114
2-2   Address Map of PSG Sound Source Registers ........ 115
2-3   Details of PSG Sound Source Registers ................... 115
2-4   How to Access PSG Sound Source .......................... 117

Contents

Chapter 4: Peripheral LSI .......................................................... 119

1. DMA Controller (Direct Memory Access Controller) …… 119
```
    1-1 Features ........................................................................... 120
    1-2 DMAC Register Address Map ..................................... 121
    1-3 Details of DMAC Registers ........................................ 122
```
2. MFP (Multi Function Peripheral) .................................... 123
```
    2-1 Features ........................................................................... 124
    2-2 MFP Register Address Map ...................................... 125
    2-3 Details of MFP Registers ......................................... 130
```
3. SCC (Serial Communication Controller) .......................... 139
```
    3-1 Features ........................................................................... 139
    3-2 SCC Register Address Map ....................................... 141
    3-3 Details of SCC Registers .......................................... 141
```
4. RTC (Real Time Clock) ....................................................... 142
```
    4-1 Features ........................................................................... 142
    4-2 RTC Register Address Map ...................................... 144
    4-3 Details of RTC Registers ......................................... 146
```
5. FDC (Floppy Disk Controller) ......................................... 148
```
    5-1 Disk Drive Features and Specifications ................. 148
    5-2 Features of FDC .......................................................... 152
    5-3 FDC Register Address Map ...................................... 153
    5-4 Details of FDC Registers .......................................... 153
    5-5 FDC Access ..................................................................... 156
```

Chapter 5: Other Hardware .................................................... 159

1. Keyboard ................................................................................. 159
```
    1-1 Sub CPU ........................................................................... 160
    1-2 Keyboard Data Processing Procedure ....................... 168
```
2. Mouse ...................................................................................... 174
```
    2-1 Mouse Data Transmission Procedure ....................... 175
    2-2 Mouse Access .................................................................. 176
```

Page [4]

Contents

3 Joystick .................................................................................................... 179
3-1 Joystick Register Address Map ............................................. 179
3-2 Joystick Register Details ........................................................ 180
3-3 Joystick Access ....................................................................... 181

4 Printer .................................................................................................... 181
4-1 Printer Access .......................................................................... 182

5 Switch and Others ................................................................................ 183
5-1 Main Unit Switch ..................................................................... 183
5-2 Power Supply ........................................................................... 184
5-3 LED ............................................................................................ 185
5-4 8255 Ports ............................................................................... 186

Appendix .................................................................................................. 187
```
1 I/O Port Address List .................................................................... 187
2 Reset ............................................................................................. 191
3 System Port .................................................................................. 192
```
```
    3-1 System Port Register Address Map .............................. 192
    3-2 System Port Register Details ........................................ 192
```
4 Interrupts .................................................................................... 195
```
    4-1 68000 MPU Interrupts .................................................... 195
    4-2 MFP Interrupts and Reading Report ......................... 195
    4-3 Interrupt Vector Settings ............................................... 196
```
```
5 IPL (Initial Program Loader) .................................................. 197
6 Character Code Table ........................................................... 198
```

Index ....................................................................................................... 199

*(This page is too faint in the original to transcribe.)*

Chapter 1 System Overview

1. System Features

(1) Employs a 16/32-bit MPU 68000 (10 MHz) CPU.
- Direct addressing of an address space of 16 M bytes (8 M words) is possible.
- Memory-mapped I/O method (standard with 1 M byte of main memory).
- Utilizes the 63450 as the DMAC (DMA controller) and the 68901 as the MFP (multi-function peripheral).
- Uses multiple custom ICs.

(2) Utilizes a bit-mapped method for text VRAM and graphic VRAM.
- Supports an actual screen size of 1024 x 1024 dots (512 x 512 dots for the graphics screen).
- Display screen sizes of 768 x 512, 512 x 512, 512 x 256, 256 x 256 are selectable.
- Supports high resolution (31.5 kHz) and standard resolution (15.98 kHz) for screen display scanning.

(3) On the graphics screen, each dot can be assigned a desired color out of 65,536 colors (in 512 x 512 mode).
- In graphic 768 x 512 mode, each dot can be assigned one of 16 desired colors out of 65,536 colors.

(4) Smooth scrolling is possible on a dot-by-dot basis.

(5) Equipped with a proprietary sprite IC.
- 128 sprites of 16 x 16 dot patterns are possible (up to 256).
- Up to 32 sprites can be displayed simultaneously in a single line.
- Up to 128 sprites can be displayed simultaneously on one screen.

(6) Equipped with a palette function to change colors instantly.

(7) Equipped with a priority function that allows text, graphics, and sprites to be ordered by priority.

Chapter 1 System Overview

(8) Semi-transparent color specification and special priority are possible.

(9) Standard resolution, overscan, superimpose functions (with support for pseudo high resolution in interlace mode).

(10) Equipped with CGROM for ANK characters and JIS level 1 and level 2 standard kanji characters.

(11) FM sound source and sound synthesis function equipped.

(12) Equipped with various interfaces such as analog RGB I/F, hard disk I/F, RS-232C I/F, printer I/F, joystick I/F, mouse I/F, etc.

(13) Uses a keyboard with cylindrical step sculpture.

(14) Equipped with two 5" floppy disk drives (2HD). Also includes a mouse trackball.

2. Specifications

(Hardware)

| Item        | Classification | Name & Model     | Content                                                   | Remarks                      |
|-------------|----------------|------------------|-----------------------------------------------------------|-----------------------------|
| CPU         | MPU            | HD68HC000        | 16/32-bit MPU (10 MHz)                                     |                             |
|             | Sub CPU        | MSM80C51         | Keyboard scanning                                         |                             |
| DMAC        |                | HD63450          | 4-channel DMA controller                                   |                             |
|             |                |                  | Peripheral device-memory data transfer control            |                             |
| MFP         |                | MC68901          | Multifunction peripheral                                   |                             |
|             |                |                  | Keyboard data reception, various interrupt control, etc.   |                             |
| SCC         |                | Z8530            | Serial communication controller                            |                             |
|             |                |                  | Dual-channel serial (RS-232C, mouse)                       |                             |
| RTC         |                | RP5C15           | Real-time clock                                            |                             |
| FDC         |                | µPD72065         | Internal 5" 2HD floppy disk drive control                  |                             |
| CRTC        | Peripheral LSI |                 | Text, graphics control CRT controller                      |                             |
|             |                |                  | Dual port VRAM controller                                  | For Super-imposed images     |
|             |                |                  | Screen scroll function                                     | Internal CRTC              |
| Sprite LSI  | (custom IC)    |                  | Sprite function                                            |                             |
| Video Controller | (custom IC) |                | Palette prioritization function, special effects mode      |                             |
| FM Sound Source | (custom IC) | YM2151          | 8-channel FM sound source playback                         | 2 channels, 8 octaves       |
| Sound Synthesis | (custom IC) | MSM6258         | Adaptive Differential PCM                                  |                             |
| PPI         |                | µPD8255          | Joystick 2 ports                                           |                             |
|             |                |                  | Sound synthesis switching control                          |                             |
| I/O Control | (custom IC)    |                  | Floppy disk, hard disk                                     |                             |
| Others      | (custom IC)    |                  | Memory controller, system controller                       |                             |

Chapter 1: Overview of the System

Item     Category     Name/Type                  Contents                              Notes

ROM
```
        IPL ROM     256 K bytes (IPL, BIOS, dictionary)
        CG ROM     768 K bytes     
                    16x16**8 double pixels,  24x24**8 double pixels  ......  Full-width (JIS 1st and 2nd level)
                    8x16     12x24  ......  Half-width
                    8x8       12x12   ......  1/4 quarter-width
```

Memory
```
        Main Memory  1 M byte                Expandable to 12 M bytes

        Text VRAM   512 K bytes
        VRAM        Bitmap format (setting of left-to-right direction for data storage)
                    1024x1024 dots  4 planes                                           Dual port DRAM adopted

        Graphic         512 K bytes
        VRAM        Bitmap format (setting of left-to-right direction for data storage)
                    1024x1024 dots  4 planes
                    (512x512 dots  16 planes)                                           Dual port DRAM adopted

        Adapter VRAM   32 K bytes
        SRAM        16 K bytes
```

Disk
```
        Built-in mini FDD   5" double-sided high-density (2HD) 2 drives installed

        4-slot FDD for triple-side (option) external FD drive
        interfex
        Hard Disk drive interfex for optional hard disk drive

        Optional Hard Disk Drive   CZ-500H, CZ-501H
                                  (10MB)
```

Built-in I/O
and other ports

```
        Keyboard Connector   for dedicated keyboard

        CRT Interface       Analog RGB output
                                                                    15 pins

        Television Control Connector  for dedicated display    8 pin DIN

        RS-232C Interface     1 channel RS-232C

        Mouse Interface        For attached Mouse and Trackball 

        Printer Interface         Centronics Parallel Printer 

        Joystick Interface        Atari Standard Interface (2 ports)
        
        Audio Input/Output Connector   Line Output, Headphone Output

        Image Input Interface       Available for SCSI interface

        (Other connectors)  Remote control, S-Video, 3D glasses, etc.
```

Expansion I/O Slot   2 slots

Table 1-1 Hardware Specifications

**<Specifications>**

| Specification | Value |
|---|---|
| Rated Voltage | AC100 V |
| Rated Frequency | 50/60 Hz |
| Power Consumption | 44 W (10 W or less in standby mode) |

Table 1-2 Hardware Specifications

**<Functionality>**

| Item | Type  | Name/Type | Contents | Remarks |
|---|---|---|---|---|
| Display Size |   | Text Screen | 1024 x 1024 dots, 4 planes | Bitmap format |
|   |   | Graphic Screen | 1024 x 1024 dots, 4 planes <br>(512 x 512 dots, 16 planes) | Bitmap format |
|   | Text Screen |   | High resolution mode | 768 x 512 dots |
|   |   |   |   | 512 x 512 |
|   |   |   | Medium resolution mode 1 | 512 x 256 (2 pages) |
|   |   |   | Medium resolution mode 2 | 256 x 256 (4 pages) |
|   | Graphic Screen |   | High resolution mode | 768 x 512 dots <br>512 x 512 |
|   |   |   | Medium resolution mode 1 | 512 x 256 (2 pages) |
|   |   |   | Medium resolution mode 2 | 256 x 256 (4 pages) |
| Display Mode |   | Text Screen | 1024 x 1024 |
|   |   | Brightness | High Resolution: 31.5 kHz <br>Low Resolution: 15.98 kHz | high resolution mode: 1024x1024 dots <br> medium resolution mode: 512x512 dots <br> (bitmap format) |
|   |   | Color Depth | High resolution: 31.5 kHz <br>Low resolution: 15.98 kHz | Per dot: up to 65536 colors from a palette <br> 256 colors displayed |
| Graphics Screen |   |   | High resolution mode | 512 x 512 dots |
|   |   |   | Medium resolution mode 1 | 512 x 256 (2 pages) |
|   |   |   | Medium resolution mode 2 | 256 x 256 (4 pages) |
|   | Raster Mode |   | High resolution mode | 512 x 512 dots |
|   |   |   | Medium resolution mode 1 | 512 x 256 (2 pages) |
|   |   |   | Medium resolution mode 2 | 256 x 256 (4 pages) |

Chapter 1 System Overview

Styles

Pattern Definition

Size: 16x16 dot/pattern
Number of Patterns: 128 patterns (BG0.1 unused: maximum 256)
Colors: 1 pattern can use 16 colors out of 65536 colors (dot units)
Entire screen: 256 colors out of 65536 colors

Display
Resolution: 1024 x 1024 dots
Display Area: Horizontal 512 dots or 256 dots / Vertical 512 lines or 256 lines
Display Ability: 128 sprites / screen 32 sprites / line

Table 1-3 X68000 Capabilities

Category

Content

Smooth Scroll Function
Text screen has dot unit longitudinal scroll, graphics screen has dot unit lateral scroll

Special Screen Capabilities:
Graphic VRAM image input function, text raster copy function, higher bit text clear, text and bitmap mask function
Priority Function:
Text, graphic, and sprite can be designated in priority. 2 out of 4 screens are available in graphic extending over 512x512 dot mode, and you can designate any one priority among texts.
Palette Function: Possible to exchange any color to any other color freely
Semi-Transparent Display: Semi-transparent color display

Special Priority Function:

Function allowing heightened priority of a certain area of the graphics screen in the display area
Super Interpose Function:
Even in high mode super scan, super interpose is possible (supports interlace method and pseudo resolution mode)

Table 1-4 X68000 Functions

Page 6

Title:
3. Block Diagram

Note:
Figure 3.1 Block Diagram

Top left:
Chapter 1 System Overview

Heading:
4. Memory Map

Labels on the map:
SUPERVISOR AREA
USER AREA
Address pointer is in 8-byte units (2^32)
MAIN MEMORY (USER AREA)
GRAPHIC VRAM (16 color mode)
GRAPHIC VRAM (256 color mode)
(65536 color mode)
TEXT VRAM
SYSTEM I/O
MEMORY SW (RAM)
CG ROM (768 KB)
IPL ROM
I/O AREA (SUPERVISOR AREA)
SYSTEM I/O (SUPERVISOR AREA)
USER I/O (USER AREA)
MEMORY SW (RAM)
RAM ON BOARD
(empty)
(empty)
(empty)
CRTC
VIDEO
DMAC
AREA SET
MFP
KCC
PRINTER
SYS. PORT
FM SOUND
Voice synthesis
FD
HD
SCC
INT1
SPRITE REGISTER
SPRITE VRAM

Address column (right side):
E80000H
E82000H
E84000H
E86000H
E88000H
E8A000H
E8C000H
E8E000H
E90000H
E92000H
E94000H
E96000H
E98000H
E9A000H
E9C000H
E9E000H
EA0000H
EB0000H
EB8000H
EBFFFFH

Bottom right:
Figure 1-2 Memory Map

**Chapter 2**
**Screen Control**

The X68000 has three independent screens: text, graphic, and sprite. The text screen and graphics screen are controlled by the CRTC, and the sprite screen is controlled by the sprite controller. The priority functions for the three screens, semi-transparency, special priority functions, palette functions per screen, and screen display functions are controlled by the video controller.

However, regardless of whether you use the CRTC, sprite controller, or video controller, be sure to set up the screen when you access it.

Figure 2-1 Screen Control Block Diagram

1) Text Screen (Bitmap Method)
The text screen displays text such as alphanumeric characters (ANK: alphanumeric-KANA) and kanji. Similar to the graphical screen of the X1 and X1turbo series, the settings are done horizontally. Scrolling on the text screen is circular scrolling.
The display mode supports high resolution (horizontal sync frequency 31.5 kHz) and standard resolution (horizontal sync frequency 15.98 kHz).

Chapter 2 Screen Control

Figure 2-2 Text Screen

2) Graphic Screen
This is the screen for performing graphic processing such as drawing lines and circles and painting. The settings will be oriented in the depth direction.

The scroll on the graphics screen is a spherical surface scroll.

As a display screen mode, it supports high resolution (horizontal synchronization frequency 31.5 kHz) and standard resolution (horizontal synchronization frequency 15.98 kHz).

Figure 2-3 Graphic Screen

3) Sprite Screen
This is the screen for moving sprite patterns smoothly dot by dot, as used in Famicom or MSX.

As a display screen mode, it supports high resolution (horizontal synchronization frequency 31.5 kHz) and standard resolution (horizontal synchronization frequency 15.98 kHz).

Page 10

1. Composition of the Text Screen

1-1 Display Screen Structure

| Actual Screen (H×V) | Simultaneous Display Colors (Palette Colors) | Number of Simultaneous Display Screens (Overlapping Screens) | Display Screen (H×V) | Notes |
|----------------------|------------------------------|---------------------------------|-----------------------------|-------|
| 1024×1024            | 16 (65536)                   | 1                               | High-Resolution Mode       | 768×512 512×512 512×256 256×256 | | 2 Deglitching 2 Deglitching |
|                      |                              |                                 | Standard Resolution Mode (Over Scan) | 512×512 512×256 256×256 | | - Deglitching in over scan mode - Image size will be smaller due to deglitching interlace |

Table 2-1. Composition of Display Screen

1-2 Memory Map of VRAM for Text

MSB           16-bit          LSB

| E00000H     |               |       T0 Plane   |
| E1FFF0H     |               |                  |
| E20000H     |               |       T1 Plane   |
| E3FFF0H     |               |                  |
| E40000H     |               |       T2 Plane   |
| E5FFF0H     |               |                  |
| E60000H     |               |       T3 Plane   |
| E7FFF0H     |               |                  |

Figure 2-4. Memory Map of VRAM for Text

**Chapter 2: Screen Control**

1-3 Text Real Screen Address Layout

**16-Bit**

T3 Plane

T2 Plane

T1 Plane

T0 Plane

Text Palette Address for each Bit

**Figure 2-5** Text Real Screen Address Layout

1-4 Text Palette Address

[READ/WRITE Permissible]

| Palette Address | Register Address | D15-D11 | D10-D06 | D05-D01 | D00 | Notes      |
|-----------------|------------------|---------|---------|---------|-----|------------|
| 00H             | E82200H          | Green   | Red     | Blue    | I   |            |
| 01H             | E82202H          |         |         |         |     |            |
| 02H             | E82204H          |         |         |         |     |            |
| 03H             | E82206H          |         |         |         |     |            |
| 0CH             | E82218H          |         |         |         |     |            |
| 0DH             | E8221AH          |         |         |         |     |            |
| 0EH             | E8221CH          |         |         |         |     |            |
| 0FH             | E8221EH          |         |         |         |     |            |

Table 2-2 Text Palette Address

However, this palette address is intended to be used in conjunction with sprite color 0.

For example, suppose the text VRAM memory data is:

```
E00000H = "0000H"
E20000H = "0021H"
E40000H = "0022H"
E60000H = "0023H"
```

In this case, the palette address for the D01 bit (horizontal 14 dots, vertical 0 lines) would be 0EH. As per Table 2-2, that palette address is E8221CH, so the palette data output will be the content of E8221CH.

※ For the palette address 00H, please enter "0000H" as a rule.

Page 13

Chapter 2: Screen Control

2. Graphic Screen Composition

2-1 Composition of Display Screen

| Actual Screen (H x V) | Simultaneous Display Colors (Palette Colors) | Simultaneous Display Areas (Combined Areas) | Display Areas (H x V) | Remarks |
|-----------------------|----------------------------------------|------------------------------------------|---------------------|---------|
| 1024 x 1024           |                                        | 1                                        | High Resolution Mode  |
|                       | 16 (65536)                             |                                          | 768 x 512            | 2 x overlap |
|                       |                                        |                                          | 512 x 512            | 2 x overlap |
|                       |                                        |                                          | 512 x 256            | 2 x overlap |
|                       |                                        |                                          | 256 x 256            |           |
|                       |                                        |                                          | Horizontal High Resolution Mode (OverScan) |
|                       |                                        |                                          | 512 x 512            | * Ne/Sw  |
|                       |                                        |                                          | 512 x 256            | Ne/Sw   |
|                       |                                        |                                          | 256 x 256            | overlap |
| 512 x 512             | 16 (65536)                             | 4                                        | High Resolution Mode |
|                       |                                        |                                          | 512 x 512            |           |
|                       |                                        |                                          | 512 x 256            | 2 x overlap |
|                       |                                        |                                          | 256 x 256            | 2 x overlap |
| 256 x 256             |                                         | 2                                        | Horizontal High Resolution Mode (OverScan) |
|                       | (65536)                                |                                          | 512 x 512            | * Ne/Sw     |
|                       |                                        |                                          | 512 x 256            | Ne/Sw     |
|                       |                                        |                                          | 256 x 256            | overlap  |
|                       | 65536 (65536) | 1                      |                                          | 512 x 512            |         |
|                       |                                        |                                          | 512 x 256            |         |
|                       |                                        |                                          | 256 x 256            |         |

Table 2-3: Graphic Screen Composition

2-2 Graphic VRAM Memory Map

(1) Actual Screen 1024 x 1024, 16 colors, 1 face mode (* is invalid)

MSB                                   LSB
(Address)                             
D15    D14    D13    D12   D11    D10    D09    D08    D07    D06    D05    D04    D03    D02   D01    D00
C00000H                                                     G03    G02    G01    G00  (X0, Y0)
C00002H                                                     G03    G02    G01    G00  (X0, Y1)
       ...                                
DEFFFEH                                                    G03    G02    G01    G00  (X1023, Y1023)

Graphic Layout Map

Page 14

2. Graphic Screen Configuration

(2) Screen Area 512×512, 16 colors, 4 screen mode (* is invalid)

MSB                                                                                  LSB

(Genesis)

SC0
(Screen 0)

SC1
(Screen 1)

SC2
(Screen 2)

SC3
(Screen 3)

G03  G02  G01  G00

(X0, Y0) 

(X512, Y512) 

(X0, Y0) 

(X512, Y512) 

(X0, Y0) 

(X512, Y512) 

G03  G02  G01  G00

(X512, Y512) 

Graphic Address

Chapter 2 Screen Control

(3) Actual Screen 512×512, 256 Colors, 2 Screen Mode (* is invalid)
(Note: D represents a data bit)

MSB                                                              LSB
```
      +-----------+-----------+-----------+-----------+-----------+
      |    D15    |    D14    |    D13    |    D12    |    D11    |
      +-----------+-----------+-----------+-----------+-----------+
```
C0000H| .... * * * * * * * * | G07 G06 G05 G04 G03 G02 G01 G00| (X0,Y0)
      +-----------+-----------+-----------+-----------+-----------+
C7FFEH| .... * * * * * * * * | G07 G06 G05 G04 G03 G02 G01 G00| (X512, Y512)
      +-----------+-----------+-----------+-----------+-----------+
C8000H| .... * * * * * * * * | G07 G06 G05 G04 G03 G02 G01 G00| (X0,Y0)
      +-----------+-----------+-----------+-----------+-----------+
CFFFFEH|.... * * * * * * * * | G07 G06 G05 G04 G03 G02 G01 G00| (X512, Y512)
```
      +-----------+-----------+-----------+-----------+-----------+
       Graphic Palette Address
```

(4) Actual Screen 512×512, 65536 Colors, 1 Screen Mode
(Note: D represents a data bit)

MSB                                                              LSB
```
      +-----------+-----------+-----------+-----------+-----------+
      |    D15    |    D14    |    D13    |    D12    |    D11    |
      +-----------+-----------+-----------+-----------+-----------+
```
C00000H| G15 G14 G13 G12 G11 G10 G09 G08 G07 G06 G05 G04 G03 G02 G01 G00| (X0, Y0)
      +-----------+-----------+-----------+-----------+-----------+
C00002H| G15 G14 G13 G12 G11 G10 G09 G08 G07 G06 G05 G04 G03 G02 G01 G00| (X0, Y1)
      +-----------+-----------+-----------+-----------+-----------+
C7FFFEH|G15 G14 G13 G12 G11 G10 G09 G08 G07 G06 G05 G04 G03 G02 G01 G00| (X512, Y512)
```
      +-----------+-----------+-----------+-----------+-----------+
       Graphic Palette Address
```

The characters `* * * * * * * *` represent "wildcards" or placeholders for unspecified data bits.

2-3 Address Mapping of Graphics Display Screen

(1) 1024×1024 Dots (16 Color Mode)

(Top diagram indicates various memory addresses and planes for different dots in a 1024×1024 graphics representation.)

Figure 2-6 Address Mapping of Graphics Display Screen (1)

(Left to right description)
[Address] MSB
2M Bytes (1M Word)
C00000H 
C00002H 
...
DFFFFEH
  
(No care)
G03 G02 G01 G00

LSB [Coordinates on Screen]
(x0, y0)
(x1, y0)
(x1023, y0)
(x1023, y1023)

Table 2-4 Memory Map

Chapter 2 Screen Control

(2) 512 x 512 Dots (16 Colors, 4-Plane Mode)

Diagram labels:
G03 G02 G01 G00 of SC.3
G03 G02 G01 G00 of SC.2
G03 G02 G01 G00 of SC.1
G03 G02 G01 G00 of SC.0
MSB 3  2  1  0 LSB

SCREEN 0
SCREEN 1
SCREEN 2
SCREEN 3

C00000  C00002 ... (G00 page)
C00400  (G01 page)
C3F000
C40000 (G02 page)
C7FC00
C7FE00 (G03 page)
C7FFFE

D00000 (G00 page)
D00002 (G01 page)
D003FE (G02 page)
        (G03 page)
DFFFFE

```
512 dots
512 dots
```

+400H (=1024)

Page B0
Page B1
B2 ... B15

Figure 2-7 Graphics Actual Screen Address Configuration (2)

[Address] MSB 15~4   3  2  1  0 LSB
don't care
G03 G02 G01 G00

C00000H
        (512 bytes)
C7FFFEH       SC.0

C80000H
              SC.1
CFFFFEH

D00000H
        2W bytes (1W word)
D7FFFEH       SC.2

D80000H
              SC.3
DFFFFEH

Table 2-5 Memory Map

2. Graphic Screen Configuration

(3) 512×512 Dots (256 Colors, 2-Screen Mode)

Figure 2-8: Address Configuration of Graphic Virtual Screens (3)

Table 2-6: Memory Map

Chapter 2 Screen Control

(4) 512 x 512 Dots (65536 Colors, Single-Plane Mode)

Diagram labels:
G15 G14 G13 G12 G11 G10 G09 G08 G07 G06 G05 G04 G03 G02 G01 G00 of SC.1
MSB 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 LSB

SCREEN 0
C00000  C00002 ... (G00 page)
C3F000
C40000
C7FC00
C7FFFE
C00000 (G15 page)
(G14 page)
(G13 page)
(G12 page)
(G11 page)
(G10 page)
(G09 page)
(G08 page)
(G07 page)
(G06 page)
(G05 page)
(G04 page)
(G03 page)
(G02 page)
(G01 page)
+400H (=1024)
```
512 dots
512 dots
```
Page B0
B1 B2 ... B15

Figure 2-9 Graphics Actual Screen Address Configuration (4)

[Address] MSB 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0 LSB
G15 G14 G13 G12 G11 G10 G09 G08 G07 G06 G05 G04 G03 G02 G01 G00

C00000H
        512K bytes (256K words)
C7FFFEH

Table 2-7 Memory Map

**2-4 Graphic Palette Address**

(1) Graphic 16 Color, 256 Color Mode [READ/WRITE Available]

| Palette VRAM Data | Register Address | D15-D11 | D10-D06 | D05-D01 | D00 | Notes |
|------|------|------|------|------|------|------|
| 00H | E82000H | Green | Red | Blue | I | |
| 01H | E82002H | | | | | |
| 02H | E82004H | | | | | |
| 03H | E82006H | | | | | |
| 0CH | E82018H | | | | | |
| 0DH | E8201AH | | | | | |
| 0EH | E8201CH | | | | | |
| 0FH | E8201EH | | | | | |
| 10H | E82020H | | | | | |
| 11H | E82022H | | | | | |
| 12H | E82024H | | | | | |
| FDH | E821FAH | | | | | |
| FEH | E821FCH | | | | | |
| FFH | E821FEH | | | | | |

Table 2-8 Graphic Palette Address (1)

- In the case of the graphic 256 color 2-layer mode, if the memory data of the graphic VRAM is 11H, the corresponding palette register address will be E82022H as per Table 2-8. Thus, the output palette data will be the content of E82022H. Also, the same applies to the 16 color mode, but only the number of palette addresses differs.
- As a rule, please input "0000H" for the data of the palette address 00H.

Page 21

Chapter 2   Screen Control

(2) Graphics 65536 Color Mode (READ/WRITE Possible)

| Palette (VA) Graphics VR AM Mode ↓ Lower Byte | Register Address | D15-D14 | D13-D09 | D08 | D07-D06 | D05-D01 | D00 | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 00H | 01H | E82000H | Red Lower | Blue Lower | 8-bit | Red Lower | Blue Lower | 8-bit | 65536 color mode palette D15-D08 in 8 bits, D07-D00 in 8 bits are selected and output as lower 8 bits. |
| 02H | 03H | E82004H | --- | --- | --- | --- | --- | --- |
| 04H | 05H | E82008H | --- | --- | --- | --- | --- | --- |
| FCH | FDH | E821F8H | --- | --- | --- | --- | --- | --- |
| FEH | FFH | E821FCH | --- | --- | --- | --- | --- | --- |

Table 2-9  Graphic Palette Address (2)

※ For the data of each palette register address, please enter the palette address value as the original. In particular, the palette structure in graphic 65536 color 1 surface mode is as shown in Table 2-9. Simply changing the upper and lower bytes will correspondingly change the 256 color palette. When setting preliminary data, please note that it is different from 16-color and 256-color mode.

※In graphics 65536 color 1-surface mode, if the graphics VRAM memory data is, for example, 0101H, the palette register address at that time will be E82002H and E82000H as in Table 2-9, and the output palette data will be E82002H for D07-D00 and E82000H for D07-D00 combined. In other words, if E82000H is 3521H, and E82002H is 4CFFH, the palette output data will be FF21H.

3. Control of Text and Graphics Screens (CRTC)

The CRTC of the X68000 is a custom CRTC that supports dual-port DRAM (MB81461) used in text and graphics VRAM. This CRTC has 23 internal registers and provides the following screen control features:

1. Generation of horizontal and vertical synchronization signals
2. Generation of display size and display timing signals
3. Scrolling of text and graphics screens
4. Image capture function to graphics VRAM
5. Cluster copy and bit mask functions for text VRAM
6. Text single/double and simultaneous two-page access switch function
7. High-speed clear function for graphics VRAM
8. External synchronization horizontal position adjustment function (when superimposing)

The CPU can always access the data in VRAM, but for setting scrolling registers and the like inside the CRTC, perform it during the blanking period of the V-DISP signal (when "0" on MFP or GPIP4 port). Also, the SAM (Serial Access Memory) in dual-port DRAM is controlled by the CRTC during horizontal blanking.

Chapter 2 Screen Control

3-1 Specifications and Internal Registers of CRTC

| Display Mode | High Resolution | High Density |
| - | - | - |
| Display Method | Non-Interlace | Non-Interlace, Interlace |
| Sync Frequency | Horizontal (kHz) | 31.5 | 15.98 |
| | Vertical (Hz) | 55.46 | 61.46 |
| Data Display Period (1) | Horizontal (usec) | 22.09 | 52.69 |
| | Vertical (msec) | 16.25 | 15.019 |
| Sync Period (2) | Horizontal (usec) | 31.75 | 62.58 |
| | Vertical (msec) | 18.03 | 16.270 |
| Sync Width (3) | Horizontal (usec) | 3.45 | 3.30 |
| | Vertical (msec) | 0.191 | 0.187 |
| Back Porch (4) | Horizontal (usec) | 4.14 | 4.94 |
| | Vertical (msec) | 1.111 | 0.876 |
| Front Porch (5) | Horizontal (usec) | 2.07 | 1.65 |
| | Vertical (msec) | 0.476 | 0.187 |

Image Signal

Sync Signal

Image Signal Analog 0.7 Vp-p (75 ohms termination) Positive Polarity
Sync Signal TTL Level Negative Polarity

Table 2-10 CRTC Specifications

(Note: Some formatting elements such as tables may not perfectly align here.)

2. Control of the Text Screen and Graphics Screen (CRTC) — p.25

Table: CRTC register map. The dots (•) in the original mark which bits of the 16-bit word are valid for each register.

| Reg | Address  | Field                                          | Remarks |
|-----|----------|------------------------------------------------|---------|
| R00 | E80000H  | Horizontal total                               | Horizontal sync signal section, in 8-dot units (note: the LSB of R00 is invalid) |
| R01 | E80002H  | Horizontal sync end position                   | " |
| R02 | E80004H  | Horizontal display start position              | " |
| R03 | E80006H  | Horizontal display end position                | " |
| R04 | E80008H  | Vertical total                                 | Vertical sync signal section, in raster units |
| R05 | E8000AH  | Vertical sync end position                     | " |
| R06 | E8000CH  | Vertical display start position                | " |
| R07 | E8000EH  | Vertical display end position                  | " |
| R08 | E80010H  | External-sync horizontal adjust                | Horizontal position fine adjustment |
| R09 | E80012H  | Raster interrupt position                      | Raster address |
| R10 | E80014H  | X-direction scroll                             | Text scroll register |
| R11 | E80016H  | Y-direction scroll                             | " |
| R12 | E80018H  | Screen 0  X                                    | Graphics scroll register |
| R13 | E8001AH  | Screen 0  Y                                    | " |
| R14 | E8001CH  | Screen 1  X                                    | " |
| R15 | E8001EH  | Screen 1  Y                                    | " |
| R16 | E80020H  | Screen 2  X                                    | " |
| R17 | E80022H  | Screen 2  Y                                    | " |
| R18 | E80024H  | Screen 3  X                                    | Graphics scroll register |
| R19 | E80026H  | Screen 3  Y                                    | " |
| R20 | E80028H  | Memory-mode set / Display-mode set             | Control register |
| R21 | E8002AH  | Text-access set / Clear-P.S                     | " |
| R22 | E8002CH  | Source raster / Destination raster             | Raster address |
| R23 | E8002EH  | Bit-mask register                              | Mask data |
| —   | E80480H  | (operation port)                               | CRTC operation port |

Chapter 2 Screen Control

DISPTMG
SYNC
Synchronization position
Display start position
Display end position
Total

- R20, R21, E80480H are READ/WRITE enabled; when writing is effective, reading returns to 0.
- R00-R19, R22, R23 are WRITE only; reading is invalid.
- The setting value of R00-R07 must include a margin of 1 for calculation.

Table 2-11 CRTC Register Address Map

| Reg. No | High Resolution (768x512, 512x512, 512x256, 256x256) | Standard Resolution (512x512, 512x256, 256x256) |
|:-------:|---------------------------------------------------------|-----------------------------------------|
| R00 E800001H | 89H (137), 5BH (91), 5BH (91), 2DH (45), 4BH (75), 4BH (75), 25H (37) |
| R01 E800002H | 0EH (14), 09H (9), 09H (9), 04H (4), 03H (3), 03H (3), 01H (1) |
| R02 E800004H | 1CH (28), 11H (17), 11H (17), 06H (6), 05H (5), 05H (5), 00H (0) |
| R03 E800006H | 7CH (124), 51H (81), 51H (81), 26H (38), 45H (69), 45H (69), 20H (32) |
| R04 E800008H | 237H (567), 237H (567), 237H (567), 237H (567), 103H (259), 103H (259), 103H (259) |
| R05 E80000AH | 005H (5), 005H (5), 005H (5), 005H (5), 002H (2), 002H (2), 002H (2) |
| R06 E80000CH | 028H (40), 028H (40), 028H (40), 028H (40), 010H (16), 010H (16), 010H (16) |
| R07 E80000EH | 228H (552), 228H (552), 228H (552), 228H (552), 100H (256), 100H (256), 100H (256) |
| R08 E800010H | 18H (27), 18H (27), 18H (27), 18H (27), 2CH (44), 2CH (44), 24H (36) |

Table 2-12 Changing CRTC Register Values for Each Screen Mode:
When capturing screen images, change the value of R08 (E80010H) as follows: 
- 512x512 Mode, 512x256 Mode: ...... 9A (154)
- 256x256 Mode: ...... EB (235)

Page 26

3. Text Screen and Graphic Screen Control (CRTC)

3-2 CRTC Register Details

(1) For R00-R07, please refer to Table 2-12.

(2) R08 (Horizontal Position Adjustment)
Adjust the horizontal displacement between the TV or video screen and the computer screen in superimpose mode on the TV or video.
Adjust the delay time of the TV and video signal horizontal synchronization signal and the computer-side horizontal synchronization signal standing up.

The adjustment range is 25.7 nsec per unit, and can be set within the range of 0~6.5535 µs (R08=0~255).

(3) R09 (Raster Address)
Set the raster address to initiate an interrupt caused by the CRTC or IRQ signal (interrupt on channel 14 of the MFP).
If you do not use this interrupt, mask it with the MFP or GPIO port interrupt.

(4) R10~R11 (Text Scroll Register)
Set the display start address for scrolling the text screen (circular scroll).

The setting range of R10 depends on the display mode:
- When in Horizontal 768 dot display mode, 0~255
- When in Horizontal 512 dot display mode, 0~511
- When in Horizontal 256 dot display mode, 0~767

The setting range of R11 is 0~1023.

(5) R12~R19 (Graphic Scroll Register)
Set the display start address for scrolling the graphics screen (circular scroll).

The setting range for R12~R13 is 0~1023.
The setting range for R14~R19 is 0~511 as these registers are only used in 512×512 dot display mode.

Chapter 2: Screen Control

(6) R20-R21 (Control Registers)
- R20 (Upper Byte)

D15 D14 D13 D12 D11 D10 D09 D08
*   *   *   *   0   0   0   0

```
0 0: Graphics 16 colors 4 screens mode
0 1: Graphics 256 colors 2 screens mode
1 0: (unused)
1 1: Graphics 65536 colors 1 screen mode
0 0: Graphics real screen 512-dot mode
1 1: Graphics pseudo screen 1024-dot mode
```

(When setting, please make sure D08="0", D09="0")

- R20 (Lower Byte)

D07 D06 D05 D04 D03 D02 D01 D00 
*   *   *   *   *   *   *   *

```
0 0 0 0: Standard resolution (15.98 kHz) 256 x 256
0 0 0 1: Standard resolution (15.98 kHz) 512 x 256 (Interlace)
0 0 1 0: Standard resolution (15.98 kHz) 512 x 512 (Raster scroll 2 screens)
0 0 1 1: High resolution (31.5 kHz) 256 x 256
1 0 0 0: High resolution (31.5 kHz) 256 x 512 (Raster scroll 2 screens)
1 0 0 1: High resolution (31.5 kHz) 512 x 256
1 0 1 0: High resolution (31.5 kHz) 512 x 512
1 0 1 1: High resolution (31.5 kHz) 768 x 512
```

- R21 (Upper Byte)

D15 D14 D13 D12 D11 D10 D09 D08 
*   *   *   *   0   0   0   0

0: Text memory CPU single access (R21 D04-D07 is invalid)
1: Text memory CPU dual access
0: Text CPU access bit mask OFF
1: Text CPU access bit mask ON

Page 28

3. Control of Text Screen and Graphics Screen (CRTC)

*R21 (Lower Byte)

| D07 D06 D05 D04 |
|-----------------|
| (R21 D08 is valid at 1) |

0: Text T0 Plane Simultaneous Access OFF   
1: Text T0 Plane Simultaneous Access ON    
0: Text T1 Plane Simultaneous Access OFF    
1: Text T1 Plane Simultaneous Access ON    
0: Text T2 Plane Simultaneous Access OFF    
1: Text T2 Plane Simultaneous Access ON    
0: Text T3 Plane Simultaneous Access OFF    
1: Text T3 Plane Simultaneous Access ON    

* D00-D03 have two uses: selecting simultaneous access planes for text raster copy, and high-speed clearing of graphics screen (1024 x 1024).

<Plane Selection for Simultaneous Access of Text Raster Copy>

| D03 D02 D01 D00 |
|-----------------|
0: Text T0 Plane/ Raster Copy Simultaneous Access OFF    
1: Text T0 Plane/ Raster Copy Simultaneous Access ON    
0: Text T1 Plane/ Raster Copy Simultaneous Access OFF    
1: Text T1 Plane/ Raster Copy Simultaneous Access ON    
0: Text T2 Plane/ Raster Copy Simultaneous Access OFF    
1: Text T2 Plane/ Raster Copy Simultaneous Access ON    
0: Text T3 Plane/ Raster Copy Simultaneous Access OFF    
1: Text T3 Plane/ Raster Copy Simultaneous Access ON    

1024 (Diagram with text T3 plane corresponding to D03 from E60000H-E7FFFEH and text T2 plane corresponding to D02 from E40000H-E5FFFEH, text T1 plane corresponding to D01 from E20000H-E3FFFEH, and text T0 plane corresponding to D00 from E00000H-E1FFFEH)

1024 - Text planes T0, T1, T2, and T3 representation

This covers the main text content on the page.

Chapter 2: Screen Control

<When Rapidly Clearing a Graphics Real Screen 1024×1024 (Valid When R20 and D10 are 1)>

- R21 (Lower 4 bits)
  
```
  +----+----+----+----+
  | D03 | D02 | D01 | D00 |
  +----+----+----+----+

  (D03−D00 are invalid)
```

- Horizontal 768 or 512 dot mode
  
```
  +-------+-------+
  | Display Range |
  |    512×512    |
  +-------+-------+

  Width: 1024

  Execute Rapid Clear

  The range to be cleared rapidly will be the vertical range from 0 to 1023 dots in the horizontal direction within the display range.
```
  
- Horizontal 256 dot mode
  
```
  +-------+-------+
  | Display Range |
  |    256×256    |
  +-------+-------+

  Width: 1024

  Execute Rapid Clear

  The range to be cleared rapidly will be the vertical range from the horizontal range and the horizontal range within the display range.
```

<When Rapidly Clearing a Graphics Real Screen 512×512 (Valid When R20 and D10 are 0)>

```
  +-------+-------+-------+-------+
  |                 Display Range                |
  |             512×512, Different Depth Screens          |
  +-------+-------+-------+-------+

   Screen 3 (16 colors, corresponds to D03)
   Screen 2 (256 colors, corresponds to D02)
   Screen 1 (65536 colors, corresponds to D01)
   Screen 0 (D00 corresponds)
```
Width: 512

3. Text Screen and Graphics Screen Control (CRTC)

- Graphics 16 Color 4 Screen Mode (Valid when D10 of R20 is 0, D09 is 0, and D08 is 0)

D03  D02 D01 D00
```
 0 : Graphics Screen 0 Display Area Clear OFF
 1 : Graphics Screen 0 Display Area Clear ON
 0 : Graphics Screen 1 Display Area Clear OFF
 1 : Graphics Screen 1 Display Area Clear ON
 0 : Graphics Screen 2 Display Area Clear OFF
 1 : Graphics Screen 2 Display Area Clear ON
 0 : Graphics Screen 3 Display Area Clear OFF
 1 : Graphics Screen 3 Display Area Clear ON
```
- Graphics 256 Color 2 Screen Mode (Valid when D10 of R20 is 0, D09 is 0, and D08 is 1)

D03  D02 D01 D00
```
 0 : Graphics Screen 0 Display Area Clear OFF
 1 : Graphics Screen 0 Display Area Clear ON
 0 : Graphics Screen 1 Display Area Clear OFF
 1 : Graphics Screen 1 Display Area Clear ON
```
- Graphics 65536 Color 1 Screen Mode (Valid when D10 of R20 is 0, D09 is 1, and D08 is 1)

D03  D02 D01 D00
```
 0 : Graphics Screen 0 Display Area Clear OFF
 1 : Graphics Screen 0 Display Area Clear ON
```
Additionally, in 256 color 2 screen mode and 65536 color 1 screen mode, if data other than the above is set, the corresponding bit screen display area will be high-speed cleared.

Chapter 2 Screen Control

(7) CRTC Operation Mode Setting Port (E80480H)
The CRTC operates various functions through dual port DRAM or SAM (Serial Access Memory). Each function has a different meaning depending on the read or write operation.

- Write Operation

D7 D6 D5 D4 D3 D2 D1 D0
*   *   *   *   *   *   0

0: Graphic write to RAM stop (normal display)
1: Execute graphic write to RAM
1: Execute graphic clear to RAM
0: Text raster copy stop
1: Execute text raster copy

- Read Operation

D7 D6 D5 D4 D3 D2 D1 D0
*   *   *   *   *   *   0

1: Graphic write to RAM in progress
0: Execute graphic clear to RAM
(When D0, D1 are both 0, the graphic is in normal display)
1: Text raster copy in progress

* Note on CRTC screen mode change:
When setting the CRTC registers, pay attention to the setting order.

(1) When switching from high display mode to low display mode:
R20 (E80028H) ..... Set display mode
R01   (E80002H)
R07   (E8000EH) .... H, V registers, etc.

(2) When switching from low display mode to high display mode:
R00 (E80000H)
R07 (E8000EH)
R20 (E80028H)

Screen mode size restrictions:
```
768 x 512 (high) > 512 x 512 (high) or 256
512 x 512 (high) > 256 x 256 (high)
256 x 256 (low)
```

Also, comparison with the current display mode and the next display mode is performed by bits 0, 1, 4 of R20.

3-3 Detailed CRTC Special Functions (Text)

The text screen has the following functions.

(1) Scroll
Scrolls the text display screen. Specifically, the X and Y coordinates of the top left of the display screen are set in single units through R10 (EB0014H) and R11 (EB0016H), and scrolling is performed up to that point.

(2) Simultaneous/Singular Access
In the right mode, it is a feature that allows switching between simultaneous access and singular access to each plane VRAM of the text. (Single access only in the rear mode.) Specifically, by setting simultaneous/singular access for text VRAM in R21 (EB002AH) D08 to 0D07-04, the target plane for simultaneous access is set. Note that for simultaneous access, if the specified plane does not exist, it will be accessed simultaneously, so be careful.

(3) Raster Copy
Any raster (because of 4 raster units, the start address is 0-255) will be completely copied to another raster position (horizontal direction of 4 raster units, total 1024 dots). Specifically, by setting plane and start address D03-D00 in R21 (EB002AH) for executing raster copy, D15-D08 of R22 (EB002CH), the destination copy will be executed in raster. If all of D03-D00 in R21 (EB002AH) are not set to "0", raster copy will not be performed. 
Also, for this raster copy, when raster copy execution occurs, data transfer is performed synchronously with the horizontal sync period.

(4) Bit Mask
In the text VRAM data access of X68000, processing is performed in 16-bit units in the horizontal direction, but it is possible to mask the lowest 16-bit pitch out of those for efficient operation. Specifically, the bit mask can be set by writing "1" into the mask bits, using R21 (EB002AH) D09 for R23 (EB002EH) of D15-D00.

Use simultaneous access or raster copy for high-speed clear of the text screen. However, be aware that if raster copy is used, it must be valuable on the execution screen rather than the display screen.

Page 33

Chapter 2 Screen Control

3-4 CRTC Special Feature Details (Graphics)

The graphics screen offers the following features:

(1) Scroll
It scrolls the graphics display screen. Specifically, in the case of an actual screen of 1024×1024, scrolling is performed by setting dot units in the X and Y coordinates of each display screen to registers (R12(E8001AH) to R13(E8001AH)). In the case of a 512×512 actual screen, scrolling is performed by setting data to registers (R12 to R19) corresponding to each screen according to the screen mode.

(2) High-speed Clear
It is a function that clears the contents of the graphics VRAM at high speed. Specifically, a graphics plane for high-speed clearing is selected by D03 to D00 of R21(E8002AH), and the graphics VRAM is cleared using D01 of E80480H. Additionally, this high-speed clear completes one horizontal period by switching the VDIP signal to the rising edge of the D00 bit of E80480H, and the CRTC writes "0" to each data within the memory SAM (1 raster unit per horizontal period). In the case of interlace, it finishes after 2 vertical periods.

(3) Image Input
By connecting the optional "Digitizer Swap" and using D00 of E80480H, it is a feature to input video image data converted via A/D to graphics VRAM. Also, the E80480H D00 bit by the rising edge of the VDIP signal latches, and the CRTC writes the video image data from the memory SAM within the input image period into one surface of the graphics VRAM. In the case of interlace, it completes after 2 vertical periods. However, this image input will not stop without writing "0" to D00 of E80480H.

4. Sprite

# 4-1 Characteristics of the sprite

The X68000 has its own sprite screen, independent from text screens and graphics screens, controlled by a custom sprite IC.

With this sprite function, you can smoothly move any sprite pattern dot by dot. Furthermore, by utilizing the sprite priority (priority order) relative to the text or graphics screens, you can construct a varied screen.

The specifications and address map of this sprite IC are shown below.

**Item Details Notes**

**Sprite Pattern Specifications**
- Size 16 x 16 dot pattern
- Regular 128 patterns (up to 256 patterns if not displaying background)
- Colors 1 pattern has 16 - 65536 (in dot unit)
- Screen maximum 256 colors - 65536 colors

**Sprite Display**
- Maximum sprite count 1024 x 1024 dots
- Vertical: 512 dots per screen up to 256 dots
- Horizontal: 512 lines per screen up to 256 lines
- Display limit 128 lines per display
- Individual lines/screen

**Other Functions**
- Horizontal flip
- Vertical flip
- Priority with BG (Background)
Priority (this function can be set for each sprite)
- Display priority (BG0 > BG1)
- (SP0 > SPn > SP127)

The above text is a detailed breakdown of the capabilities and functions of the sprite feature in the X68000, detailing pattern sizes, display counts, color limits, and other notable features such as flipping and priority settings.

**Chapter 2 Screen Control**

EB0000H - 16 bit
EB0002H - Sprite scroll register
EB0400H - Reserved
EB0800H - BG scroll X register
EB0802H - Screen scroll Y register
EB0812H - Reserved

**Register Address**
EB8000H - PCG area
EBFCFEH

**PCG Area**

The PCG area's text area is generally divided into 16K word segments, as shown above, into 2 parts. However, the use of BG allows the following arrangement.

Example 1
EB8000H - PCG area
EBC000H - Text area 0

Example 2
EB8000H - PCG area
EBC000H - Text area 0
EBE000H - Text area 1

Example 3
EB8000H - PCG area

1. Both text areas 0 and 1 can be used for background 1, allowing it to be displayed on two screens. If only text area 0 is used, background 1 can be specified in the scroll register as "Text SEL".

2. If background 1 is only displayed on one screen, only 1 text area is necessary. The remaining text area can be used as the PCG area.

3. If background 1 is not displayed, the entire 16K words can be used as the PCG area. This results in 256 possible sprite patterns.

Figure 2-10. Sprite register address map

Page 36

4-2 Sprite Register Address Map

[Sprite, Background, and Scroll Registers] (note: Can be expanded) (All registers can be READ/WRITE)

| Name   | Width Bit        | D15 D14 D13 D12 D11 D10 D09 D08 D07 D06 D05 D04 D03 D02 D01 D00 | Notes                                          |
|--------|------------------|-------------------------------------------------------------|--------------------------------------------------|
|        |                  |                                                               | A set of four registers is allocated for each sprite.     |
|        | EB0000           | O O O O O O O O O O O O O O X | X-coordinate                   |
|        | EB0002           | O O O O O O O O O O O Y | Y-coordinate                      |
| SP 0   | EB0004           | O O O O COLOR (SP) SP CODE |                                  |
|       | EB0006           | VR HR DISP O O O O O O PRW  |                                   |
|        |                  |                                                               | VR: Vertical Flip (Sprite)                    |
|        |                  |                                                               | HR: Horizontal Flip (Sprite)                   |
|        | EB03F8           | O O O O O O O O O O O O O O X | X-coordinate                   |
| SP 127 | EB03FA           | O O O O O O O O O O O Y | Y-coordinate                      |
|        | EB03FC           | O O O O COLOR (SP) SP CODE |                               |
|        | EB03FE           | VR HR DISP O O O O O O PRW |                                   |

|        | BGD              |                                                               |                                              |
|        | EB0800           | O O O O O O O O X | X-coordinate                       |
|        | EB0802           | O O O O O O O Y | Y-coordinate                        |
| BGI    | EB0804           | O O O O O O O O X | X-coordinate                       |
|        | EB0806           | O O O O O O O Y | Y-coordinate                        |

| BGI    | EB0808           | O DISP O O O O BGi BG                                          |
| BGZ    |                  |                                                                              |
| Total  | EB080A           | O O O O O O O O H total | Horizontal Total                       |
|        | EB080C           | O O O O O O O O H disp | Horizontal Display Start Position       |
|        | EB080E           | O O O O O O O O V disp | Vertical Display Start Position         |
|        | EB0810           | O O O O O O O O L/H freq  |                                               |
| Total  |                  | V Res. H Res.                                                   | Resolution                                      |

Table 2-14 Sprite Register Address Map (1)

Chapter 2 Screen Control

[PCG Area] (All registers READ/WRITE possible)

| Name     | Address | D 15 | D 14 | D 13 | D 12 | D 11 | D 10 | D 09 | D 08 | D 07 | D 06 | D 05 | D 04 | D 03 | D 02 | D 01 | D 00 | Remarks                        |
|----------|---------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|-------------------------------|
| EB8000   |         | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    |                               |
| EB8007   |         |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |                               |
| EB8001   |         | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    |                               |
| EB801E   |         |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |                               |
| EB8020   |         | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    |                               |
| EB803E   |         |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |                               |
| EB8040   |         | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    |                               |
| EB805E   |         |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |                               |
| EB8060   |         | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    |                               |
| EB807E   |         |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |                               |
| EB8080   |         | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    |                               |
| EB80FE   |         |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |                               |
| EB8100   |         | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    |                               |
| EB817F   |         |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |                               |
| EBBF80   |         | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    | I    | G    | R    | B    |                               |
| EBBFFE   |         |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |                               |

Remarks:

- SP code sizes configuration to PCG allocation:
```
   0 2
   1 3
  16 Bit mode.
```

- Horizontal 512 dot mode.
  SP code size configuration (0123) = BG code size = 16x16 dot.

- Horizontal 256 dot mode.
```
  SP code size configuration (0123) = 16x16 dot.
  BG code size:
   - Upper (0) OR
   - Lower (1) OR
   - Upper (2) OR
   - Lower (3)
   = 8x8 dot.
```

For details, please refer to the main text (4-5 PCG area).

Note: The maximum values of the sprite code and background code are determined by the size of the PCG area.
1. For text area EBC000H to EBBFFE H (8K words), the code is 0 to 127
2. For text area EBC000H to EBBFFE H (4K words), the code is 0 to 191
3. If the background is not displayed, the sprite code is 0 to 255

[Text Area] (All registers READ/WRITE permitted)

| Name     | VR   | HR   | O   | O   | COLOR (BG)       | BG Code  | Remarks
|----------|------|------|-----|-----|------------------|----------|------------------------------------------------
| ECB000   |      | VR   | HR  | O   | COLOR (BG)       | BG Code  | Remarks
| EBC002   |      |      |     |     |                  |          | VR: Inverse (Background)
| EBBFFC   |      |      |     | O   | COLOR (BG)       | BG Code  | HR: Inverse (Background)
| EBBFFE   |      | VR   | HR  | O   | COLOR (BG)       | BG Code  | 
| EBB002   |      |      |     |     |                  |          |
| EBBFFC   |      |      |     | O   | COLOR (BG)       | BG Code  |
| EBBFFE   |      | VR   | HR  | O   | COLOR (BG)       | BG Code  |

Table 2-16 Sprite Register Address Map (3)

Chapter 2: Screen Control

4-3 Details of Sprite Scroll Registers

(1) X Coordinate (SP), Y Coordinate (SP)
Set the display position of the sprite in the sprite temporary coordinates.

X Coordinate (SP) ............ 0 - 1023
Y Coordinate (SP) ............ 0 - 1023

Below is an example showing the relationship between the display screen and the sprite temporary coordinates.

Example:
Display Screen Mode | Display Screen Range
```
512 dots × 512 lines: (16, 16) ~ (527, 527)
256 dots × 256 lines: (16, 16) ~ (271, 271)
```

._________________ X Coordinate
|
|
| Y Coordinate
|
|
|
|
|
|
|
|
|
|
|
| Display Screen

Sprite Temporary Coordinates System

Figure 2-11: Display screen and sprite temporary coordinates

4. Sprite

(2) PRV (Priority) Set the display priority order between sprite and background (2 planes).

| D01 | D00 | Display Priority Order |
|:----|:----:|:----------------------:|
|   0  |  0   |  Don't display sprite  |
|   0  |  1   |  BGO > BG1 > SP        |
|   1  |  0   |  BGO > SP > BG1        |
|   1  |  1   |  SP > BGO > BG1        |

**Figure 2-17** Display Priority Order

When the color data B, R, G, I in the PCG area is 0000H, it is considered transparent and the lower priority plane is displayed.

(3) For details on SP Code, COLOR (SP), H inversion (SP), and V inversion (SP), please refer to "4-6 Texture Area (1)" in this chapter.

Chapter 2 Screen Control

4-4 Background Scroll Registers and Screen Mode Registers

(1) X Coordinate (BG) and Y Coordinate (BG)
Sets the display starting position of the background surface in the text coordinate system.

• X Coordinate (BG) ...... 0~511 or 0~1023 (When BGO, it's EB0800H, when BG1, it's EB0804H)

```
      EB0800H  0 0 0 0 0 0 0 0  <--- Background Surface 0 X Coordinate ---> 
                                  D15 D14 D13 D12 D11  D10 D09 D08 D07 D06 D05 D04 D03 D02 D01 D00

      EB0804H  0 0 0 0 0 0 0 0  <--- Background Surface 1 X Coordinate ---> 
```

• Y Coordinate (BG) ...... 0~511 or 0~1023 (When BGO, it's EB0802H, when BG1, it's EB0806H)

```
      EB0802H  0 0 0 0 0 0 0 0  <--- Background Surface 0 Y Coordinate ---> 
                                  D15 D14 D13 D12 D11  D10 D09 D08 D07 D06 D05 D04 D03 D02 D01 D00

      EB0806H  0 0 0 0 0 0 0 0  <--- Background Surface 1 Y Coordinate ---> 
```

The size of the text coordinate system changes depending on the value set in the "H Res." bit (D01, D00 of EB0810H) in the screen mode registers.

4. Sprite

[Top left]
H Res.=00
(256 Dot Mode)

[Top box]
X Coordinate
Y Coordinate
BG Display Screen

[Middle box]
Text Area

[Bottom left]
H Res.=01
(512 Dot Mode)

[Bottom box]
Background 0 Display Screen

Figure 2-12 Text Area Dimensions

In 512-dot display mode, only the background 0 face is displayed, and the settings for the background 1 face are ignored.

Chapter 2 Screen Control

(2) DISP/CPU (EB0808H on D09)

Bits | D15 D14 D13 D12 D11 D10 D09 D08 D07 D06 D05 D04 D03 D02 D01 D00
EB0808H |_| 0 |_| 0 |_| 0 |_| 0 |_| 0 |_| 0 |_| 

BGO ON/OFF
TEXTSEL (BGO)
BG1 ON/OFF
TEXTSEL (BG1)
DISP/CPU
*Not used (4-4 bits left)

Cut all sprite and background display and release PCG and registers access to CPU.
- 0 ... Sprite and background display OFF. PCG and register access to CPU is fast.
- 1 ... Sprite and background display ON. CPU access is slow.

(3) TEXT SEL (BGO is D01~D02 of EB0808H, BG1 is D04~D05 of EB0808H) 
Set which of text area 0 or text area 1 to use.
- 00 ... Use text area 0 (PCG address: EBE000H~EBFFFEH).
- 01 ... Use text area 1 (PCG address: EBE000H~EBFFFEH). 
*BGO and BG1 may use the same text area.

(4) BGO ON/OFF, BG1 ON/OFF (BGO is D00 of EB0808H, BG1 is D03 of EB0808H)
Set the display of BGO area and BG1 area to ON ("1") / OFF ("0").
If you do not display the background area by setting BGO ON/OFF and BG1 ON/OFF to (OFF), you can use all PCG addresses from EB8000H to EBFFFEH (16k words) as PCG area. At that time, you can register up to 256 sprite patterns.
*BG1 is not displayed in 512 dot display mode.

(5) H total (EB080AH), H disp (EB080CH), V disp (EB080EH)
H total displays the horizontal total, H disp displays the horizontal display start position, and V disp displays the vertical display start position. For the definitions of each, refer to [4-8 CPU access methods].

4. Sprite

(6) L/H freq. (EB0810H D04)
Set the scan frequency.

D15 D14 D13 D12 D11 D10 D09 D08 D07 D06 D05 D04 D03 D02 D01 D00
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
EB0810H

|          H Res.          |
|         V Res.         |
| L/H freq. |

Frequency mode: 0: Standard resolution mode (15.98 kHz)
1: High-resolution mode (31.5 kHz)

(7) V Res. (EB0810H D02~D03)
Set the display resolution for the vertical direction.

D15 D14 D13 D12 D11 D10 D09 D08 D07 D06 D05 D04 D03 D02 D01 D00
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
EB0810H

|          H Res.          |
| V Res. | 0: 256 lines 0: 512 lines 0: (Not used) 1: (Not used)
| L/H freq. |

(8) H Res. (EB0810H D00~D01)
Set the display resolution for the horizontal direction.

D15 D14 D13 D12 D11 D10 D09 D08 D07 D06 D05 D04 D03 D02 D01 D00
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
EB0810H

| H Res. | 0: 256 dots 0: 512 dots 0: (Not used) 1: (Not used)
| V Res. |
| L/H freq. |

Page 45

Chapter 2 Screen Control

| Screen Mode Register | High Resolution | Standard Resolution |
|----------------------|-----------------|---------------------|
|                      | 512×512         | 256×256 2 colors/dot | 2 colors/dot | 256×256 |
| High Resolution      | 512×256 16 colors/dot | 256×256  2 colors/dot | 2 colors/dot | 256×512 Interlaced | 512×256 16 colors/dot |
| Standard Resolution  | 512×512 Interlaced | 512×256 16 colors/dot | 256×256 2 colors/dot | 256×256 2 colors/dot |   |
                    

|H total (EBO80AH)           | FFH (255)                              | FFH (255)                         | 25H (37) |
|H disp (EBO80CH)             | 15H (21) | 15H (21) | 0AH (10) | 09H (9) | 09H (9) | 04H (4) |
|V disp (EBO80EH)             | 28H (40) | 28H (40) | 28H (40) | 10H (16) | 10H (16) | 10H (16)
|L/H freq                      | V Res. (EBO810H)       | 15H (21)  | 11H (17) | 10H (16) | 05H (5) | 01H (1) | 00H (0)   |
|H Res.                       |                                     |           |           |           |           |         |
|Background Display            | 1 screen | 1 screen | 2 screens  | 1 screen | 1 screen | 2 screens   |

Table 2-18 Screen Mode Register List
Upper row ( ) : Decimal number 
Lower row ( ) : Hexadecimal number

Note: When setting the sprite screen mode register

-If you set a value other than "FFH" in mode register 0 (H Total), you must set a value other than "130 µs delay" after setting mode register 1 for 256 standard resolution mode. Set mode register 0 to 0.

************ Sample Program ************
```
    MOVE.W  #$4, EB800CH.L
    BSR     DELAY
    MOVE.W  #$25, EB80AH.L
    RTS
```

DELAY:      MOVE    #$FF, DO
LOOP:       DBF     DO, LOOP
            RTS

Note on sprite access

When accessing PCG and text (address: EB8000H-EBFFFEH) after powering on, set the extended bit (D10 bit) of the background control register (address: EBB808H) to "0" before accessing PCG.

# 4-5 PCG Area

(1) Relationship between PCG Address and PCG Code

The PCG code includes two types: sprite code and background code. 
Sprites are always of a 16x16 dot pattern configuration, but backgrounds can be of either a 16x16 dot pattern configuration or an 8x8 dot pattern configuration.
Therefore, when the background is in a 16x16 dot pattern configuration, it is possible for the sprite code and background code to share the same pattern. However, when the background is in an 8x8 dot pattern configuration, attention is required because the sprite code and background code differ.
Also, the background dot pattern configuration (16x16 dot pattern or 8x8 dot pattern) is determined by the screen mode. In horizontal 512 dot mode, it is a 16x16 dot pattern configuration, and in horizontal 256 dot mode, it is an 8x8 dot pattern configuration (refer to Figure 2-13 for details).

BG: 16x16 dot pattern configuration
16 dots   ⎡ ⎤
          ⎢SP Code = 0⎥
16 dots   ⎢BG Code = 0 ⎥
          ⎣          ⎦

BG: 8x8 dot pattern configuration
16 dots   ⎡ ⎢ 0 2 ⎥ ⎤
```
          ⎢ 1 3 ⎥ ⎥
          ⎣          ⎦
```
SP Code = n, BG Code = 4n, 4n+1, 4n+2, 4n+3

Figure 2-13 PCG Pattern Configuration

Chapter 2 Screen Control

The correspondence between PCG addresses and PCG codes is as follows.

For BG: 16 x 16 + SP/Pattern For BG: 8 x 8 + SP/Pattern 

| PCG Address | 16-bit Data | SP Code | BG Code | SP Code | BG Code | 
|-------------|-------------|---------|---------|---------|---------|
| EB8000H     |             |         | 0       | 0       |         |   +10H    |
| EB8020H     |             |         | 0       | 1       |         | 0 
| EB8040H     |             |         |         |         | 2 
| EB8060H     |             |         | +40H    |         | 3 
| EB8080H     |             | 1       | 1       | 1       | 4 
| EB80A0H     |             |         |         |         | 5 
| EB80C0H     |             |         |         |         | 6 
| EB80E0H     |             |         |         |         | 7 
| EB8100H     |             |         |         |         | 8 
| EB8120H     |             | 2       | 2       | 2       | 9 
| EB8140H     |             |         |         |         | 10 
| EB8160H     |             |         |         |         | 11 
| EB8180H     |             |         |         |         | 12 
| EB81A0H     |             | 3       | 3       | 3       | 13 
| EB81C0H     |             |         |         |         | 14 
| EB81E0H     |             |         |         |         | 15 

Table 2-19 Relationship between PCG address and code

4-6 Details of the Text Area (1)

(1) V Flip
Writing 1 will flip the pattern vertically. When it’s 0, the display is normal.

(2) H Flip
Writing 1 will flip the pattern horizontally. When it’s 0, the display is normal.

(3) COLOR (SP, BG)
Specifies the upper 4 bits of the sprite palette address (sprite color table 0~15). Thus, each sprite and background pattern unit can specify one of the 16 groups and 1 color table group (all registers are READ/WRITE allowed).

Palette Address

| COLOR |    | PCG Data  | Register Address | Notes             
| D11   | D10| D09 | D08 | I G R B |                                                |
| 0     | 0  | 0  | 0  |  0 0 0 0 | E82200H | \[16 Bits\]      | (Transparent) / Shared with text palette
                                                          /
|        |    |    |    |                        | E82202H |                                          |       
|        |    |    |    |  1 1 1 1 | E8221EH |                                          |
| 0     | 0  | 0  | 1  |                        | E82220H |                                          |
|        |    |    |    |                        | E82222H |                                          |
|        |    |    |    |                        | E8232EH | (Transparent)/                                             
|                                                                                                         Table 0
|                                                                                                         Table 1 

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

| 1  | 1  | 1  | 1 |   0 0 0 1\] | EB32E0H |                                          |
|        |    |    |    |                        | EB32F2H |                                          |
|        |    |    |    |                        | EB32F3H | (Transparent) / Table 15

Table 2-20 Specification of Sprite Color Table

Page 49

Chapter 2  Screen Control

The I, G, R, B data in the PCG area specifies the lower 4 bits of the sprite palette address. In other words, for each sprite and background pattern you can specify, on a per-dot basis, any 16 colors out of 65536 colors. Also, when the I, G, R, B color data defined in the PCG area is 0000H, it is treated as transparent.

(4) BG Code (SP, BG)
Sets which pattern in the PCG area to display (0-255).

4-7 Details of the Text Area (2)

The text area basically consists of two areas, Text Area 0 and Text Area 1. As shown below, the two areas can be considered exactly the same except for the difference in addresses.

(1) Address layout of the PCG in Text Area 0 (EBC000H~EBDFFEH; 4K words)

(EBC000H + ****H)

64 patterns

Diagram labels:
C000 C002 C004 C006 ... C07C C07E
C080 C082 C084 C086 ... C0FC C0FE
...
DF00 DF02 DF04 DF06 ... DF7C DF7E
DF80 DF82 DF84 DF86 ... DFFC DFFE

BG: 8x8-dot/pattern structure     BG: 16x16-dot/pattern structure
```
512 dots                          1024 dots
512 dots                          1024 dots
```

Figure 2-14  Address Layout of Text Area 0

4. Sprite

(2) Address layout of the PCG in Text Area 1 (EBE000H~EBFFFEH; 4K words)

(EBE000H + ****H)

64 patterns

Figure 2-15 Address Layout of Text Area 1

4-8 CPU Access Methods

(1) CPU Access Methods
```
   MOVE.W    Dn, (An)    ... Write to PCG / text from a register (n=0~7)
   MOVE.W    (An), Dn    ... Read   word
   An: address (E8000H~EBFFFEH)
   Dn: 16-bit data
   * CPU access is performed on a word basis (byte transfer is prohibited).
```

(2) CPU-Accessible Periods
```
   - Sprite Scroll Register
     Accessible at any time during the display period.
     A CPU period is secured once per character clock (1 QD).
     Therefore, a wait time of up to 1.8 QD (580 ns or 1440 ns) may occur.

   * 1 QD period = 320 ns (high-resolution mode) or 800 ns (standard-resolution mode)
   * Setting "DISP/CPU" to "0" (background dot control register; E8008H, R09)
     prohibits sprite/background display during the period but allows
     high-speed RAM access; sprite and background display are halted.
```

Chapter 2: Screen Control

All screen displays are cut off during the V blanking period. Therefore, upon entering the V blanking period, first set the “DISP/CPU” bit to “0” (display cut off), and then you can efficiently access the sprite registers (refer to section “4-4 Background Scroll Registers and Screen Mode Registers”).

Figure 2-16 CPU Access Timing

The readout time for registers for display use is as follows (although there may be slight variations).

Figure 2-17 Register Readout Timing

Therefore, if you want to write to the sprite scroll registers during the V blanking period, you need to rewrite 2 lines before V-DISP. Also, if you want to write during the H blanking period, you need to rewrite up to 4 characters or clock cycles before H-DISP. Please note that the sprited scroll register changes will take effect 3 lines after being written.

*In superimpose mode at high resolution, H blanking period part QD can stop when overlapping occurs during CPU access and potential delays may happen (the worst being around 60µs).

● Background Scroll Registers and Screen Mode Registers
It is possible to access them during any display period including the vertical blanking period.
Basically, the CPU registers and internal registers have a two-stage register structure. The CPU registers can access the CPU, and usually the access is completed within one wait. The contents written into the CPU registers are transferred to the internal registers at a specific timing once during each horizontal period, and become effective inside the chip. Therefore, even if the CPU rewrites the registers, it does not become effective immediately.

However, regarding the bit information below, since there is only one stage of register structure up to the CPU registers, when the CPU rewrites the registers, it becomes effective inside the chip immediately:
```
    - Background Scroll Registers: Address EB0808H "DISP/CPU" bit (D09)
    - Screen Mode Registers: Address EB080AH "H total" bit (D07-D00)
```

The period required to transfer the CPU registers to the internal registers is approximately as follows:

[Figure 2-18 Register Transfer Timing]

Consequently, for example, if the background scroll registers are rewritten for each line, writing during the H display period before one line is sufficient (However, it should be completed by 3-4 QD before H-DISP).

If there is a collision with the CPU not finishing the write cycle during the transfer period, a wait will occur on the CPU side. There is no wait for read cycles.

● Access to Background Scroll Registers and Screen Mode Registers of CPU is not affected during superimpose.

# Chapter 2: Screen Control

● PCG and Text
Access is possible throughout the display period. 
During the CPU period, it is synchronously confirmed once every character clock (QD). As a result, a minimum wait time of approximately 2.8 QD (900 ns or 2240 ns) may occur.

*Note: If the "DISP/CPU" bit (Background Control Register; EB0080H or D09) is set to "0" (CPU side), the display period for PCG and text is stopped, and the CPU can access for the entire duration, ensuring high-speed access. However, during this time, all screen displays including sprites and background will be disrupted. Therefore, to achieve effective PCG and text access, it is recommended to set the "DISP/CPU" bit to "0" (display cut) during the synchronization period (refer to "4-4 Background Control Scroll Register & Screen Mode Register" in the main text).

Figure 2-19 CPU Access Timing

The reading period for PCG and text is as shown below.
**H-Display Period**
- H-Disp (H Display Period)
- H Sync Period
**V-Display Period**
- PCG/Text Read Period

Communication timing within 1 line:
- Display Period: ~31.8µs or 61.4µs
- H Sync Period: ~1.8ms or ~1.4ms

Figure 2-20 Register Read Timing

Therefore, when rewriting PCG and text within the V-Synchronization period, it must be rewritten up to 1 line before V-DISP. During the H-Synchronization period, rewrites should be minimized (the display will be almost in the screen mode).

*Note: For high-resolution displays and superimpose modes, screen disruptions may temporarily stop H-Display, resulting in extended wait times during CPU access (maximum ~60µs).

5. Video Controller

The X68000 video controller has 3 registers, each with the following functionalities:
(1) Register 1
```
   - Setting the actual size of the graphic display
   - Setting the color mode of the graphic memory
```

(2) Register 2
```
   - Setting priority on graphic, text, and sprite screens
   - Setting the page priority of the graphics screen
```

(3) Register 3
```
   - Setting semi-transparent mode
   - Setting special priority (a function to maximize the priority of any area on the graphics screen)
   - Setting display mode for graphics, text, sprites, and border color
```

Please carry out access to the video controller's registers, just like with the CRTC, during V-DISP signal blanking periods (when the MFP or GPIP4 port is "0").

Chapter 2  Screen Control

5-1 Video Controller Register Address Map

*1: G size   *3: Sprite display ON/OFF   *5: 1024x1024 Graphic display ON/OFF
*2: 1024/512 *4: Text display ON/OFF

Register Address | D15 D14 D13 D12 D11 D10 D09 D08 D07 D06 D05 D04 D03 D02 D01 D00

Register 1
E82400H
Reserved
Memory Mode Setting
*1 G. Mode
*2 CL1  CL0

Register 2
E82500H
Reserved
Gr./Tx./Sp. inter-priority setting | Graphics screen page priority setting
Sprite  SP1 SP0
Text    TX1 TX0
Graphic GR1 GR0
Priority 4 page number
Priority 3 page number
Priority 2 page number
Priority 1 page number

Register 3
E82600H
Special Mode | *3 *4 *5 512 Graphic display ON/OFF
Ys  AH  (note)VHT  EXON  H/P  B/P  G/G  G/T  -  SON  TON  GS4  GS3  GS2  GS1  GS0

Table 2-21 Video Controller Access Map

* Note: all registers are READ/WRITE capable; * marks fields that are invalid (no effect).

* (note) The VHT signal is used by the optional "Color Image Unit".

5-2 Details of Video Controller Registers

(1) Register 1 (E8240H)
Setting the actual screen size of the graphics memory and color mode (Set values to D10-D08 as with R20 of the CRTC)

| D02 D01 D00 | Mode            |
|-------------|-----------------|
| 0 : 0 : 0   | 16 colors 4 pages mode (Valid only when D02 = 0) |
| 0 : 0 : 1   | 256 colors 2 pages mode (Valid only when D02 = 0) |
| 0 : 1 : 1   | 65536 colors 1 page mode (Valid only when D02 = 0) |
| 1 : 0 : 0   | Actual drawing screen mode 512×512 |
| 1 : 0 : 1   | Actual drawing screen mode 1024×1024 (Ensure D00 = 0, D01 = 0)   |

(2) Register 2 (E8250H)
In the lower byte of Register 2 (D07-D00), settings for the priority between pages of the graphics screen can be made.

| D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | 
|-----|-----|-----|-----|-----|-----|-----|-----|
|Page Priority Setting| 

Most preferred graphics page number:

| 0 | 0 | 0 : Graphics screen page 0              |
| 0 | 0 | 1 : Graphics screen page 1              |
| 0 | 1 | 0 : Graphics screen page 2              |
| 0 | 1 | 1 : Graphics screen page 3              |
| 1 | 0 | n-1: Graphics page number with n-1 priority (higher priority than graphic page number of 1|
|Second preferred graphics page number|Higher priority than graphic page number of|More preferred graphics page number|High priority than  more preferred graphic page number|

<Explanation>
★ Meaning of Graphic Screen Page Numbers and Priority in Each Mode ★

1. Graphics Actual Screen 1024×1024
In a mode with an actual screen of 1024×1024 dots, the graphics screen page number is assigned as shown in Figure 2-21. The display page has only one side, and this represents the priority of the values of graphics screen page numbers.

Chapter 2 Screen Control

Diagram labels:
G00 G01 G02 G03
Page 0   Page 1
Page 2   Page 3

Figure 2-21 Graphic Screen Page Number (1)

Normally the bit configuration is as follows (fixed).

D07 D06 D05 D04 D03 D02 D01 D00
 1   1   1   0   0   1   0   0

2. Graphics Actual Screen 512 x 512
In this mode, the graphics screen page numbers are assigned as shown in Figure 2-22.

Diagram labels:
SC0 SC1 SC2 SC3
(16 color mode)   (256 color mode)   (65536 color mode)
Page 3            Page 2             Page 0
Page 1
Page 0

Figure 2-22 Graphic Screen Page Number (2)

5. Video Controller

● When the graphic mode is 65536 colors on 1 page, the bit structure is as follows (fixed). Note that it is not possible to set the same graphics screen number at different priority levels.

D07 D06 D05 D04 D03 D02 D01 D00
1 1 0 0 1 0 0 0

● When the graphic mode is 256 colors on 2 pages, 16 colors on 2 pages, the graphics screen pages 0 to 3 can be used. In other words, when a higher priority is given to graphics screen pages 0 and 1, or conversely, when a higher priority is given to graphics screen pages 2 and 3, the bit structure is as follows. Note that it is not possible to set the same graphics screen number at different priority levels.

- When a higher priority is given to graphics screen pages 0 and 1

D07 D06 D05 D04 D03 D02 D01 D00
1 1 0 0 0 0 0 0 (fixed)

- When a higher priority is given to graphics screen pages 2 and 3

D07 D06 D05 D04 D03 D02 D01 D00
0 1 0 0 1 1 0 0 (fixed)

● When the graphic mode is 16 colors on 4 pages, the graphics screen number for each priority level will be set. Note that it is not possible to set the same graphics screen number at different priority levels.

Furthermore, the screens given priority here will be subject to special settings (display ON/OFF control, semi-transparency function, special priority functions) in the future.

Page 59

Page 2: Screen control

For register 2 (EB2500H), the lower byte (D13 to D08) sets the priority of the graphic, text, and sprite screens.

| D13 | D12 | D11 | D10 | D09 | D08 |
|-----|-----|-----|-----|-----|-----|

Graphics screen priority (D08, D09):
00: Lowest priority
01: Priority level 1
10: Priority level 2
11: Priority level 3

Text screen priority (D10, D11) (The same method as above)
Sprite screen priority (D12, D13) (The same method as above)

Note that for the graphics screen (D08, D09), text screen (D10, D11), and sprite screen (D12, D13), the same value cannot be set for each data.

(3) Register 3 (EB2600H)

The upper 4 bits of register 3 can be used to set the on/off display of the actual 512 x 512 graphics screen. Note that this setting is only valid when D02-0 of register 1 is on.

| D03 | D02 | D01 | D00 |
|-----|-----|-----|-----|
|     |     |     |     |
0: Display of the highest priority screen OFF
1: Display of the highest priority screen ON
0: Display of the second highest priority screen OFF
1: Display of the second highest priority screen ON
0: Display of the third highest priority screen OFF
1: Display of the third highest priority screen ON
0: Display of the fourth highest priority screen OFF
1: Display of the fourth highest priority screen ON

When in 65536 color one surface mode, the bit configuration will be as follows (fixed).

| D03 | D02 | D01 | D00 |
|-----|-----|-----|-----|
|  1  |  1  |  1  |  1  |

However, in the case of any dot, if the palette address is 0000H, and the palette data is 0000H, it will become transparent.

5. Video Controller

However, regardless of the palette address indicated by any dot, 0000H will be outputted (transparent).

• In graphic 256-color 2-page mode, the bit composition will be as follows (fixed).
∙ When displaying a graphic page with the highest priority and controlling the display of the next priority graphic page:

D03 D02 D01 D00

Display OFF 0 0 0 0

Display the second graphic page ON 1 1 1 1

However, if the palette address is 00H for any dot on the higher priority graphic page, the palette data of the dot of the higher priority page will be output. However, if the palette address is 00H, the palette data of the palette address 00H will not be output. Note that if the palette data of the palette address 00H is 0000H, it will become transparent.

D03 D02 D01 D00

Turning off the second graphic page display 0 0 1 1

However, if the palette address is 00H for any dot on the higher priority graphic page, the palette data of the palette address 00H will be output. Note that if the palette data of the palette address 00H is 0000H, it will become transparent.

• When controlling the display without displaying the graphic page with the highest priority and displaying the next priority graphic page:

D03 D02 D01 D00

Turning off the second graphic page display 0 1 1 0

However, if the palette address is 00H for any dot on the higher priority graphic page, the palette data of the palette address 00H will be output. Note that if the palette data of the palette address 00H is 0000H, it will become transparent.

Page 61

Chapter 2: Screen Control

Secondary Graphic Display Page OFF

D03 D02 D01 D00
0   0   0   0

However, at any dot, if its palette address indicates transparent palette data, 0000h is output (transparent).

Note that in the case of graphic 16 colors 4 pages and 256 colors 2 pages mode, the page with the priority set in register 2 is targeted.

In bit D04 of register 3, you can set the display ON/OFF for the actual graphics screen 1024x1024 (valid when D02-D01 of register 1 are enabled).

D04
0: Screen display OFF
1: Screen display ON

In bits D06-D07 of register 3, you can set the text and sprite display ON/OFF. Note that bit D07 is invalid.

D07 D06 D05
    *
0: Text screen display OFF
1: Text screen display ON
0: Sprite screen display OFF
1: Sprite screen display ON

In the X68000, the priority between the graphic pages in modes with two text and sprite screens or more than two graphic pages is decided by the palette in each case (the palette of the text and sprite screen is shared, the graphic palette of the two or four pages is shared). Therefore, the priority of the palette address value is decided. Especially when the palette address is 00H, regardless of its palette data, the palette data of the next priority graphic page with the effective palette address will be used.

However, when combining multiple graphics screens, if any one of the screen displays is set to ON with the palette address of all graphic pages being 00H, and even if only one screen display is set to ON, the palette address 00H is effective.

The content of address 00H will be output. However, if the screen display is all OFF, the content of palette address 00H will be output regardless of the screen display. In addition, the priority of the graphics screen and text (sprite) screen for each palette is determined independently, with the displayed order determined by the priority data of the palette address.

• Example of overlapping in graphics real screen 512x512, 16 colors, 4 pages mode:

The screen of the four pages that overlap here is as shown below. However, the empty part is set as palette address 00H.

(1) Page of the graphics screen with the highest priority
(2) Page of the graphics screen with the second highest priority
(3) Page of the graphics screen with the third highest priority
(4) Page of the graphics screen with the lowest priority

When these are overlapped:

(1)(2)(3)(4) Overlapping display
(1) Only (1) display
(2) Only (2) display
(1)(2) Overlapping display
(3) Only (3) display
(4) Only (4) display
(3)(4) Overlapping display
(1)(4) Overlapping display

Page 63

Chapter 2 Layer Control

(1)(3) Overlapping Display (2)(4) Overlapping Display (1)(2)(3) Overlapping Display
(1)(2)(4) Overlapping Display (1)(3)(4) Overlapping Display (2)(3)(4) Overlapping Display

Display Omitted

Figure 2-23 Examples of overlapping displays in graphics screen layers of 4 layers mode

In the upper byte of Register 3, half-transparency mode and special priority function settings are performed.

| D15 | D14 | D13 | D12 | D11 | D10 | D09 | D08 |
| Ys | AH | VH | EO | HP | BP | GG | GT |

GG:
0: Normal mode -
1: Allows for mask by filling the specified area on a graphic page, regardless of the layer assigned. If it's allowed for a graphic page, it becomes the highest priority for that graphic page, and it can be displayed over text (sprite) in that page. Except, when either D12 or D11 is set to 1, the GG mode setting will be limited to partial or full palette.

GT:
0: Normal mode -
1: Sets a graphic page as a pseudo-horizontal page of 2 vertical pages, and displays text (sprite) of the lower priority pages based on color for a more detailed display.

Reserve
D12:
0: Normal mode -
1: When either D12 or D11 is set to 1, VRAM pages of the graphic VRAM overwrite each other, enabling special priority display.
EO:
0: Normal mode -
1: When either D12 or D11 is set to 1, special priority mode is assigned.
BP:
0: Normal mode -
1: Enables half-transparency mode -
0: Normal mode -
1: Priority adjustment, when GG mode is set and the EO bit is 0. Enables normal display's highest priority graphic page to overwrite the text page being used, similar to the video RAM page.

GT:
0: Normal mode -
1: Allows priority control of color-based VRAM text (sprite) palette memory $00 to $FF.

Ys:
0: Deactivate (Ys) signal.
1: Temporarily activates (Ys) signal and outputs the superimpose screen as black and white on a TV screen (TV screen is cut).

Page 64

5-3 Details of Special Modes

(1) Transparent Mode

Transparent mode refers to the condition between the graphics screens in the display screen where:

a. Between the graphic page of higher priority (semi-transparent area designation page) and the graphic page of next higher priority.

b. Between the graphic page of higher priority (semi-transparent area designation page) and the text (sprite) screen with lower priority than the graphics screen.

c. Also, in superimpose mode, this refers to the condition between the graphic page of higher priority (semi-transparent area designation page) and the TV/video screen, where the designated region is blended at each part's half-tone (50%).

It refers to D13="1" of register 3. Essentially, if bit D12 and D11 of the video controller register 3 are set to "1", it becomes the transparent mode.

Figure 2-24 illustrates the concept of transparent mode.

```
              ----

             Green (D15-D11)           Red (D10-D06)           Blue (D05-D01)           I  (D00)
              | (Addition)                 | (Addition)                  | (Addition)              |
```
Green (D15-D11)           Red (D10-D06)           Blue (D05-D01)           I  (D00)
```
               | (Shift right)               | (Shift right)                      | (Shift right)
               |       1/2                        |      1/2                             |     1/2
```
Green (D15-D11)           Red (D10-D06)           Blue (D05-D01)
```
               |                                    |                                          |
               |                                    |                                          |
              G                                   R                                        B
              DAC                               DAC                                     DAC
              (Output)                        (Input)                                (Input)

                    ----       (Text (sprite) palette data or graphics palette data)
```

Figure 2-24 Transparent Mode

Chapter 2: Screen Control

Let's explain the details of various transparency modes below.

[1] Regardless of screen color mode, transparency is performed between the graphics screen and a text (sprite) screen to merge with the content at palette address 00H.

[Diagram with bits and flags]
E82600H

```
 Palette Address
 Contents of 00H
```

Picture of a boat on a graphical, text (sprite) screen

Screen combined with text displays the contents and transparency of palette address 00H.

Figure 2-25: Transparency Mode (1)

[2] The transparency is performed between the graphic page screen and text (sprite) screen. Although the domain where the transparency is conducted is designated on the graphics screen, in this case, it requires that the graphic page is displayed on screen with the highest priority. If the priority of the text (sprite) screen is higher and does not transparently overlap, the text (sprite) screen is displayed as-is. Additionally, if transparency is performed, the colors of the graphic will become half.

[Diagram with bits and flags]
E82600H

Priority of Dot Domain

Graphic Page

Text (Sprite) Screen

Transparency

Figure 2-26: Transparency Mode (2)

# 5. Video Controller

[3] In a mode with two or more graphic pages, the most prioritized graphic page and the next prioritized graphic page form a semi-transparent region. Note that the area is defined in the graphic page with the highest priority among overlapping areas. Also, the number of colors available for use in that graphic page will be halved.

E82600H table:
| D15 | D14 | D13 | D12 | D11 | D10 | D09 | D08 |
|----|----|----|----|----|----|----|----|
| X |  0  |  0  |  1  |  1  |  1  |  1  |  0  |

(X denotes don't care)

Illustrations:
- Diagram on the left shows Graphics Page 0 with a semi-transparent hatched area.
- Diagram on the right shows the layering of Graphics Page 1, resulting in semi-transparency.

**Figure 2-27** Semi-transparent Mode (3)

[4] The functions of both [2] and [3] are activated.

E82600H table:
| D15 | D14 | D13 | D12 | D11 | D10 | D09 | D08 |
|----|----|----|----|----|----|----|----|
| X |  0  |  1  |  1  |  1  |  1  |  1  |  0  |

(X denotes don't care)

[5] This is the semi-transparent mode in superimpose mode. First, the [2] semi-transparency function works and then another semi-transparency is performed in the same region defined by the [2] semi-transparency region for TV or video signals.

E82600H table:
| D15 | D14 | D13 | D12 | D11 | D10 | D09 | D08 |
|----|----|----|----|----|----|----|----|
| X |  0  |  1  |  1  |  1  |  1  |  0  |  1  |

(X denotes don't care)

Illustrations:
- Left: the TV (video) screen.
- Right: shows the outcome of the semi-transparency application with a dot matrix in the overlapping area.

**Figure 2-28** Semi-transparency Mode (4)

Chapter 2: Screeng Control

[6] This is the semi-transparent mode for superimposing. First, the function of [3] operates, and additionally, the semi-transparent function is performed in the same area as where the transparency function was already operating, with the TV and video signals.

| D15 | D14 | D13 | D12 | D11 | D10 | D09 | D08 |
|-----|-----|-----|-----|-----|-----|-----|-----|
|  1  |  1  |  1  |  1  |  1  |  1  |  1  |  0  |

(E82600H)  (X: Arbitrary)

(3) Screen

TV (Video) Screen

Figure 2-29 Semi-transparent Mode (5)

[7] The functions of both [5] and [6] operate.

| D15 | D14 | D13 | D12 | D11 | D10 | D09 | D08 |
|-----|-----|-----|-----|-----|-----|-----|-----|
|  0  |  1  |  1  |  1  |  1  |  1  |  1  |  1  |

(E82600H)  (X: Arbitrary)

Additionally, if both D08 and D09 are "0," the semi-transparent function does not work even if the area is specified. Therefore, when using the semi-transparent function, please use the initial setting values of D08 to D15 of register 3 as follows.

| D15 | D14 | D13 | D12 | D11 | D10 | D09 | D08 |
|-----|-----|-----|-----|-----|-----|-----|-----|
|  0  |  0  |  1  |  1  |  1  |  0  |  0  |  0  |

(E82600H)

Page 68

# 5. Video Controller

(2) Special Priority Mode

By setting bit D12 of register 3 of the video controller to "1" and D11 to "0", you enable the special priority mode.

The special priority mode uses the memory data of a high graphics page to specify an area within the graphics screen shown. The parts of the area specified (special priority area screen) where the priority is higher than the text (sprite) screen will be displayed in front of the text (sprite) screen. Conversely, when the priority of the text (sprite) screen is higher, it will be displayed in front of the specified area (special priority area screen).

         D15  D14  D13  D12  D11  D10  D09  D08
EB2600H   X    X    X    1    0    X    X    X  (* X is ignored)

[Diagram labeling]
Dotted line labeled special priority area
Graphics screen page 1
Graphics screen page 0
Text (sprite) screen

Figure 2-30 Special Priority Mode

Chapter 2: Screen Control

- Special priority function area specification (using D10, which specifies semi-transparent or special priority functions) and screen display page setting are set in the graphics VRAM memory data of the graphics screen pages with higher priority. (If setting the semi-transparent area specifies, "1", then using this function specifies. As for this, text and sprites can be used normally.)

Using the graphics VRAM bit of the memory data (LSB) as an area specification (when D10="1")

[Diagram]
- Graphics Screen 0
- Sprite
- Text
- Graphics Screen 1
- G03 Page
- G02 Page
- G01 Page
- G00 Page

- Page graphics palette address
- Palette address
- Area specification bit
```
    - The above semi-transparent or special priority function area specification is displayed with higher priority graphics screen pages, and it is set in dot units within the graphics VRAM. 
   - Use odd-numbered numbered half palettes in the graphics VRAM memory data LSB. (The palette address will be pseudo-addressed.)
```

The dotted line indicates the effective range of the semi-transparent/special priority.

Note: When specifying semi-transparency, other hits at LSB (semi-transparent area bit) must all be "0". Do not set anything to LSB (semi-transparent specified bit) to "1".

Note: If area specification is performed at the LSB of graphics VRAM memory data (D12="1", D11="1", D10="1"), the diagram 2-32 shows the configuration for the graphics palette. In this mode, except numbers, set the value of the palette address to match with the same value of the palette address content. Be careful when performing semi-transparency on the graphics screen.

Page 70

5. Video Controller

Graphical Face 1
(Even Palette)
(Specified by transparent display)

Graphical Face 2
(Odd Palette)
(Transparent display masking)

Figure 2-32 Structure of the graphical screen's palette

(4) CMP-OUT (Ys) signal (Standard resolution superimposed pose)

[1] D15="1"

CRT screen

Superimposed Pose

Computer screen

Black (transparent)

Superimposed Pose

[2] D15="0"

CRT screen

Superimposed Pose

TV, Video screen

(Dotted area represents the superimposed computer screen)

Figure 2-33 CMP-OUT signals

Page 71

Chapter 2 Screen Control

(5) Palette Address
[1] Text (Sprite) Palette Address
[READ/WRITE Available]

| Palette Address | Register Address | D15-D11   | D10-D06   | D05-D01 | D00 | Remarks         |
|-----------------|------------------|-----------|-----------|---------|-----|-----------------|
| 00H             | E82200H          | Green     | Red       | Blue    | I   |                 |
| 01H             | E82202H          |           |           |         |     |                 |
| 02H             | E82204H          |           |           |         |     |                 |
| 0FH             | E8221EH          |           |           |         |     |                 |
| 10H             | E82220H          |           |           |         |     | Text, Sprite    |
| 1FH             | E8223EH          |           |           |         |     | Common Palette  |
|                 |                  |           |           |         |     |                 |
|                 |                  |           |           |         |     | Sprite Palette  |
| F0H             | E823E0H          |           |           |         |     |                 |
| FFH             | E823FEH          |           |           |         |     |                 |

Table 2-22 Text (Sprite) Palette Address
[2] Graphic Palette Address (16 Colors, 256 Color Mode)
[READ/WRITE Available]

| Palette Address/Graphic VRAM Data | Register Address | D15-D11   | D10-D06   | D05-D01 | D00 | Remarks                        |
|-----------------------------------|------------------|-----------|-----------|---------|-----|--------------------------------|
| 00H                               | E82000H          | Green     | Red       | Blue    | I   | Graphic Palette               |
| 01H                               | E82002H          |           |           |         |     | (16 or 256 colors)            |
| 02H                               | E82004H          |           |           |         |     |                                |
| 0FH                               | E8201EH          |           |           |         |     |                                |
| 10H                               | E82020H          |           |           |         |     |                                |
| FFH                               | E821FEH          |           |           |         |     | Graphic Palette (256 colors)  |

Table 2-23 Graphic Palette Address (1)
(For the data of Palette Address 00H, please enter "0000H" as the initial value.)

5. Video Controller

[3] Graphic Palette Address (65536 Color Mode)

[READ/WRITE OK]

Table (lower byte):
Palette Address / Graphic VRAM memory data, lower byte | Register Address | D15~D14 | D13~D09 | D08 | D07~D06 | D05~D01 | D00 | Remarks
                                                       |                  | Red lower | Blue | I | Red lower | Blue | I |
00H 01H | E82000H | <- 8 bits ->        | <- 8 bits -> | 65536 color mode palette. Selects the 8 bits
02H 03H | E82004H |                                    | from either D15~D08 or D07~D00 and outputs
04H 05H | E82008H |                                    | them as the lower 8 bits.
  :  :  |   :     |
FCH FDH | E821F8H |
FEH FFH | E821FCH |

Table (upper byte):
Palette Address / Graphic VRAM memory data, upper byte | Register Address | D15~D11 | D10~D08 | D07~D03 | D02~D00 | Remarks
                                                       |                  | Green | Red upper | Green | Red upper |
00H 01H | E82002H | <- 8 bits -> | <- 8 bits -> | 65536 color mode palette. Selects the 8 bits
02H 03H | E82006H |                            | from either D15~D08 or D07~D00 and outputs
04H 05H | E8200AH |                            | them as the upper 8 bits.
  :  :  |   :     |
FCH FDH | E821FAH |
FEH FFH | E821FEH |

Table 2-24 Graphic Palette Address (2)

* As a rule, enter the palette address value into the data of each palette register address.

Chapter 2: Screen Control

6. CGROM

6-1 Specifications of CGROM

(1) Font Composition
```
    - 1/4 Width Characters (8x8, 12x12)
    - Half-Width Characters (8x16, 12x24)
    - Full-Width Characters (16x16, 24x24)
```
    
(2) Character Face
```
    - 1/4 Width Characters (6x7, 10x10)
    - Half-Width Characters (7x13, 10x18)
    - Full-Width Characters (15x16, 24x24)
```
    
(3) Number of Characters
```
    - 1/4 Width Characters: 256 characters
    - Half-Width Characters: 256 characters
    - Full-Width Characters: Non-Kanji...752 characters (JIS Code [Upper Address] 21H~28H, [Lower Address] 21H~7EH)
          First Level Kanji...3008 characters (JIS Code [Upper Address] 30H~4FH, [Lower Address] 21H~7EH)
          Second Level Kanji...3478 characters (JIS Code [Upper Address] 50H~74H, [Lower Address] 21H~7EH)
```

**6-2 CGROM Address Map**

MSB               16-bit                LSB
F00000H ──────────────────────────────
             16x16 Font (Alphanumeric 752 characters)
F05000H ──────────────────────────────
```
             16x16 Font
             (1st level kanji 3008 characters)
```
F1D600H ──────────────────────────────
```
             16x16 Font
             (2nd level kanji 3478 characters)
```
F398C0H ──────────────────────────────
F3A0000H ─────────────────────────────
             8x8 Font (256 characters)
F3A8000H ─────────────────────────────
             8x16 Font (256 characters)
F3B800H ─────────────────────────────
             12x12 Font (256 characters)
F3D000H ─────────────────────────────
             12x24 Font (256 characters)
F40000H ─────────────────────────────
             24x24 Font (Alphanumeric 752 characters)
F4D3800H ─────────────────────────────
```
             24x24 Font
             (1st level kanji 3008 characters)
```
F821800H ─────────────────────────────
```
             24x24 Font
             (2nd level kanji 3478 characters)
```
FBF380H ─────────────────────────────
FBFFEFH ─────────────────────────────

Figure 2-34 CGROM Address Map

Chapter 2: Screen Control

6-3 Structure of CGROM Address

(1) 8x8 Font

```
        MSB                       16 Bits                         LSB
        F3A000H   0     1
        F3A002H   2     3
                       :
        F3A004H   4     5
                       :
        F3A006H   6     7
                       :
        F3A008H    0    1
                       :
        F3A00AH    2    3
```

ASCII Code 00H Font

Fig. 2-35 CGROM Address (1)

(2) 8x16 Font

```
        MSB                       16 Bits                         LSB
        F3A800H       0      1
        F3A802H       2      3
                       :
        F3A804H       4      5
                       :
        F3A806H       6      7
                       :
        F3A808H       8      9
                       :
        F3A80AH   10    11
                       :
        F3A80CH   12    13
                       :
        F3A80EH   14    15
                       :
        F3A810H       0     1
```

ASCII Code 00H Font

Fig. 2-36 CGROM Address (2)

Page 76

Top Left:
"(3) 16x16 Font"

Labels in the table on the left:
"← 16-bit"
"0 1"
"2 3"
"4 5"
...
"26 27"
"28 29"
"30 31"

Labels in the table on the right:
"MSB 16-bit LSB"
F00000H 0 1
F00002H 2 3
F00004H 4 5
F00006H 6 7
F00008H 8 9
F0000AH 10 11
F0000CH 12 13
F0000EH 14 15
F00010H 16 17
F00012H 18 19
F00014H 20 21
...
F0001AH 26 27
F0001CH 28 29
F0001EH 30 31

Near the table on the right:
"JIS Code 2121H font"

Bottom:
"Fig. 2-37 CGROM Address (3)"

Chapter 2 Screen Control

(4) 12x12 Font

<--12 Bits-->
```
0   1
2   3
4   5
```
|   |
```
18  19
20  21
22  23
```

MSB  16 Bits  LSB

F3B800H     0   1   0000
F3B802H     2   3   0000
F3B804H     4   5   0000
F3B806H     6   7   0000
F3B808H     8   9   0000
F3B80AH     10  11  0000
F3B80CH     12  13  0000
F3B80EH     14  15  0000

F3B810H     16  17  0000
F3B812H     18  19  0000
F3B814H     20  21  0000
F3B816H     22  23  0000

ASCII Code
Font of 00H

Figure 2-38 CGROM Address (4)

Page 78

6.  CGROM

(5)  12×24 Font

MSB        16 Bits         LSB           
[F3D000H]   0      : 1       0000      
[F3D002H]   2      : 3       0000    
[F3D004H]   4      : 5       0000     
...

[F3D02AH]   42   : 43      0000    
[F3D02CH]   44   : 45      0000     
[F3D02EH]   46   : 47      0000     
...

ASCII Code 00H Font

Figure 2-39 CGROM Address (5)

(6)  24×24 Font

MSB           16 Bits           LSB           
[F3D000H]    0       : 1        0000  
[F3D002H]    2       : 3        0000     
[F3D004H]    4       : 5        0000     
...

[F3D02AH]   66     : 67       0000    
[F3D02CH]    68     : 69       0000   
[F3D02EH]    70     : 71       0000   
...

JIS Code 2121H Font

Figure 2-40 CGROM Address (6)

This document seems to be describing the CGROM (Character Generator ROM) addresses for different font sizes and associated character codes.

Chapter 2 Screen Control

7. Superimpose and Overscan

The X68000 supports the following computer screen display modes:

(1) Standard Resolution Mode (Horizontal synchronization frequency 15.98 kHz, Vertical synchronization frequency 60.52 Hz)
- As a display mode, the computer screen supports two modes: superimpose screen and computer screen (when connected to a dedicated display).
- In this mode, where you use the overscan method for the display on the computer screen, the size displayed on the actual display becomes smaller than the physical screen size (approximately 8% smaller horizontally and vertically).

| Standard Resolution Mode Physical Screen Size | Actual Displayed Screen Size |
|-------------------------|---------------------------|
| 512x256 (dot)           | Approx. 471x236 (dot)     |
| 256x256                 | Approx. 236x236           |
| 512x512                 | Approx. 471x471 (Interlace) |

Figure 2-25 Standard Resolution Mode

[Overscan]
[Normal Scan (usual display method)]

(Note: Dotted lines indicate the area of the overscanned computer screen)

CRT screen (display field)
Computer screen
Border

Figure 2-41 Standard Resolution Mode

7. Superimpose and Overscan

In this mode, in addition to supporting the superimpose mode as in the conventional X1 and X1turbo series, it also supports the interlace method superimpose mode with enhanced resolution. Note that in either case it is overscan.

Table 2-26 Superimpose Mode

| Conventional Superimpose Mode |        |
|---------------------------------|-------|
| 512 x 256                       |       |
| 256 x 256                       |       |

| Suspected High Resolution Superimpose Mode | (Interlace) |
|--------------------------------------------|-------------|
| 512 x 512                                  |             |

Figure 2-42 Superimpose Mode

[Conventional Superimpose Mode]      |         [Suspected High Resolution Superimpose Mode]

CRT Screen                            |         CRT Screen
(Display Example)                     |         (Display Example)
                                      |         
Same memory byte access               |         Each differs
Same memory byte access               |         Memory byte access
Same memory byte access               |         Memory byte access
Same memory byte access               |         Memory byte access
Same memory byte access               |         Memory byte access
Scanline of the above fields          |         Odd field scanline
Scanline of the below fields          |         Even field scanline

[Access the same memory data for both odd and even fields as with the TV monitor] (However, the dot pattern is a computer screen overscanned with points)

[Access different memory data for both odd and even fields as with the TV monitor]

Page 81

**Chapter 2: Screen Control**

(2) High-Resolution Mode (Horizontal synchronization frequency: 31.5 kHz, Vertical synchronization frequency: 55.46 Hz)
- As a display mode, it only supports computer screen displays and does not support Super Impose screen displays.
- The computer screen only displays in normal scan (however, on dedicated display sides it also supports over-scan).

**Figure 2-43 High-Resolution Mode**

(Caption of the illustration)
**Normal Scan**
CRT screen (display area)
Computer Screen
Border

- The 512x256 and 256x256 2 display modes operate in the same way as the high-resolution 200 line mode of X1turbo (however, the horizontal/vertical synchronization frequency is different).

(3) Determination of Super Impose by the main CPU
By sending the vertical synchronization signal from external source to DMA on PCLO (pin 8), and checking this signal through the DMA register, it is possible to determine whether it is in Super Impose mode.

<Summary> When the vertical synchronization signal from an external source is sent to DMA on PCLO, it remains "L" if it is not in Super Impose mode, and does not change. However, in the case of Super Impose, since the vertical synchronization signal from an external source is being input, a "H" signal is input every vertical synchronization period. Therefore, to determine if the change from "L" to "H" occurs every vertical synchronization period indicates Super Impose mode, and if there is no change from "L", it means modes other than Super Impose (computer mode / TV mode).

<Method> The PCLO mode can be determined by reading PCLO by setting DCRO (DMAC channel 0; register address E840004H) bit 0,1 (PCL) to 00. The content of PCLO is CSR (also DCRO channel 0; register address E840000H) bit 0 (PCS) read; "H" or "L".

Page: 82

Chapter 3
Sound Function

In the X68000, the YM2151 is used as the FM sound-source LSI and the MSM6258 is used as the voice-synthesis LSI.

Block diagram labels:
Data    Buffer
Address Decoder
Control

Vcc1 Vss CLK (4 MHz)
FM Sound Source (YM2151)

Vcc1 Vss
uPD8255  PC

Vcc1 Vss CLK (4 MHz)
ADPCM (MSM6258)
PCM PAN

Amp
Internal Speaker
Headphone Out
L line Out
R line Out
R TV AUDIO
L TV AUDIO
line In

Figure 3-1 Sound System Block Diagram

Chapter 3: Sound Functions

1. FM Sound Source

The X68000 uses YM2151 as the FM sound source LSI.

1-1 Features

- It can produce sounds up to 8 notes. However, if limited to sine waves, it can produce up to 32 notes.
- It can produce noise.
- It can modulate the tone color over time.
- It is possible to significantly modify the harmonics of the basic waveform.
- It can perform octave-wide frequency modulation.
- Volume can be set in intervals of 1.6 cents.
- It supports vibrato and tremolo effects.
- By significantly altering the harmonics of the basic waveform, or by deeply applying vibrato and tremolo effects, it can produce various sounds.
- It incorporates two timers.

1-2 FM Sound Source Block Diagram

```
                     Each Slot Block Diagram
                             +---------+
                             | Sin     |
                             | Table   |
                             |(PG)     |
                             +---------+
                             | EG      |
                             +---------+

                             +---------+
                             | M1: Slot.1|
                             | M2: Slot.9|
                             | C1: Slot.17|
                             | C2: Slot.25|
                             +---------+
                             | Operator|
                             |(OP)     |
                             +---------+
                                 |
                                 |
```
Ch. 1 +------------------------+

```
                             +---------+
                             | M1: Slot.2|
                             | M2: Slot.10|
                             | C1: Slot.18|
                             | C2: Slot.26|
                             +---------+
                             | OP      |
                             +---------+
                                 |
                                 |
```
Ch. 2 +------------------------+

```
                             +---------+
                             | M1: Slot.3|
                             | M2: Slot.11|
                             | C1: Slot.19|
                             | C2: Slot.27|
                             +---------+
                             | OP      |
                             +---------+
                                 |
                                 |
```
Ch. 3 +------------------------+

```
                             +---------+
                             | M1: Slot.4|
                             | M2: Slot.12|
                             | C1: Slot.20|
                             | C2: Slot.28|
                             +---------+
                             | OP      |
                             +---------+
                                 |
                                 |
```
Ch. 4 +------------------------+

```
                             +---------+
                             | M1: Slot.5|
                             | M2: Slot.13|
                             | C1: Slot.21|
                             | C2: Slot.29|
                             +---------+
                             | OP      |
                             +---------+
                                 |
                                 |
```
Ch. 5 +------------------------+

```
                             +---------+
                             | M1: Slot.6|
                             | M2: Slot.14|
                             | C1: Slot.22|
                             | C2: Slot.30|
                             +---------+
                             | OP      |
                             +---------+
                                 |
                                 |
```
Ch. 6 +------------------------+

```
                             +---------+
                             | M1: Slot.7|
                             | M2: Slot.15|
                             | C1: Slot.23|
                             | C2: Slot.31|
                             +---------+
                             | OP      |
                             +---------+
                                 |
                                 |
```
Ch. 7 +------------------------+

```
                             +---------+
                             | M1: Slot.8|
                             | M2: Slot.16|
                             | C1: Slot.24|
                             | C2: Slot.32|
                             +---------+
                             | OP      |
                             +---------+
                                 |
                                 |
```
Ch. 8 +------------------------+

Noise Slot Common Use
                         
YM2151
+---------+
| LFO     |
|(OPM)    |
+---------+

YM3012
                        
+---------+
| Phase   |
| Accm.   |
| Accumu- |
| lator   |
|(ACC)    |
+---------+

DAC (Digital to Analog Converter)
+---------+
| L       |
+---------+
| R       |
+---------+

LFO: Low-Frequency Oscillator
OPM: Operator Module
PG: Phase Generator
EG: Envelope Generator
OP: Operator (FM)
ACC: Accumulator
DAC: Digital-Analog Converter

M1: Modulator 1
M2: Modulator 2
C1: Carrier 1
C2: Carrier 2

Note: Each channel is controlled individually in two paths המשך כל הערוצים נשלטים בנפרד משני הנתיבים

Diagram 3-2 FM Sound Source Block Diagram

Chapter 3: Sound Functions

1-3 Structure of FM Sound Source Registers

| Item       | Register     | Function                                             |
|------------|--------------|------------------------------------------------------|
|            | CT KON       | Corresponds to output terminals CT1, CT2, external control. Toggles the channel number on/off in key slots. |
| Registers  | PG (PHASE GENERATOR) | OCT (up to 8 octaves) and NOTE settings. Sets the pitch and frequency for 1.6 steps. Determines the effective range of F-number values. |
|            | KC KF        | Determines the center and fine frequency values. Gives scaling by KC. Provides information of KC for scaling. Provides complex vibrato, tremolo effects to the sound. |
|            | MUL DT1 DT2 PMS | Gives modulation index values, provides delays by KC to set timing. |
| Registers  | EG (ENVELOPE GENERATOR) | Settings for Attack time (TA). Fast decay time (TDI) setting, variable KC scaling. Second decay time (TD2) setting, variable KC scaling. Release time (TR) setting, variable KC scaling. Controls AR, D1R, D2R, RR envelope levels. Settings for EG pause/drift, attack and decay time transition from the Sustain level. Adjusts the envelope levels according to the total level, AMS. |
|            | AR D1R D2R RR KS D1L TL AMS | Adjusts amplitudes and levels effectively to the music. |
| Registers  | OP (FM OPERATOR) | Settings for FM OP structure (8 types). Controls feedback level and shifts bit information. |
|            | CON FL       |                                                      |
|            | NOISE (NOISE GENERATOR) | Noise settings. Frequently modulates noise. |
|            | NE NFRQ      |                                                      |
| Registers  | LFO (LOW FREQUENCY OSCILLATOR) | Sets vibrato modulation frequency. Modulation (FM) and amplitude modulation (AM) modulation widths. Controls LFO signal output level. |
|            | LFRQ W PMD AMD | Controls frequency modulation output level. Adjust output according to frequency modulation (FM) and amplitude modulation (AM). |
| Registers  | ACC          | LR              | Accumulates signals from OP to produce series or parallel chains. |
| Registers  | TIMER        | CLKA1 CLKA2 CLKB LOAD F RESET IRQEN CSM | Generates Timer A and Timer B Power-up settings. Controls overflow. Resets Timer A, Timer B settings. Generates overflow interrupt signals. Allows CSM enabling. |
| Plug Registers in READ MODE | B IST        | Indicates register data under processing. Shows Timer A, B status. |

Table 3-1 FM Sound Source Registers

1-4 FM Sound Source Register Address Map

| Register Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | Notes |
|------------------|-----|-----|-----|-----|-----|-----|-----|-----|-------|
| E90001H          |     |     |     |     |     |     |     |     | FM Sound Source Register Address Port (WRITE) |
| E90003H          |     |     |     |     |     |     |     |     | FM Sound Source Data Port (READ/WRITE) |

Table 3-2 FM Sound Source Register Address Map

The internal structure of the FM sound source register is as shown in Table 3-3. To write data to these registers:

1. First, write the internal register value (00H~FFH, refer to Table 3-3 for details) that you want to access by the register address E90001H.
2. Next, write the data value you want to set to the register address E90003H.

Additionally, if you read data from register address E90003H, the internal register value of the register address E90001H becomes undefined.

Note: At reset, all data in each internal register becomes "0".

| Address | D7  | D6  | D5  | D4  | D3  | D2  | D1  | D0  | Notes |
|---------|-----|-----|-----|-----|-----|-----|-----|-----|-------|
| 01H     |     |     |     |     |     |     |     |     | TEST, D1 is LFO RESET |
| 08H     |     |     | KON |     |     |     |     |     | KON |
| 0FH     | NE  |     |     |     |     |     |     |     | NFRQ |
| 10H     |     |     |     |     |     |     |     |     | CLK A1 |
| 11H     |     |     |     |     |     |     |     |     | CLK A2 |
| 12H     |     |     |     |     |     |     |     |     | CLK B |
| 14H     | CSM |     |     |     | RESET | TRQEN | LOAD |     | Notes: CSM, RESET, TRQEN, LOAD |
| 18H     |     |     |     |     |     |     |     |     | LFRQ |
| 19H     |     |     |     |     |     |     | PMD/AMD | | Notes: PMD/AMD |
| 1BH     | CT  |     |     |     |     |     | W      | | Notes: CT, W |

Notes: 
- D3-D6 is slot number.
- D0-D2 is channel number.

Chapter 3 Sound Functions

| Ad | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 | Remarks |
|----|----|----|----|----|----|----|----|----|--------|
| 20H | LR | FL | CON | | Channel 1 |
| | | | | | | |
| 27H | LR | FL | CON | | Channel 8 |
| | | | | | | |
| 28H | | | KC | | | Channel 1 | 
| | | | | | (D4-D6 is octave group, D0-D3 is NOTE) |
| | | | | | | |
| | | | | | | Channel 8 |
| 2FH | | | KC | | | (D4-D6 is octave group, D0-D3 is NOTE) |
| | 30H | KF | | | | Channel 1 |
| 37H | KF | | | | | | Channel 8 | Channel unit |
| 38H | PMS | | | | AMS | | Channel 1 |
| | | | | | | |
| | 3FH | PMS | | | | AMS | | Channel 8 |
| 40H | DT1 | | MUL | Slot 1 |
| | | | | | | |
| 5FH | DT1 | | MUL | Slot 32 |
| 60H | | | TL | Slot 1 |
| | | | | | | |
| 7FH | | | TL | Slot 32 | Slot unit |
| 80H | KS | | AR | Slot 1 |
| | | | | | | |
| 9FH | KS | | AR | Slot 32 |
| A0H | AMS | | | DIR | Slot 1 (D7 is AMS-EN) |
| | | | | | | |
| BFH | AMS | | | DIR | Slot 32 (D7 is AMS-EN) |

1. FM Sound Source

| Address | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 | Remarks         |
|---------|----|----|----|----|----|----|----|----|-----------------|
| C0H     | DT2|    | D2R|    |    |    |    |    | Slot 1          |
|         |    |    |    |    |    |    |    |    |                 |
| DFH     | DT2| x  | D2R|    |    |    |    |    | Slot 32         |
|         |    |    |    |    |    |    |    |    |                 |
| E0H     | D1L|    | RR |    |    |    |    |    | Slot 1          |
|         |    |    |    |    |    |    |    |    |                 |
| FFH     | D1L|    | RR |    |    |    |    |    | Slot 32         |
|         |    |    |    |    |    |    |    |    |                 |

*Table 3-3: FM Sound Source Internal Register Address Map: WRITE MODE*

| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 | Remarks       |
|----|----|----|----|----|----|----|----|---------------|
| B  | x  | x  | x  | x  | x  | x  | IST|               |

*Table 3-4: FM Sound Source Internal Register Address Map: READ MODE*

1-5 Channel and Slot

The YM2151 sound source circuit has two sets of FM modulation circuits, and they operate on a time-sharing basis. The cycle table is read four times, so a total of 8 sound generation is possible. The circuit is thus configured to operate on a time-sharing basis over 32 slots. The relationship between the sound generation channel and slot number is shown below.

| FUNCTION | M1             | M2             | C1             | C2             |
|----------|----------------|----------------|----------------|----------------|
|          | Modulator 1    | Modulator 2    | Carrier 1      | Carrier 2      |
| Slot No. | 1 2 3 4 5 6 7 8| 9 10 11 12 13 14 15 16| 17 18 19 20 21 22 23 24| 25 26 27 28 29 30 31 32|
| Channel No. | 1 2 3 4 5 6 7 8| 1 2 3 4 5 6 7 8| 1 2 3 4 5 6 7 8| 1 2 3 4 5 6 7 8|

This slot turns into a noise slot when Noise is ENABLE (NE=1).

*Table 3-5: Relationship between Channel and Slot*

Chapter 3 Sound Functions

1-6 Details of FM Sound Registers

<KON: KEY ON>

| 08H | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|     |   X |   S |  N | CH.No.|

When a 3-bit channel number (CH.No) and a 4-bit slot number (SN) are given a key-on (key-off), the sound generation function starts (or the function ends).

```
SN = "1" ...... Key-On  
SN = "0" ...... Key-Off
```

Refer to tables 3-5 for the channel numbers. For SN D3, D4, D5, and D6 bits, corresponding slot numbers for M1, M2, C1, and C2 are used, respectively.

<CT: CONTROL OUTPUT>

| 1BH | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|     | CT | X | X | X | X | X | X | W |

CT1 (Sound Synthesis Block Switching Port)  
0: 8 MHz  
1: 4 MHz  
CT2 (FDC Forced READY Port)  
0: FDD Ready State (Normal Operation)  
1: Forced READY

Bits D6 and D7 correspond to output terminals CT1 and CT2, which are output ports capable of external control.  
On the X68000, CT1 switches between 4 MHz and 8 MHz for the sound synthesis block standard development frequency. Writing "0" selects 8 MHz, writing "1" selects 4 MHz. Note that the reset state is "0", so 8 MHz is selected.

CT2 is used to force the READY state of the FDC (Floppy Disk Controller) READY terminal, verifying the connection of the FDD (Floppy Disk Drive). Writing "1" forces the READY state. Normally (reset state), "0" is written, which allows the FDC to receive the FDD READY state.

For details on sound synthesis, refer to this chapter, and for details on disks, refer to Chapter 4.

1. FM Sound Source

<PG: PHASE GENERATOR>

From the registers described below, the KC, KF, MUL, DT1, DT2, and PMS data generate the phase information used to determine the carrier frequency and the modulator frequency. The vibrato effect and frequency modulation (effect sounds, etc.) produced by data from the LFO are also performed here.

- KC: KEY CODE (OCT, NOTE)

         D7 D6 D5 D4 D3 D2 D1 D0
28H/2FH  x  | OCT  |  NOTE     |

A key code is 1 data per note. One data consists of 7 bits: the upper 3 bits represent OCT (8 octaves) and the lower 4 bits represent NOTE. Refer to Table 3-6 for the relationship between OCT and NOTE.

- KF: KEY FRACTION

         D7 D6 D5 D4 D3 D2 D1 D0
30H/37H  |     KF        | x  x |

There is 1 data per note, and one data consists of 6 bits. With this 6-bit data, the phase information for the difference of one semitone (100 cents) can be obtained in steps of about 1.6 cents (refer to Table 3-6).

D approx. 36.7 Hz                               D approx. 4698.6 Hz

D6~D4 | 0 1 2 3 4 5 6 7
OCT   | 0 1 2 3 4 5 6 7

D3~D0 | 0 1 2 4 5 6 8 9 10 12 13 14
NOTE  | C# D# E F F# G G# A A# B  C  C# D

D7~D2  | 0 1 ... 16 17 ... 32 33 ... 48 49 ... 63 0
KF(cent)| 0   ...      ...      ...        ... 100 0

Table 3-6 Relationship between OCT and NOTE (at 4 MHz clock)

Chapter 3 Sound Functions

• MUL: PHASE MULTIPLY

40H  
5FH     
```
 D7 D6 D5 D4 D3 D2 D1 D0    
 X  DT1 MUL
```
1 Sound is set with 4 data bits, 4 bits long. For the positional information provided by KC and KF, the multiplication rate information indicated in Table 3-7 can be assumed.

MUL=D3-D0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
MULTIPLY | 0.5 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
Table 3-7 MUL Positional Information

• DT1: DETUNE (1)

40H  
5FH     
```
 D7 D6 D5 D4 D3 D2 D1 D0    
    DT1
```
1 Set sound with 4 data bits, 3 bits long. For the positional information provided by KC and KF, the detuned positional information indicated in Table 3-8 can be assumed. Additionally, the detuned positional information given by this DT1 is scaled by the KEY CODE (the top 2 bits of OCT and NOTE).

1. FM sound source

| OCT | NOTE | FD=0 (D-CENT) | FD=1 | FD=2 | FD=3 | FD=0 (D-FREQ) (HZ) | FD=1 | FD=2 | FD=3 |
|-----|------|---------------|------|------|------|------------------|------|------|------|
| 0 | 1 | 0.000 | 0.000 | 5.025 | 10.036 | 0.000 | 0.000 | 0.053 | 0.107 |
| 0 | 2 | 0.000 | 0.000 | 4.228 | 8.445 | 0.000 | 0.000 | 0.053 | 0.107 |
| 0 | 3 | 0.000 | 0.000 | 3.559 | 7.110 | 0.000 | 0.000 | 0.053 | 0.107 |
| 1 | 0 | 0.000 | 2.515 | 5.995 | 11.988 | 0.000 | 0.053 | 0.107 | 0.213 |
| 1 | 1 | 0.000 | 2.515 | 5.025 | 10.036 | 0.000 | 0.053 | 0.107 | 0.213 |
| 1 | 2 | 0.000 | 2.718 | 4.228 | 8.445 | 0.000 | 0.053 | 0.107 | 0.160 |
| 1 | 3 | 0.000 | 2.515 | 3.559 | 7.110 | 0.000 | 0.053 | 0.107 | 0.160 |
| 2 | 0 | 0.000 | 1.496 | 5.995 | 11.988 | 0.000 | 0.107 | 0.213 | 0.427 |
| 2 | 1 | 0.000 | 1.258 | 5.025 | 10.036 | 0.000 | 0.107 | 0.213 | 0.427 |
| 2 | 2 | 0.000 | 1.057 | 4.228 | 8.445 | 0.000 | 0.107 | 0.213 | 0.320 |
| 2 | 3 | 0.000 | 0.889 | 3.617 | 7.535 | 0.000 | 0.107 | 0.213 | 0.267 |
| 3 | 0 | 0.000 | 0.748 | 2.647 | 5.355 | 0.000 | 0.107 | 0.160 | 0.267 |
| 3 | 1 | 0.000 | 0.889 | 1.778 | 3.170 | 0.000 | 0.107 | 0.213 | 0.320 |
| 3 | 2 | 0.000 | 0.748 | 1.629 | 2.615 | 0.000 | 0.107 | 0.213 | 0.320 |
| 3 | 3 | 0.000 | 0.657 | 1.514 | 2.262 | 0.000 | 0.107 | 0.213 | 0.320 |
| 4 | 0 | 0.000 | 0.793 | 1.586 | 2.114 | 0.000 | 0.160 | 0.213 | 0.427 |
| 4 | 1 | 0.000 | 0.793 | 1.587 | 2.114 | 0.000 | 0.160 | 0.213 | 0.427 |
| 4 | 2 | 0.000 | 0.667 | 1.334 | 1.869 | 0.000 | 0.160 | 0.320 | 0.533 |
| 4 | 3 | 0.000 | 0.567 | 1.308 | 1.507 | 0.000 | 0.160 | 0.320 | 0.533 |
| 5 | 0 | 0.000 | 0.529 | 1.057 | 1.586 | 0.000 | 0.213 | 0.427 | 0.640 |
| 5 | 1 | 0.000 | 0.445 | 1.014 | 1.464 | 0.000 | 0.213 | 0.427 | 0.640 |
| 5 | 2 | 0.000 | 0.467 | 1.308 | 1.308 | 0.000 | 0.267 | 0.533 | 0.747 |
| 5 | 3 | 0.000 | 0.394 | 1.234 | 1.253 | 0.000 | 0.267 | 0.533 | 0.747 |
| 6 | 0 | 0.000 | 0.397 | 1.033 |

Chapter 3 Sound Features

• DT2: DETUNE (2)

COH
DFH | D7 D6 D5 D4 D3 D2 D1 D0
------|------------------------
      | DT2  ×  D2R

1 piece of data for 4 tones is set, which consists of 2 bits. By setting the detune information in tables KC and KF, it's possible to obtain a very large detune as shown in table 3-9. This is effective in creating sound effects.

| DT2 = D7~D6 | 0 | 1 | 2 | 3 |
| (cent)         | 0 | +600 | +781 | +950 |
| DETUNE       | 1 | +1.41 | +1.57 | +1.73 |
Table 3-9 DETUNE (1) Quantization precision

• PMS: PHASE MODULATION SENSITIVITY

38H
3FH | D7 D6 D5 D4 D3 D2 D1 D0
-----|-------------------
    |  ×  PMS  ×  AMS

1 piece of data for 1 tone is set, consisting of 3 bits. The subsequent LFO (Low-Frequency Oscillator) designation, expressed as modulation depth using 8 bits, is combined with the KC and KF settings, thereby obtaining effects similar to vibrato, tremolo, etc. This sensitivity can be controlled in 8 steps including 0, as shown in table 3-10. The values shown here are measured when the LFO output is at its maximum.

| PMS=D6~D4 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| MOD.MAX (cent) | 0±5 | ±10 | ±20 | ±50 | ±100 | ±400 | ±700 |
Table 3-10 PMS Sensitivity

<EG: ENVELOPE GENERATOR>

When the output of the EG is given a key-on, this EG changes as shown in the figure below. The envelope amount is represented by relative values. The attack part is exponential, and the decay part is all linear changes. The transition from TA to TD1 and from TD1 to TD2 is executed when the envelope amount is at 0 db, and at the fast decay level (D1L).

- AR: ATTACK RATE

Set 1 out of 16 data for each tone. One data consists of 5 bits. When a key-on is given to the EG, the envelope amount decreases, and after the TA time, the envelope amount reaches 0 db. This attack time (TA) can be set to 3-11, 3-12, etc., according to the AR. Additionally, AR is keyed by KEY CODE. Please refer to Figure 3-3 for scaling.

- DIR: 1st DECAY RATE

Set 1 out of 16 data for each tone. One data consists of 5 bits. When the EG's envelope amount is 0 db, it automatically reaches the fast decay level. This fast decay time (TD1) can be set according to the DIR to 3-11, 3-12, etc. Additionally, DIR is scaled by KEY CODE. Please refer to Figure 3-3.

Chapter 3 Sound Functions

• D2R: 2nd DECAY RATE

1 Set the data to 4 for the sound, 1 Data will be 5 bits as shown above. When the EG shifts to the second decay while passing through the fast decay level, this state will continue until the EG turns off. This second decay time (TD2) can be set according to D2R in Table 3-11 and Table 3-12. Additionally, D2R is scaled by KEY CODE, so please refer to Figure 3-3.

• RR: RELEASE RATE

1 Set the data to 4 for the sound, 1 Data will be 4 bits as shown above. When the EG moves to release while the key is off, it decays towards the maximum attenuation level (96db). This release time (TR) can be set according to RR in Table 3-11 and Table 3-12. Additionally, RR is scaled by KEY CODE, so please refer to Figure 3-3. The RR has one less bit compared to D1R and D2R, so the resolution worsens.

• KS: KEY SCALING

1 Set the data to 4 for the sound, 1 Data will be 2 bits. This KS scales the AR, D1R, D2R, RR, and related rates according to the KEY CODE. The scaling level can be controlled in four stages as shown in Table 3-3. The attack, fast decay, and release times are determined by the respective rates after scaling.

Page 96

1. FM Sound Source

*The scaled rate after key scaling is obtained by adding the value (RKs) shown in the table below to twice the rate (R).*
RATE = 2 × R + RKs
R: Various rates
AR, D1R, D2R are fixed rates written in the register, but RR is input as a value twice the value written in the register, and the rate calculation formula starts from RATE = 0.
*When calculation exceeds 63, it is set to RATE = 63

RKs: Values determined by KEY CODE and KS (left table).
However, in this case, we discard the lower 2 bits of NOTE as shown in the figure below, and use KC.

```
               KC
     +---------+-------------+
     | D6  D5  D4  D3  D2  D1  D0  |
     +---------+-------------+
         OCT        NOTE
```
Figure 3-3 Key Scaling

Tables 3-11 and 3-12 divide the 6-bit rate after key scaling determined by Figure 3-3 into the upper 4 bits and the lower 2 bits.

Chapter 3 Sound Functions

(10% -> 90%) or (90% -> 10%)

※ Indicates the time taken for the level to transition from 10% to 90% or from 90% to 10%.
※ This table is calculated assuming an O of 4.0 MHz.

<table>
<tr>
```
    <th>EG ATTACK TIME</th>
    <th></th>
    <th>EG DECAY TIME</th>
    <th></th>
```
</tr>
<tr>
```
    <th>RATE</th>
    <th>msec (10% -> 90%)</th>
    <th>RATE</th>
    <th>msec (90% -> 10%)</th>
```
</tr><tr>
```
    <td>15</td>
    <td>0.00</td>
    <td>15</td>
    <td>1.22</td>
```
</tr><tr>
```
    <td>15</td>
    <td>0.24</td>
    <td>15</td>
    <td>1.22</td>
```
</tr><tr>
```
    <td>15</td>
    <td>0.24</td>
    <td>15</td>
    <td>1.22</td>
```
</tr><tr>
```
    <td>14</td>
    <td>0.37</td>
    <td>14</td>
    <td>1.62</td>
```
</tr><tr>
```
    <td>14</td>
    <td>0.52</td>
    <td>14</td>
    <td>2.39</td>
```
</tr><tr>
```
    <td>14</td>
    <td>0.59</td>
    <td>14</td>
    <td>2.43</td>
```
</tr><tr>
```
    <td>13</td>
    <td>0.96</td>
    <td>14</td>
    <td>3.28</td>
```
</tr><tr>
```
    <td>13</td>
    <td>1.20</td>
    <td>13</td>
    <td>3.26</td>
```
</tr><tr>
```
    <td>13</td>
    <td>1.16</td>
    <td>13</td>
    <td>3.89</td>
```
</tr><tr>
```
    <td>12 </td>
    <td>2.02</td>
    <td>13</td>
    <td>4.87</td>
```
</tr><tr>
```
    <td>12</td>
    <td>2.40</td>
    <td>12</td>
    <td>5.57</td>
```
</tr><tr>
```
    <td>12</td>
    <td>2.21</td>
    <td>12</td>
    <td>6.49</td>
```
</tr><tr>
```
    <td>12</td>
    <td>3.64</td>
    <td>12</td>
    <td>7.79</td>
```
</tr><tr>
```
    <td>11</td>
    <td>3.91</td>
    <td>11</td>
    <td>19.48</td>
```
</tr><tr>
```
    <td>10</td>
    <td>4.48</td>
    <td>11</td>
    <td>22.26</td>
```
</tr><tr>
```
    <td>10</td>
    <td>5.22</td>
    <td>10</td>
    <td>25.96</td>
```
</tr><tr>
```
    <td>10</td>
    <td>6.27</td>
    <td>10</td>
    <td>31.16</td>
```
</tr><tr>
```
    <td>10</td>
    <td>7.87</td>
    <td>10</td>
    <td>38.95</td>
```
</tr><tr>
```
    <td>9</td>
    <td>8.95</td>
    <td>9</td>
    <td>44.52</td>
```
</tr><tr>
```
    <td>9</td>
    <td>10.44</td>
    <td>9</td>
    <td>52.83</td>
```
</tr><tr>
```
    <td>9</td>
    <td>12.52</td>
    <td>9</td>
    <td>52.83</td>
```
</tr><tr>
```
    <td>9</td>
    <td>15.65</td>
    <td>9</td>
    <td>77.90</td>
```
</tr><tr>
```
    <td>8</td>
    <td>17.49</td>
    <td>8</td>
    <td>69.03</td>
```
</tr><tr>
```
    <td>8</td>
    <td>20.87</td>
    <td>8</td>
    <td>103.86</td>
```
</tr><tr>
```
    <td>8</td>
    <td>25.05</td>
    <td>8</td>
    <td>124.64</td>
```
</tr><tr>
```
    <td>8</td>
    <td>31.32</
```

1. FM Sound Source

(96 dB -> 0 dB) or (0 dB -> 96 dB)

* This indicates the time it takes for the level to go from 0% to 100% or from 100% to 0%.
* This table is calculated with CLOCK = 4.0 MHz.

EG ATTACK TIME                 EG DECAY TIME
RATE | msec (96dB->0dB)        RATE | msec (0dB->96dB)
```
15 3 | 0.00                    15 3 | 6.02
15 2 | 0.47                    15 2 | 6.02
15 1 | 0.47                    15 1 | 6.02
15 0 | 0.47                    15 0 | 6.02
14 3 | 0.94                    14 3 | 6.02
14 2 | 1.00                    14 2 | 9.04
14 1 | 1.00                    14 1 | 9.04
14 0 | 1.00                    14 0 | 9.04
13 3 | 1.53                    13 3 | 12.76
13 2 | 1.53                    13 2 | 12.76
13 1 | 1.99                    13 1 | 19.27
13 0 | 1.99                    13 0 | 19.27
12 3 | 2.78                    12 3 | 27.52
12 2 | 2.78                    12 2 | 27.52
12 1 | 4.18                    12 1 | 38.53
12 0 | 4.18                    12 0 | 38.53
11 3 | 6.97                    11 3 | 55.04
11 2 | 6.97                    11 2 | 55.04
11 1 | 9.29                    11 1 | 96.33
11 0 | 9.29                    11 0 | 96.33
10 3 | 11.15                   10 3 | 110.09
10 2 | 11.15                   10 2 | 110.09
10 1 | 13.94                   10 1 | 128.43
10 0 | 13.94                   10 0 | 128.43
```
```
 9 3 | 15.93                    9 3 | 154.12
 9 2 | 18.58                    9 2 | 154.12
 9 1 | 22.30                    9 1 | 192.65
 9 0 | 27.88                    9 0 | 192.65
 8 3 | 27.88                    8 3 | 220.17
 8 2 | 31.86                    8 2 | 220.17
 8 1 | 41.53                    8 1 | 308.25
 8 0 | 44.60                    8 0 | 385.31
```

Continued (right columns):
```
 7 3 | 63.72
 7 2 | 74.34
 7 1 | 89.20
 7 0 | 111.51
 6 3 | 148.43
 6 2 | 211.72
 6 1 | 223.01
 6 0 | 254.87
 5 3 | 297.35
 5 2 | 356.42
 5 1 | 396.47
 5 0 | 509.74
 4 3 | 713.63
 4 2 | 823.02
 4 1 | 941.18
 4 0 | 1189.53
 3 3 | 1784.08
 3 2 | 2038.95
 3 1 | 2378.78
 3 0 | 2854.53
 2 3 | 3568.16
 2 2 | 4077.90
 2 1 | 4757.55
 2 0 | 5709.66
 1 3 | 7136.33
 1 2 | infinity
 1 1 | infinity
 1 0 | infinity
 0 3 | infinity
 0 2 | infinity
 0 1 | infinity
 0 0 | infinity
```

Note: "infinity" denotes an infinite time in msec.

Table 3-12 ATTACK, DECAY TIME (2)

Chapter 3 Sound Functions

• D1L: 1st DECAY LEVEL

| D7 D6 D5 D4 D3 D2 D1 D0 |
| --- --- --- --- --- --- --- --- |
| D1L | RR |

Set 4 decays for 1 sound, and 1 data consists of 4 bits. EG moves from first decay to second decay through this level. With a resolution of 3 dB, each bit is weighted as in the table below.

| D7 | D6 | D5 | D4 |
| --- | --- | --- | --- |
| 24 | 12 | 6 | 3 |

When all D7-D4 are "1" (-45 dB), the decay amount is further calculated as 48 dB.

• TL: TOTAL LEVEL

| D7 D6 D5 D4 D3 D2 D1 D0 |
| --- --- --- --- --- --- --- --- |
| TL | RR | 

Set 4 decays for 1 sound, and 1 data consists of 7 bits. The total level (expressed in attenuation amount) at each time calculated by the EG is added and output to the OP to control pitch (vibration adjustment) and volume. The minimum resolution is 0.75 dB, and each bit is weighted as in the table below.

| 48 | 24 | 12 | 6 | 3 | 1.5 | 0.75 |

**AMS: AMPLITUDE MODULATION SENSITIVITY**

```
                      D7  D6  D5  D4  D3  D2  D1  D0
                   38H                     X      PMS   X      AMS
                   3FH                     X                  EN   DIR
                   A0H             AMS-EN Switch
                   B0H             1: AMS Enabled
                                       0: AMS Disabled
```

Set the data to 1 for one sound, the data ranges from 2 bits. EG data can perform amplitude modulation control with 8-bit data from LFO to LFA. This amplitude modulation control is set as follows in terms of the maximum modulation rate. You can select whether to apply changes for each slot by the AMS-EN switch. The data of AMS is set for each channel.

AMS  |  AM MOD (Max)
```
0            |  0 
1            |  23.90625 dB 
2            |  47.8125 dB
3            |  95.625 dB
```

Table 3-13 AMS max modulation rate

**OP: FM OPERATOR**

Reads the signal sample from the phase information of PG. The read signal will be calculated using envelope information from EG. Then, the switching of the continuous circuit configuration of FM-OP is performed, and if necessary, the control of the feedback amount according to the phase information of itself is carried out. The signal transformed by FM is sent to ACC here. 

(Page) 101

Chapter 3: Sound Function

• CON: CONNECTION

20H
```
D7 D6 D5 D4 D3 D2 D1 D0
    LR  FL  CON=(fs)
```

27H

1 By setting one data for each sound, it consists of the three bits as shown above. Due to this CON, it is possible to take the FM-OP circuit structure (refer to Fig. 3-4) of 8 sounds, and to produce 8 different tones respectively.

[Diagram]
Fig. 3-4 Configuration of FM-OP

Page 102

1. FM Sound Source

◇FL: SELF FEED BACK LEVEL

| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|----|----|----|----|----|----|----|----|
| 20H  | LR | FL | CON |
| 27H  |    |

You set 1 sound to 1 data, using 3 bits. The FL level is as shown in Table 3-14, and can be controlled for each sound.

| FL=(D5~D3) | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|------------|---|---|---|---|---|---|---|---|
| LEVEL      | OFF | π/16 | π/8 | π/4 | π/2 | π | 2π | 4π |

Table 3-14 FL Level

◇NOISE: NOISE GENERATOR

When NOISE is enabled, the 32nd slot changes to a NOISE slot. The value of the NOISE GENERATOR's slot can be controlled externally.

In addition, the envelope uses the envelope function of the 32nd slot, but instead of this being a logarithmic transformation, the attack part is exponential, and the decay part changes linearly.

◇NE: NOISE ENABLE

| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|----|----|----|----|----|----|----|----|
| OFF | NE | X | X | NFRQ |

When setting the NE bit (= D7) to "1", the 32nd slot becomes a NOISE slot.

◇NFRQ: NOISE FREQUENCY

The relationship between NFRQ and noise is

fNoise = fM (kHz) / 32 * (NFRQ)

Note: fM = 4000 kHz (YM2151 additional clock frequency).

Chapter 3 Sound Functions

In other words, it can be changed between approximately 4.0 kHz to 125 kHz. The noise period at this time is:

\[ T_{\text{noise}} = \frac{2^{17} - 1}{f_{\text{noise}}\ (\text{Hz})}\ (\text{sec}) \]

Therefore, the value ranges from approximately 32.8 sec to approximately 1.05 sec.

<LFO: FREQUENCY OSC>

It is possible to control the oscillating frequency with a wide range from approximately 53 Hz to approximately 0.008 Hz. You can select one of the waveforms: sine wave, square wave, triangular wave, or noise, and perform frequency modulation of the sound source and amplitude modulation. At this time, the output level can be controlled separately for frequency modulation and amplitude modulation.

- LFRQ: LOW FREQUENCY

```
     D7   D6   D5    D4    D3    D2    D1    D0
     18H  LFRQ
```
     
You can set the oscillating frequency with 8 bits. Please refer to Table 3-15 for the setting values.

- W: WAVE FORM

```
     D7   D6   D5    D4    D3    D2    D1    D0
     18H  CT   x     x     x     x     x     W
```
     
Using the above 2 bits, four types are output for frequency modulation (FM) and amplitude modulation (AM). (See Figures 3-5)

Page 104

1. FM Sound Source

| DATA (HEX) | FREQ. (Hz) | DATA (HEX) | FREQ. (Hz) | DATA (HEX) | FREQ. (Hz) | DATA (HEX) | FREQ. (Hz) | DATA (HEX) | FREQ. (Hz) | DATA (HEX) | FREQ. (Hz) |
|------------|------------|------------|------------|------------|------------|------------|------------|------------|------------|------------|------------|
| FF         | 59.1278    | BF         | 3.6955     | 7F         | 0.2310     | 3F         | 0.0144     |
| FE         | 57.2205    | BE         | 3.5763     | 7E         | 0.2235     | 3E         | 0.0140     |
| FD         | 55.3131    | BD         | 3.4571     | 7D         | 0.2161     | 3D         | 0.0136     |
| FC         | 53.4058    | BC         | 3.3379     | 7C         | 0.2086     | 3C         | 0.0130     |
| FB         | 51.4948    | BB         | 3.2187     | 7B         | 0.2012     | 3B         | 0.0126     |
| FA         | 49.5911    | BA         | 3.0994     | 7A         | 0.1937     | 3A         | 0.0120     |
| F9         | 47.6837    | B9         | 2.9802     | 79         | 0.1863     | 39         | 0.0114     |
| F8         | 45.7764    | B8         | 2.8618     | 78         | 0.1788     | 38         | 0.0112     |
| F7         | 43.8690    | B7         | 2.7418     | 77         | 0.1714     | 37         | 0.0107     |
| F6         | 41.9617    | B6         | 2.6226     | 76         | 0.1639     | 36         | 0.0102     |
| F5         | 40.0543    | B5         | 2.5034     | 75         | 0.1565     | 35         | 0.0098     |
| F4         | 38.1470    | B4         | 2.3842     | 74         | 0.1490     | 34         | 0.0093     |
| F3         | 36.2396    | B3         | 2.2649     | 73         | 0.1416     | 33         | 0.0088     |
| F2         | 34.3323    | B2         | 2.1458     | 72         | 0.1342     | 32         | 0.0083     |
| F1         | 32.4249    | B1         | 2.0266     | 71         | 0.1267     | 31         | 0.0079     |
| F0         | 30.5175    | B0         | 1.9074     | 70         | 0.1193     | 30         | 0.0074     |
| EF         | 29.5639    | AF         | 1.8477     | 6F         | 0.1155     | 2F         | 0.0072     |
| EE         | 28.6102    | AE         | 1.7881     | 6E         | 0.1118     | 2E         | 0.0070     |
| ED         | 27.6566    | AD         | 1.7285     | 6D         | 0.1081     | 2D         | 0.0066     |
| EC         | 26.7029    | AC         | 1.6689     | 6C         | 0.1043     | 2C         | 0.0063     |
| EB         | 25.7492    | AB         | 1.6093     | 6B         | 0.1006     | 2B         | 0.0061     |
| EA         | 24.7955    | AA         | 1.5497     | 6A         | 0.0969     | 2A         | 0.0056     |
| E9         | 23.8419    | A9         | 1.4901     | 69         | 0.0931     | 29         | 0.0054     |
| E8         | 22.8882    | A8         | 1.4305     | 68         | 0.0894     | 28         | 0.0050     |
| E7

Chapter 3 Sound Function

D4 | 9.5367   94 | 0.5950   54 | 0.0373   14 | 0.0023
D3 | 9.0598   93 | 0.5662   53 | 0.0354   13 | 0.0022
D2 | 8.5831   92 | 0.5364   52 | 0.0335   12 | 0.0021
D1 | 8.1062   91 | 0.5086   51 | 0.0317   11 | 0.0020
D0 | 7.6294   90 | 0.4768   50 | 0.0298   10 | 0.0019
CF | 7.3910   8F | 0.4619   4F | 0.0289   0F | 0.0018
CE | 7.1526   8E | 0.4470   4E | 0.0279   0E | 0.0017
CD | 6.9141   8D | 0.4321   4D | 0.0270   0D | 0.0017
CC | 6.8757   8C | 0.4172   4C | 0.0261   0C | 0.0016
CB | 6.4373   8B | 0.4023   4B | 0.0251   0B | 0.0016
CA | 6.1989   8A | 0.3874   4A | 0.0242   0A | 0.0015
C9 | 5.9605   89 | 0.3725   49 | 0.0233   09 | 0.0015
C8 | 5.7220   88 | 0.3576   48 | 0.0224   08 | 0.0014
C7 | 5.4836   87 | 0.3427   47 | 0.0214   07 | 0.0013
C6 | 5.2452   86 | 0.3278   46 | 0.0205   06 | 0.0013
C5 | 5.0068   85 | 0.3129   45 | 0.0196   05 | 0.0012
C4 | 4.7684   84 | 0.2980   44 | 0.0186   04 | 0.0012
C3 | 4.5300   83 | 0.2831   43 | 0.0177   03 | 0.0011
C2 | 4.2915   82 | 0.2682   42 | 0.0168   02 | 0.0010
C1 | 4.0531   81 | 0.2533   41 | 0.0158   01 | 0.0010
C0 | 3.8147   80 | 0.2384   40 | 0.0149   00 | 0.0009

Table 3-15 LFO

Waveform diagram labels:
(W)   (PM)                     (AM)
3       (NOISE)                (NOISE)

Figure 3-5 WAVE FORM

1. FM Sound Source

- PMD: PHASE MODULATION DEPTH
- AMD: AMPLITUDE MODULATION DEPTH

```
          D7 D6 D5 D4 D3 D2 D1 D0
   19H   [        PMD/AMD]
                                   F=1 : PMD
                                   F=0 : AMD
```

Each data has 7 bits, and the data is distinguished by assigning the highest bit to PMD or AMD. PMD/AMD controls the output level of phase modulation (or amplitude modulation) with a 1/128 resolution. The output controlled by PMD consists of 2's complement numbers, while the output controlled by AMD is in binary form.

- TEST (LFO RESET)

```
          D7 D6 D5 D4 D3 D2 D1 D0
   01H   [         TEST]
                              LFO RESET
```

TEST is a signal provided for testing purposes. Among these, when "1" is written once to the LFO RESET bit (D1) at key-on and "0" is written again, it resets the output waveform of the LFO, as shown in FIGs. 3 to 5, and restarts from the left-end part of the waveform. This allows synchronization of the timing at key-on for each modulation.

* Caution: Since it is used for testing purposes, writing data with level "1" to any bit other than the specified bit (D1) will make the device enter test mode. Please be careful.

<ACC: ACCUMULATOR>

Receiving the L and R control signals from the register, the musical sound signal data from the OP is accumulated in the L series, R series, or both series simultaneously. The accumulated L and R signals are output as two-series signals alternately, with a mantissa part of 10 bits (including the sign bit) and an offset of the exponent part of 3 bits, in binary format, serially from the LSB.

Chapter 3: Sound Functions

- LR: LEFT CH. ENABLE/RIGHT CH. ENABLE

```
   D7 D6 D5 D4 D3 D2 D1 D0
  -------------------------
```
20H | LR FL CON |
```
  -------------------------
  | LEFT CH. ENABLE 1: Enable
  |                0: Disable
  | RIGHT CH. ENABLE  1: Enable
  |                0: Disable
```

When there are signals from bit 2 and bit OP, they are divided into L series and R series, or both series are input to the accumulation rate simultaneously as control signals.

<TIMER>

Two timers: 10-bit timer A and 8-bit timer B (each can be preset). They have functions to start, stop, and set flags in the data bus during overflow and require interrupt requests to process these events. Timer A also has a function to generate interrupt requests during overflow within the device. This allows for stopping interrupt requests.

- CLKA1/CLKA2
```
   D7 D6 D5 D4 D3 D2 D1 D0
  -------------------------
```
10H | CLKA1 | X X X X 
11H |                 CLKA2 |
|  NA  |<------------------------->|  (As it is connected, combining CLKA1 and CLKA2 = 10 bits)
|       CLKA1       | |      CLKA2       |
                                                                                       (Clock frequencies added using 4000kHz YM2151)
Combining the above two words into 10 bits forms Timer A, which generates an overflow at the period indicated by the following formula. NA is derived as shown in the diagram connecting CLKA1 and CLKA2.

            64 x (1024 - NA)
TA (ms) = ----------------------
```
                    fM (kHz)

 * Note: fM (kHz) = 4000 kHz (added clock frequency for YM2151)
```

Page 108

1. FM Sound Source

- CLKB

|  D7  |  D6  |  D5  |  D4  |  D3  |  D2  |  D1  |  D0  |
|------|------|------|------|------|------|------|------|
|  12H |             CLKB              |

Given 8 bits, Timer B overflows with the following period:

\[ TB (\text{ms}) = \frac{1024 \times (256 - \text{CLKB})}{fM (\text{kHz})} \]

Note: \( fM (\text{kHz}) = 4000 \text{kHz (Clock frequency added to YM2151)} \)

- LOAD

|  D7  |  D6  |  D5  |  D4  |  D3  |  D2  |  D1  |  D0  |
|------|------|------|------|------|------|------|------|
|  14H |    x    |           LOAD           |
|            |            |            |
|            | Timer A Stop (0) | Timer A Start (1)
|            | Timer B Stop (0) | Timer B Start (1)

Using 2 bits, controls the start/stop of Timers A and B. "1" to start, "0" to stop.

- F RESET

|  D7  |  D6  |  D5  |  D4  |  D3  |  D2  |  D1  |  D0  |
|------|------|------|------|------|------|------|------|
|  14H |    x    |         F RESET        |
|                         | Timer A Flag Register Reset
|                         | Timer B Flag Register Reset

These 2 bits reset the contents of the flag register indicating that each timer described above has overflowed (reset with "1").

Chapter 3 Sound Functions

- IRQEN

14H:
D7 D6 D5 D4 D3 D2 D1 D0
X    IRQEN
Timer A IRQEN
Timer B IRQEN

These 2 bits register overflow occurrence from the timers into the flag register. Interrupt requests can also be made.

- CSM

14H:
D7 D6 D5 D4 D3 D2 D1 D0
CSM X
Timer A

By writing “1”, all sound slots are key-on when an overflow from timer A occurs.

<B: WRITE Busy FLAG (READ MODE)>

```
B:
D7 D6 D5 D4 D3 D2 D1 D0
```
X  X  X  X  X  X  X  X

This 1 bit is a flag indicating that it is in the middle of writing. The 68 bit time is needed from receiving the write command until the writing is completed. During this period, this flag becomes “1”. When writing data continuously, this flag must be read and confirmed to be “0” before writing the next data.

Page 110

**<IST (READ MODE)>**

**(Diagram depicting binary register)**
| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
| X  |  X  |  X  |  X  |  X  |    |IST |

**IST Description:**
Timer B Flag
Timer A Flag

These 2 bits indicate the status of the flag register. When the pin terminal IRQ is in a "0" state, it indicates that one of the two flag register bits is in a "1" state due to an overflow from Timer A or Timer B.

**1-7 Method of Compensation When the System Clock is 4 MHz**
(For using YM2203 data in YM2151)

The YM2151's tone scale is determined by the KC (KEY CODE; FM tone generator internal register 28H~2FH) and KP (KEY FRACTION; internal register 30H~37H), but when the YM2151 has a system clock of 3.579545 MHz, it stores data within the device such that the value of KF is zero. Therefore, when the system clock is 3.579545 MHz, the tone scale is determined by setting KC and changing the value.

**(Diagram depicting binary register**
| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
| 28H| X  |    |   OCT   |   NOTE   |
| 2FH| X  |    |                   (0~7)                 |

**Table 3-16 Relationship of KC and Tone Frequency when KF=0 (3.579545 MHz Clock)**

| NOTE |  C# |  D |  D# |  E |  F |  F# |  G |  G# |  A |  A# |  B |  C |  |
|-----|----|----|----|----|----|----|----|----|----|----|----|----|
|  0   |  1   |  2  |  3   |  4  |  5  | 6  |  7  | 8  |  9   | 10 | 11| 12|   

However, if you change the system clock, the tone scale value indicated will deviate.

Chapter 3: Sound Functions

log (fMX/fM) × 1200 [cents]

log (2) fMX: New system clock frequency
```
                   4 MHz
                   fM : 3.579545 MHz
```
1 cent: 1/100 [semitone]

Now, if fMX = 4 MHz,

log (4/3.579545)
× 1200 = 192.27 [cents]
log 2

That is, if the system clock frequency is changed from 3.579545 MHz to 4 MHz, the pitch will increase by approximately 192.27 cents.

■Correction Method
If the system clock frequency is changed from 3.759545 MHz to 4 MHz and KC and KF are not adjusted, there will be an automatic increase in pitch by approximately 192.27 cents. Therefore, by adjusting the value of KF to correct the pitch deviation to approximately 200 cents, the pitch level will be raised by 1 semitone, and the new pitch levels according to the KC NOTE table will be as shown below.

KC's         Frequency       Frequency       KC's NOTE
      3.579545 MHz     at 4 MHz        Value
```
0              C#                D#               6        200.56
1               D                 E                 5        198.98
2              D#                F                 6        200.71
4               E                 F#               5        199.06
5               F                 G                 5        199.79
6              F#                G#               5        199.37
8               G                A                 5        199.81
9              G#               A#               4        198.90
10              A                 B                 5        199.73
12             A#                C                 6        200.02
13              B                 C#               5        199.19
14              C                 D                 5        199.80
```

Table 3-17 Differences in Pitch Due to Clock Frequency

Therefore, at 4 MHz, the relationship between the KC value and pitch is as follows.

![Diagram]

              D7  D6 D5 D4 D3 D2 D1 D0
28H       ×  OCT   NOTE
2F(H)
                 (0~7)

NOTE  D#  E  F   F#  G  G#  A  A#  B  C  C#  D
            0    1   2    3    4   5   6    7    8    9  10 11 12 13 14

Table 3-18  Relationship between KC and pitch when KF = 0 (at 4 MHz clock)

Also, due to changes in the system clock, the lowest pitch within the same octave becomes D#. Thereafter, E, F, F# ... become higher, and D becomes even higher. Therefore, the output frequency range shifts from D# of octave 0 to D of octave 1, and compared to the case of a system clock of 3.579545 MHz, one sound lower is produced instead of one sound.

![Diagram]

```
        Octave 0                                    Octave 1
       D#                                             D
```
4 MHz frequency range
                                      C#
3.579545 MHz frequency range
```
                                       C
                1 tone                      1 tone
```

Figure 3-6 Difference in frequency range due to clock frequency

Chapter 3: Sound Functions

2. Sound Synthesis

The X68000 uses the MSM6258 in the ADPCM format as the sound synthesis LSI. In addition, PCM output control and sample rate switching are performed on port C of the 8255.

This LSI performs operations such as sound synthesis using S&H (Sampling & Hold), AD converter to PCM (Pulse Code Modulation) code conversion using ADPCM (Adaptive Differential PCM), where signal differences in consecutive samples are quantized and encoded to compress the information.

For synthesis, the reverse process is performed, restoring the original analog sound using a digital-to-analog converter (DAC).

In the sound synthesis of the X68000, the audio signal input from the line-in terminal is first converted to A/D. This data is stored in memory, then converted back from memory to D/A converting the data to audio signal, and then outputted from the line-out terminal. If the sample rate is 7.8 kHz, an audio signal for 1 minute is converted into approximately 229 Kbytes of A/D conversion data.

2-1 Features

(1) Straight 4-bit ADPCM format
(2) Built-in ADPCM recording/playback function
(3) Built-in DRAM refresh, MPU interface circuit
(4) Sampling frequencies: 3.9, 5.2, 7.8 kHz
(5) Master clock frequency: 4 MHz
(6) Built-in A/D converter: 8 bits
(7) Built-in D/A converter: 10 bits
(8) D/A output format: Class A (voltage type)

Page 114

2-2 Address Map of Sound Synthesis Registers

| Register Address |  D7  |  D6  |  D5  |  D4  |  D3  |  D2  |  D1  |  D0  | Notes |
|------------------|------|------|------|------|------|------|------|------|-------|
| E92001H          | READ | REC/ | 1    | 0    | 0    | 0    | 0    | 0    | ADPCM Status |
|                  | WRITE| 0    | 0    | 0    | REC ST | PLAY ST | SP | ADPCM Command |
| E92003H          | READ | B3  | B2  | B1  | B0  | B3  | B2  | B1  | Input Data |
|                  | WRITE| Output Data |
| E9A005H          | WRITE| IOC7 | IOC6 | IOC5 | IOC4 | Sampling Rate | PCM PAN | ADPCM Output/Sampling Frequency Switching |
| E92003H (E90001H = 1BH) | WRITE | CT2 | CT1 | x | x | x | x | WAVE FORM | ADPCM Clock Switch (FM Sound Register Port) |

Table 3-19 Sound Synthesis Register Address Map

2-3 Details of Sound Synthesis Registers

(1) ADPCM Status (READ)

|  D7  |  D6  |  D5  |  D4  |  D3  |  D2  |  D1  |  D0  |
|------|------|------|------|------|------|------|------|
|  1   |  0   |  0   |  0   |  0   |  0   |  0   |  0   |

0: ADPCM PLAY in progress
1: ADPCM RECORD in progress

(2) ADPCM Command (WRITE)

|  D7  |  D6  |  D5  |  D4  |  D3  |  D2  |  D1  |  D0  |
|------|------|------|------|------|------|------|------|
|  0   |  0   |  0   |      |  0   |      |      |      |

0: ADPCM RECORD/PLAY stopped
1: ADPCM RECORD/PLAY completed
0: ADPCM PLAY not started
1: ADPCM PLAY started
0: ADPCM RECORD not started
1: ADPCM RECORD started

Page 115

Chapter 3 Sound Functions

(3) ADPCM Sound Data (READ/WRITE)
E92003H
```
D7   D6  D5  D4  D3  D2  D1  D0
 B3  B2  B1  B0 
 
 B3: Sign Bits
 B2: MSB
 B1: SSB
 B0: LSB
```

(4) ADPCM Output (PLAY only) / Switching Sampling Frequency (WRITE)
 * In order to use this feature, set the 8255 control word register (E9A007H) to 92H in advance.
E9A005H
D7  D6  D5  D4  D3  D2  D1  D0

0: ADPCM sound output cut
1: ADPCM sound output (Left) out
1: ADPCM sound output (Right) out
1: ADPCM sound output (Left & Right) out

0: ADPCM Sampling Frequency 3.9 kHz/7.8 kHz (4MHz/8MHz)
1: ADPCM Sampling Frequency 5.2kHz/10.4kHz
1: ADPCM Sampling Frequency 7.8kHz/15.6kHz
1: Do not use (disabled)

0: Joystick No.1 Normal Operation
1: Option Function (Signal Number IC04)
 
0: Joystick No.2 Normal Operation
1: Option Function (Signal Number IC05) 
 
0: Joystick No.1 Normal Operation
1: Option Function (Signal Number IC04)

0: Joystick No.1 Normal Operation
1: Option Function (Signal Number IC06) 

However, the MSM6258 operates regardless of the data in D0 and D1. For details of the joystick, please refer to 3 of chapter 5.

2. Sound Synthesis

(5) FM sound source register data port (WRITE)
*To use this function, be sure to set 1BH (internal register) to the FM sound source register address port of YM2151 (E90001H).

  D7  D6  D5  D4  D3  D2  D1  D0
E92003H       x    x         W

WAVE FORM
CT1 ... Sound synthesis clock switching port (switching resolution frequency)
```
  0 : 8 MHz
  1 : 4 MHz
```
CT2 ... FDC forced READY port
```
  0 : FDD's READY state (normal operation)
  1 : Forced READY
```

For details, please refer to Chapters 1-6.

2-4 Sound Synthesis Access

The procedure for performing the sound synthesis is as follows.

(1) Set port C (output) of 8255 to mode 0.
   Set the E9A007H to 92H.

(2) Set the sampling frequency for ADPCM sound output (PLAY only).
   Set ADPCM sound output/sampling frequency data to E9A005H.

(3) Set the registers for each channel of 63450 DMAC (set to dual address mode in external request cycle steal mode).
   To end operations like entering a normal vector interrupt in DMAC transfer, it is necessary to insert a program to terminate ADPCM operation (set 01H to E92001H).

(4) Set the start of ADPCM PLAY (RECORD).
   For ADPCM PLAY start, set E92001H to 02H. Conversely, for ADPCM RECORD start, set E92001H to 04H.

(5) When ADPCM PLAY (RECORD) is completed and a normal vector interrupt occurs in DMAC transfer, the ADPCM operation ends during that interrupt cycle.

(blank or illegible page)

Chapter 4
Peripheral LSI

1. DMA Controller (Direct Memory Access Controller)

The X68000 uses the 63450 as its DMAC. This features 4 independent DMA channels, allocated as shown in Table 4-1 for the X68000.

| Channel Number | Assignment              | Transfer Request          | Block Transfer                      |
|----------------|--------------------------|---------------------------|------------------------------------|
| 0              | Internal 2HD             | External transfer request cycle steal mode | All channels, dual address mode   |
| 1              | Hard Disk (Optional)     | Same as above             | All channels (programmable), contiguous mode, array chain mode, link array chain mode |
| 2              | Memory                   | Auto request, related clock, maximum speed |
| 3              | Sound Synthesis          | External transfer request cycle steal mode |

Table 4-1 DMAC Channel Assignment

Diagram 4-1 DMAC Block Diagram

- 68000
```
  - Address Bus
  - Data Bus
  - Control Bus
  - CLK (10 MHz)
  - Vcc1
  - Vss
```

- 63450 DMAC
```
  - Ch 0: Internal 2HD
  - Ch 1: Hard Disk (Optional)
  - Ch 2: Memory
  - Ch 3: Sound Synthesis
```

Chapter 4 Peripheral LSI

# 1-1 Features

This DMAC has the following features. Additionally, Table 4-2 shows the DMAC transfer request methods, and Table 4-3 shows DMAC data block transfers.
1. Equipped with 4 independent DMA channels (priority order is programmable)
2. Transfer between memory, memory, and memory I/O devices
3. Supports block transfer functions in continuous, array chain, and link array chain modes
4. Programmable transfer using internal registers
5. Supports data transfer functions with high reliability including error detection, error interrupt vectors, and exception handling
6. Maximum 5M bytes/second (10 MHz)
7. 68000 bus compatible

**Table 4-2 DMAC Transfer Request Methods**

- External Transfer Request (using REQ pin)
```
  - Cycle Steal Mode: Transfers one bus round per transfer request.
  - Cycle Steal Burst-Hold Mode: Transfers one bus round per transfer request. However, the transfer period is limited.
  - Burst Mode: Transfers multiple bus rounds per transfer request.
```
- Internal Transfer Request (not using REQ pin)
```
  - Limited Burst Mode: Transfers multiple bus rounds sequentially. However, it provides the bus periodically.
  - Maximum Burst Mode: Transfers multiple bus rounds sequentially. However, it interrupts and provides the bus only when necessary.
  - Auto Request (initial bus band transfer only): External transfer request (2nd and subsequent bus band transfers)
```

**Table 4-3 DMAC Data Block Transfer**

Single Data Block Transfer:
- DMAC writes transfer address to internal register and initiates the transfer.

Multiple Data Blocks Transfer:
- Continuous Mode: DMAC writes the transfer address to internal register and initiates the transfer. Sets CNT bit to notify the presence of next data block.
- Array Chain Mode: Creates an array table in the main memory.
- Link Array Chain Mode: Creates a link array table in the main memory.

1. DMA Controller (Direct Memory Access Controller)

1-2 DMAC Register Address Map

| Ch No. | Register Address | D07 (D15) | D06 (D14) | D05 (D13) | D04 (D12) | D03 (D11) | D02 (D10) | D01 (D09) | D00 (D08) | Remarks |
|--------|-----------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|---------|
| | E84000H | COC | BTC | NDT | ERR | ACT | DIT | PCT | PCS | CSRO (Channel Status Register) |
| | E84001H | 0 | 0 | 0 | ERROR CODE | CERO (Channel Error Register) |
| | E84004H | XRM | DTYP | DPS | 0 | PCL | DCR0 (Device Control Register) |
| | E84005H | DIR | BTD | SIZE | CHAIN | REQG | OCRD (Operation Control Register) |
| | E84006H | 0 | 0 | 0 | MAC | DAC | SCRO (Sequence Control Register) |
| | E84007H | STR | CNT | HLT | SAB | INT | 0 | 0 | CCRO (Channel Control Register) |
| | E8400AH | | | | | | | | | MTCO (Memory Transfer Counter) |
| | E8400BH | | | | | | | | | MAR0 (Memory Address Register) (H) |
| | E8400CH | | | | | | | | | MAR0 (Memory Address Register) (L) |
| | E8400DH | | | | | | | | | |
| | E8400EH | | | | | | | | | |
| 0 Ch | E8400FH | | | | | | | | | |
| | E84010H | | | | | | | | | DAR0 (Device Address Register) (H) |
| | E84015H | | | | | | | | | DAR0 (Device Address Register) (L) |
| | E84016H | | | | | | | | | |
| | E84017H | | | | | | | | | BTCO (Burst Transfer Counter) |
| | E8401AH | | | | | | | | | BAR0 (Base Address Register) (H) |
| | E8401BH | | | | | | | | | BAR0 (Base Address Register) (L) |
| | E8401CH | | | | | | | | | |
| | E8401DH | | | | | | | | | NIVO (Normal Interrupt Vector) |

Page 121

Chapter 4 Peripheral LSI

| Ch No. | Register Address | D07 (D15) | D06 (D14) | D05 (D13) | D04 (D12) | D03 (D11) | D02 (D10) | D01 (D09) | D00 (D08) | Notes |   |
|--------|------------------|------------|------------|------------|------------|--------------|--------------|--------------|--------------|---------|---|
|        |                  |            |            |            |            |             |             |             |             |         |   |
| 0 Ch   | E84027H          |            |            |            |            |             |             |             |             | EIV0    | (Error Interrupt Vector Register)  |
|        | E84029H          | 0          | 0          | 0          | 0          | 0          | FC2          | FC1          | FC0          | MEC0    | (Memory Function Code Register)  |
|        | E8402DH          | 0          | 0          | 0          | 0          | 0          | 0            | 0            | ←——CP   | CPR0    | (Channel Priority Register)  |
|        | E84031H          | 0          | 0          | 0          | 0          | FC2        | FC1          | FC0          |   | DFCO    | (Device Function Code Register)  |
|        | E84039H          | 0          | 0          | 0          | 0          | FC2        | FC1          | FC0          |   | BFCO    | (Base Function Code Register)  |

| 3 Ch   | E840FFH          | 0          | 0          | 0          | 0          |   | BT           | BR           |   | GCR    | (General Control Register)  |

(Note 1) Channel No. 1 is Channel No. 0’s address + 40H
```
         Channel No. 2               "                      + 80H
         Channel No. 3               "                      + C0H
```

* CER (Channel Error Register) is Read only. Other registers can read/write

Table 4-4 DMAC Register Address Map

1-3 Details of DMAC Registers
For details of each register, please refer to the datasheet of the HD63450 series.

2. MFP (Multi Function Peripheral)

The X68000 uses the 68901, which belongs to the 68000 family, for data communication with the keyboard, various timer functions, and various interrupt controls.

Caption under the diagram:

Fig 4-2 MFP Block Diagram

Chapter 4 Peripheral LSI

2-1 Features

This MFP has the following features:
(1) Interrupt control for 16 channels (interrupts from different signals)
(2) Built-in 4 timers (Display mode 3 channels, Event count mode 1 channel)
(3) Built-in dual-channel USART for 1 channel (used for keyboard communication)

Encoders for decoding:
```
 IPL0
 IPL1      <Decoder>
 IPL2

                                                                     <68901 MFP Interrupt, Priority Channels>
```
** Priority Level **                           ** Interrupt Channel **
```
                          High  15     GPII7 (CRTC H-SYNC signal)
                                    14     GPII6 (CRTC IRQ signal)
                                    13     Timer A (CRTC V-DISP signal)
                                    12     Receive Buffer Full (Keyboard receive data)
                                    11     Receive Error (Keyboard receive data error)
                                    10     Transmit Buffer Empty (Keyboard transmit data)
                                      9     Transmit Error (Keyboard transmit data error)
                                      8     Timer B (USART serial clock)
                                    NC                                                   7     N/A
                                    6       GPIP4 (CRTC V-DISP signal)
                                    5       Timer C (8-bit customizable timer)
                                    4       Timer D (8-bit customizable timer)
                                    3       GPIP3 (FIRM main power ON signal)
                                    2       GPIP2 (POWER save mode ON/OFF signal)
                                    1       GPIP1 (Drive select/Motor ON EXPHON signal)
                          Low    0        GPIP0 (RTC ALARM signal ON/OFF output)
```

Figure 4-3 MFP Interrupt Block Diagram

2. MFP (Multi Function Peripheral)

TAI (CRTC's V-DISP signal)
8-bit counter
1/2
TAO (NC)
Event Count Mode
TACR (08H)

(4 MHz)
TBCR (01H)
Prescaler (1/4)
8-bit counter
1/2
TBO (USART serial clock)
38400 Hz

TCDR
8-bit counter
1/2
TCO (NC)

(4 MHz)
TCDCR
Prescaler
TDDR
8-bit counter
1/2
TDO (NC)

Figure 4-4 MFP Timer Block Diagram

TBO
TXD Pin
USART (x16)
SI (Keyboard Receive Data)
SO (Keyboard Send Data)
SR (Receive Data Status)
TR (Send Data Status)

Asynchronous Communication
2400 Baud
Start bit 1, Data 8 bits, No Parity, Stop bit 1

Figure 4-5 MFP USART Series Block Diagram

Ch No.

Functions Details Explanation

GPIP7
CRTC's H-SYNC signal’s rising or falling edge triggers an interrupt (set "0" in the active edge register).

GPIP6
If an interrupt occurs at the address set in CRTC's R09 (EB0012H), it triggers an interrupt due to the rising or falling edge of the IRQ signal (set "0" in the active edge register when CRTC IRQ signal's rising or falling edge triggers an interrupt).

Timer A
When V-DISP signal from the CRTC is input into Timer A (Event Count Mode), triggers an interrupt at pre-set counts (interrupts are generated either at the rising or falling edge of the input signal or rising and falling edges generate an interrupt and set a value to the down counter, decrease the 8-bit down counter from the set value and upon reaching 00H, an interrupt is generated).

Receive Buffer Full
When data is received from the keyboard, an interrupt occurs when the data is transferred from the receive register to the receive buffer and D07 of the receive buffer register becomes "1".

# Chapter 4 Peripherals LSI

| Channel No. | Function | Details |
|-------------|-----------|---------|
| Receive Error       | When data is received from the keyboard, an error (overrun error, parity error, synchronization error, pre-election error) occurs. (When receive data register D6, D5, D3 are 1). |
| Transmit Buffer Empty | When data is sent to the keyboard (when the send data is sent from the send buffer to the shift register and the send data register D7 becomes 1), an interrupt occurs. |
| Transmit Error     | When keyboard data is sent and an error (overrun error or synchronization error) occurs, an interrupt occurs. (When send data register D6 or D4 is 1). |
| Timer B            | Reservation lock (4 MHz). When a timer (delay mode) is assigned, an interrupt occurs when the count of the internal clock reaches 38,400 Hz. However, since it is used as a reservation lock for the keyboard, the interrupt will not occur. |
| GPI4               | Reads the status of the V-DISP signal from CRTC. "1" indicates "H", and stops the motor while being cleared periodically. When "0", it continues to perform high-speed data transfer processing. (Interrupt not possible). |
| Timer C            | Reservation lock (4 MHz). When a timer (delay mode) is assigned, it uses the low-speed mode scan clock. When the datum counter reaches 00H, it generates an interrupt. |
| Timer D            | Reservation lock (4 MHz). When a timer (delay mode) is assigned, it uses the low-speed mode scan clock. When the datum counter reaches 00H, it generates an interrupt. |
| GPI3               | Generates an interrupt at the falling edge of the FM reset IRQ signal. |
| GPI2               | POWER switch (main computer power switch). Determines whether the computer's power supply (Vcc1) has been turned on. Normally, the POWER switch is "OFF" when "0" is read, and "ON" when "1" is read. However, in the case of the POWER switch, use the usual method of processing the signal to determine whether secondary power distribution is turned on or not. |
| GPI1               | Reads the EXPON signal using expansion I/O slots to determine whether the computer's power supply (Vcc1) has been turned on. Normally, it is considered "OFF" when "0" is read, and "ON" when "1" is read. However, if the computer's main power supply is "OFF" or "0", it cannot enter "1". Normally, it becomes "0". If the MPU can read the GPI1 port, and the EXPON signal from the expansion I/O slot is read as "ON", it continues as normal. |
| GPI0               | Generates an RTC ALARM signal to check whether an ALARM signal (alarm set in ON) is issued to the computer's power supply (Vcc1) or not. Normally, when "0" is read, it is "OFF", and when "1" is read, it is "ON" roughly every 16 seconds, even if the computer is turned off. If the ALARM signal has not been generated by the computer's main power supply, it cannot read "1". If the ALARM signal is "OFF", it renders the status. |

**Table 4-5 Detailed MFP Channel Specifications**

**2. MFP (Multi Function Peripheral)**

**[Power ON/OFF and LED]**

Vcc1 turns ON

Check the contents of SRAM and the validity of the timer

**Timer valid**
**Timer invalid**

**TIMER LED turns ON**
    (RTC register address EA8001H (BANK 1; Main text 4 reference) write 00H)

**TIMER LED does not turn ON**
    (RTC register address EA8001H (BANK 1; Main text 4 reference) write 07H)

Check MFP's GPIO2

**POWER Switch** turned ON
    Check MFP's GPIO1

**Timer valid**
**Timer invalid**

**TIMER LED turns ON**
    (RTC register address EA8001H (BANK 1; Main text 4 reference) write 00H)
**TIMER LED does not turn ON**
    (RTC register address EA8001H (BANK 1; Main text 4 reference) write 07H)

Check MFP's GPIO2

**"0"**

Turned ON by EXPWON signal from Extension I/O slot
**Check MFP's GPIO0**

**"0"**
**"1"**

Jump to RTC’s ALARM timer, turned ON by ALARM signal

If (1) is not met, use GPIO2, GPIO1, and GPIO0 to create and check the power control loop. Then, write the system port EB800FH with "0H" "0H" "FH" to POWER OFF

**Fig 4-6** Flowchart for checking power ON.

Chapter 4 Peripheral LSI

2-2 MFP Register Address Map

| Register Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | Remarks |
|-----------------|-----|-----|-----|-----|-----|-----|-----|-----|---------|
| E88001H         | GPIP7 | GPIP6 | GPIP5 | GPIP4 | GPIP3 | GPIP2 | GPIP1 | GPIP0 | GPIP Data Register (Read only) |
| E88003H         | "    | "    | "    | "    | "    | "    | "    | "    | Active Edge Register (AER)     |
| E88005H         | "    | "    | "    | "    | "    | "    | "    | "    | Data Direction Register (DDR)  |
| E88007H         | GPIP7 | GPIP6 | Timer Buffer A | RCV Full | Error | Empty | XMIT Buffer | Timer B | Interrupt A Enable Register A (IERA) |
| E88009H         | GPIP5 | GPIP4 | Timer C | Timer D | GPIP3 | GPIP2 | GPIP1 | GPIP0 | Interrupt A Enable Register B (IERB) |
| E8800BH         | RCV  | XMIT | GPIP7 | GPIP6 | Timer Buffer A | RCV Full | Error | Empty | Interrupt Pending Register A (IPRA) |
| E8800DH         | GPIP5 | GPIP4 | Timer C | Timer D | GPIP3 | GPIP2 | GPIP1 | GPIP0 | Interrupt Pending Register B (IPRB) |
| E8800FH         | RCV  | XMIT | GPIP7 | GPIP6 | Timer Buffer A | RCV Full | Error | Empty | Interrupt Service Register A (ISRA) |
| E88011H         | GPIP5 | GPIP4 | Timer C | Timer D | GPIP3 | GPIP2 | GPIP1 | GPIP0 | Interrupt Service Register B (ISRB) |
| E88013H         | RCV  | XMIT | GPIP7 | GPIP6 | Timer Buffer A | RCV Full | Error | Empty | Interrupt Mask Register A (IMRA) |
| E88015H         | GPIP5 | GPIP4 | Timer C | Timer D | GPIP3 | GPIP2 | GPIP1 | GPIP0 | Interrupt Mask Register B (IMRB) |
| E88017H         | V7   | V6   | V5   | V4   | S    | *    | *    | * | Vector Register |
| E88019H         | Reset | AC3 | AC2 | AC1 | AC0 | TAO  | *  | *  | Timer A Control Register (TACR) |
| E8801BH         | Reset | BC3 | BC2 | BC1 | BC0 | TAO | BCO  | *  | Timer B Control Register (TBCR) |
| E8801DH         | CC2  | CC1  | CC0  | *  | *  | DC2 | DC1 | DCO | Timer C, D Control Register (TCDCR) |
| E8801FH         | D7   | D6   | D5   | D4   | D3   | D2   | D1   | D0   | Timer A Data Register (TADR)  |
| E88021H         | "    | "    | "    | "    | "    | "    | "    | "    | Timer B Data Register (TBDR)  |
| E88023H         | "    | "    | "    | "    | "    | "    | "    | "    | Timer C Data Register (TCDR)  |
| E88025H         | "    | "    | "    | "    | "    | "    | "    | "    | Timer D Data Register (TDDR)  |

Page 128

2. MFP (Multi Function Peripheral)

Name   | Description
E88027H | Concurrent Character Register (Unused)
E88029H | USART Control Register (UCR)
E8802BH | Receiver Status Register (RSR)
E8802DH | Transmitting Status Register (TSR)
E8802FH | USART Data Register (UDR)

**Table 4-6 MFP Register Address Map**

Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | Description
E88001H |   GPIP Data Register (Read Only)
E88003H | P | P | P | P | P | P | P | P | Active Edge Register (AER)
E88005H | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | Data Direction Register (DDR)
E88007H | P | P | P | P | P | P | P | 1 | Interrupt Enable Register A (IERA)
E88009H | P | P | 1 | 0 | P | P | P | P | Interrupt Enable Register B (IERB)
E8800BH | . | . | P | . | . | . | . | P | Active Pending Register A (IPRA)
E8800DH | P | P | 1 | . | . | . | P |   | Active Pending Register B (IPRB)
E8800FH | 1 | P | P | P | . | . | . | P | In-Service Register A (ISRA)
E88011H | . | . | 1 | . | P | . | P | 0 | In-Service Register B (ISRB)
E88013H | P | 0 | P | P | 0 | 0 | 0 |   | Mask Register A (IMRA)
E88015H | 0 | 1 | P | 1 | 1 | 0 | 0 | 1 | Mask Register B (IMRB)
E88017H | 1 | P | . | . | P | . | . | P | Interrupt Vector Register (IVR)
E88019H | 0 | 0 | 0 | 1 | 0 | P | P | 0 | Timer Control Register A (TACR)
E8801BH | 0 | P | 0 | 0 | 0 | 1 | 0 | 0 | Timer Control Register B (TBCR)
E8801DH | P | 0 | 0 | 0 | 0 | P | 0 | 1 | Control Register for Timer A, C, D (TCDCR)
E8801FH | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | Timer Data Register A (TADR)
E88021H | P | P | P | P | . | P | P | P | Timer Data Register B (TBDR)
E88023H | P | P | P | P | P | P | P | P | Timer Data Register C (TCDR)
E88025H | 0 | P | 0 | P | 1 | 0 | 1 | 0 | Timer Data Register D (TDDR)
E88027H | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | Concurrent Character Register (Unused)
E88029H | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | USART Control Register (UCR)
E8802BH | . | . | P | . | . | P | P | P | Receiver Status Register (RSR)
E8802DH | . | . | . | P | . | P | 0 | P | Transmitting Status Register (TSR)
E8802FH | P | . | . | P | 0 | P | 0 | 0 | USART Data Register (UDR)

In the above, "P" denotes "programmable."

**Table 4-7 MFP Register Reset Values**

Chapter 4 Peripheral LSI

2-3 Detailed Information on MFP Registers

(1) GPIP Control

· GPIP Data Register (E88001H)
The MFP's GPIP port (8 bits) can be designated as a regular port or an interrupt port on a per-bit basis. In the X68000, GPIP0 and GPIP1 are used as read-only ports using timer A in event count mode, GPIP4 is also read-only using timer A, and GPIP2, GPIP6, and GPIP7 (GPIP0) can be used as interrupt ports (GPIP5 is not used). In any case, all bits are read-only. However, all bits will be 0 at reset.

D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0
*  |    |    |    |    |    |    |    |  (Not used)

0: RTC or ALARM signal "L" (turns computer on by ALARM timer)
1: RTC or ALARM signal "H"
0: Expansion I/O slot EXPON signal "L"
1: Expansion I/O slot EXPON signal "H"
0: Front switch on computer "L"
1: Front switch on computer "H"
0: Front switch signal OFF "H"
1: Front switch signal ON "L"
0: CRTC C video interruption (frame initialization) "H"
1: CRTC C video interruption (frame initialization) "L"
0: CRTC D video non-display period "L"
1: CRTC D video non-display period "H"
0: CRTC C IRQ signal "H"
1: CRTC C IRQ signal "L"
0: CRTC D IRQ signal "H"
1: CRTC D IRQ signal "L"
0: CRTC D H-SYNC signal "H"
1: CRTC D H-SYNC signal "L"

·Active Edge Register (E88003H)

D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0
*  |    |    |    |    |    |    |    |  (Not used)

0: RTC or ALARM signal health, interrupt occurs with rising edge
1: RTC or ALARM signal health, interrupt occurs with falling edge
0: Expansion I/O slot EXPON signal health, interrupt occurs with rising edge
1: Expansion I/O slot EXPON signal health, interrupt occurs with falling edge
0: Power switch off condition "0", interrupt occurs at rising edge
1: Power switch off condition "1", interrupt occurs at falling edge
0: Image reply IRQ signal number 1 "1", interrupt occurs at rising edge
1: Image reply IRQ signal number 1 "1", interrupt occurs at falling edge
0: Timer (CRTC C V-DISP) signal issue when "1", interrupt occurs at rising edge
1: Timer (CRTC C V-DISP) signal issue when "0", interrupt occurs at falling edge
0: CRTC C IRQ signal "H", interrupt occurs at rising edge
1: CRTC C IRQ signal "L", interrupt occurs at falling edge
0: CRTC D IRQ signal "H", interrupt occurs at rising edge
1: CRTC D IRQ signal "L", interrupt occurs at falling edge
0: CRTC D H-SYNC signal "H", interrupt occurs at rising edge
1: CRTC D H-SYNC signal "L", interrupt occurs at falling edge

However, all bits will be 0 at reset.

Page 130

2. MFP (Multi Function Peripheral)

- Data Direction Register (E88005H)
Specifies the input and output of the GPIP port. On the X68000, all 8 bits are used as input, so 00H is set in E88005H. However, all bits are reset to 0 initially.

(2) Interrupt Control

- Interrupt Enable Register A (E88007H)
a. When the corresponding bit is set (1):
To enable the interrupt, write 1.

b. When the corresponding bit is cleared (0):
To disable the interrupt, write 0 (the relevant bit in IPRA also becomes 0).

```
Diagram:
D7    D6    D5    D4    D3    D2    D1    D0
  ↓     ↓     ↓     ↓     ↓     ↓     ↓     ↓
```
```
1 : TimerB Interrupt Enable   0: TimerB Interrupt Disabled (Normal)
1 : TimerA Interrupt Enable   0: TimerA Interrupt Disabled (Normal)
1 : Transmit Error Interrupt Enable/Disable
1 : Transmit Buffer Empty Interrupt Enable/Disable
1 : Receive Error Interrupt Enable/Disable
1 : Receive Buffer Full Interrupt Enable/Disable
1 : TimerA Interrupt Enable/Disable (Normal)
1 : GPIP7 Interrupt Enable/Disable
1 : GPIP6 Interrupt Enable/Disable
1 : GPIP1 Interrupt Enable/Disable
1 : GPIP0 Interrupt Enable/Disable
```

Chapter 4 Peripheral LSI

- Interrupt Enable Register B (E88009H)
```
  a. When the corresponding bit is set (1)
    * To make the interrupt channel enable, write 1.
  b. When the corresponding bit is cleared (0)
    * To make the interrupt channel disable, write 0 (the corresponding bit in IPRA will also become 0).
    * When reset.

D7 D6 D5 D4 D3 D2 D1 D0
 │   │  │   │   │   │   │   │
 ├──┘ └──┬──┘  │   │  │   │  
 │        │   │   │   │   │
 0: GPI0 Interrupt Enable (Normal)
 1: GPI0 Interrupt Disable
 0: GPI1 Interrupt Enable (Normal)
 1: GPI1 Interrupt Disable
 0: GPI2 Interrupt Enable (Normal)
 1: GPI2 Interrupt Disable
 0: GPI3 Interrupt Enable (Normal)
 1: GPI3 Interrupt Disable
 0: TimerB Interrupt Enable (Normal)
 1: TimerB Interrupt Disable
 0: TimerC Interrupt Enable (Normal)
 1: TimerC Interrupt Disable
 0: GPI4 Interrupt Enable (Normal)
 1: GPI4 Interrupt Disable
 0: GPI5 Interrupt Enable (Normal)
 1: GPI5 Interrupt Disable
```

- Interrupt Pending Register A (E88008H), B (E8800DH)
```
  This register cannot be cleared (0) or set (1) by the MPU. The corresponding bits for interrupt channels are also the same as IERA and IERB.
  a. When the corresponding bit is set (1)
    * When the corresponding bit of IERA (IERB) is 1 (enable) and interrupts the channel.
     However, in this state, if the corresponding bit of IMRA (IMRB) is 0 (masked), the corresponding bit of IPRA (IPRB) is set (1).
  b. When the corresponding bit is cleared (0)
    * When writing 0 (disable) to the corresponding bit of IERA (IERB).
    * The pending interrupt is passed to the MPU, and the interrupt vector passed to the MPU during the IACK cycle.
    * Writing 0 to the corresponding bit, and writing 1 to all bits other than the corresponding bit.
    * When reset.
```

2. MFP (Multi Function Peripheral)

- Interrupt Service Register A (E8800FHD), B (E88011HD)
This register can be set (1) but cannot be cleared (0) by the MPU. The assignment of the interrupt channel to each bit is the same as IERA and IERB.
a. When the corresponding bit is set (1),

* When the corresponding bit is set, the interrupt vector is sent to MPU during the IACK cycle and the MPU starts interrupt processing. After that, when the D03 bit of the interrupt vector register becomes 0 during automatic interruption of all channels (meaning the automatic interruption has finished), the corresponding bit is forcibly set to 0 after the interrupt processing is completed by MPU.
In automatic end mode for all channels, at the time of receiving some channel interrupt requests, during interrupt processing at the highest priority within MPU, MFP cannot receive such interrupt requests. When the interrupt is masked in such a condition that the interrupt enable register of the corresponding channel is set (1) and the interrupt pending register of the corresponding bit is set (1) while MFP is performing other interrupt processing or after completing automatic processing at the end of NMI, MFP won't receive such interrupt requests. When the interrupt mask register of the corresponding channel has been set to (1), the lower priority interrupts will not be received during interrupt processing at the resolution mode at such stage of interrupt request reception. Similarly, the interrupt vector register also has been set (1) and waits for interrupt services.

By the same, if the bit of the interrupt vector register D03 bit becomes 1 during the automatic termination mode for all-channel software interrupts, at last just like the mode stated above, the interruption processing ends and the associated bit is forcedly set to 0 if the MPU ends current interrupt and software processing.
In this way, the registered bit remains set (1). The interrupt processing does not end until the software ends the interrupt process by setting the corresponding bit manually to 0.
For the interrupt requests of high priority which are waiting for the acceptance among other interrupt requests, the corresponding channels' interrupt enabling register is set (1) while NMI executes the ongoing interrupt process, the higher priority's interrupt's pending register set (1) and further interrupt processing will proceed for subsequent requests till it completes at the software end accordingly.

Chapter 4 Peripheral LSI

If a channel Mi requests the MPU, and the request is accepted, the interrupt processing is executed. If however, there is no "1" in the bit of the interrupt service system for the corresponding interrupt, other interrupts are not accepted.

b. When the corresponding bit is cleared (0)
When the D03 bit of the interrupt vector register DO is 0 (All-channel auto interrupt completion mode), interrupt processing begins in the MPU and finishes when the processing is completed.
When the interrupt vector register is set to 0, write a "1" to all bits except the corresponding bit.
When it is reset.

- Interrupt Mask Register A (E88013H), B (E88015H)
For the assignment of each interrupt channel to each bit, as with IERA and IERB.

a. When the corresponding bit is set (1)
To clear the interrupt mask, write a 1.

b. When the corresponding bit is cleared (0)
To mask the interrupt, write a 0 again. However, if the corresponding bit of IERA (IERB) is "1" (enabled) and masked, and the interrupt goes through, a "1" is written in the corresponding bit of IPRA (IPRB).
When it is reset.

- Interrupt Vector Register (E88017H)

0: All-channel auto interrupt completion mode
1: All-channel software interrupt completion mode (ISRA, ISRB enabled)
The interrupt vector is 7 bits.
(The bottom 4 bits correspond automatically to the MEP (0-16) for each interrupt channel number)

However, when reset all bits are set to 0.

2. MFP (Multi Function Peripheral)

(3) Timer

- Timer A Control Register (E88019H)
D7 D6 D5 D4 D3 D2 D1 D0
0  0  0  1  0  0  0  0
Timer A Event Count Mode
0: Do not reset TAO signal
1: Reset TAO signal

However, when resetting, all bits will be 0.

- Timer B Control Register (E8801BH)
D7 D6 D5 D4 D3 D2 D1 D0
0  0  0  0  1  0  0  1
Timer B Delay Mode (1/4 Prescaler)
0: Do not reset TBO signal
1: Reset TBO signal

However, when resetting, all bits will be 0.

- Timer C, D Control Register (E8801DH)
D7 D6 D5 D4 D3 D2 D1 D0
0  0
00: Timer D Stop (Count Prohibited)
01: Timer D Delay Mode (1/4 Prescaler)
02: Timer D Delay Mode (1/10 Prescaler)
03: Timer D Delay Mode (1/16 Prescaler)
04: Timer D Delay Mode (1/50 Prescaler)
05: Timer D Delay Mode (1/64 Prescaler)
06: Timer D Delay Mode (1/100 Prescaler)
07: Timer D Delay Mode (1/200 Prescaler)

However, when resetting, all bits will be 0.

Page 135

Chapter 4 Peripheral LSI

- Timer A Data Register (E8801FH): Set the down-counter value to generate an interrupt in Timer A (interrupt level 13). When an interrupt occurs, the register will be set to 00H.

- Timer B Data Register (E88021H): Please set 0DH (cannot be interrupted as it generates a keyboard serial clock).

- Timer C Data Register (E88023H): Set the down-counter value to generate an interrupt in Timer C (interrupt level 5). When an interrupt occurs, the register will be set to 00H.

- Timer D Data Register (E88025H): Set the down-counter value to generate an interrupt in Timer D (interrupt level 4). When an interrupt occurs, the register will be set to 00H.

(4) USART (Serial Communication with Keyboard)

- USART Control Register (E88029H)
In X68000, asynchronous communication using the USART function of MFP is used for communication with the sub-CPU 80C51 in the keyboard, and for keyboard data input. This asynchronous communication is conducted in the following sequence.

1. Input a clock 16 times larger to the MFP RC, TC terminal.
2. Set the baud rate to 2400.
3. Set 1 start bit, data 8 bits, no parity, and 1 stop bit.

(* Invalid during WRITE, during READ only [0] can be read)

However, upon reset, all bits will be set to 0.

2.  MFP (Multi Function Peripheral)

- Receive Status Register (E8802BH)

| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|---|---|---|---|---|---|---|---|
| - | - | - | - | - | - | - | 0 |

When "0" is written, all flags are cleared, and the register becomes readable.
When "1" is written, this register is in the "4F" readable state.

| Flag | Description |
|------|-------------|
| D0    | 1: Start bit received |
| D1    | 1: Frame error detection (unable to detect stop bit) |
| D2    | 1: Receive frame error (unable to detect stop bit) |
| D3    | 1: Break Detection (hardware detects Break condition) |
| D4    | 1: Overrun error |
| D5    | 1: Parity error |
| D6    | 1: Overrun error |
| D7    | 1: Receive buffer full |

Note that when D7 = "1" (buffer full), D6 = "1" (overrun error), or D5 = "1" (parity error), D3 = "1" (break detect) occurs, a Receive Error (MFP level 11 interrupt) occurs. Also, even if the receive error interrupt is disabled, the full receive buffer interrupt will still occur. However, all bits will be reset to 0 during reset.

Chapter 4 Peripheral LSI

- Transmission Status Register (E8802DH)

```
  | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |

  - When "0" is set and D6="0", D4="1", the transmitter becomes disabled.
  - When "1" is set, it becomes a transmit signal enable. At this time, 1 bit is added before the data transmission starts.
  - Normal transmission operation:
  1. Send a break character (character of all 8 bits 0 with stop bits).
      Note: At this time, since D7 is not set, please be careful.
  2. When D0=1 (transmit disable flag), the character to be transmitted immediately follows the transmission.
  3. When D0=0 (transmit disable flag) is set (in case the data byte sending with sending data is ongoing).
  4. When D0=0 (transmit disable flag), normal transmission state:
     - When "1" is set, bit "1" at this time becomes the transmit disable flag and a break character is transmitted.
     - After the transmission is completed, it automatically becomes a signal line mark (RNS D0=0).
  5. When the Transmission Shift Register (TSR) is empty and the transmitter becomes disabled (D0=0).
  6. Transmission error occurrence (occurred at MFP 9 level when D0 (L=L) is reached):
     1. When a transmit error is detected within the Transmission Shift Register (TSR), data transmission is suspended.
     2. Transmit data (RNR RRN RDN EXC) transmission character stream when a transmit data character error frame was detected.
  7. Transmission Buffer (TBU) is empty or an error is detected in the transmission data character stream.

  Note: When D7="1" (buffer empty), a Transmit Buffer Empty (MFP 10 level interrupt) occurs, and when D6="1" (under-run error) or D4="1" (transmission end state), a Transmit Error (MFP 9 level interrupt) occurs. However, at the time of reset, all bits become 0.
```

- USART Data Register (E8802FH)
  It is an 8-bit input/output data register of USART.

3. SCC (Serial Communication Controller) 

The X68000 uses the Z8530 SCC of the Z8000 family as the serial communication controller to support the RS-232C mouse. Also, Figure 4-7 shows the block diagram.

3-1 Features

This SCC has two independent double channels, each with 14 write registers, seven read registers, and baud rate generators.

(1) Channel A (RS-232C)
● Asynchronous Mode
- 5, 6, 7, 8 bits/character
- 1, 1.5, 2 stop bits/character
- Odd parity, even parity, no parity
- x1, x16, x32, x64 clock mode
- Detection of break and loss
- Detection of parity, overrun, framing errors

● Synchronous Mode
- Byte-synchronous mode: Character synchronization can be either internal or external
```
  1 or 2 synchronous characters
  6 or 8-bit synchronous character support
  Deletion of appended synchronized characters
  Generation and checking of CRC
```
- SDLC/HDLC Mode: Generation and detection of abort sequence 
```
  Automated insertion and deletion of zeros
  Automated flag insertion in message field
  Detection of address field
  Information field bits processing
  Generation and checking of CRC
  Escape and detection for EOP check in SDLC loop mode (On-line)
```

- Data transfer rate:
```
  Maximum 1.5 Mbps (asynchronous, NRZ)
  Maximum 375 Kbps (FM character mode, DPLL) 
  Maximum 187 Kbps (NRZI character mode, DPLL)
```

Chapter 4 Peripheral LSI

(2) Channel B (Mouse)
● Asynchronous Communication
- Baud Rate ............. 4800 Baud
- Start Bit ............. 1 Bit
- Data Bit .............. 8 Bits
- Parity .................... None
- Stop Bits ........... 2 Bits
- Data Bus ................. RxDB
- Control Bus ....... RTSB

Mouse Connector Jack
Mouse
Keyboard
RS-232C

Fig. 4-7 SCC Block Diagram

Page 140

3. SCC (Serial Communication Controller)

3-2 SCC Register Address Map

(All registers are READ/WRITE)

| Ch. No. | Register Address |  D07  |  D06  |  D05  |  D04  |  D03  |  D02  |  D01  |  D00  | Notes       |
|:-------:|:----------------:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|------------|
|    B    |     E98001H      |       |       |       |       |       |       |       |       | Command Port |
|    B    |     E98003H      |       |       |       |       |       |       |       |       | Data Port   |
|    A    |     E98005H      |       |       |       |       |       |       |       |       | Command Port |
|    A    |     E98007H      |       |       |       |       |       |       |       |       | Data Port   |

Table 4-8  SCC Register Address Map

3-3 SCC Register Details

For details of each register, please refer to materials such as the Z8530 SCC data sheet. Table 4-9 shows the clock counts for each baud rate in the Baud Rate Generator.

| Baud Rate | Clock Count at 5 MHz | Notes                                        |
|:---------:|:---------------------:|:--------------------------------------------:|
|   9600    |         14 (000EH)     | 5×10^6                                      |
|   4800    |         31 (001FH)     | Clock Count = 2× (Baud Rate ×16) - 2        |
|   2400    |         63 (003FH)     |                                              |
|   1200    |         128 (0080H)    |                                              |
|   600     |         258 (0102H)    |                                              |
|   300     |         519 (0207H)    |                                              |
|   150     |        1040 (0410H)    | However, assuming input clock (PCLK) is 5 MHz |
|   75      |        2081 (0821H)    | and the data rate is 16 times, the correct clock is used. |

Table 4-9  Clock Counts for Baud Rate Generator

(Note) Access to each write/read register (excluding write-only register WR8 and read-only register RR8) is performed as follows:
1. Using the command port, set the bit data of D02 to D00 in the addressable write register WR0. This designates the register to be accessed.

Chapter 4: Peripheral LSI

2. Next, if you write control data to the command port, read it out, or access the various registers, it will function. Additionally, by accessing the data port regarding write register WR8 and read register RR8, you can write data or read it out.

4. RTC (Real Time Clock)

In X68000, the RP5C15 is used as the real-time clock.

[Diagram]

Figure 4-8 RTC Block Diagram

4-1 Features

The RP5C15 is a real-time clock that can be read/written in the same way as memory, and allows setting and reading out the time. It has the following features:

1. Direct connection to a 16-bit CPU enables high-speed access.
2. 4-bit bidirectional data bus (D0D~D03).
3. 4-bit address input.
4. Built-in count for time (hours, minutes, seconds) and calendar (leap year, year, month, day, day of the week).
5. Alarm function included.
6. All time data is represented in BCD code.
7. 30-second adjustment function included.
8. Battery backup is possible (minimum of 2.0V).
9. Outputs a 16 Hz or 1 Hz timing pulse for alarm usage.
10. Outputs a 1 Hz clock.

4. RTC (Real-Time Clock)

In particular, on the X68000, the alarm function and clock output of the RP5C15 are used as follows:

- Alarm Function (Alarm Timer)
This is used to set the reservation time for turning on the computer's power (Vcc1 ON). When the set date and time match the internal clock of the computer, the computer's power turns on and the alarm terminal outputs an alarm signal (signal that is output every 16 Hz or 1 Hz from the clock). This signal is read and input into a terminal such as MFP or GPIO5 (Level Interrupt Input). Once input, software processing can select the output signal from the alarm terminal, and it may be input to the MFP as an interrupt signal. Also, when setting the alarm timer, in addition to writing 00H into E8A001H for TIMER LED OFF (BANK1), system reset E8B00DH should write 31H and make the SRAM writable. After that, information that SRAM TIMER LED OFF (E8A001H bit information) is set, finally resetting the system should write 00H into E8B00DH and make the SRAM read-only. (This processing is necessary due to the write protection until Vcc2 is directly connected in the MFP.)

- Clock Output
1 Hz clock is output from the CLOCKOUT terminal and it is input into MFP or GPIO5 (Level Interrupt Input) terminals. This signal can also be input as an interrupt signal to the MFP. In addition, this 1 Hz signal is used for lighting and turning off the main body front panel's POWER LED and TIMER LED. For details on the LEDs, please refer to Chapter 5-3. Furthermore, for RP5C15 backup purposes, the normal battery for Vcc2 is connected, so if using the timer, do not turn off the rear power switch.

Chapter 4 Peripheral LSI

4-2  Address Map of the RTC Registers

Tables 4-10 and 4-11 show the register address map of the RTC. Note that * indicates that the bit is invalid on WRITE and always reads as 0 on READ.
However, E8A001H of BANK 1 is used to set the TIMER LED, so be careful of the bit states when writing to it.

<BANK 0>

| Register Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | Remarks |
|----|-------|------|------|------|------|------|------|------|----|
| E8A001H | * |  |  |  |  |  |  | | 1-second counter (READ/WRITE) |
| E8A003H | * |  |  |  |  |  |  | | 10-second counter (READ/WRITE) |
| E8A005H | * |  |  |  |  |  |  | | 1-minute counter (READ/WRITE) |
| E8A007H | * | * | * |  |  |  |  | | 10-minute counter (READ/WRITE) |
| E8A009H | * | * | * |  |  |  |  | | 1-hour counter (READ/WRITE) |
| E8A00BH | * | * | * | * |  |  |  | | 10-hour counter (READ/WRITE) |
| E8A00DH | * | * |  |  |  |  |  | | day-of-week counter (READ/WRITE) |
| E8A00FH | * | * |  |  |  |  |  | | 1-day counter (READ/WRITE) |
| E8A011H | * | * | * | * |  |  |  | | 10-day counter (READ/WRITE) |
| E8A013H | * | * |  |  |  |  |  | | 1-month counter (READ/WRITE) |
| E8A015H | * | * | * |  |  |  |  | | 10-month counter (READ/WRITE) |
| E8A017H | * | * | * | * |  |  |  | | 1-year counter (READ/WRITE) |
| E8A019H | * | * | * | * |  |  |  | | 10-year counter (READ/WRITE) |
| E8A01BH | * | * |  |  |  |  |  | | MODE register (READ/WRITE) |
| E8A01DH | * |  |  |  | 0 | 0 | 0 | 0 | TEST register (WRITE) |
| E8A01FH | * |  |  |  |  |  |  | | RESET control, etc. (WRITE) |

Table 4-10  RTC Register Address Map (1)

4. RTC (Real Time Clock)

<BANK 1>
| Register Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | Remarks |
|-----------------|-----|-----|-----|-----|-----|-----|-----|-----|---------|
| E8A001H | * | * | * | * | 1 | 0 | 0 | 1 | CLKOUT Register (READ/WRITE) 1 Hz signal output (rising edge counts up the clock, duty 50%) |
| E8A003H | * | * | * | * | * | * | * | * | Adjust (READ/WRITE) |
| E8A005H | * | * | * | * | * | * | * | * | Alarm 1-minute Register (READ/WRITE) |
| E8A007H | * | * | * | * | * | * | * | * | Alarm 10-minute Register (READ/WRITE) |
| E8A009H | * | * | * | * | * | * | * | * | Alarm 1-hour Register (READ/WRITE) |
| E8A00BH | * | * | * | * | * | * | * | * | Alarm 10-hour Register (READ/WRITE) |
| E8A00DH | * | * | * | * | * | * | * | * | Alarm day-of-week Register (READ/WRITE) |
| E8A00FH | * | * | * | * | * | * | * | * | Alarm 1-day Register (READ/WRITE) |
| E8A011H | * | * | * | * | * | * | * | * | Alarm 10-day Register (READ/WRITE) |
| E8A013H | * | * | * | * | * | * | * | * | (unused) |
| E8A015H | * | * | * | * | * | * | * | * | 12-hour / 24-hour Selector (READ/WRITE) |
| E8A017H | * | * | * | * | * | * | * | * | Leap-year Counter (READ/WRITE) |
| E8A019H | * | * | * | * | * | * | * | * | (unused) |
| E8A01BH | * | * | * | * | * | * | * | * | MODE Register (READ/WRITE) |
| E8A01DH | * | * | * | 0 | 0 | 0 | 0 | 0 | TEST Register (WRITE) |
| E8A01FH | * | * | * | * | * | * | * | * | RESET Controller etc. (WRITE) |

Table 4-11  RTC Register Address Map (2)

Page 145

Chapter 4 Peripheral LSI

4-3 Details of RTC Registers

- When 00H is written to BANK 1 at E8A001H, the TIMER LED will light up (turn on). When 07H is written, the TIMER LED will turn off (WRITE only).

- Registers from E8A001H to E8A019H in BANK 0 are used for date and time settings (BCD code).

- Registers from E8A005H to E8A011H in BANK 1 are used for alarm date and time settings (BCD code).

- BANK 1 E8A003H

D7 D6 D5 D4 D3 D2 D1 D0
*  *  *  *  *  *  *  0: Adjust OFF
                       1: Adjust ON (if adjusted within 0 to 29 seconds of counter counting seconds, seconds become 0. If adjusted within 30 to 59 seconds, seconds become 0 and minutes are incremented by 1).

- BANK 1 E8A015H

D7 D6 D5 D4 D3 D2 D1 D0
*  *  *  *  *  *  *  0: 12-hour format (select PM with E8A00BH bit D1=1, select AM with D1=0)
                       1: 24-hour format

- BANK 1 E8A017H

D7 D6 D5 D4 D3 D2 D1 D0
*  *  *  *  *  0  0  0: This year is a leap year
```
                       1: 1 year after the last leap year
                       2: 2 years after the last leap year
                       3: 3 years after the last leap year (next year is a leap year) (Auto-increment occurs every 4 years unless correctly initialized, battery is replaced and year count does not stop. Auto-increment occurs until 2099).
```

4. RTC (Real Time Clock)

• E8A01BH

D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0
• | • | • | • | • | | | 
0: BANK 0 Select
1: BANK 1 Select
0: Alarm Output Disable (except 16 Hz and 1 Hz signals)
1: Alarm Output Enable
0: Stopwatch Counter Stop
1: Stopwatch Start

• E8A01DH

When all bits D3 to D0 are "0", normal clock operation is possible.

• E8A01FH

D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0
• | • | • | • | | | | 
0: Alarm Register Reset OFF
1: Alarm Register Reset ON
0: Stopwatch Time Limit Reset OFF
1: Stopwatch Time Limit Reset ON
0: Alarm Terminal 16 Hz Clock Pulse Output ON
1: Alarm Terminal 16 Hz Clock Pulse Output OFF
0: Alarm Terminal 1 Hz Clock Pulse Output ON
1: Alarm Terminal 1 Hz Clock Pulse Output OFF

# 5. FDC (Floppy Disk Controller)

The X68000 is equipped with two 5" 2HD (double-sided high-density) type FDDs (floppy disk drives). The FDC (Floppy Disk Controller) controlling these FDDs uses the µPD72065. The FDD peripheral block diagram is shown in Figure 4-9.

**X68000 Disk Specifications (1.28 MB formatted)**

- 128, 256, 512, 1024 bytes/sector
- 26, 16, 8 sectors/track
- 77 tracks/side
- 154 tracks/disk

**FDC Input Clock**

- 2HD (8 MHz), 2DD/2D (4 MHz) switchable
  - If connecting the 2DD/2D type FDD, please use the expansion floppy disk connector. When connecting a 2D/2DD type FDD for X1 or X1turbo, make sure pins 20 to 29 of the connection cable are N.C. (not connected) (optional for X68000).

**Transfer Method**

- MFM and FM switchable

# 5-1 Disk Drive Features and Specifications

The X68000 FDD is equipped with the following unique features:

1. Eject Function
   - Automatic ejection mechanism for media inserted into the specified drive

2. Activity LED Indicator (2-color LED)
```
   - LED indication feature for the specified drive’s activity
   - Green: Indicates media inserted into the specified drive
   - Red: Lights up when the drive is selected, and when ready to ON
```

Page 148

5. FDC (Floppy Disk Controller)

| Power SW on the main unit | Activity LED | Eject LED | 
|----------------------------|--------------|-----------|
| ON State                   | If media is in the FDD  | - Normal lighting                      | Eject switch masking function ON: 
|                            |                  | -Eject switch masking function OFF: Normal lighting or off   | - OFF: Normal lighting |
|                            | If media is not in the FDD and LED normal lighting is ON: Normal lighting | If media is not in the FDD and eject switch masking function is OFF: Normal lighting or off | OFF: Normal lighting |
|                            | If media is not in the FDD and LED normal lighting is OFF: Off | OFF: Off /Blown |
|                            | FDD re-read/write (track select ON, LED ON) | -Normal lighting: Switch to colored in normal state  | 
| OFF State                  | Media is in FDD:           | - Normal lighting              | Media is in FDD: Normal lighting |
|                            | Media is not in FDD: ~ OFF: Off |                             | Media is not in FDD: Off       |

| Table 4-12 Meanings of Disk Drive LEDs |
|----------------------------------------|

(3) Eject switch masking function

A function to mask the eject operation so that ejects cannot be performed during access

(4) Media search function

A function to monitor the insertion and non-insertion state constantly across all drives

(5) Media mis-insertion detection function

A function to detect media mis-insertion for each drive

(6) Interrupt Function

An interrupt notification function during media insertion and ejection

Chapter 4 Peripheral LSI

- I/O Controller
- Hard Disk Control
- Hard Disk Data Bus
- HD (Hard Disk)
- FD (Floppy Disk)
- FDD Option Control

- Control Bus
- Address Bus
- Data Bus

- 2HD/2DD/2D Switching

- FDC (µPD72065)
- VFO Circuit (SED9420AC)

- ACK
- SEL
- RESET
- REQ
- BUSY
- I/O
- C/O
- MSG
- D0-D7

- OPTION SELECT 0~3
- EJECT
- EJECT MASK
- LED BLINK
- FHD IN
- FDD IN
- DISK IN
- TRK 00
- WRITE PROTECT
- DRIVE SELECT 0~3
- READY
- INDEX
- DISK TYPE SELECT
- DIRECTION
- STEP
- WRITE GATE
- WRITE DATA
- SIDE SELECT
- MOTOR ON
- READ DATA

- Fig. 4-9 FDD Peripheral Block Diagram

- MIN/STD
- Vcc1
- Vss
- 16 MHz

Page 150

5. FDC (Floppy Disk Controller)

                           Unformatted              1667
Capacity
```
  Formatted                   1065            IBM standard 26 sectors
  (K bytes)                                          256 bytes / high density mode
  Number of tracks            10.42
```
Data transfer rate           500
  (K bits/s)
Access time                  3
```
  Track-to-track seek time
  (msec)                      15              Cylinder wait time =   
                                          Track-to-track seek time
  Average seek time           95              Average access time =  
                                             Cylinder seek time
```
Media rotation speed         360
  (rpm)
Spindle motor               0.5
  startup time (sec)
Recording density           9870
  (BPI)
Number of tracks   
```
  TRACK/SIDE                  77
  TRACK/DISK                 154
```
Tracks density               96
  (TPI)
Number of heads                2
Recording method              MFM           FM method available
External dimensions        27.0 (H) x 148.0 (W) x
  (mm)                      198.0 (D)
Weight                      900 g
Other                       Auto clamp eject mechanism, auto retract plate function,
                            VFO (SED9420AC)

Table 4-13 Specifications of built-in FDD

Chapter 4 Peripheral LSI

5-2 Characteristics of the FDC

In the X68000, the µPD72065 is used as the FDC to control the two installed FDDs. The following points differ when compared to the FDC MB8877A that was used in the conventional X1, X1turbo series.

µPD72065
- The execution result (status) check of read/write systems can be performed in advance via an interrupt.
- The output terminal for drive select and head select is abolished, and these are unnecessary as I/O ports.
- The current head position on each drive is retained in the FDC, simplifying the program.
- Video data can be given to the FDC without the need for formatting (coding).
- If an error is detected, the command is terminated immediately without retries. (e.g., during a read/write, when a media defect is detected, but the head does not stop.)

MB8877A
- The execution result (status) check of read/write systems can be performed via polling in advance.
- The output terminals for drive select and head select are required as I/O ports.
- It is necessary to retain track numbers that store the current head position of each drive on the main RAM, complicating the program.
- It requires formatting (coding) for one track (approximately 6KB - 8KB capacity). Then, the program gets complicated.
- Sometimes, if there is no response to an error, the command continues. (e.g., during a read/write, when a media defect is detected, and sometimes the head keeps spinning without stopping.)

Table 4-14 Comparison points between µPD72065 and MB8877A

# 5. FDC (Floppy Disk Controller)

# 5-3 FDC Register Address Map

| I/O  | Register Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | Note | |
|------|------------------|-----|-----|-----|-----|-----|-----|-----|-----|------|-----|
| In   | Read |
|      | E94001H          |     |     |     |     |     |     |     |     | FDC Status Register |
|      | E94003H          |     |     |     |     |     |     |     |     | FDC Data Register |
|      | E94005H          |     |     |     |  0  |  0  |  0  |  0  |  0  | Drive Status (optional signal) |
|      | E9C001H          |     |     |     |     |     |     |     |     | Interrupt vector status |
| Out  | Write |
|      | E94003H          |     |     |     |     |     |     |     |     | FDC Data Register |
|      | E94005H          |     |     |     |  0  |  0  |     |     |     | Drive Control (optional signal) |
|      | E94007H          |  0  |  0  |     |     |     |     |     |     | Access drive select, 2HD/2DD, 2D switch |
|      | E9C001H          |  0  |  0  |     |     |     |     |     |     | Interrupt vector mask |
|      | E9C003H          |     |     |     |     |     |     |     |     | Interrupt vector number |

Table 4-15: FDC Register Address Map

# 5-4 Details of the FDC Registers

1. Regarding FDC Status Register (E94001H) and FDC Data Register (E94003H), please refer to the µPD72065 data sheet for further details.

2. Drive Status (In) - optional signal:
```
    - E94005H
  
  | D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
  |----|----|----|----|----|----|----|----|
  |  0 |  0 |  0 |  0 |  0 |  0 |--|--|
 
  - Description:
     - Media Absent or Other: 0
     - Media Present: 1
```

Page 153

Chapter 4 Peripheral LSI

(3) Drive Control (Out) ... Option Signals
- E94005H

D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0

1: Option signal for Drive 0 enabled
0: Option signal for Drive 0 disabled
1: Option signal for Drive 1 enabled
0: Option signal for Drive 1 disabled
1: Option signal for Drive 2 enabled
0: Option signal for Drive 2 disabled
1: Option signal for Drive 3 enabled
0: Option signal for Drive 3 disabled
1: Ejection enabled
0: Ejection disabled
1: Injection switch mask enabled
0: Injection switch mask disabled
1: LED lighting (ON, OFF effective when no media is inserted)
0: LED lighting OFF

(4) Access Drive Select, 2HD / 2DD • 2D Switching (Out)
- E94007H

D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0

0: Access Drive 0 selected
1: Access Drive 1 selected
0: Access Drive 2 selected
1: Access Drive 3 selected
0: 2HD (1.6M type)
1: 2DD or 2D (1M or 500K type)
0: Drive select disable, motor OFF
1: Drive select enable, motor ON

Page 154

5. FDC (Floppy Disk Controller)

(5) Interrupt Signal Status (In)
• E9C001H
```
D7 D6 D5 D4 D3 D2 D1 D0
  1  0  0  1  1  0  1  0

D7:
  0: Printer interrupt mask set
  1: Printer interrupt mask cleared

D6:
  0: FDD interrupt mask set
  1: FDD interrupt mask cleared

D5:
  0: FDC interrupt mask set
  1: FDC interrupt mask cleared

D4:
  0: Hard disk interrupt mask set
  1: Hard disk interrupt mask cleared

D3:
  0: Printer interrupt
  1: Printer interrupt (BUSY=1) - data not sent to printer

D2:
  0: FDD interrupt
  1: FDD interrupt - Media insert (media not ready or reject, or media eject time out), recalibration complete

D1:
  0: FDC interrupt
  1: FDC interrupt - Light/Phase down by resulting status data reading request, SEEK, RECALIBRATE command's E-PH WITH ASE command, SENSE INTERRUPT STATUS command's end, or SENSE INTERRUPT STATUS command's timeout request

D0:
  0: FDC interrupt mask set
  1: FDC interrupt mask cleared
```

(6) Interrupt Signal Mask (Out)
• E9C001H
```
D7 D6 D5 D4 D3 D2 D1 D0
  0  0  0  0  0  0  0  0

D7:
  0: Printer interrupt mask
  1: Clear printer interrupt mask

D6:
  0: FDD interrupt mask
  1: Clear FDD interrupt mask

D5:
  0: FDC interrupt mask
  1: Clear FDC interrupt mask

D4:
  0: Hard disk interrupt mask
  1: Clear hard disk interrupt mask
```

Page 155

Chapter 4 Peripheral LSI

(7) Interrupt Vector Numbers (Out)
- E9C003H

| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|----|----|----|----|----|----|----|----|
| 0  | 0  | 0  |    |    |    |    |    | 0 0: FDC interrupt
|    |    |    |    |    |    |    |    |
|    |    |    |    |    |    |    |    | 0 1: FDD interrupt
|    |    |    |    |    |    |    |    |
|    |    |    |    |    |    |    |    | 1 0: Hard Disk interrupt
|    |    |    |    |    |    |    |    |
|    |    |    |    |    |    |    |    | 1 1: Printer interrupt

5-5 FDC Access

(1) Usage of auto eject, LED indication, and eject switch mask function
Among the functions of the drive controller (E9400H) that you want to operate, set the desired function bit (D5~D7) to "1" and OUT it to specify the drive to operate the option signal with D0~D3.

(2) Media insertion, media removal, media presence detection, media insertion detection, media insertion eject, and removal interrupt function usage
First, an interrupt occurs when media is inserted or removed.
Next, in the interrupt processing routine, specify the drive to output the option signal at D0~D3 and OUT it. However, at this time, D5~D7 records the previous state of each drive, and this will be OUT. Next, read the E9400H, check bits D6 and D7, and determine according to Table 4-16.

| D7 (DISK IN) | D6 (ERROR DISK) | Function     |
|--------------|-----------------|--------------|
| 1            | 1               | Media detected (In this case, an interrupt occurs with media insert or eject) |
| 1            | 0               | Media inserted |
| 0            | 0               | Media not inserted |

Table 4-16 Media Insertion Determination

Page 156

5. FDC (Floppy Disk Controller)

```
    When a media is inserted, the media interrupt starts by initially setting D7 to "0". If media is automatically set in the media insertion process, it will eventually be set to "1" and E90405H will be output. Other bits are processed the same as the first OUT.

    This series of operations takes place for drives 0 through 3, and the host side grasps the state of each drive.
```

(3) Utilizing the Forced Ready Function

```
    The YM2151 (FM sound source) CT2 port is used to check the connection to the FDD.

    The CT2 port is used to forcibly set the FDC READY terminal to a READY state, and the following procedure is used to determine whether the FDD's power is on and whether the FDD is connected.
```

■ Determination method

```
  1. Write "1" to CT2 port of YM2151 (forced READY).
  
  2. Send the "RECALIBRATE" command to the FDC (to FDD#1-4, to four drives).
  
  3. Send the "SENSE INTERRUPT STATUS" command to the FDC.
  
  4. Check the D4 bit (EC) of the Result Status (ST0).

     - EC="0": Connection OK
     - EC="1": Not connected (or power not on)
  
  5. Write "0" to CT2 port of YM2151 (normal operation).

    Note: The READY terminal of the FDC means the power is on, media is inserted, the clamp is executed, and the motor is turned on after execution. When the motor reaches constant rotation, it becomes "H".

    Refer to Chapters 1-6 of Chapter 3 for details on the FM sound source (CT2 port).
```

*(This page is too faint in the original to transcribe.)*

**Chapter 5**

**Other Hardware**

1. **Keyboard**

The X68000 uses the keyboard and mouse in the block structure as shown in Figure 5-1.

**[Main Unit]**

**[Keyboard]**

Figure 5-1: Keyboard and Mouse Block Diagram

Chapter 5: Other Hardware

Regarding mouse and TV control, please use either the main unit control or the keyboard control exclusively.

1-1 Sub CPU

The keyboard of the X68000 uses a sub CPU as 80C51, which performs the roles shown in Table 5-1.

| Data Transmission Format for Keyboard |
|---------------------------------------|
| Baud Rate      | 2400 Baud           |
| Start Bit      | 1                   |
| Data Length    | 8                   |
| Parity (None)  |                     |
| Stop Bit       | 1                   |
Table 5-1: Keyboard Data Transmission Format

(1) The key code obtained by key scan is sent to MFP (refer to Table 5-3, Figure 5-3). Unlike the X1 and X1turbo series, in the case of the X68000 keyboard, the key scan code is converted to ASCII code and stored in the corresponding key code, and information whether the key is pressed or released is sent as a 1-byte serial data.

Additionally, regarding repeat, you can control the delay time before entering repeat and the interval time until the next repeat (Speed). After this the delay time, while the repeat function operates, the pressed signal (MSB) is sent. Note that the repeat is effective for all keys (refer to Figure 5-12).

(2) TV control remote signal output (refer to Table 5-3, Figure 5-5)
In the X1 and X1turbo series, the remote control signal was output from the main unit's 80C49 on P27 (pin 38), but in the X68000, the same signal is output from the keyboard's 80C51 T1 terminal. In the X68000, the method of outputting this TV control remote signal uses key operations on the keyboard (such as the SHIFT key) to send the 1-byte data to the MFP via the main unit or 80C51. Thus, depending on whether the main unit or the keyboard control is enabled, it allows you to send or invalidate the TV control code (refer to Figure 5-13).

Page 160

> 6 reference). Also, TV control by OPT.2 keys and CFG on keys can be enabled or disabled in the same way (Figure 5-13 reference).
> 
> Additionally, if the keyboard is not connected to the main unit's connector, TV control will be possible even if a remote control signal is sent with software-based timing management while using the system port E8E003H D03 as "0". Conversely, if the keyboard is connected to the main unit, TV control is possible only when the system port E8E003H D03 is set to "0". For normal use, please set it to "0" (Figure 5-2 reference). The only available functions when entering TV control from the keyboard with a repeat enabled are volume up, volume down, channel up, and channel down.
> 
> (3) Keyboard LED control (Figure 5-8 reference)
> 
> You can control the LEDs - 7 LEDs for kana, romaji, code input, CAPS, INS, kana input, full corner - on the keyboard via software. In other words, when the LED key is pressed, the keyboard side detects it and sends 1 byte of data from the MFP on the main unit to the 80C51, allowing any LED to be turned on or off.
> 
> Also, when the keyboard is reset (either when the AC adapter is plugged in or when the keyboard power is turned on), a request code is sent from the 80C51 on the keyboard to the MFP to set the LED state to off. The brightness can be configured using the following operations when pressing the key:
> 
> - If no key is pressed: Bright
> - Reset while pressing XF3: Slightly bright
> - Reset while pressing XF4: Slightly dim
> - Reset while pressing XF5: Dim

Chapter 5 Other Hardware

(4) Mouse Control Signal Control (Refer to Fig. 5-9)
By sending 1 byte of data from the main unit’s MFP to the 80C51, it is possible to make the MSCTRL signal "H" or "L". However, this is valid only when the keyboard’s mouse socket is used. For details on the mouse, refer to Section 2 of this chapter.

(5) Keyboard Send/Receive Code (Refer to Fig. 5-10)
Normally, the main loop scans the keys and outputs the key data, but if the main unit’s MFP settings are not performed and the RDY (MFP’s RR pin level) signal is fixed to "L" or when the system port E8E007H D01 is "0", the DMAC will transfer busily, and the 80C51 will neither send key data nor halt key scanning, resulting in a stop state. Naturally, in such a state, TV control and other operations cannot be performed. However, in the case of the X68000, by sending 1 byte of data to the main unit’s MFP with this data send/receive code, the 80C51 prevents the data from being unsendable and ensures that the key scan will not be halted (RDY signal "H" or system port E8E007H D01 “1” enables key sending).

(6) Special Control Keys in Compact TV Mode (Refer to Fig. 5-11)
As shown in Table 5-2, 1 byte of data is sent from the MFP to the 80C51 regarding the control keys to use as TV controller keys on the X1 Compact.

| Operation Key | X68000                                | X1 Compact Mode                     |
|---------------|----------------------------------------|-------------------------------------|
| SHIFT +       | Superimpose/Superimpose Release Toggle Key | Superimpose                         |
| SHIFT =       | TV/External Input Toggle Key           | TV                                  |
| SHIFT .       | TV/Computer Screen Toggle Key          | Computer                            |

Table 5-2 X1 Compact TV Controller Code

(Page 162)

1. Keyboard

From 8051 to MFP, 1 byte data
The key correspondence code is as shown in Figure 5-4

Key Correspondence Code
0: Key is pressed
1: Key is released

Figure 5-3 Key Scan Data Format
The key code is a 16-bit number

BREAK COPY
ESC F1 F2 F3 F4 F5 F6 F7 F8 F9 F10 BS
TAB Q W E R T Y U I O P RETURN
CTRL A S D F G H J K L ; : "
SHIFT Z X C V B N M , . / SHIFT
CAPS KANA CAPS ROMAJI HELP
LOCK SYSTEM SYSTEM HELP
ROLL UP ROLL DOWN

INSTANT DELETE CLEAR 7 8 9 +
UNDO  4 5 6 -
```
1 2 3 *
0 . ENTER
```
OPTION 1 OPTION 2

Figure 5-4 Key Code List

Chapter 5 Other Hardware

- From MFP to 8051, 1-byte data is sent.
```
  - If `SHIFT` is available, or by using `OPT. 2` key, TV control is performed.
  - Each code corresponds to the following list.
```

TV Control Code
```
D7 D6 D5 D4 D3 D2 D1 D0
 0  0                |                   SHIFT  ^                         OPT. 2
```
|--------------------|
TV Control Code Table

| D5 | D4 | D3 | D2 | D1 | D0 | Corresponding Key | Command          | Function                           |
|----|----|----|----|----|----|-------------------|------------------|------------------------------------|
| 0  | 0  | 0  | 0  | 0  | 1  | ↑                 | Vol. up          | Volume Up (repeatable)             |
| 0  | 0  | 0  | 0  | 1  | 0  | ↓                 | Vol. down        | Volume Down (repeatable)           |
| 0  | 0  | 0  | 1  | 0  | 0  | -                 | Vol. normal      | Volume Normal                      |
| 0  | 0  | 1  | 0  | 0  | 0  | CLR               | Call             | Channel call                       |
| 0  | 1  | 0  | 0  | 0  | 1  | -                 | CS down          | TV initial screen (reset)          |
| 0  | 0  | 1  | 1  | 0  | 0  | -                 | Mute             | Sound mute                         |
| 1  | 0  | 0  | 0  | 1  | 0  | -                 | CH16             |                                   |
| 0  | 1  | 0  | 1  | 0  | 0  | ↑                 | BR up            | TV/Computer Screen Switch - Toggle control |
| 0  | 1  | 0  | 1  | 1  | 0  | ↓                 | BR down          | TV input & Computer/Normal - High-speed Skipping |
| 0  | 1  | 1  | 0  | 1  | 0  |                   | BR 1/2           | Brightness 1/2                     |
| 0  | 1  | 1  | 1  | 0  | 1  | -                 | CH up            | Channel Up (repeatable)            |
| 0  | 1  | 1  | 1  | 1  | 0  | -                 | CH down          | Channel Down (repeatable)          |
| 0  | 1  | 1  | 1  | 1  | 1  | -                 | Power ON/OFF     | TV Power ON/OFF                    |
| 0  | 1  | 1  | 1  | 1  | 1  | -                 | CS 1/2           | Super-1 (contrast down) and removal toggle |
|----|----|----|----|----|----|-------------------|------------------|------------------------------------|

| 1  | 0  | 0  | 0  | 0  | 0  | Ten Key 1         | CH 1             | Channel 1                          |
| 1  | 0  | 0  | 0  | 0  | 1  |                   | CH 2             | Channel 2                          |
| 1  | 0  | 0  | 0  | 1  | 0  |                   | CH 3             | Channel 3                          |
| 1  | 0  | 0  | 0  | 1  | 1  |                   | CH 4             | Channel 4                          |
| 1  | 0  | 0  | 1  | 0  | 0  |                   | CH 5             | Channel 5                          |
| 1  | 0  | 0  | 1  | 0  | 1  |                   | CH 6             | Channel 6                          |
| 1  | 0  | 0  | 1  | 1  | 0  |                   | CH 7             | Channel 7                          |
| 1  | 0  | 0  | 1  | 1  | 1  |                   | CH 8             | Channel 8                          |
| 1  | 0  | 1  | 0  | 0  | 0  |                   | CH 9             | Channel 9                          |
| 1  | 0  | 1  | 0  | 0  | 1  |                   | CH 10            | Channel 10                         |
| 1  | 0  | 1  | 0  | 1  | 0  |                   | CH 11            | Channel 11                         |
| 1  | 0  | 1  | 0  | 1  | 1  |                   | CH 12            | Channel 12                         |
|

1. Keyboard 

(TV control and remote signal transmission) 
(Transmission of remote signals "0" and "1")

Formal signal      Reverse signal
48msec                  48msec

250 µs    250 µs
```
    |------|------|
    |    1msec    |

    "0"
```

250 µs    250 µs
```
    |------|------|
    |    2msec    |

    "1"
```

(Formal signal)
```
C1  C2  C3  C4  C5  C6  C7  C8  C9  C10  C11  K
 0    0    0    1    0    0    0    0    0      1      0     0
D0   D1   D2   D3   D4
 0    0     0    1   0
```

Example (0 0 0 1 0) ← TV control code (Table 5-3 reference)

(Reverse signal)
```
C1  C2  C3  C4  C5  C6  C7  C8  C9  C10  C11  K
 1    1    1    0    1    1    1    1    1      0      1     1
```
Reverse signal data example (1 1 1 0 1)

Figure 5-5 TV control and remote signal 

```
D7   D6   D5   D4   D3   D2   D1   D0
 0      1      0     1      1      1      *      *
```

- Data from MFP to 8051: 1 byte
- Effective by key operation TV control-code related effect*
*Effective at reset

0: Invalid
1: Valid

Figure 5-6 TV control code control code format from this book

Chapter 5: Other Hardware

MFP to 8051 1-byte data
All flags are cleared upon reset, and the LED lighting request code FFH is sent from 8051 to MFP.

0: Off (Kana)
1: On (Kana)
0: Off (Roman characters)
1: On (Roman characters)
0: Off (Ten-key input)
1: On (Ten-key input)
0: Off (CAPS)
1: On (CAPS)
0: Off (INS)
1: On (INS)
0: Off (Hiragana)
1: On (Hiragana)
0: Off (Fullwidth)
1: On (Fullwidth)

Figure 5-7 LED Lighting Control Code Format

D7 D6 D5 D4 D3 D2 D1 D0
0 1 0 1 0 1 * *

0: Bright
1: Slightly Bright
0: Slightly Dark
1: Dark

Figure 5-8 LED Key Brightness Adjustment Format

MFP to 8051 1-byte data
* is invalid
"R" upon reset 

0: Set mouse control (MSCTRL) to "L"
1: Set mouse control (MSCTRL) to "H"

Figure 5-9 Mouse Control Code Format

1. Keyboard

![Diagram]

- 1 byte data from MFP to 80C51
*: Invalid.
- During reset, transmission is prohibited.

D1: Key data transmission prohibition
1: Key data transmission permitted

Fig 5-10 Key data transmission prohibition code format

![Diagram]

- 1 byte data from MFP to 80C51
*: Invalid.
- During reset, X1 compact cancellation

D1: X1 Compact
1: X1 Compact Cancellation

Fig 5-11 X1 compact cancellation code format for a specific TV control key

(Setting of delay time before repeat)

![Diagram]

- 1 byte data from MFP to 80C51
- Repeat start delay time (msec)
= 200 msec + (N * 100 msec) (at least 200 msec - at most 1700 msec)
- During reset, 500 msec

N (Note: set integer value from 0 to 15)

(Setting of repeat interval time)

![Diagram]

- Repeat interval time (msec)
= 30 msec + (N * 25 msec) (at least 30 msec - at most 1155 msec)
- During reset, 110 msec

N (Note: set integer value from 0 to 15)

Fig 5-12 Repeat start delay time and setting code format for repeat interval time

![Diagram]

- 1 byte data from MFP to 80C51
*: Invalid.
- During reset, valid.

D1: Valid (Used as TV control key)
1: Invalid

Fig 5-13 OPT. TV control code format by 2 key and 2 signals

Chapter 5 Other Hardware

1-2 Key Data Processing Procedure

(1) Initial Setting for Key Data Processing (Common for Input/Output)

[MFP]

1. Set 0 to each of the Allocation Enable Registers A (E88007H) for D04, D03, D02, D01, and D00.
2. Set the allocation vector to the Allocation Vector Register (E88017H) (Automatic allocation stops at mode D03="0").
3. Set 01H to Timer B Control Register (E8801BH).
4. Set 0DH to Timer B Data Register (E88021H).
5. Set 88H to USART Control Register (E88029H).
6. Set 00H to Receive Status Register (E8802BH).
7. Set 04H to Send Status Register (E8802DH).
8. Set 0 to D03 in System Port (E88007H).

(2) Enable various allocation for MFP.

1. Set 1 to each of the Allocation Enable Registers A (E88007H) for D04, D03, and D01; set 0 to D02 and D00.
2. Set 1 to each of the Allocation Enable Registers B (E88013H) for D04, D03, and D01; set 0 to D02 and D00.
3. Set 01H to the Receive Data Register (E8802BH).
4. Set 1 to D03 in System Port (E88007H).

(3) Key input interrupt (MFP’s 12-level interrupt) occurs, and key data is retrieved.

[Input]
In the initial setting described in (1), when key data is received and transferred from the receive register to the receive buffer, the interrupt for Receive Buffer Full occurs. In cases of overrun error, parity error, or break detection, the Receive Error interrupt occurs. Especially in the interrupt handler for Receive Buffer Full, please pay attention to the following:

a. If the key data is a valid key code, a control signal from the key is determined as follows:
   01H–06H, 70H–77H: Key code (or 81H–ECH, F0H–F7H, or 78H–7FH: control signal (or F8H–FFH))

b. If it is key code:
   If the key is pressed and released, the determination is made by the MSB flag of the key code.

Some keys may be pressed —

1. Keyboard

When pressed, the key code is sent. At this time, the MSB is 0, and the remaining 7 bits are the key code. 
Also, as long as this key is kept pressed, the same code (MSB = 0) continues to be input at the set delay time intervals. When this key is released, the MSB becomes 1, and the corresponding code with the lower 7 bits as the key code is sent. 

c. In the case of control signals 

A control signal FFH indicates a request for LED data from the keyboard. Regarding the request for LED data: The LED data is in the off state when the power is turned on. However, when the keyboard is reset (when the power switch is turned on, or the inserted keyboard is removed), a signal is sent from the keyboard's 8C51 to request the LED status settings. This signal indicates that the keyboard has been reset.

[Output] 
1. Set the transmission status register (E8802HD) to 05H 
2. Read the transmission status register (E8802HD)
3. Check D0=1 (buffer empty) (loop until D0 becomes 1) 
4. Set the USART data register (E8802FH) with the control code for output to the keyboard 
5. Read the transmission status register (E8802HD)
6. Check D0=1 (buffer empty) (loop until D0 becomes 1) 
7. Set the transmission status register (E8802HD) to 04H 
8. Error handling: In the event of a control code output error or abnormal insertion error detection, a transmit error interrupt will occur if the transmitted signal is swamped.

Additionally, the output commands from the main unit MFP to the keyboard might include the following:

- TV control code for TV Control Code*
- Control code to request LED key lighting status 
- Mouse control signal (MSCTRL) control code 
- Modem commands 
- TV control mode-specific X1 composite control code
- Setting the delay and speed for repeat start time and subsequent repeat intervals 
- TV control mode and mouse control mode control codes

Chapter 5: Other Hardware

Next, the following is a flowchart of each interrupt routine. Please refer to Chapter 4, Section 2 for MFP.

Flowchart:

1. Read Receiver Status Register (E8802BH)
2. Check D04
```
   - If "1":
     - Read USART Data Register (E8802FH)
   - If "0":
     - Handle frame error
     - Return
```
3. Read USART Data Register (E8802FH)
4. Check Key Code
```
   - If "Y":
     - Key Code Check
       - [01H–6CH (81H–ECH), 70H–77H (F0H–F7H)]
```
5. If Key Code is not "Y":
```
   - Check FFH
       - If "N":
         - Handle Error
         - Return
```
6. Otherwise:
```
   - Set 05H in Transmitter Status Register (E8802DH)
   - Read Transmitter Status Register (E8802DH)
   - Check D07
       - If "0":
         - Return
```

Note: Key Code Processing Routine (Buffering)

1. Keyboard

USART Data Register (E8802FH) Set to LED Control Codes

Read Communication Status Register (E8802DH)

Check D07

Set Communication Status Register (E8802DH) to 04H

Return

Figure 5-14 Receive Buffer Full Interrupt Routine Flowchart

Page: 171

Chapter 3 Sound Functions

Receive Status Register (E8802BH) Read

D05 Check "1"

USART Data Register (E8802FH) Read Parity Error Handling Return

"O"

USART Data Register (E8802FH) Read

00H ? "Y"

"N" Overrun Error Handling

Return

D02 Check "1"

"O" Stop Bit Detection

Error Handling

Return

Start Bit Detection Brake Error Handling

Return

Figure 5-15 Receive Error Interrupt Routine Flowchart

Note: 

1. Keyboard

Transmit status register (E8802DH) read

D04 Check

"1"                                    "0"

Transmit disabled detected        Transmit enabled detected

          Return                       Return

Under-run error processing 
(Return to the main routine for retransmission)

          Return

Figure 5-16 Transmit Error Interrupt Routine Flow Chart

Chapter 5: Other Hardware

2. Mouse

In the X68000, both the main unit and the keyboard have their own mouse connectors, which can send coordinate data when requested from the main unit. Therefore, control signals from the main unit and data lines from the mouse are synchronized with two procedures.

As shown in the block diagram of figure 1, in the case of the main unit connector, the mouse control (MSCTRL) is controlled by the SCC B channel RTSB signal, and in the case of the keyboard connector, it is controlled by the 80C51. In either connector, mouse data (MSDATA) is connected to the RXDB terminal of SCC B channel.

(Note: This might refer to the Sharp X68000, a personal computer sold in Japan.)

[Diagram of the mouse's external appearance]

The main unit can slide 90°.

Switch 2

Switch 1
Indicates the Y direction.

Trackball

Y (+)
Y (-)
X (+)
X (-)

[Table showing mouse data communication standards and data transmission procedures]

Communication mode:
Asynchronous communication
Baud rate: 4800 baud

Mouse data format:
Start bit: 1
Data length: 8 bits
Stop bit: 2

(Mouse data structure)
Start bit
D0 D1 D2 D3 D4 D5 D6 D7
Stop bit

[Diagram of mouse connector]

Mouse connector

Pin numbers | Signal name
```
1 | Vcc
2 | MSCTRL
3 | MSDATA
4 | GND
5 | GND
```

Table 5-4: Mouse data communication standards and data transmission procedures

Page 174

2-1 Mouse Data Transfer Sequence

(1) When the main unit requests data from the mouse, the mouse control (MSCTRL) is set from "H" to "L". The mouse detects this signal change and transmits one block (3 bytes) of data to the main unit. Note that if there is no change in the mouse control (MSCTRL: "L"), the mouse will not output anything.

Figure 5-18 Mouse data transfer

Tc1 > 500 µs
Tc > 500 µs
Td < 750 µs

Data A denotes relative data, where TA is designated relative X or Y mouse movement value.
Data B denotes relative data, where TB is designated relative X or Y mouse movement value.

(2) The mouse sends 3 bytes of data. The data structure is as follows:

- Switch information (status data)
- X coordinate (right is positive, left is negative)
  -128 (80H) to -1 (FFH), 0 (00H), +1 (01H) to +127 (7FH)
- Y coordinate (down is positive, up is negative)
  -128 (80H) to -1 (FFH), 0 (00H), +1 (01H) to +127 (7FH)

Note: For both X and Y coordinates, -129 or below means underflow (status data bit D7 or D5 is set to "1"), and +128 or above means overflow (status data bit D6 or D4 is set to "1").

Chapter 5 Other Hardware

Mouse Data (MSDATA)
1st Byte: Status Data

2nd Byte: X-Axis Data -128~127

3rd Byte: Y-Axis Data -128~127

(Status Data)
```
D7 D6 D5 D4 D3 D2 D1 D0
   0   0
```
0: Switch 1 (Right) OFF
1: Switch 1 (Right) ON
0: Switch 2 (Left) OFF
1: Switch 2 (Left) ON
1: 1~127 - Overflow on X-Axis
1: X=-128 - Overflow on X-Axis
1: 1~127 - Overflow on Y-Axis
1: Y=-128 - Overflow on Y-Axis

Table 5-5 Mouse Data Format

2-2 Mouse Access

(1) Initial Settings
* Set the respective registers listed in SCC’s Channel B (Set the interrupt vector).

1. Set Write Register WR9 to 0CH
2. Set Write Register WR4 to 4CH
3. Set Write Register WR1 to 00H
4. Set the interrupt vector to Write Register WR2
5. Set Write Register WR3 to 0DH
6. Set Write Register WR5 to 62H
7. Set Write Register WR9 to 01H
8. Set Write Register WR10 to 00H
9. Set Write Register WR11 to 56H
10. Set Write Register WR12 to 1FH
11. Set Write Register WR13 to 00H
12. Set Write Register WR14 to 02H

Page 176

1. Timer Interrupts
```
    - Timer Interrupts (Mouse Control): Set the registers for Timer C or Timer D in MFP for timer interrupt intervals (For reference: The timer interrupt interval for the mouse in XTturbo is 16 msec).
        1. Set the interrupt enable register B (E88009H) for Timer C or Timer D to interrupt enable.
        2. Set the interrupt vector register (E88017H) to the interrupt vector (Specify interrupt completion mode).
        3. Set the prescale value in the Timer C and Timer D control registers (E8801DH) for the timer.
        4. Set the down-counter value in the Timer C data register (E88023H) and Timer D data register (E88025H).
```

(2) SCC transmission and reception enable interrupts, and enabling MFP timer interrupts.
```
    1. Set write control register WR3 to 1CH.
    2. Set write control register WR6 to 6AH.
    3. Set write control register WR0 to 80H.
    4. Set write control register WR14 to 03H.
    5. Set write control register WR15 to 00H.
    6. Set write control register WR1 to 10H.
    7. Set write control register WR0 to 10H.
    8. Set write control register WR1 to 10H.
    9. Set write control register WR9 to 09H.
    10. Set interrupt enable register B (E88009H) for Timer C and Timer D in MFP to interrupt enable.
    11. Set interrupt mask register B (E88015H) for Timer C and Timer D in MFP to interrupt mask enable.
```

(3) Timer Interrupt (MFP Interrupt)
```
    By Timer Interrupt (MFP Interrupt), the mouse control (MSCTRL) changes from "H" to "L".
    Note: The timer interrupt loop serves to control the mouse control (MSCTRL), so please execute this program. At this time, it is unclear if both the keyboard and mouse are connected, so please set both mouse controls to "H" and then to "L" as follows.
```

Chapter 5 Other Hardware

[When using the main unit (SCC) mouse connector]
Set SCC channel D write register WR5 to 60H, output to 500 µs or longer later, set 62H.
[When using the keyboard (80C51) mouse connector]
First output MFP to 80C51 41H, 500 µs or longer, output 40H.
(4) Interrupt triggered by data reception from the mouse (SCC interrupt) receives 3-byte data.
In the previous (1) initialization setting, an interrupt is triggered when valid mouse data is received or a special reception condition (such as overrun error, framing error) occurs. The interrupt vector at this time is as follows:
- When valid mouse data is received
D7   D6   D5   D4   D3   D2   D1   D0
V7   V6   V5   0   1   0   1   0

In this interrupt routine, 3-byte data from the mouse is processed, and then SCC channel D write register WR5 is set to 60H, MFP outputs 41H to 80C51 setting 41H.
- When a special reception condition occurs
D7   D6   D5   D4   D3   D2   D1   D0
V7   V6   V5   0   1   1   1   0

In this interrupt routine, first, determine whether a special reception condition (such as overrun error, framing error) occurred in the SCC channel D read register RR1, handle the corresponding error, then set SCC channel D write register WR5 to 60H, output 41H from MFP to 80C51, and finally perform error reset (set SCC channel D write register WR0 to 30H).
For MFP, refer to Set 2, Chapter 4, and for SCC, refer to Set 3, Chapter 4.

<Page 178>

3. Joystick

In the X1 and X1turbo series, accessing joysticks involved using PSG registers 14 and 15, but on the X68000, it leverages two ports of the 8255 to use two joysticks. Note that when using these two joysticks (input), you must set 92H to E9A007H.

Address
Data
Control

µPD8255
Port A: Joystick No.1
Port B: Joystick No.2
Port C: Sound synthesis PCM control

Figure 5-19 Joystick Block Diagram

3-1 Address Map of Joystick Register

Register Address
      D07  D06  D05  D04  D03  D02  D01  D00
E9A001H
                               -> Joystick No.1 ->
E9A003H
                               <- Joystick No.1 <-
E9A005H     IOC7 IOC6 IOC5 IOC4    S.R.  PCM PAN

Table 5-6 Joystick Register Address Map

(S.R. = Sampling Rate)

Chapter 5: Other Hardware

3-2 Details of the Joystick Register

(1) Joystick No.1 (READ)

D7  D6  D5  D4  D3  D2  D1  D0

E9A001H

(all bits negative logic)

IOA0 (FORWARD)
IOA1 (BACK)
IOA2 (LEFT)
IOA3 (RIGHT)
IOA5 (TRIGGER A)
IOA6 (TRIGGER B)

(2) Joystick No.2 (READ)

D7  D6  D5  D4  D3  D2  D1  D0

E9A003H

(all bits negative logic)

IOB0 (FORWARD)
IOB1 (BACK)
IOB2 (LEFT)
IOB3 (RIGHT)
IOB5 (TRIGGER A)
IOB6 (TRIGGER B)

(3) Joystick Control

D7  D6  D5  D4  D3  D2  D1  D0

E9A005H

(all bits negative logic)

PCN PAN (sound balance switch)
Sampling Rate (sound synthesis sampling rate switch)
IOC4 (Joystick No.1 strobe)
```
 0: normal operation
 1: disable Joystick No.1
```

IOC5 (Joystick No.2 strobe)
```
 0: normal operation
 1: disable Joystick No.2
```

IOC6 (Joystick No.1 Option A)
```
 0: normal operation
 1: option function
```

IOC7 (Joystick No.1 Option B)
```
 0: normal operation
 1: option function
```

3-3 Accessing the Joystick 

(1) To set mode 8255, please set 92H in E9A007H (refer to Chapter 5-4 for details).

(2) To set the joystick to normal mode, set the upper 4 bits (D04 to D07) of port C in E9A005H to "0".

(3) Input data No. 1 from the joystick is read from E9A001H. Also, when inputting data No. 2 from the joystick, it is read from E9A003H.

4. Printer

The X68000, like the X1 and X1turbo series, is equipped with a Centronics-standard 8-bit parallel I/F as a printer I/F.

To send 1 byte of data to the printer from this device, a control signal, the BUSY signal, and the STROBE signal are used. The BUSY signal is the input signal from the printer, and no data can be sent when this signal is at "H" level. In other words, when the BUSY signal is at "H" level, the device waits until it goes down to "L" level before sending. Also, the STROBE signal is the output signal to the printer from the device, and by sampling data on this STROBE signal, the printer receives the data. However, before the STROBE signal is output, the data should be latched into the data register of E8C001H.

In the X68000, in addition to the printing functions of the X1 and X1turbo series, a feature has been added that allows the software to mask the BUSY signal interrupt. By using this feature, there is no need to check the BUSY signal, and the status of the printer can be known through interrupts.

Chapter 5 Other Hardware

Register Address

| Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 |
|---------|-----|-----|-----|-----|-----|-----|-----|-----|
| E8C001H | X   | X   | X   | X   | X   | X   | X   | X   | Printer Output Data                | Printer Data Register (Light only)                         |
| E8C003H | X   | X   | X   | X   | X   | X   | X   | STRO | Printer Control Register (Light only)                      |

(Light only)
0: Printer Busy Interrupt Mask
1: Printer Busy Interrupt Mask Release
0: FDD Write Interrupt Mask
1: FDD Write Interrupt Mask Release
0: FDC Write Interrupt Mask
1: FDC Write Interrupt Mask Release
0: Hard Disk Insert Interrupt Mask
1: Hard Disk Insert Interrupt Mask Release

| E9C001H | X   | X   | X   | X   | X   | X   | X   | X   | 

(Read only)
0: Printer Busy Interrupt Mask (re)
1: Printer Busy Interrupt Mask Release
0: FDD Write Interrupt Mask
1: FDD Write Interrupt Mask Release
0: FDC Write Interrupt Mask
1: FDC Write Interrupt Mask Release
0: Hard Disk Insert Interrupt Mask
1: Hard Disk Insert Interrupt Mask Release

0: Printer Busy Interrupt Mask (W)
1: Printer Busy Interrupt Mask Release
0: FDD Write Interrupt
1: FDD Write Interrupt ON
0: FDC Write Interrupt OFF
1: FDC Write Interrupt ON

0: Printer Busy OFF (BUSY=0)
1: Printer Busy ON (BUSY=0)

| E9C003H | Interrupt Vector | 1 | 1 | Printer Busy Interrupt Vector |

* Table 5-7 Printer Register Map (X is invalid)

4-1 Printer Access

(1) Check the Printer BUSY Signal
- In case of polling
a) To mask the interrupt caused by the printer busy, set D00 of E9C001H to "0" (Other bits retain their previous states).
b) Read E9C001H and confirm D05="1".

**In case of an interrupt:**
a) Set the interrupt vector to E9003H, and initialize the interrupt processing routine's (2) and (3) processing programs.
b) To release the printer's interrupt mask, set "1" to bit D00 in E9C001H (other bits retain their previous state).
   If BUSY = '0' (printer sends data), the program moves to the interrupt processing routine.

2) Set Printer Output Data:
   Set 1 byte output data to the printer to E8C001H

3) Printer Data Sample (Strobe signal rise):
   Set bit D00 of E8C003H to "0", and then to "1" to raise the strobe signal.

# 5. Miscellaneous Switches

5-1 Switches at the Front of the Main Unit

The front of the X68000 has the following 3 switches:

(A) Reset Switch
    Press this switch to initiate a hardware reset. Processing addresses that are written to 000000H on the main memory will be executed.

(B) NMI Switch
    Use this switch for system debugging. Pressing the switch triggers the highest priority interrupt (NMI Level-7) and executes exception processing starting from the address written at 000007H in the main memory. At the end of the NMI processing routine, please set "1" to bit D02 of E8C007H to generate a system report. If "1" is not set to system port E8C007H bit D02, the NMI processing routine will escape after NMI processing and jump again to the NMI processing routine.

Page 183

Chapter 5: Miscellaneous Hardware

(C) POWER Switch
The POWER switch on the X68000 becomes ON (Vcc1 ON) by working the hardware circuit when switched ON, but if it is OFF, this is recognized by the MFP by an interrupt due to the MFP detecting the POWER SW being switched off (MFP level 2 interrupt). That is, when the POWER switch is turned ON, before cutting off the power, the MFP recognizes it. Then, the MPU determines from this interrupt, performs a check around the interrupt handling routines, and writes the values "00", "OFF", "OFF" to the system port E8E00FH in sequence if there are no abnormalities, and executes POWER OFF (Vcc1 OFF). This prevents mistakes such as turning off the power in the middle of accessing a floppy disk.

5-2 Power System

The X68000 has the following three power systems. For the X68000, you can know whether Vcc1 has turned ON from MFP. For details, refer to 2 of this chapter.

(A) Vcc2 (power supply to RTC, SRAM, keyboard, etc.)
This can be turned ON and OFF by the rear power switch. Note, do not absolutely turn off this rear power switch when using timers, TV control, etc.

(B) Vcc1 (power other than RTC, SRAM, keyboard, etc.)
Most circuits operate on this power. When the POWER switch is ON, the rear power switch can turn it ON and OFF.
- When the rear power switch is ON, the front POWER switch can turn it ON.
- When the rear power switch is ON, the EXPMON signal in the expansion I/O slot can turn it ON.
- When the rear power switch is ON, the ALARM signal from the RTC ALARM timer can turn it ON.

Note: For Vcc1 OFF, it is only possible by writing "00", "OFF", "OFF" values to the system port E8E00FH sequentially through software.

(C) Backup Battery
Generally, it is continually charged by connections to Vcc2, but in the case that Vcc2 is cut off, it is used as a backup for the RTC and SRAM.

5-3 LED

On the front of the X68000, there are LEDs as shown below. However, Vcc2 is always assumed to be ON.

(A) POWER LED
The front POWER switch lights when it is in the ON state (Vcc1 ON). However, if the POWER switch is OFF but the EXP/MON signal from an expansion I/O slot or the RTC or ALARM signal is ON, the POWER switch will be OFF but the LED will light until Vcc1 is actually turned off. However, when only Vcc2 is ON, the red LED lights. When both Vcc1 and Vcc2 are ON, the green LED lights.

(B) TIMER LED
When using the RTC ALARM timer function, write 00H to the RTC CLKOUT register (BANK 1 of E8A001H) to turn on the TIMER LED. Conversely, write 07H to turn it off when not using the timer function. For details, refer to Chapter 4-3.

(C) H/L Res. LED
When Vcc1 is ON, the LED automatically lights up in the high-resolution mode (horizontal sync frequency of 31.5 kHz) and turns off in the standard resolution mode (horizontal sync frequency of 15.98 kHz).

(D) Floppy Disk Drive LED (Refer to Chapter 4-5)

|               | Activity LED              | Eject LED                               |
|---------------|----------------------------|-----------------------------------------|
| POWER         | Media is in the FDD --> Lights up            | Only when the eject switch is ON --> Lights up |
| ON state      | Media is in the FDD and indicator is on --> Lights up yellow   | Media is in the FDD during sleep mode --> Lights up green or red |
|               | Media is in the FDD and indicator is off --> Goes out        |                                          |
|               | Reading from FDD (when RDY is ON, indicates LED --> Lights up red) |                                          |
| POWER         | Media is in the FDD --> Stays lit             | Media is in the FDD --> Lights up     |
| OFF state     | Media is in the FDD     | --> Stays lit when media is in FDD        | 
|               | Otherwise, turns off | Otherwise, turns off | 

(Table 5-8 FDD LEDs)

Page 185

Chapter 5 Other Hardware

5-4 8255 Port

In X68000, ports A and B of the 8255 are used as input ports for the joystick 2 port, and port C is used as an output port for sound synthesis output control and sampling frequency switching. Therefore, by using the control word register of this 8255, it is necessary to specify port A, B input, and port C output in mode 0.

<8255 Control Word Register (E9A007H)>

| D7 | D6 | D5 | D4 | D3 | D2 | D1 | D0 |
|----|----|----|----|----|----|----|----|
| 1  | 0  | 0  | 0  |   |   |   |   |

- 0 : Port C (Lower 4 bits) output (for sound synthesis use)  
- 0 : Port B output  
- 1 : Port B input (for Joystick No. 2)  
- 0 : Port C (Upper 4 bits) output  
- 0 : Port A output  
- 1 : Port A input (for Joystick No. 1)  

For details on the joystick, refer to Chapter 6; for details on sound synthesis, refer to Chapter 4.

Appendix

1. I/O Port Address List
(Note: * is invalid, W is WRITE only, R is READ only, R/W is READ/WRITE available)

| Item  | Port Address | Function | Remarks |
|-------|--------------|----------|---------|
| CRT   | E800000H     | W        | Horizontal total position       |                  |
|       | E800001H     | W        | Horizontal display position     |                  |
|       | E800002H     | W        | Horizontal sync position        |                  |
|       | E800003H     | W        | Horizontal sync width position  |                  |
|       | E800004H     | W        | Vertical total position         |                  |
|       | E800005H     | W        | Vertical display position       |                  |
|       | E800006H     | W        | Vertical sync position          |                  |
|       | E800007H     | W        | Vertical sync width position    |                  |
|       | E800008H     | W        | External sync adjustment        |                  |
|       | E800009H     | W        | Raster control                  |                  |
|       | E80000AH     | W        | X direction scroll              |                  |
|       | E80000BH     | W        | Y direction scroll              |                  |
|       | E800016H     | W        | Screen 0 X Y                    |                  |
|       | E800017H     | W        | Screen 1 X Y                    |                  |
|       | E800018H     | W        | Screen 2 X Y                    |                  |
|       | E800019H     | W        | Screen 3 X Y                    |                  |
|       | E800024H     | W        | Text mode / display mode set    |                  |
|       | E80002AH     | R/W      | Text address, high-speed clear  |                  |
|       | E80002EH     | R/W      | Source / destination register   |                  |
|       | E800030H     | W        | Hit mask register               |                  |
|       | E800040H     | R/W      | CRTC command setting port       |                  |
| Graphics Palette | E82000H       | R/W   | 16 color mode / 255 color mode / 65536 color mode | Graphics Palette |
|                   | E82010H      | R/W   |                                                     |      |
| Palette (1)       | E8210FEH     | R/W   |                                                     |      |
| Text RAM Scroll Control | E82200H | R/W | Text (Sprite Color Table 0) / Shared Palette | Text, Sprite Palette |
|                   | E82210H       | R/W   |                                                     |      |
|                   | E82323H       | R/W   | Sprite Color Table 1 Palette                     | Sprite Palette |
  
Page 187

Appendix

|  Item  | Port Address | Function | Notes |
|--------|--------------|----------|-------|
| Sprites & Text Screen |  E82240H  | R/W  | Sprite color table 2 palette |  Sprite use palette |
|           |  E8225EH  | R/W  | Sprite color table 15 palette | |
|         |  Video Controller | E82400H  | R/W | Memory preset | Semi-transparent, special priority |
|           |  E82500H  | R/W  | Sprite area setting |  |
|           |  E82600H | R/W | Special mode, screen display limit |   |

DMA Controller |
| E84000H | R/W | Channel status register | Left-side port addresses are for Channel 0 only, otherwise other channels follow next port addresses |
| E84010H | R/W | Channel control register |
| E84020H | R/W | Device control register |
| E84030H | R/W | Device control register |
| E84040H | R/W | Device control register |
| E84050H | R/W | Device control register |
| E84060H | R/W | Device control register |
| E84070H | R/W | Area expansion (Identity register) ||
| E84080H | R/W | Even/odd refresh rate sync |
| E84090H | W  | Memory function code |
| E840A0H | W  | Memory function code (Word) |
| E840B0H | W  | Memory address counter (Word) |
| E840C0H | W  | Memory address counter (Long word) |
| E840D0H | W  | Base address register (Long word) |
| E840FFH | R/W | Channel control Register |
|  Edit Set |  E86001H | W  | Supervisor scalar adjustment |

MFP |
| E88000H | R | GPIP data register | Unused |
| E88003H | W | Active edge register |
| E88005H | R/W | Data direction register |
| E88007H | R/W | Timer A control register |
| E88009H | R/W | Timer B control register |
| E8800BH | R/W | Timer C control register |
| E8800DH | R/W | Timer D control register |
| E8800FH | R/W | Service register A |
| E88011H | R/W | Service register B |
| E88013H | R/W | Interrupt vector register |
| E88015H | R/W | IP interrupt enable register |
| E88017H | R/W | IS interrupt status register |
| E88019H | R/W | Timer A data register |
| E8801BH | R/W | Timer B data register |
| E8801DH | R/W | Timer C data register |
| E8801FH | R/W | Timer D data register |
| E88021H | R/W | Device management register |
| E88023H | R/W | Sync/Async control register |
| E88025H | R/W | USART control register |  |

# 1. I/O Port Address List

| Item    | Port Address | R/W | Device                                             | Function                        | Remarks            |
|---------|--------------|-----|----------------------------------------------------|---------------------------------|--------------------|
|         | E8B02BH      | R/W | Receive Data Register                              |                                 |                    |
| M       | E8B02DH      | R/W | Transmit Data Register                             |                                 |                    |
| F       | E8B02FH      | R/W | USART Data Register                                |                                 |                    |
| P       | E8A000H      | W   | Timer Counter/CLKOUT Select                        |                                 |                    |
|         | E8A002H      | W   | Timer Counter/Adjust                               |                                 |                    |
|         | E8A005H      | R/W | Minute Counter/Alarm 1 Register                    |                                 |                    |
|         | E8A007H      | R/W | Minute Counter/Alarm 10 Register                   |                                 |                    |
|         | E8A009H      | R/W | Hour Counter/Alarm 1 Register                      |                                 |                    |
| R       | E8A00BH      | R/W | Hour Counter/Alarm 10 Register                     |                                 |                    |
| T       | E8A00DH      | R/W | Day Counter/Day of Week Register                   |                                 |                    |
| C       | E8A00FH      | R/W | Day Counter/Alarm Enable Register                  |                                 |                    |
|         | E8A011H      | R/W | Day Counter/Alarm 1 Register                       |                                 |                    |
|         | E8A013H      | R/W | Day Counter/Alarm 10 Register                      |                                 |                    |
|         | E8A015H      | R/W | Month Counter/12-24 Hour Select                    |                                 |                    |
|         | E8A017H      | R/W | Control Register                                   |                                 |                    |
|         | E8A019H      | R   | Test Register                                      |                                 |                    |
|         | E8A01BH      | W   | Reset Controller                                   |                                 |                    |
| Printer | E8C001H      | R   | Printer Data                                       | Write                           |                    |
|         | E8C003H      | W   | Printer Strobe                                     | Write                           |                    |
|         | E8C005H      | R   | Printer Busy                                       | Read                            |                    |
| System  | E8E001H      | R/W | Contrast Adjustment (D/A)                          |                                 |                    |
| Board   | E8E003H      | W   | Contrast Control                                   |                                 |                    |
|         | E8E005H      | R/W | MNL LED ON/OFF, NMI Reset, Keyboard Control        |                                 |                    |
|         | E8E006H      | W   | SRAM Write Enable Control                          |                                 |                    |
|         | E8E00FH      | W   | POWER OFF Control                                  |                                 |                    |
| FM      | E9O001H      | R/W | FM Sound Register Address Port                     |                                 |                    |
| Sound   | E9O003H      | R/W | FM Sound Register Data Port                        |                                 |                    |
| Synthesis| E92001H     | R/W | ADPCM Data I/O (IN)/ADPCM Command (OUT)            |                                 |                    |
|         | E92003H      | R/W | ADPCM Data I/O (IN/OUT)                            |                                 |                    |
|         | E9A005H      | R   | ADPCM Output, Loop Switching Register              | 8255 Port C                     |
| Floppy  | E94001H      | R   | FDC Status Register (IN)                           |                                 |                    |
| Disk    | E94003H      | R/W | FDC Data Register (IN/OUT)                         |                                 |                    |
|         | E940005H     | R/W | Drive Status (IN)/Drive Control (OUT)              | Objection Signal                  |
|         | E94007H      | W   | "Busy" Signal Reset, 2HD/2DD-2D Switch (OUT)       |                                 |
| Hard Disk | E96001H  | R/W | HD Data (IN/OUT)                                   |                                 |
|         | E96003H      | R/W | Status (IN)/Select Reset (OUT)                    |                                 |
|         | E96005H      | R/W | Controller Board Reset (OUT)                       |                                 |
|         | E96007H      | W   | Select Reset (OUT)                                 |                                 |
| SCC     | E98001H      | R/W | SCC Command Port B                                 |                                 |
|         | E98003H      | R/W | SCC Data Port B                                    |                                 |
|         | E98005H      | R/W | SCC Command Port A                                 |                                 |
|         | E98007H      | R/W | SCC Data Port A                                    |                                 |
|         | E98009H      | R/W | SCC Register Control                               |                                 |
| Joystick| E9A001H      | R   | Joystick 0                                         | 8255 Port A                     |
|         | E9A003H      | R   | Joystick 1                                         | 8255 Port B                     |

Page 189

Attachment

| Item | Port Address | Access | Function | Remarks |
| --- | --- | --- | --- | --- |
| 8255 | E9A007H | W | 8255 Control Word Register | |
| FD, PR, HD | E9C001H | R/W | FDC, FDD, HD, Printer Interrupt Status (IN) | |
| | E9C002H | R/W | FDC, FDD, HD, Printer Interrupt Status (OUT) | |
| FD, PR | E9C003H | R/W | FDC, FDD, HD, Printer Interrupt Vector | |
| Sprite | EB8000H | R/W | Sprite X Coordinate | Sprite 0 |
| | EB8002H | R/W | Sprite Y Coordinate | |
| | EB8004H | R/W | Sprite Control | |
| | EB8006H | R/W | Sprite Priority | |
| | EB803FH | R/W | Sprite X Coordinate | Sprite 127 |
| | EB803EH | R/W | Sprite Y Coordinate | |
| | EB803CH | R/W | Sprite Control | |
| | EB803EH | R/W | Sprite Priority | |
| | EB8000H | R/W | Background KO X Coordinate | |
| | EB8002H | R/W | Background KO Y Coordinate | |
| | EB8004H | R/W | Background KO X Coordinate | |
| | EB8006H | R/W | Background KO Y Coordinate | |
| | EB8008H | R/W | Background KO Control | |
| | EB800AH | R/W | Raster Counter | |
| | EB800CH | R/W | Window Display | |
| | EB800EH | R/W | Blinking Display | |
| | EB8010H | R/W | Disable Display | |
| Sprite PCG Area | EB8000H | R/W | Sprite 0 PCG Area | |
| | EB8007EH | R/W | | |
| | EB8F80H | R/W | Sprite 127 PCG Area | |
| | EBBFFEH | R/W | | |
| Sprite Text Area | EBC000H | R/W | Text Area 0 | |
| | EBDFEEH | R/W | | |
| | EBE000H | R/W | Text Area 1 | |
| | EBBFFEH | R/W | | |

Table A-1 I/O Port List

2. Area Set

In X68000, within the area from the beginning of 2M bytes (000000H-1FFFFFFH), by setting data in the E86001H register, it is possible to set any location in 8K byte units as a supervisor area.

- Register Support – Address E86001H, Write only, 8-bit register (However the upper bit ** is disabled)

E86001H: ** ** ** ** D7 D6 D5 D4 D3 D2 D1 D0
                  (Lower 8 bits are effective)

- Operation: Within the range of the first 2M bytes of main memory, the supervisor area can be specified by setting data. However, the setting is in 8K byte units (the 2M bytes are divided into 256 parts).

Example: Memory Map when setting data to 7FH

000000H                  Port Setting Value
          Supervisor Area

0FFFFFH                  7FH (127)
100000H                  Supervisor & User Area

200000H
          Supervisor & User Area

BFFFFFH

```
  Key: Port Setting Value     Supervisor Area
      0                               0 ~ 1FFFH (8 KB)
      1                               0 ~ 3FFFH
      2                               0 ~ 5FFFH
      3                               0 ~ 7FFFH
      4                               0 ~ 9FFFH
      5                               0 ~ BFFFH

      127                            0 ~ FFFFFH (1 MB)
      128                            0 ~ 101FFFH
      ...
      254                            0 ~ 1FDFFFH
      255                            0 ~ 1FFFFFH (2 MB)
```

* The area beyond 200000H can be accessed from both supervisor and user sides.

Diagram A-1 Example of Area Set

3. System Port

3-1 System Port Register Address Map

(* means invalid, * means FIELD(READ))

| No. | Register Address |    | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | Remarks |
|-----|------------------|----|-----|-----|-----|-----|-----|-----|-----|-----|---------|
| 1   | E8E001H          |    | *   | *   | *   | *   |     | Contrast adjustment |
| 2   | E8E003H          |    | *   | *   | *   |     | TV control | * | 3D L | 3D R |
| 3   | E8E005H          |    | *   | *   |     |     | Video input control |
| 4   | E8E007H          |    | *   | *   | *   | *   | *   | Key control | NMI reset | HRL |
| 5   | E8E00DH          |    | SRAM Write Enable Control |
| 6   | E8E00FH          |    | POWER OFF Control |

Table A-2 System Port Register Address Map

3-2 Details of System Port Registers

(1) E8E001H [READ/WRITE]
* 16-step computer screen contrast adjustment (OH [dark] - FH [bright])

(2) E8E003H [READ/WRITE]
* See Table A-3.
* In WRITE MODE, by controlling "0" and "1" in D03, it can be used as a TV remote control signal (normally write "0"). In READ MODE, you can know the TV ON/OFF status ("0" for TV ON, "1" for TV OFF). However, TV remote control and keyboard cannot be used at the same time. See Chapter 3, Section 1 (2).
* D00 and D01 are related to stereo vision.

3. System Port

| Bit  | WRITE             | READ              |
|------|-------------------|-------------------|
| D00  | 3D R              | 3D R              |
| D01  | 3D L              | 3D L              |
| D02  | *                 | FIELD             |
| D03  | TV Remote Signal  | TV ON/OFF Status  |

Table A-3 System Port Register E8E003H

0: Shutter OPEN
1: Shutter CLOSE

(3) E8E005H [WRITE]
- This is the system port for controlling the optional "digitizer dropout" using a computer.

(4) E8E007H [READ/WRITE]
- Please refer to Table A-4.
- D01 is used for switching the dot clock, so usually set it to "0".
- When the NMI switch is pressed, the MPU moves to the highest-level edge (forced edge level), shifting to the NMI processing loop. In this NMI processing loop, at the end of the loop processing, it is necessary to write "1" to D02 to reset NMI again. If "1" is not written to D02, the MPU remains in the NMI processing loop and will not exit, causing the NMI to fire continuously.
- In WRITE mode, D03 is used as the data transmission permission signal from the sub-CPU 8051 of the keyboard to the MPP (RR terminal). Writing "1" permits data transmission, and writing "0" cancels data transmission. In READ mode, you can know the state (whether the key jacket is inserted or not; "1" when inserted, "0" when removed) by checking if the keyboard key jacket is inserted.

| Bit  | WRITE            | READ       |
|------|------------------|------------|
| D01  | HRL              | HRL Status |
| D02  | NMI Reset        | .......... |
| D03  | Key Ready        | Key Jacket Status |

Table A-4 System Port Register E8E007H

Appendix

(5) EB00DDH [WRITE]

- Normally, SRAM is Read-Only, but this port is designed to protect the contents of SRAM from being destroyed during program runaway.
- Writing 31H enables SRAM Write, and any other code will be Read-Only.

(6) EB00FFH [WRITE]

- When input in the order of 00H→01H→FFH, only POWER OFF (Vcc1 OFF) will be effective, and any other code will be invalid. In other words, this makes it so that POWER OFF cannot be easily executed.

4. Interrupts

4-1 Interrupts of the 68000 MPU

| Level | Interrupt | Cause |
|-------|-----------|-------|
| High 6 | NMI | Interrupt by external NMI switch (Auto vector interrupt) |
|       | MFP | Various timers, key data reception, H-SYNC, V-DISP, etc. (Auto vector interrupt) |
| 5 | SCC | Interrupt by RS-232C, mouse data reception (Vector interrupt) |
| 4 | Floppy | Expansion I/O slot B |
| 3 | DMAC | Interrupt during DMA transfer position (Vector interrupt) |
| 2 | Floppy | Expansion I/O slot A |
| Low 1 | Disk | Interrupt by FDC, FDD, hard drives, printer BUSY, etc. (Auto vector interrupt) (Note, FDC <-> FDD HD -> Printer outputs are output by the disc hardware controlled by the DMA) |
| 0 | Printer | Table A-5 Interrupts by MPU (Vector interrupt) |

4-2 Interrupt read-out report of the MFP (Multi-Function Peripheral)

| Masking level | Interrupt | Cause | General name in function |
|---------------|-----------|-------|------------------------|
| High 15 | 1111 | H-SYNC signal from CRTC | General Purpose Interrupt 7 (17) |
| 14 | 1110 | IRQ signal from CRTC (Specify row in raster) | General Purpose Interrupt 6 (16) |
| 13 | 1101 | V-DISP signal from CRTC | Timer A |
| 12 | 1100 | KEY data reception completion | Receive Buffer Full |
| 11 | 1011 | KEY data reception error | Receive Error |
| 10 | 1010 | KEY data transmission completion | Transmit Buffer Empty |
| 9 | 1001 | KEY data transmission error | Transmit Error |
| 8 | 1000 | USART (keyboard) serial flow | Timer B |
| 7 | 0111 | Unused | General Purpose Interrupt 5 (15) |
| 6 | 0110 | CRTC V-DISP signal status change | General Purpose Interrupt 4 (14) |
| 5 | 0101 | 8-bit dedicated size (bus clock 4 MHz) | Timer C |
| 4 | 0100 | 8-bit dedicated size (bus clock 4 MHz) | Timer D |
| 3 | 0011 | FM sound source interrupt mismatch detection | General Purpose Interrupt 3 (13) |
| 2 | 0010 | POWER SW ON/OFF status detection | General Purpose Interrupt 2 (12) |
| 1 | 0001 | Expansion I/O slot B EXPIOIN signal ON/OFF detection | General Purpose Interrupt 1 (11) |
| Low 0 | 0000 | RTC ALARM signal ON/OFF detection | General Purpose Interrupt 0 (10) |

Table A-6 Interrupts read out by MFP

Page 195

4-3 Settings for Interrupt Vectors

-Assignee-                          -Register Address-                                                   

MFP                                   E88017H                                       

```
                                          D07     D06     D05     D04     D03     D02     D01     D00
                                          ───────  Setting   ───────  0: Automatic interrupt end
                                                                                           1: Software interrupt ending
```

SCC (Channels A, B shared)    Write to Register 2

DMAC (Channel 0)                   EB4025H             (Normal Interrupt 0)

(Internal 2HD)                       EB4027H
                                           (External Interrupt 0) 

DMAC (Channel 1)                    EB4065H             (Normal Interrupt 0)

(Hard Disk)                          EB4067H
                                           (External Interrupt 0)

DMAC (Channel 2)                    EB40A5H             (Normal Interrupt 0)

(Memory: Memory)                EB40A7H
                                           (External Interrupt 0)

DMAC (Channel 3)                    EB40E5H             (Normal Interrupt 0) 

(Audio Synthesis)                   EB40E7H             
                                            (External Interrupt 0) 

Disk and Printer                     E9C ■■ 3H           

```
                                            D07     D06     D05     D04     D03     D02     D01     D00
                                            ──────────────── Setting ──────────────────

                                            FDC Interrupt: 00
                                            FDD Interrupt: 01
                                            Hard Disk Interrupt: 01
                                            Printer Interrupt: 11
```

Table A-7 Settings for Interrupt Vectors

Page 196

5. IPL (Initial Program Loader)

- IPL ROM address: FC0000H ~ FFFFFFH (256 K bytes)
  
- Access:
```
  (1) Supervisor program, data area
  (2) Read-only
```

At reset:

1. At reset, the portion of IPL ROM 1 (FF****H) appears in the first 64 K bytes (000000H ~ 00FFFFH) of the memory map.

2. From the beginning of this IPL ROM 1, the 68000 MPU will perform initializing processes, and the program counter and stack pointer values are written from the first two long words.

3. When the reset signal is released, the MPU switches the two long words read from ROM (address control data) into the memory map and starts execution.

4. The MPU processes the first instruction of the program counted from the address written into the two long words read previously. At the same time, the image inside IPL ROM 1 will disappear from the memory map (refer to Figure A-3).

Note:
The program counter and stack pointer value written at the top of the IPL ROM 1 are handled so that the IPL image of IPL ROM 1 does not disappear from the memory map by accessing outside the range (FC0000H ~ FFFFFFH) of IPL ROM 1.

Only when the ROM image is powered on, or during manual reset, the use of the memory map (Figure A-2) will be observed. (During the execution of the reset command for the 68000 MPU, the ROM image will not appear.)

[Figure descriptions:]
Figure A-2: Reset time map
Figure A-3: Reset processing map

# 6. Character Code Table

| Upper digit → | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
|----------------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Lower digit↓   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
| 0              |   |   |   |   |   |   |   |   |   |   | ! | " | # | $ | % | & | ' |
| 1              | ( | ) | * | + | , | - | . | / |
| 2              | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; | < | = | > | ? |
| 3              | @ | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O |
| 4              | P | Q | R | S | T | U | V | W | X | Y | Z | [ | ¥ |] | ^ | _ |
| 5              | ' | a | b | c | d | e | f | g | h | i | j | k | l | m | n | o |
| 6              | p | q | r | s | t | u | v | w | x | y | z | { | | | } | ~ | ␣ |
| 7              | あ | い | う | え | お | か | き | く | け | こ | さ | し | す | せ | そ |
| 8              | た | ち | つ | て | と | な | に | ぬ | ね | の | は | ひ | ふ | へ | ほ |
| 9              | ま | み | む | め | も | や | ゆ | よ | ら | り | る | れ | ろ | わ | を |
| A              | ん | ア | イ | ウ | エ | オ | カ | キ | ク | ケ | コ | サ | シ | ス | セ | ソ |
| B              | タ | チ | ツ | テ | ト | ナ | ニ | ヌ | ネ | ノ | ハ | ヒ | フ | ヘ | ホ |
| C              | マ | ミ | ム | メ | モ | ヤ | ユ | ヨ | ラ | リ | ル | レ | ロ | ワ | ン | ヲ |
| D              | a | b | c | d | e | f | g | h | i | j | k | l | m | n | o | p |
| E              | q | r | s | t | u | v | w | x | y | z |   
| F              |         |                | の        |

Table A-8: Character Code Table

Kanji codes comply with JIS C-6226-1983. For details, please refer to the instruction manual attached to the X68000 main unit.

Index

<Numbers>
1/4 square characters ................74

<A>
ADPCM .................................3, 114, 115, 116
AD converter............................114 
AD transformation.......................34 
ANK ....................................9 

<C>
CGROM .................................2, 74 
CGROM address..........................76 
CPU access.............................51 
CPU register...........................53 
CRC ....................................139 
CRTC .................................3, 9, 23, 24, 27, 57, 125, 130 
CRTC register...........................26, 27 
CRTC register address map...............26 
CRTC special features...................33 

<D>
DMAC .................................1, 3, 117, 119, 120, 121 

<F>
FDC ...................................3, 90, 148, 152, 156 
FDC register............................153 
FM sound source.......................3, 83, 84, 85, 86, 87, 126 
FM sound source register................90 
FM sound source support.................117 

<G>
GPIB data register ....................130

<I>
8255 ................................116, 117, 179, 186 
I/O controller...........................3 
I/O port address.......................187 
IPL ...................................197 

<J>
JIS code ...............................74, 77 

<L>
LED ................................143, 148, 156, 161, 166, 169, 185 
LFO ....................................94 

<M>
MFP ...............................1, 3, 27, 123, 124, 168, 177, 178, 195 
MFP register ..........................130 
NMI switch ...........................183 

<P>
PCG ....................................54 
PCG7 access ............................46 
PCG7 address....................47, 48, 50, 51 
PCG area ........................36, 38, 44, 47 
PCG board ........................47, 48 
PPI ...................................3 
PSG ..................................179 

<Q>
QD ...................................51, 52, 54 

<R>
RAM ....................................4 
ROM ....................................4 
RS-232C ...............................2 
RTC ..........................3, 126, 142, 144, 184 

<S>
SAM .................................23, 34 
SCC ................................3, 139, 174, 178 
SCC register .........................141 
SRAM ...............................184 

<U>
USART .....................124, 125, 126, 136 
USART control register ............136

Index

<V>
V-DISP .................... 23
VRAM .....................1

<X>
X1 ....................... 9, 81, 162, 167, 179, 181

<A>
Analog Simulator ................ 107, 108
Access ................... 9, 29, 141
Access Drive Select ................ 154
Active Register ................ 130
ASCII Code ................... 76
Assumption ................... 86, 95, 96
Address Setting .................. 12
Address Bus ................... 119
Address Field .................. 139
Address Map .................. 12
Analog RGB ................... 2
Analog Data .................. 114
Analog Processing ............... 139
Alarm ................... 142, 143

<I>
Interrupt Switch Mask Function ........... 149
Phase Information .................. 92, 94, 101
Event Count Mode .............. 130, 135
Interface .................. 4, 114
Interface .................. 2, 11, 14, 24, 34

<U>
Leap Year ................... 146
Wait .................. 53, 54

<E>
Export .................. 95, 103
Error Reset .................. 191
Round Mode .................. 9, 27
Enveloped .................. 101, 103

<O>
Autocorrection .................. 148, 156
Oscillator .................. 2, 11, 48, 80
Overflow .................. 86, 108, 109, 110, 111

<O>
Overrun .................. 139
Overrun Error .................. 137
Octal .................. 84, 86, 91, 113
Offset .................. 9, 81, 115, 137
Sound .................. 95, 100
Synthesizer .................. 83, 90, 114
Synthesizer Address .............. 117
Synthesizer Register .............. 115
Sound .................. 95, 100

<K>
Resolution .................. 45
Counter .................. 125
Expansion Slot 1/Expansion Slot 2 ............. 126
Overlap .................. 63
Image Input .................. 4, 34
Image Size ................... 80
Image Control .................. 119, 140, 181, 185
Display Mode Register .............. 36, 37, 42, 46, 53, 53

<K>
Canvas ..................86, 90, 96
Key On ..................86, 90, 95, 107, 108
Keyhole ..................91, 163
Key Scan .................. 160
Key Skewing .................. 97
Key Field .................. 124, 125, 126, 130, 133, 142, 157, 178, 184

Odds Field .................. 81
Character Clock ........... 52, 54
Carrier .................. 91
Central Processing Unit .......... 10, 27
Forced READY .......... 157
Expected Resolution .......... 81

<K>
Short Horizontal .................. 94
Clock ..................91, 103, 109, 111, 112, 126, 139, 143, 148
Odd Field .............. 81
Graphic .................. 18, 14, 21, 22, 70
Graphic VRAM ........... 14, 21, 22, 70
Graphic Scroll Register ............... 25, 27

Page 200

Graphics Palette Address ............................ 14, 18, 21, 22, 72

Graphics Screen .................................. 5, 10, 14, 23, 60, 62, 63, 66

Graphics Actual Screen Address.............. 17, 19

Graphics Actual Screen Address Placement ... 20

<Ka>

Decoration........................................... 95, 100

<Ko>

High Resolution ..................................... 5, 9, 11, 14, 26, 28, 45, 46, 51, 82

High Resolution Clear .......................... 30, 33, 34

High Brightness ....................................... 84

Command Port .................................. 141, 142

Control Signal ....................................... 169

Control Panel .................................. 119, 140

Control Register ......................... 25, 28

Control Word Register ........ 116, 186

Computer Screen ............................................. 27

<Sa>

Silkscreen Steel ............................................120

Sign Table .......................................................... 93

Significance ............................................................95

Sound Function .......................................................83

Sound CPU .............................................................. 160

Triangle Mark............................................................. 94

Sampling Count ............................ 114, 115, 116, 117

<Shi>

System ............................................................... 7

System Report ......................................................... 192

System Register ................................................81, 104, 107

Frequency Counter ............................. 91, 104, 107

Seal ..................................................... 107

Serial Interface ......................................................... 33

Flip Screen ........................................................... 60

Time Counter............... 91, 104, 107

Joystick ............................................ 2, 116, 179, 186

Joystick Controller .......................... 180

Information Field ................................... 139

<Se>

Synchronization Signal ...................... 82

Vertical Display Start Location .............. 44

Switch .......................................................... 183

Horizontal Position Fine Adjustment..... 27

Horizontal Position Signal ........................... 2, 14, 27, 52, 53, 71, 80

Horizontal Display Area .............................................191

Scroll ........................................................... 23

Scroll Register ........................................................ 34

Scro Compact disc ...................... 86, 92, 95, 96

Star Bit............................................................ 140

Status Register .................................................153

Stop Bit........................................... 139, 140

Stroke ........................................................... 183

Sprite ................................... 1, 4, 6, 35

Sprite Access ................. 46

Sprite Virtual Resolution..................................... 40

Sprite High Color Table ................................................... 49

Sprite High Resolution Screen ............. 10, 60, 62

Sprite Code .................. 38, 39, 47

Sprite Controller ........................................3, 9

Sprite Scroll Register ............................ 36, 37, 40, 51, 52

Sprite Palette Address ................................................ 49

Sprite Register Address .................................36, 38

Smooth Scroll........................................................ 6

Slot .....................................4, 86, 88, 89, 101, 103

<Se>

Set ................................................... 91, 112

Centronics ................................................. 181

Full Angle ........................................ 139

Full Width Character............................................. 74

<Sou>

Running Frequency............................................45

Running Style ................................ ............81

<Ta>

Title ......................................... 109, 110, 111, 123, 124, 125, 127, 135, 168, 185

Title Fill In ........................ 177

First Horizontal Character..........................180

Second Horizontal Character.......................74

Page 201

Index

<Ch>
Channel......................................88,89,101,119,120,124,139,140
Synchronization Mode........................139

<Te>
Definition....................................5
Text..........................................4,54
Text NVRAM..................................11,13,23,33
Text Area.................................36,39,39,43,44,49,50,51
Text Screen............................5,9,10,11,23,33,60,62
Text Sequence................................42
Text Actual Screen........................12
Text Scroll Register..................25,27
Text Slot Address.......................12,13,72
Text Star Copy..............................36
TV Control................................4,160
TV Control Code........................62
Data Transmission Rate.................139
Data Point.....................108,119,140,142
Data Stack...................................153
Device.............................86,95,96,100,103
Disk.................................148
Disk Drive...............................125
Decoder.......................................4,52
Digital Dropper...........................34
Device.....................107,108,111
Dual Port DRAM............4,23,32
Power......................................184
Power ON.................................127

<To>
Transparency..............................41
Special Screen Control..................6
Special Priority......2,6,55,59,64
Special Transparent Mode..............69
Special Mode.............................174
Trackball....................................174
Transceiver.................................138
Synchronization Circuit........................24
Synchronization Effect....................24
Synchronization Access.................33
Driver Control............154,156

<Na>
Internal Register.........................120

<No>
Noise..............................84,86,94,103,104
Noise State Mode......................94
Noise Trace Mode.....................24

<Ha>
Hard Disk.........................2,4
Half Character..............................74
Semi-transparency........................62
Semi-transparent Mode........2,6,55,59
Semi-transparent Attribute................64,65
Semi-transparent Region Specification.....
Hand Sync...............................174
Byte Designation Mode..................139
Byte Time Detailed Mode................139
Binary.......................................107
Backup Data............................39,47
Background Code.......................54
Background Display Control Register....46,54
Background Scroll Register...36,37,42,53
Background Turn Pattern................35
Background Display........................35
Battery Backup..........................142
Pattern Definition...............................
Parity...........................139,140
Parity Error......................................37
Palette.............................................6
Palette Address.....61,62,66,72
Palette Configuration.....................71
Palette Data........................60,61,65
Power Switch...................126,184

<Hi>
Non Display Characters.................74
Non Display Mode.....................139
Display Control..................................44
Display Screen..............................5
Display Region Mode.......................40
Display Priority Region.......................41

**Symbol Resolution Degree**

..5, 9, 11, 14, 26, 28, 45, 46, 51, 54, 71, 80   
Bit Map...............................9   
Video Controller.....................3, 9, 55, 69   
Video Controller Register..........56, 57   
Video Screen.......................27, 84, 86, 91, 94   

**(a)**
Feedback............................86, 101   
Format.............................107, 148, 152   
Font.......................................74   
Label................................139   
Flag.........................86, 110, 111, 139   
Framing..............................139   
Floppy Disk Drive.....................2, 185   
Block Diagram........................7   
Block Transfer....................120   
Branch................................100, 107   
Priority...1, 6, 35, 41, 55, 57, 60, 62, 63   
Processor.............................125   
Print...................2, 155, 181   
Print Access.......................182   
Plain.................11, 17, 29   

**(i)**
Vector....................................117   
Transformation.............84, 107, 148   

**(u)**
Border Color.........................55   
Ball Point...........................140   
Point Generator.........................141   
Point...........................32   
Boarding..................................182   

**(e)**
Mouse.................2, 139, 159, 174   
Mouse Access......................176   
Mouse Control.........162, 175, 177   
Mouse Data............175, 176, 178   
Mouse Trackball....................2   

**(o)**
Main Memory......................120   
Media.................................156   
Memory.................................4   
Memory Map.....8, 11, 17, 18, 19, 20   

**(k)**
Mode Register.....................36   
Modulator.......................91   
Monochrome.......................139   

**(s)**
User Domain.......................191   

**(ra)**
Raster Address........25, 27, 33, 125   
Raster Copy Bit Mask............33   

**(tu)**
Real-Time Clock...................142   
Reset.............87, 90, 183   
Repeat................................160   
Repeat Control.....................167   
Remote Control.....................160   
Resource.............................96   

**(na)**
Rate.................................97   
Register Transfer....................53   

**(ha)**
Interrupt.......................108, 110   
........117, 123, 124, 149, 153, 157, 168, 170, 183, 195   
Interrupt Control.....................131   
Interrupt Wait Mode...................133   
Interrupt Signal Status...............155   
Interrupt Signal Mask.................155   
Interrupt Vector......................196   
Interrupt Vector Register....133, 134, 133, 134

Page 203

X68000
Technical Data Book

First Edition Published on September 1, 1987

Price: 3,000 Yen

Supervision:
TV Division, SHARP Corporation
Editing:
ASCII Publishing Bureau Techwrite

Publisher: Keiichiro Tsukamoto

Published by: ASCII Corporation
Postal code 107: Three-F Minami-Aoyama Building, 6-11-1 Minami-Aoyama, Minato-ku, Tokyo
Phone: 03-486-1111 (Main)
Inquiries: 03-498-0299 (Direct)
Sales Department: 03-486-1977 (Direct)

© SHARP Corporation
© ASCII Corporation

Unauthorized copying and reproduction of part or all of this book without permission is prohibited.

Editing in charge: Kenji Higuchi
Production in charge: Yoshiko Furuya
Printing program in charge: Eiko Akanaruse
Printing: Aoshodo Co., Ltd.
Binding: Seishosha

ISBN4-87148-426-2 C3055 ¥3000E

*(Blank page in the original.)*

ISBN4-87148-426-2 C3055 ¥3000E

List Price: 3,000 yen

Technical Data Book.
