# X68000 Service Manual (CZ-634C / CZ-644C)

*English translation from the Japanese original*

**SHARP**
Service Manual
No. CZ-134

**X68000**
Personal Computer
CZ-634C-TN
CZ-644C-TN

Distribution targets: Sharp Engineering (Co.) Ltd. SS, SB.

Issued: April 1991

**Contents**

1. Hardware Structure------------------------------------------2
1-1. Features------------------------------------------------3
1-2. Specifications-----------------------------------------6
1-3. Block Diagram----------------------------------------8
1-4. System Configuration-------------------------------9
2. Names of Each Part------------------------------------10
2-1. Front of the Computer Body---------------------11
2-2. Rear of the Computer Body----------------------11
3. Hardware-----------------------------------------------12
3-1. Memory Map-----------------------------------14
3-2. I/O Port Address List----------------------------15
3-3. Interrupts-----------------------------------------18
3-4. System Report----------------------------------22
3-5. IPL---------------------------------------------25
4. Control of Video Screen and Graphic Screen (CRTC)-28
4-1. Sprites------------------------------------------33
4-2. Priority Controller-------------------------------36
4-3. Text and Graphics Screen Control-----------39
4-4. Others------------------------------------------41
4-5. Keyboard and Mouse--------------------------43
5. Color Palette------------------------------------------43
6. CRT Controller-----------------------------------------45
7. Peripheral Devices-----------------------------------45
8. Devices---------------------------------------------45
8-1. DMA Controller--------------------------------46
8-2. Priority Interrupt Controller--------------------49
8-3. Enhanced Memory-------------------------------54
8-4. MFP--------------------------------------------55
8-5. SCC--------------------------------------------53
8-6. RTC--------------------------------------------57
9. Peripherals------------------------------------------59
9-1. Disks--------------------------------------------62
9-2. Printer--------------------------------------------62
9-3. Joystick--------------------------------------------62
9-4. Expansion Slot----------------------------------63
9-5. Other Connectors-------------------------------66
10. Main Circuit Board----------------------------------67
10-1. Main Circuit Board (1)------------------------71
10-2. Main Circuit Board (2)------------------------72
10-3. Main Circuit Board (3)------------------------73
11. Sub Circuit Board-----------------------------------75
11-1. Sub Circuit Board (1)-------------------------76
11-2. Sub Circuit Board (2)-------------------------77
12. Controller Circuit Board---------------------------80
13. Keyboard Controller-------------------------------85
14. LED of FD Connector, SCSI Connector---------89
15. Basics of the Control Circuit---------------------91
16. Digital LED, FD LED------------------------------91
17. FD Controller-------------------------------------92
18. Analog Board-------------------------------------94
19. CPU Board---------------------------------------99
20. ROM Board--------------------------------------103
21. Sound Board-------------------------------------105
22. Video Board--------------------------------------106
23. Connector Board----------------------------------107
24. Sub Connector Board---------------------------110
25. Printer Output Board-----------------------------111
26. Power Supply Design----------------------------112
27. Power Supply Method----------------------------113
28. Printer Separation Transformer--------------114

**(Note at the bottom)**
● Prompt and reliable service leads to repeat business.
● Proper maintenance connects you with customers.
Ensure trust... Issue without fail.

**Sharp Corporation**
Electronics Systems Division, Product Production Center

1. Hardware Configuration

1-1. Features

1) CPU Peripheral

- Uses 68000 (16.67 MHz), a 16-bit MPU.
- Capable of directly addressing up to 16MB of address space.
- Memory-mapped I/O (standard 2MB main memory equipped).
- Uses DMAC for 63450 and MFP for 68901.
- Multiple catalog ICs are supported.

2) Text VRAM and Graphics VRAM use bit-mapping methods.

- Screen resolution of 1024x1024 dots (supports display screens of 512x512 dots for graphics)
- Display resolutions can be selected from 768x512, 512x512, and 256x256.
- Supports both high resolution (31.5 kHz) and low resolution (15.98 kHz).
- In graphics mode, supports a color palette of 65536 colors, with 65536 selectable colors from the color palette (512x512 dots at selection time).
- In graphics mode at 768x512 dots, up to 16 colors from the 65536 colors can be arbitrarily selected per dot.

4) Smooth scrolling is possible in single dot units.

5) Sprite Features

- Can generate up to 128 sprites of a 16x16 dot pattern (maximum of 256 images).
- Up to 32 sprites can be displayed simultaneously in one line.
- Can display up to 128 sprites simultaneously on one screen.

6) Background switching capability.

7) Equipped with a function to prioritize sprites over the background in graphics mode.

8) Transparency specification, equipped with a semi-transparent sprite function.

9) Equipped with a superimpose function that uses high-resolution overlaid images (supports interlace method for reduced flicker).

10) CGROM includes ANK characters; JIS Level 1 and Level 2 Kanji are equipped as standard.

11) Equipped with FM sound source and voice-synthesis functions.

12) Equipped with a SCSI interface to support optical disk drives, such as CDROM as the next media, as well as analog RGB/I/F, RS-232C I/F, printer I/F, joystick I/F, mouse I/F, and other types of I/F.

13) Uses a cylindrical stepper motor type keyboard.

14) Equipped with 2 units of 5-inch floppy disk drives (2HD). Equipped with a trackball mouse.

15) Equipped with a 3.5-inch 80MB hard disk (CZ-634C-TN model comes with an internal optional hard disk).

16) SRAM Initialization Method

A simple function to initialize SRAM has been added to this machine. Without booting the OS, pressing the `CLR` key leads to a quick reset, and a message appears on the screen prompting for initialization. Press the `Y` key to initialize, or `N` key to cancel. This causes the SRAM to start in initialized state.

Note: Specifications and external appearance are subject to change without notice.

***

CZ-623C to major changes

■ Gate Array iX1197CE (OHM-2) …… changed to iX1748CE (ASA)
                iX1099CE(MESSIAH) …… changed to iX1749CE (DOSA)
■ Inhibit indicator connector addition
■ MPU HD68HC000PS10 …… changed to MC68HC000B16
■ FPU IC socket added
■ MPU clock can be set to two modes: 16.67MHz/10MHz.
■ 4M x 2 ROM iX1614CE (EVEN) …… changed to iX1775CE
                  iX1615CE (ODD) …… changed to iX1776CE
■ BIOS ROM replacement IC socket can be fitted on the 2MB expansion RAM module (CZ-6B2EA).
■ The SCSI connector can only be connected to SCSI-specification devices. (Non-SCSI devices such as the CZ620H cannot be connected.)
■ SCSI connector power terminal has a fuse to prevent overcurrent, with a 1A fuse installed. Do not use any fuses other than the designated ones.

About service correspondence for print substrate modules
For electronic controlled substrates, print substrate modules are subdivided as shown below. Please handle repairs by the respective method.

| Part name                  | Distribution code | Service response method                   |
|----------------------------|-------------------|-------------------------------------------|
| Main substrate unit        |                   | Response by unit parts exchange in the substrate |
| FD controller substrate unit|                   |                                           |
| Control substrate unit     |                   |                                           |
| I/O substrate unit         |                   |                                           |
| Power LED substrate unit   |                   |                                           |
| FD-LED substrate unit      |                   |                                           |
| Video substrate unit       |                   |                                           |
| Analog substrate unit      |                   |                                           |
| Keyboard unit              |                   |                                           |
| SCSI controller substrate unit | (CZ-644C)  |                                           |
| SCSI controller substrate unit | (CZ-634C)  |                                           |

**1-2. Specifications**
**<Hardware>**

| Item | Category | Name & Type | Contents | Notes |
| ---- | -------- | ----------- | -------- | ----- |
| CPU  | MPU      | MC68HC000   | 16-bit MPU (16.67MHz) |       |
|      | Sub CPU  | MSM80C51    | Keyboard scan         |       |
|      | DMAC     | HD63450     | 4-channel DMAC        |       |
|      | FPU      | MC68881     | Floating point arithmetic processor (16.67MHz) | Option |
|      | MFP      | MC68901     | Multifunction peripheral KEY scan presence, peripheral set inclusion |       |
|      | CRTC     | IX1093CEZZ (VICON) | Text/graphics control CRTC. Dual port DRAM control. Scroll function |       |
| Peripheral | LSI | 
| Sprite Controller | iX0906CEZZ (CYNTHIA) | Sprite function |
| FDC            | µPD72065          | Controls built-in 5-inch 2HD FDD |
| Video Controller | iX1095CEZZ (VIPS) | Display priority function. Special effects function |
| SCSI Controller | MB89352         | SCSI control |
| SCC            | Z8530            | Serial communication controller. Dual-channel (RS-232C, mouse) |
| RTC            | RP5C15           | Real-time clock |
| FM Sound Source | YM2151          | 8-channel FM sound source generation |
| PCM            | MSM6258          | Adaptive Differential PCM |
| Synthesis PPI  | µPD8255          | Joystick support. Sound source switching control |
| I/O            | iX1604CEZZ       | Floppy disk, peripheral IC decoder |
|                | iX1748CEZZ       | Memory controller (ASA) |
|                | iX1749CEZZ       | System controller (DOSA) |
|                | iX1094CEZZ       | Video data selector |
|                | iX1096CEZZ       | Video clock controller |

Note: CEZZ appears to be suffix for LSI chip codes, specifics can be machine dependent.

**Item** | **Category** | **Name/Type** | **Content** | **Remarks**

**Memory**

**ROM** | **CG ROM (combined IPL ROM)** | 1M byte (JIS first and second standards) | - |  

**RAM** | **Main Memory** | 2M bytes (Standard) | Can be expanded to 12M bytes (Selectable up to 6M bytes with inbuilt connector, in 2M byte units.) |  

**Text VRAM** | Bit Map Method | 1024 x 1024 Dot | 4 Planes |  

| | 512K x 4 Bit | - | Dual Port Type, for DRAM |  

**Graphics V-RAM** | Bit Map Method | 512K bytes x 1024 x 1024 Dot | 4 Planes | Dual Port Type, for DRAM | 

| | (512 x 512 Dot | 16 Planes) | - |  

**Sprite V-RAM** | 32K byte | - | - |  

**S-RAM** | 16K byte | - | - |  

**Media Storage**

- Inbuilt 3.5-inch hard disk 80M byte (Optional for CZ-634C) 
- Expansion floppy disk drive for disk expansion 

**Interface**

- **Floppy Disk Interface:** - 
- **SCSI Interface:** - 
- **Keyboard Connector:** For dedicated keyboards. 
- **CRT Interface:** For analog RGB output. 
- **TV Control Connector:** For dedicated display TV control. 
- **RS-232C Interface:** 1 channel RS-232C. 
- **Mouse Interface:** For attached trackball mouse. 
- **Printer Interface:** Centronics standard format. 
- **Joystick Interface:** Atari standard format (2 connectors). 
- **Audio Input/Output Connector:** Line in/output, headphone output. 
- **Video Input Connector:** For optional color image unit. 

**Additional Connections**

- **Other:** EXPWON, VHT
- **Expansion Slots:** 2 Slots
- **Power Supply:** AC 100V
- **Frequency:** 50/60Hz
- **Power Consumption:** CZ-644C: 46W, CZ-634C: 41W 

**Page 5**

<Functionality>

Item        Classification      Name-Category               Content                                                        Remarks
           Display Surface     Text Screen                 1024 x 1024 dots  4-plane        Bitmap Method
Size       Graphics Screen   1024 x 1024 dots  4-plane        Bitmap Method
```
                                                              (512 x 512 dots  16-plane)

           Text Surface       High-Resolution Mode          768 x 512 dots
                                                              512 x 512 

                                                              256 x 256 (2-plane reading)

                             Low-Resolution Mode            256 x 256
                             (Overscan)                     512 x 512
                             (Interlaced)

           Display Surface    High-Resolution Mode          768 x 512 dots                    Per dot 65536 colors
```
1024 x 1024                                                                         of which any 16 colors can be specified

```
                                                              512 x 512

                                                              512 x 256 (2-plane reading)
                                                              256 x 256 (2-plane reading)

                             Low-Resolution Mode            512 x 256
                             (Overscan)                     256 x 256

                             (Interlaced)

                                                              512 x 512

           Graphics Screen    High-Resolution Mode                                                          Per dot, 65536 colors out of which any
                                                                                                              16 colors can be specified (1 screen)
                                                                                                              Per dot, 65536 colors out of which any
                                                                                                              256 colors can be specified (2 screens)

                             Low-Resolution Mode

                                                          512 x 256 (Overscan) 256 x 256                                                                    Per dot, 65536 colors out of which any 
                                                          512 x 512 (Interlaced)                                                                        16 colors can be specified 
                                                                                                                                                                              (4 screens)
                                                                                                              512 x 512                                                                                  Per dot, 65536 colors out of which any 
                                                                                                                                                                              256 colors can be specified (2 screens)
                                                              256 x 256 (2-plane reading)

                                                                                                                                                                              Actual display screen size is smaller than 
                                                                                                                                                                              the left specified size.
```

CZ-634C-TN
CZ-644C-TN

Item	Content

Smooth Scroll Function
Text screens can be scrolled circularly in dot units. Graphics screens can be scrolled spherically in dot units.

Special Screen Control Function
Graphics VRAM image input function, text raster copy function, graphics high-speed clear, text bit mask function.

Priority Function
- Priority order can be specified among text, graphics, and sprites.
- Priority order can be specified for each graphics screen when using 2, or 4, graphics screens in the 512 x 512 dot mode of the graphics actual screen.

Palette Function
Any color can be switched instantaneously.

Half-Transparency Function
Half-transparent display is supported.

Special Priority Function
A function that can give the highest priority to any area of the graphics screen within the displayed screen.

Superimpose Function
- Low resolution overscan superimpose is supported. (Pseudo high resolution by interlace method is also supported)

Item	Class	Name/Type	Content
Sprite	Sprite	Pattern Definition	Size	16 x 16 dot pattern
```
			Number of Definitions	128 patterns (BG0,1 unused)
				(up to 256 patterns)
			Colors	16 colors / 65536 colors per pattern
				(dot units)
				256 colors / 65536 colors for the whole screen
		Display	Coordinate System	1024 x 1024 dots
			Display Screen	Horizontal 512 dots or 256 dots
				Vertical 512 lines or 256 lines
			Display Limit	128 sprites / screen
				32 sprites / line
```

1-3. Block Diagram

[Textual summary of the fold-out block diagram. Component names and clock values
were read directly from the source page); the original is a
large interconnected diagram that cannot be linearised exactly. The original text layer
of this page was unrecoverable noise and has been replaced.]

Processor / bus
- MPU: MC68HC000 (16.67 MHz / 10 MHz, 2-mode)
- FPU: MC68881 (IC socket)
- DMAC: HD63450
- CG / BIOS ROM: 1 Mbyte
- SRAM: 64 Kbyte

Clocks
- Main oscillator: 40 MHz / 33.33 MHz; also 16 MHz and 4 MHz
- Video / CRTC dot clocks: 38.863632 MHz, 69.5519 MHz, 50.350 MHz
- Sprite clock: 32.209 MHz

Video
- CRTC
- TEXT VRAM 512 Kbyte ×2
- GRAPHIC VRAM 512 Kbyte ×2
- Sprite controller + Sprite VRAM 32 Kbyte
- Video controller (GVA), Palette, D/A → CRT

Sound
- OPM (YM2151)
- ADPCM (MSM6258)
- PCM-PAN mixer → Amplifier → headphone/speaker, Line out, MIC in

Peripherals
- RTC (RP5C15, 32.768 kHz crystal)
- PPI (8255): ports A / B / C; Joystick 1, 2
- SCSI (MB89352) → SCSI HD
- FDC
- SCC → RS-232C
- MFP (MC68901)
- System controller, I/O control bus

# 1-4. System Configuration

This diagram shows the system expansion centered around the main unit.

**Main Unit**
- X68000
```
  CZ-63AC-TN
  CZ-64AC-TN
```

**Exclusive Display TV**

**Expansion Board**
- Expansion RAM Board (2M)
```
  CZ-6BE2 Expansion RAM (2M)
  CZ-6BE2B
```
- Expansion RAM Board 2 (4M)
  CZ-6BE4

**Universal I/O Card**
- CZ-6BU1

**GP-IB Board**
- CZ-6BG1

**Joystick Card**
- CZ-8NJ1

**Device RS-232C Card**
- CZ-6BF1

**Device Processor Board**
- CZ-6BP1

**Device Control Board**
- CZ-6BP2

**FAX Board**
- CZ-6BC1

**MIDI Board**
- CZ-6BM1

**Sound Amplifier Speaker**
- AN-S100

**Peripherals**
- Intelligent Joy Unit Controller
  CZ-8NU2

- Mouse
  CZ-8NM2A

- Mouse Trackball
  CZ-8NM3

**Network**
- Module Unit Controller
  CZ-8TM2

- RS232C Cable
```
  CZ-8LM1 (Programming)
  CZ-8LM2 (Library Link)
```

- LAN Port
```
  CZ-6BL1 (For Local Area Network)
  LAN Kit
  CZ-6BL2 (Including Adapter and TAP)
```

**Imaging and Image Input/Output Switch**
- Color Image Copier
  CZ-6VT1

- Color Image Scanner
  CZ-8NS1 GX-220X

- Video Capture Card
  CZ-6BV1

**Printer**
- 24-Dot Matrix Color/Monochrome Printer
  CZ-8PC3

- 48-Dot Matrix Color Printer
  CZ-8PC4

**Display Section**
- RGB System Selector
  CZ-6TU

**File Section**
- Removable Mass Storage Disc System (594MB)
  CZ-6MO1

**Print Buffer**
- Constant Print Buffer
  CZ-6EB1

**System Rack**
- System Rack
  CZ-6SD1

**24-Pin Dot Impact (13 Color)**
  CZ-8PG1

- 24-Pin Dot Impact (13 Color)
```
  Portable Printer
  CZ-8PG2
```

- Color Video Printer
  CZ-6PV1

- Color Image Printer
  I/O-735X I/O-735X-B

**24-Pin Dot (13 Color) with Scanner**
  CZ-8PK10

**CRT Filter**
  BF-6BP10 (14/15 inches)

2. Names of Each Part

2-1. Front of the Computer Body

1. Floppy disk drive access display lamp  
2. 5-inch floppy disk drive  
3. Eject button  
4. Headphone jack (PHONES)  
5. Joystick connector (JOY STICK 1)  
6. Power switch (POWER)  
7. Volume control knob (VOLUME)  
8. Keyboard connector (KEYBOARD)  
9. Mouse connector (MOUSE)  
10. Indicator panel  
11. Clock frequency switching switch (CLOCK SPEED)  
12. Reset switch (RESET)  
13. Interrupt switch (INTERRUPT)  
14. Carrying handle  

Page 10

2-2. Rear View of Computer Unit

1. Slot Cover (I/O SLOT)
2. Remote Terminal (REMOTE)
3. Printer Connector (PRINTER)
4. Frame Arm (FG)
5. Stereoscopic
6. Dedicated Stereo Display TV Control Terminal (TV CONTROL)
7. See-Through Color Terminal (SEE THROUGH COLOR)
8. Image Input Connector (IMAGE IN)
9. Analog RGB Signal Output Connector (ANALOG RGB OUT)
10. RS-232C Connector (RS-232C)
11. Audio Input Terminal (AUDIO IN)
12. Video Output Terminal (AUDIO OUT)
13. Joystick Terminal (JOY STICK 2)
14. Grounding Cord
15. Main Power Switch (POWER)
16. Service Connector (AC 100V OUT)
17. External Floppy Disk Drive Connector (EXPANSION FDD)
18. SCSI Connector

**CZ-634C-TN
CZ-644C-TN

3. Hardware
3-1. Memory Map**

**Key:**
- **CRTC**: Cathode Ray Tube Controller
- **VIDEO**: Video
- **DMA/C**: Direct Memory Access/Controller
- **NMI SET**: Non-Maskable Interrupt Set
- **INT**: Interrupt
- **R/W CTRL**: Read/Write Control
- **PRT IC**: Printer Integrated Circuit
- **FDD**: Floppy Disk Drive
- **HDC**: Hard Disk Controller
- **SCC**: Serial Communication Controller (Z8530)
- **8255**: Programmable Peripheral Interface (8255)
- **INT**: Interrupt
- **FPU**: Floating Point Unit
- **SPRITE REGISTER**: Sprite Register
- **SPRITE VRAM**: Sprite Video RAM
- **EEPROM**: Electrically Erasable Programmable Read-Only Memory
- **USER I/O AREA**: User Input/Output Area
- **SUPERVISOR I/O AREA**: Supervisor Input/Output Area
- **MEMORY SW (RAM)**: Memory Switch (RAM)
- **SYSTEM I/O**: System Input/Output
- **CG-ROM (128 KB)**: Character Generator Read-Only Memory
- **IPL ROM**: Initial Program Load Read-Only Memory
- **MAIN MEMORY (USER AREA)**: Main Memory (User Area)
- **GRAPHIC VRAM**: Graphic Video RAM
- **TEXT VRAM**: Text Video RAM
- **SUPERVISOR AREA**: Supervisor Area (User Area)

Additional labels within blocks:
- **06B0000H**: (Hexadecimal address), etc.
- **00FFFFFFH**: (Hexadecimal address limit)

Note: The addresses provided (like 06B0000H, 00CFFFFF, etc.) appear to be hexadecimal memory addresses used in the context of the system's memory map.

3-2 I/O Port Address List

* Indicates invalid. W is WRITE only, R is READ only, and R/W is READ/WRITE.

| Item | Port Address | Function | Remarks |
|------|--------------|----------|---------|
|  C   | E80000H      | Horizontal Scroll |
|  R   | E80002H      | Horizontal Synchronization End Position |
|  T   | E80004H      | Horizontal Display Start Position |
|  C   | E80006H      | Horizontal Display End Position |
|  C   | E80008H      | Vertical Scroll (Y) |
|  R   | E8000AH      | Vertical Synchronization End Position |
|  W   | E8000CH      | Vertical Display Start Position |
|  E   | E8000EH      | Vertical Display End Position |
|  T   | E80010H      | External Synchronization Adjust |
|  H   | E80012H      | Raster Register Write Position |
|  W   | E80014H      | X Axis Scroll X |
|  E   | E80016H      | Y Axis Scroll Y |
|  W   | E80018H      | Screen 0 X |
|  A   | E8001AH      | Screen 0 Y |
|  H   | E8001CH      | Screen 1 X |
|  E   | E8001EH      | Screen 1 Y |
|  O   | E80020H      | Screen 2 X |
|  P   | E80022H      | Screen 2 Y |
|  L   | E80024H      | Screen 3 X |
|  E   | E80026H      | Screen 3 Y |
|  S   | E80028H      | Memory Mode; Display Mode Setting |
|  E   | E8002AH      | Text Access, High-Resolution Clear Plane |
|  R/W | E8002CH      | Work Area Initialization Raster |
|  E   | E8002EH      | Bit Mask Register |
|  H   | E80040H      | CRT Control Register |
| Gra  | E82000H      | 16 Color Mode - 256 Color Mode | Graphics Palette |
| Pal  | E82010H      | or 65536 Color Mode | |
| let  | E8210EH      | |
|      | E82020H      | |
|      | (B821FEH) R/W |
| Tex& | E82200H      | Text (Sprite Color Table 0) Common Palette | Text, Sprite Palette |
| SP   | E8221EH      | |
| Pal  | E82210H      | |
| let  | (E82220H)    | Sprite Color Table 1 Palette | Sprite Palette |
|      | E8223EH      | |
|      | E82240H      | Sprite Color Table 2 Palette |
|      | E8225EH      | |
|      | (E8230EH)    | Sprite Color Table 15 Palette |
|      | E8232EH      | |
|      | E8233EH      | |
|      | E823F0EH)    | |
| Video| E82400H      | Memory Mode Setting |
| Cont-| E82500H      | Priority Setting |
| roller|E82600H      | Special Mode, Screen Display Control | Special Priority (Semi-Transparent) |

**CZ-634C-TN  
CZ-644C-TN**

| No. | Port Address | Function | Remarks |
|---|---|---|---|
| D | E84000H | R/W | Channel Status Register | However, regarding the addresses of each channel port, the port address (E$$$$$H) is added as follows: <br> Channel 0 <br> $$$$$H + 00H |
| M | E84001H | R | Channel Error Register |
| A | E84004H | R/W | Device Control Register |
| C | E84005H | R/W | Operation Control Register |
|   | E84006H | R/W | Sequence Control Register |
|   | E84025H | R/W | Normal Interrupt Vector |
|   | E84027H | R/W | Error Interrupt Vector |
|   | E8402DH | R/W | Channel Priority Register |
|   | E84029H | R/W | Memory Function Code |
|   | E84031H | R/W | Device Function Code |
|   | E84039H | R/W | Base Function Code |
|   | E8400AH | R/W | Memory Transfer Count (Word) |
|   | E8401AH | R/W | Base Transfer Count (Word) |
|   | E8400CH | R/W | Memory Address Register (LongWord) |
|   | E8401CH | R/W | Device Address Register (LongWord) |
|   | E8401DH | R/W | Base Address Register (LongWord) |
|   | E840FFH | R/W | General Control Register |
| Area Set | E86001H | W | Supervisor Domain Setting |
| M | E88001H | R | GRIP Data Register |
| F | E88003H | W | Active Edge Register |
|   | E88005H | W | Data Direction Register A |
|   | E88007H | R | Interrupt Enable Register A |
|   | E88009H | R/W | Interrupt Enable Register B |
|   | E8800FH | R/W | Interrupt Pending Clear A |
|   | E8800DH | R/W | Interrupt Pending Clear B |
|   | E8800EH | R/W | Interrupt Service Level A |
|   | E8800FH | R/W | Interrupt Service Level B |
|   | E88010H | R/W | Interrupt Mask Register A |
|   | E88011H | R/W | Interrupt Mask Register B |
|   | E88015H | R/W | Vector Register |
|   | E88091H | W | Type A Control Register |
|   | E88093H | W | Type B Control Register |
|   | E8808FH | W | Type C/D Control Register |
| P | E88071H | R/W | Type A Data Register |
|   | E88081H | R/W | Type B Data Register |
|   | E880E1H | R/W | Type C Data Register |

| Item | Port Address | Function | Remarks |
|------|--------------|----------|---------|
| M | E88025H | R/W | Timer D-Data Register | |
| F | E88027H | R/W | Sync Character Register | Unused |
| P | E88029H | W | USART Control Register | |
|   | E8802BH | R/W | Receive Status Register | |
|   | E8802DH | R/W | Receive Status Register | |
|   | E8802FH | R/W | USART Data Register | |

| R | E8A001H | R/W | 1 Second Counter / ICKLOUT Select | |
| T | E8A003H | R/W | 10 Second Counter / Adjust | |
| C | E8A005H | R/W | 1 Minute Counter / Alarm 1 Minute Register | |
|   | E8A007H | R/W | 10 Minute Counter / Alarm 10 Minute Register | |
|   | E8A009H | R/W | 1 Hour Counter / Alarm 1 Hour Register | |
|   | E8A00BH | R/W | 10 Hour Counter / Alarm 10 Hour Register | |
|   | E8A00DH | R/W | Day Counter / Alarm Day Register | |
|   | E8A00FH | R/W | 1 Day Counter / Alarm 1 Day Register | |
|   | E8A011H | R/W | 10 Day Counter / Alarm 10 Day Register | |
|   | E8A013H | R/W | 1 Month Counter | |
|   | E8A015H | R/W | 10 Month Counter / 12-24 Hour Select | |
|   | E8A017H | R/W | 1 Year Counter / 10 Year Counter | |
|   | E8A019H | R/W | 10 Year Counter | |
|   | E8A01BH | R/W | Mode Register | |
|   | E8A01DH | W | Test Register | |
|   | E8A01FH | W | Reset Controller | |

| Printer | E8C001H | W | Printer Data | |
|          | E8C003H | R | Printer Strobe | |
|          | E9C001H | R | Printer Busy | |

| System Port | E8E001H | R/W | Contrast Adjustment (D/A) | |
|              | E8E003H | R/W | TV Control | |
|              | E8E005H | W | Video Input Control | |
|              | E8E007H | R/W | H/L LED Lighting, NMI Reset, Key Control | |
|              | E8E00BH | R | MPU Operation Clock Frequency Determination Port | |
|              | E8E00DH | W | SRAM Write Enable Control | |
|              | E8E00FH | W | POWER OFF Control | |

| FM Sound Source | E90001H | W | FM Sound Register / Address Port | |
|                | E90003H | R/W | FM Sound Register / Data Port | |

| Sound Synthesis | E92001H | R/W | ADPCM Status (IN) / ADPCM Command (OUT) | |
|                  | E92003H | R/W | ADPCM Data Register (IN/OUT) | |
|                  | E9A005H | W | ADPCM Output, Sampling Frequency Switching Register | 8255 Port C |

| Item          | Port Address | Function                                                      | Remarks                      |
|---------------|--------------|---------------------------------------------------------------|------------------------------|
| Floppy Disk   | E94**1H R    | FDCA Status Register (IN)                                     |                              |
|               | E94**3H R/W  | FDC Data Register (IN/OUT)                                    |                              |
|               | E94**5H R/W  | Drive Status (IN/Drive Control OUT)                           | Optional Signal              |
|               | E94**7H W    | Access Drive Select, 2HD/2DD Switching (OUT)                  |                              |
| SCSI          | E96021H R/W  | Bus Device ID                                                 |                              |
|               | E96023H R/W  | SCSI Control                                                  |                              |
|               | E96025H R/W  | Command                                                       |                              |
|               | E96029H R/W  | Interrupt                                                     |                              |
|               | E9602BH R/W  | R...Re-Examine Status W...SCSI Controller Diagnosis           |                              |
|               | E9602DH R    | Status                                                        |                              |
|               | E9602FH R    | System Status                                                 |                              |
|               | E96031H R/W  | Phase Control                                                 |                              |
|               | E96033H R    | Data Transfer Counter                                         |                              |
|               | E96035H R/W  | Data Address                                                  |                              |
|               | E96037H R/W  | Temporary Register                                            |                              |
|               | E96039H R/W  | Transfer Byte Count High                                      |                              |
|               | E9603BH R/W  | Transfer Byte Count Mid                                       |                              |
|               | E9603DH R/W  | Transfer Byte Count Low                                       |                              |
| SCC           | E98001H R/W  | SCC Command Port B                                            |                              |
|               | E98003H R/W  | SCC Data Port B                                               |                              |
|               | E98005H R/W  | SCC Command Port A                                            |                              |
|               | E98007H R/W  | SCC Data Port A                                               |                              |
| Joystick      | E9A001H R    | Joystick 0                                                    | 8255 Port A                  |
|               | E98003H R    | Joystick 1                                                    | 8255 Port B                  |
| 8255          | E9A007H W    | 8255 Control Word Register                                    |                              |
| FD, PR        | E9C**1H R/W  | FDC, FDD, Printer Interrupt Status (IN)                       |                              |
|               | E9C**3H R/W  | FDC, FDD, Printer Interrupt Mask (OUT)                        |                              |
|               | E9C**5H R/W  | FDC, FDD, Printer Interrupt Vector                            |                              |
| FPU           | E9E000H R    | Response Register                                             | Internal Option              |
|               | E9E002H W    | Control Register                                              |                              |
|               | E9E004H R    | Status Register                                               |                              |
|               | E9E006H R/W  | Restore Register                                              |                              |
|               | E9E008H R/W  | Operation Word Register                                       |                              |
|               | E9E00AH W    | Command Register                                              |                              |
|               | E9E00CH -    | (Reserved)                                                    |                              |
|               | E9E00EH W    | Condition Register                                            |                              |
|               | E9E010H R/W  | Operand Register High Word                                    |                              |
|               | E9E012H R/W  | Operand Register Lower Word                                   |                              |
|               | E9E014H R    | Register Select                                               |                              |
|               | E9E016H -    | (Reserved)                                                    |                              |
|               | E9E018H W    | Instruction Address Register High Word                        |                              |
|               | E9E01AH W    | Instruction Address Register Lower Word                       |                              |
|               | E9E01CH R/W  | Operand Address Register High Word                            |                              |
|               | E9E01EH R/W  | Operand Address Register Lower Word                           |                              |

CZ-634C-TN
CZ-644C-TN

Item	Port Address	Function	Remarks
Expansion memory board / super visor setting port	EAFF81H W	Setting port for memory area 200000H~3FFFFFH	Valid only when an option board is installed.
```
	EAFF83H W	Setting port for memory area 400000H~5FFFFFH
	EAFF85H W	Setting port for memory area 600000H~7FFFFFH
```

Sprite	EB0000H R/W	Sprite X coordinate
```
	EB0002H R/W	Sprite Y coordinate	Sprite 0
	EB0004H R/W	Sprite control
	EB0006H R/W	Sprite priority

	EB03F8H R/W	Sprite X coordinate
	EB03FAH R/W	Sprite Y coordinate	Sprite 127
	EB03FCH R/W	Sprite control
	EB03FEH R/W	Sprite priority

	EB0800H R/W	Background 0 X coordinate
	EB0802H R/W	Background 0 Y coordinate
	EB0804H R/W	Background 1 X coordinate
	EB0806H R/W	Background 1 Y coordinate
	EB0808H R/W	Background control
	EB080AH R/W	Horizontal total
	EB080CH R/W	Horizontal display
	EB080EH R/W	Vertical display
	EB0810H R/W	Resolution
```

Sprite PCG area	EB0800H R/W	Sprite 0 PCG Area
```
	EB807EH R/W
	EBBF80H R/W	Sprite 127 PCG Area
	EBBFFEH R/W
```

Sprite text area	EBC000H R/W	Text area 0
```
	EBDFFEH R/W
	EBE000H R/W	Text area 1
	EBFFFEH R/W
```

**3-3. Area Set**

In this book, the data can be set in the register of E86001H in the range from the beginning of the memory to 2MB (000000H - 1FFFFFH), allowing any location to be set as a supervisor area in 8KB units from the beginning of the memory. 
- **Register Port Address**: E86001H, Write only 8-bit Register

```
D7  D6  D5  D4  D3  D2  D1  D0
       (Lower 8 bits are valid)
```

- **Operation**: In the range specification of 2MB from the beginning of the main memory, it becomes possible to specify the supervisor area by data settings.
```
    However, the setting is 8KB units (dividing 2MB into 256 parts).
    Example: Memory map when setting data is 7FH
```

000000H      Supervisor Area
000000H      Port Setting Value                    Port Data Setting Value         Supervisor Area
FFFFFFFFH
100000H      Supervisor & User Area               0                                0 ~ 1FFFFH (8KB)
```
                                                  1                                0 ~ 3FFFH
                                                  2                                0 ~ 5FFFH
                                                  3                                0 ~ 7FFFH
                                                  4                                0 ~ 9FFFH
                                                  5                                0 ~ BFFFH
                                                                                     .
                                                                                     .
                                                                                     .
```
                                             
200000H      Supervisor & User Area               127                              0 ~ FFFFFFH (1MB)
```
                                                                                     .
                                                 128                              0 ~ 10FFFFH
                                                                                     .
                                                                                     .
```
                                             
FFFFFFFH                                       254                                0 ~ 1FDFFFH
```
                                              255                                0 ~ 1FFFFFH (2MB)
                                                  
             Supervisor & User Area
```
FFFFFFFH

- **Expansion Memory Board Supervisor Setting Port**
    By writing data into the supervisor area setting port, it is possible to specify the supervisor area in 256KB units for the memory area on the extension board.

Memory Area               Supervisor Area Setting Port
200000 ~ 3FFFFFH          EAFF81H
400000 ~ 5FFFFFH          EAFF83H
600000 ~ 7FFFFFH          EAFF85H
                                  (Supervisor area mode write only port)

Writing Data
```
D7  D6  D5  D4  D3  D2  D1  D0
       (Lower 8 bits are valid)
```

Note: H means hexadecimal in the context of memory and register addresses.

Writing data of the 2-bit lower digit corresponds to each 256K byte memory region. Writing 0 addresses it to Supervisor-only region, and writing 1 addresses to Supervisor & User region. The initial state is set to Supervisor & User region.  
(Example) When EAFB| | HC-07 bit is written to the supervisor mode,  
200000 to 2BFFFFH: Supervisor Mode  
2C0000 to 3FFFFFH: Supervisor & User Mode

| Memory Region (HEX) | Corresponding Bit |
| --- | --- |
| Memory Region 0 | 000000~03FFFF | D0 |
| Memory Region 1 | 040000~07FFFF | D1 |
| Memory Region 2 | 080000~0BFFFF | D2 |
| Memory Region 3 | 0C0000~0FFFFF | D3 |
| Memory Region 4 | 100000~13FFFF | D4 |
| Memory Region 5 | 140000~17FFFF | D5 |
| Memory Region 6 | 180000~1BFFFF | D6 |
| Memory Region 7 | 1C0000~1FFFFF | D7 |

The above is valid when the optional 2M byte unit memory board is installed via the internal port connector. 
For example, in the case of expanding by 2M bytes, respond to each memory region 400000~5FFFFH and 600000~7FFFFH.   Note: EAFP83H and EAFP85H may become inactive.
Note) Models CZ-6BE2, 4/2/4M byte memory have the same port and function as the built-in ports.

3-4. System Ports

| No. | Register Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 |
|-----|----------------|-----|-----|-----|-----|-----|-----|-----|-----|
| 1   | E8E001H        | *   |     |     | *   |     |     |     |     | Contrast Adjustment |
| 2   | E8E003H        | *   |     |     | *   |     |     | 3DL | 3DR | TV Control FIELD |
| 3   | E8E005H        | *   |     | *   |     |     |     |     |     | Image Input Control |
| 4   | E8E007H        | *   |     | *   | *   |     |     | HRL |     | Key Control NMI Reset |
| 5   | E8E00BH        | *   | *   |     | *   | *   | *   | *   | *   | 10MHz/16MHz |
| 6   | E8E00DH        |     |     | SRAM Write Enable Control |
| 7   | E8E00FH        | *   |     | *   | *   | *   |     |     | *   | POWER OFF Control |

● System Port Register Address Map (* is invalid)
● System Port Register Details

| Bit | WRITE       | READ                 |
|-----|-------------|----------------------|
| D00 | 3DR         | 3DR                  |
| D01 | 3DL         | 3DL                  |
| D02 |             | FIELD                |
| D03 | TV Remote Signal | TV ON/OFF Status |

1. E8E001H[READ/WRITE]
    - 16-level contrast adjustment for the computer screen (value from 0H[dark]—FH[bright]).

2. E8E003H[READ/WRITE]
    - D03 WRITE MODE: By controlling “0” and “1”, it can be used as a TV remote signal. In READ MODE, you can know the TV ON/OFF status (0 for TV ON, 1 for TV OFF). However, it cannot be used simultaneously with the TV remote from the keyboard.

3. E8E005H[WRITE]
    - A system port for computer control of the optional "Digital Tape Recorder".

4. E8E007H[READ/WRITE]
   
| Bit | WRITE         | READ            |
|-----|---------------|-----------------|
| D01 | HRL           | HRL Status      |
| D02 | NMI Reset     |                 |
| D03 | Key Ready     | Key Jack Status |

Page -20-

.D01 is usually used for switching the dot clock, so usually set it to “0.”
Turn the NMI switch ON, and the MPU processes the highest priority interrupt (NMI interrupt). 
This NMI interrupt processing can be processed until the next clock interruption only when a reset is issued. 
So, if “1” is written to D02 after the CPU processing in the NMI interrupt routine, there is no need to reset this NMI. 
Also, if “1” is not written to D02, the NMI interrupt processing will not return, and the NMI switch will not function.

.D03 is used for WRITE MODE. During this mode, data can be sent from the CPU80C51 on the board to the MFPR (terminal).
The written data cannot be sent to the keyboard or the printer when “1” is written. In READ MODE, you can know whether the keyboard jack is connected to the keyboard by seeing if it is in a floating state ("1" when there is no connection and "0" when there is a connection).

5. E8E00BH[READ]

This port is used to determine the current operation mode of the MPU by setting it to Read Only.
Among the 8-bit data read to the port, only the value of bit 0 is valid (all other bits remain “1”).
When bit 0 is “1,” the MPU is in 10MHz operation mode, and when bit 0 is “0,” the MPU is in 16MHz operation mode (MPU operates at a clock frequency of 16.67MHz).

Note 1: For the 10MHz operation mode of CZ-600C series only, if this port is accessed, all bits other than bit 0 will remain “1.”

6. E8E00DH[WRITE]

Usually used for SRAM. It is set to Read Only, protecting the SRAM contents from being destroyed due to program runaway.
When “1" is written, SRAM Write Enable is set, and by writing any other value, it will be in Read Only mode.

7. E8E00FH[WRITE]

When entering 00H --> 0FH ---> 0FH in that sequence, the power (Vcc1 OFF) will be turned off.
Any other code sequence will be invalid. By doing so, it ensures that the power is not easily turned off.

# 3-5 Interrupts
< MPU68000 Interrupts >

| Level | Source | Description | Reason |
|-------|---------|--------------|--------|
| High 7 | NMI | Interrupt by external NMISW etc. (auto vector interrupt) | Auto vector interrupt |
| High 6 | MFP | Various timers, KEY data reception, H-SYNC, V-DISP interrupts (vector interrupt) | Vector interrupt |
| 5 | SCC | RS-232C, mouse data reception interrupt (vector interrupt) | Vector interrupt |
| 4 | Expansion | Expansion I/O slot | - |
| 3 | DMAC | Interrupts by data transfer etc. (vector interrupt) | Vector interrupt |
| 2 | Expansion | Expansion I/O slot | - |
| Low 1 | Floppy | FDC, FDD, hard disk, printer BUSY etc. interrupt | Printer (FDC > FDD > HD > Printer order of priority is configured) | Vector interrupt |

< MFP (Multi-Function Peripheral) Interrupts, read-out ports >

| Priority | Channel | Description | General Name |
|----------|---------|-------------|---------------|
| High 15 | 1111 | H-SYNC signal from CRTC | General Purpose Interrupt 7(7) |
| High 14 | 1110 | IRQ signal from CRTC (any raster selectable) | General Purpose Interrupt 6(6) |
| 13 | 1101 | V-DISP signal from CRTC | Timer A |
| 12 | 1100 | KEY data reception completion | Receiver Buffer Full |
| 11 | 1011 | KEY data reception error | Receive Error |
| 10 | 1010 | KEY data transmission completion | Transmit Buffer Empty |
| 9 | 1001 | KEY data transmission error | Transmit Error |
| 8 | 1000 | USART (keyboard) serial clock | Timer B |
| 7 | 0111 | CLKOUT signal from RTC (1Hz) | General Purpose Interrupt 5(5) |
| 6 | 0110 | V-DISP signal status from CRTC | General Purpose Interrupt 4(4) |
| 5 | 0101 | 8-bit general purpose timer (input clock 4MHz) | Timer C |
| 4 | 0100 | 8-bit general purpose timer (input clock 4MHz) | Timer D |
| 3 | 0011 | Interrupt detection from FM sound source | General Purpose Interrupt 3(3) |
| 2 | 0010 | ON/OFF detection by POWER switch | General Purpose Interrupt 2(2) |
| 1 | 0001 | ON/OFF detection by EXPWON signal from expansion I/O slot | General Purpose Interrupt 1(1) |
| Low 0 | 0000 | ON/OFF detection by ALARM signal from RTC | General Purpose Interrupt 0(0) | 

<Interrupt Vector Settings>

Breakdown        Register Address      D07  D06  D05  D04  D03  D02  D01  D00
MFP              E88017H                      Set
```
                                                    0 - Automatic interrupt end mode
                                                    1 - Software interrupt end mode
```

SCC
(Channels A and B shared)         Set in Register 2 for write

DMAC              E84025H                     Set
(Channel 0)                                   (Normal Interrupt Vector)
(Internal 2HD)       E84027H                     Set
                                                (Error Interrupt Vector)

DMAC              E84065H                     Set
(Channel 1)                                   (Normal Interrupt Vector)
(Hard Disk)          E84067H                     Set
                                                (Error Interrupt Vector)

DMAC              E840E5H                     Set
(Channel 2)                                   (Normal Interrupt Vector)
(Memory)            E840A7H                     Set
(Memory)                                    (Error Interrupt Vector)

DMAC              E840A5H                     Set
(Channel 3)                                   (Normal Interrupt Vector)
(Audio Synthesis)   E840E7H                     Set
                                                (Error Interrupt Vector)

Floppy            E9C003H                     Set
·Printer                                      FDC Interrupt       0 0
```
                                                FDD Interrupt       0 1
                                                Hard Disk Interrupt   1 0
                                                Printer Interrupt   1 1
```

(Note: "MFP," "SCC," "DMAC," "FDC," "FDD," and the like typically refer to specific hardware components or functionalities in computing, e.g., Multi-Function Peripheral, Serial Communication Controller, Direct Memory Access Controller, Floppy Disk Controller, Floppy Disk Drive, etc.)

# 3-6. IPL
- **IPL ROM address**: FC0000H - FFFFFFFH (256 KB)
- **Access**:
```
  1. Supervisor program, data area
  2. Read-only
```

Reset Sequence:
1. Upon reset, part of IPL ROM 1 (F******H) appears in the top 64 KB of the memory map (000000H-00FFFFH).
2. At the beginning of the IPL ROM 1, there are two long words that store the program counter and stack pointer values for the 68000 MPU reset exception process.
3. Once the reset signal is removed, the MPU fetches the long word data from the ROMs shown at the top of the memory map.
4. At this time, the MPU executes instructions based on the program counter. Meanwhile, the IPL ROM 1 image disappears, and the system goes into the state shown in figure 3-2.
> Note: The value of the program counter stored in the IPL ROM 1 must point within the address range of IPL ROM 1. This is because the hardware is designed so that accessing addresses (FF0000H-FFFFFFFH) makes the IPL ROM 1 image disappear from the top of the memory map. 
> The ROM image appears in the memory map upon power-on reset or manual reset (Figure 3-1). (The ROM image does not appear for the 68000 MPU reset command execution.)

Diagram 3-1 Diagram 3-2
| FC0000H ----                   | 
| IPL ROM1 ----------------| ------- IPL ROM1 |
| 00000H                    | --|
| 00FFFFEH                 | Main Memory 

**4. Screen Configuration and Control**  
**4-1. Screen Configuration**  

This machine has three independent screens: text, graphics, and sprite. Control of the text screen and graphics screen is carried out by the CRTC, and control of the sprite screen is carried out by the sprite controller. Additionally, various functions such as text screen, graphics screen, sprite screen priorities, .transparency, special priority functions, window functions on each screen, and screen blanking functions are controlled by the video controller.  
When accessing the screen, set the CRTC and sprite controller numbers regardless of whether they are used or not.

(Figure showing screen control block diagram)

**1) Text Screen (Bitmap Method)**

- Screen used for displaying ANK characters and kanji characters
- Similar to the graphics screen setting of the conventional X1 & X1turbo series, the display data direction is horizontal
- Scrolling of the text screen is cylindrical scrolling
- As a display mode, it supports both high resolution (horizontal scan frequency 31.5kHz) and low resolution (horizontal scan frequency 15.98kHz)

2) Graphics Screen
- A screen for performing graphics processing such as line drawing or painting.
- The display data settings are performed in the background.
- The scrolling of the graphics screen is a dual screen scroll.
- As a display mode, it supports high-resolution (horizontal sync frequency 31.5kHz) and low-resolution (horizontal sync frequency 15.98kHz).

[Illustration]
Top
Display Screen
Left  Right
Bottom

3) Sprite Screen
- A screen for smoothly moving sprite patterns dot by dot, as used in NES or MSX.
- As a display mode, it supports high-resolution (horizontal sync frequency 31.5kHz) and low-resolution (horizontal sync frequency 15.98kHz).

4-2. Control of Text Screen and Graphics Screen (CRTC)
This CRTC has the capabilities to support the dual port DRAM (MB81461) used in the text and graphics VRAM and has internal registers unique to the custom CRTC-23, providing the following screen control functions:
(1) Generation of horizontal and vertical sync signals
(2) Generation of display start and display timing signals
(3) Scrolling of text and graphics screens
(4) Automatic data transfer functions to graphics VRAM
(5) Line copy and bit mask functions for text VRAM
(6) Display single/double switching function, simultaneous access, and switching function
(7) Graphics VRAM high-speed access function
(8) External sync signal control function (at superimpose time)

Note that it can temporarily interrupt the CPU access to VRAM, depending on the need for V-DISP signal period (at MFPG0 GPIP4*="0"). Moreover, concerning DRAM's SAM (Serial and Control Merge) refresh cycle, it is controlled by the CRTC during the horizontal blanking period.

Page 26

**● CRTC Specifications and Internal Registers**

**Table 4-1 CRTC Specifications**

| Summary       | High Resolution | Low Resolution |
|--------------|----------------|----------------|
| Display Mode | Non-Interlace     | Interlace       |

|               | Horizontal (kHz) | Horizontal (usec) | Vertical (Hz) | Vertical (msec) |
|:-------------:|:---------------:|:----------------:|:-------------:|:---------------:|
| Synchronous Frequency |         31.5          |                  |      55.46      |                 | 
|                |        22.09          |     16.25             |     55.46       |   16.25           |
| Data Display Period (1) |        31.75         |     52.69             |      16.25      |   16.270          |
| Synchronization Period (2) |        31.75          |     3.45             |      18.03      |   0.191           |
| Synchronization Retrace Width (3)|   3.45             |     4.14             |      0.191      |   1.111           |
| Back Porch (4)|         4.14          |     4.94             |      1.111      |   0.876           |
| Front Porch (5)|        2.07          |     1.65             |      0.476      |   0.187           |

**[Diagram]**

(1) Video Signal
(2) Synchronization Signal
(3) Front Porch
(4) Back Porch
(5) Synchronization Retrace Width

* Video Signal: Analog 0.7Vp-p (75Ω termination) positive polarity
* Synchronization Signal: TTL level negative polarity

**Note**: The numbers `(1), (2), (3), (4), (5)` correspond to the parts of the diagram provided below the table in the original document.

**Special CRT Controller Features (Text)**
The text screen has the following features:
(1) Scroll
Performs scrolling on the display screen. Specifically, setting the horizontal register for R10 (E80014H) and the vertical register for R11 (E80016H) in terms of dot units will perform scrolling in the corresponding location.
(2) Simultaneous/Single Access
In light pen mode, enables simultaneous access to each plane of the text VRAM, or single access mode to perform single access with multiple simultaneous access. Specifically, in the case of single access mode, setting R21 (E8002AH) D08 allows simultaneous/single access to multiple planes of text VRAM for each address on D07-D04, respectively. If simultaneous access mode is chosen, please note that the specified planes will be accessed simultaneously.
(3) Raster Copy
Any raster (raster unit = 4 raster units) can have its address (0-255) copied to another raster position as a 4 raster line segment (1024 raster lines in each direction - up and down). Specifically, setting the source address of the raster copy registers R21 (E8002AH) D03-D00 to define the plane to copy from, then setting the source address for the destination raster registers R22 (E80020CH) D15-D08 and the destination address for the destination raster registers R DO7-D00 as the address to where the raster copy is performed. Therefore, if R21 (E8002AH) D03-D00 is set to '0', raster copy will not be performed.
For raster copying that uses the destination video RAM address during the horizontal blank period of the CRT controller source, once the raster line to be copied is allocated to the SAM (raster unit memory), and when the destination video RAM address is set, the horizontal blank period data is used to transfer the memory data to SAM.
(4) Bit Mask
The text VRAM read can be processed in 16-bit diagonal units in the horizontal direction. Specifically, a mask can be set for each 1 bit in the 16-b diagonal space (0-15) in 128X1 dot units. By setting bit D15-D08 in R23 (E8002EH) and bit mask 7 in D15-D00, then setting bit D09 in R21 (E8002AH) to '1' to use the bit mask. As for the speed in the text screen VRAM, uses simultaneous access and raster copy together. Be careful as using raster copy will have effects beyond mere display and can lead to actual data being affected.

**Special CRT Controller Features (Graphics)**
The Graphics screen has the following features:
(1) Scroll
Performs scrolling on the display screen. Specifically, setting the names of R12 (E80018H) and R13 (E8001AH) for the actual display 1024x1024 in terms of left and right scroll registers and vertical register in terms of dot units, scrolling is performed at that location. In the case of actual screen size of 512x512, the register (R12-R19) data corresponding to the graphics screen data is set to perform scrolling.

(2) High-Speed Clear

A function to clear the contents of the graphic VRAM at high speed. Specifically, the graphic display plane for high-speed clear of D00 to D02 is selected by R21 (E8002AH), and the graphic VRAM is cleared at high speed using E80480H D01. In this high-speed clear, the rising edge of the VDISP signal of E80480H D01 is latched, and the CRTC writes '0' (that is, clears the data) to the memory in the graphic VRAM every 1 horizontal blanking period by using the SAM (raster unit of the memory) inside the CRTC, resulting in the end of the period (2 vertical periods in the case of interlace).

(3) Image Capture

The function to capture TV and video images by connecting a digital sync tip option and using E80480H D00. That is, this image input is latched on the rising edge of the VDISP signal of E80480H D00 bit and the CRTC writes the image data of 1 screen to the graphic VRAM in the memory SAM (raster unit) inside the CRTC every 1 horizontal blanking period, ending at 1 vertical period (2 vertical periods in the case of interlace). However, this image input will not stop unless '0' is written to E80480H D00.

Page 29

4-3. Sprite
<Sprite Features>
This device is equipped with a unique sprite IC, and the sprite screen is independent of the text screen and graphics screen.
By using this sprite hardware, you can move any sprite pattern smoothly on a dot-by-dot basis. You can also use it in combination with the text and graphics screen's priority to configure various game screen structures.
Table 4-2 shows the specifications of the sprite IC and address map.

Table 4-2 Sprite Specifications

| Item      | Details                                       | Remarks                       |
|-----------|-----------------------------------------------|-------------------------------|
| Sprite Pattern |                                               |                               |
| Definition |                                               |                               |
| Size      | 16x16 dot pattern                              |                               |
| Fixed Number | 128 patterns in general                          | BG is not displayed           |
|           |                                               | Can define up to max 256 patterns |
| Colors    | 16 colors per 1 pattern                         | 16/65536 colors (dot units)   |
|           | Total for screen                               | 256 colors/65536 colors       |
| Display   |                                               |                               |
| SP Display |                                               |                               |
| SP Display High Resolution | 1024x1024 dots                        |                               |
| Display Units |                                               |                               |
| Display Control | Horizontal: 512 dots or 256 dots             |                               |
|           | Vertical: 512 lines or 256 lines               |                               |
| Display Units | 128 SP/screen                                 |                               |
|           | 32 SP/line                                      |                               |
| Additional Features | H-Flip, V-Flip, BG Priority               | Priority (BG0>BG1)            |
|           |                                               | SP Priority (SP0>SPn>SP127)   |
|           |                                               | (These features can be set    |
|           |                                               | on a per SP basis.)           |
  
| Background Pattern |                                               |                               |
| Display           |                                               |                               |
| Size              | 8x8 dot pattern                                |                               |
|                   | 16x16 dot pattern                              |                               |
| Fixed Number      | 8x8 dot pattern                                 | max 256 patterns              |
| Colors            | Shared with BG pattern and                    |                               |
|                   | sprite patterns                                |                               |
|                   | 16 colors per 1 pattern                         | 16/65536 colors (dot units)   |
|                   | Total for screen                               | 256 colors/65536 colors       |
| Display           |                                               |                               |
| BG Display        | Text scroll type                               | max 1024x1024 dots            |
| Max Screens       | Can display max 2 screens                      | (2 independent scrolls possible) |
| Display Units     |                                               |                               |
| Display Control   | Horizontal: 512 dots or 256 dots             |                               |
|                   | Vertical: 512 lines or 256 lines               |                               |
|                   | When BG1 is displayed with 512 lines          | (BG2 pattern size is fixed    |
|                   | 16x16 dots                                     | to 16x16 dots for display)    |
|                   | 256 dots fixed when displayed with BG2        | BG2 is also displayed in 8x8 dots fixed |

| Additional Features | H-Flip, V-Flip                               |                               |
|           | (These features can be set    |                               |
|           |  on a per BG basis.)            |                               |

4-4. Video Controller
This device's video controller has three internal registers, each having the following functions:

● Reg.1
· Setting the screen size of the graphics
· Setting the color mode of the graphics memory

● Reg.2
· Setting the priority between graphics, text, and sprites on the screen
· Setting the priority of the graphics screen

● Reg.3
· Setting the semi-transparent mode
  (This function enhances the priority of the graphics screen in a specified area on the display screen.)
· Setting the display mode of graphics, text, and sprites

When accessing the registers inside the video controller, please follow the same procedure as when accessing the CRTC signal, ensuring that the V-DISP signal within the MFP0 GPIP4 is set to "0".

4-5. Super Impose and Over Scan
This device supports the following two display modes:

(1) Low-resolution mode (Horizontal scan frequency 15.98kHz, Vertical scan frequency 60.52Hz)
· As a display mode, it supports two modes: Copy screen and Super Imposed screen. (When connected to a home-use display.)
· In Over Scan mode, the physical screen size displayed on the screen may decrease due to over scanning. (The screen size will largely remain the same both horizontally and vertically.) (Interlace)

| Physical Screen Size in Low-Resolution Mode | Actual Display Screen Size |
| --------------------------------------- | -------------------------- |
| 256×256                                 | Approximately 236×236      |
| 512×512                                 | Approximately 471×471      |

[Overscan] | [Normal Scan] (Traditional Display Method)

(Note: The dotted line represents the overscanned computer screen.)

- In this mode, in addition to the traditional superimpose modes from the X1 and X1turbo series, interlace-method pseudo high-resolution superimpose modes are also supported. In either case, it's overscan.
```
  Traditional Superimpose Mode:
  - Pseudo High-Resolution Superimpose Mode
  - 256x256
  - 512x512 (Interlace)
```

[Traditional Superimpose Mode] [Pseudo High-Resolution Superimpose Mode]

(Note: The dotted line represents the overscanned computer screen.)
Access the same memory data in both the odd and even fields of television scan lines.
Access different memory data in the odd and even fields of television scan lines.

(2) High-resolution image mode (horizontal sync frequency: 31.5kHz, vertical sync frequency: 55.46Hz)

- As a display mode, the computer screen is supported, but the superimposed screen is not supported.
- The computer screen only displays in normal scan.

[NORMAL SCAN]

<Diagram>

CRT screen display area

Border

Computer screen

The 256 x 256 two-tone reading mode is performed in the same way as the X1turbo high resolution 200-line mode.
(However, the horizontal and vertical sync frequencies are different.)

5. Miscellaneous Switches
(1) This unit is equipped with the following 3 types of switches.

(A) Reset Switch
- When you press this switch, a hardware reset is performed, and the processing begins at the address written in main memory 00000H.

(B) Interrupt Switch
- When you press this switch, the lowest bit of the status register and the NMI (non-maskable interrupt) signal come in, an external interrupt request is made to the address written in main memory 00007CH. The NMI processing routine writes 1 to E8E007H D02 and then performs an NMI reset. If D02 is not written to 1, the NMI processing routine is exited, and the NMI process is invoked again.

(C) POWER Switch
- The POWER switch has two modes: ON and OFF. When on (Vcc1 ON), the circuit operates at one stage. In the OFF mode, MPFP = POWER SW is in "OFF" (MPFP level 2 interruption), processing before sending MPFP to the MPU. If the MPU does not detect this condition within a control processing routine, it sends a stern instruction "OFF" "ON", "OFF" to the status register E8E00FH and prevents the missing detection. This prevents access to floppy disks and whenever the power is turned off.

(D) CLOCK SPEED Switch
- By this switch, you can set the clock speed of the MPU to either 10MHz or 16MHz.
- When operating (in Vcc1 ON state) change the clock speed, turn POWER OFF once, then switch and turn the power back on after switching.

Notes:
1) If you switch during operation (Vcc1 ON), the mode does not change. 
2) When you perform a reset switch during operation, you can change the mode, but normal operation of the system thereafter is not guaranteed.
3) The reset operation by software cannot change the mode.

Inspection results of power supply systems: In particular, the V1c1 may be turned ON due to the MPF1C failure and can be recognized.

(A) Vcc2 (RTC, SRAM, supply power for various circuits)

- Controlled by the rear power switch, can be turned ON and OFF. Do not use with timers and TV controls. Turn OFF the rear power switch after use.

(B) Vcc1 (RTC, SRAM, EXCLUDING key switches, supply power for almost all other circuits)

- The POWER2 switch is subject to an ON and OFF setting in reverse order of the rear power switch.
- The rear power switch being ON sets the front POWER switch to ON.
- The rear power switch being ON enables the expansion EXPWON signal in the expansion I/O slot.
- The rear power switch being ON enables the RTC2/ALARM timer signal in RTC ALARM time.
However, regarding Vcc1OFF, software system board E8E00FH having the value of "00", "OFF" and "OP" are meaningless.

(C) Backup power supply

- The rear power switch being OFF backs up the RTC SRAM. The backup power supply used to use two manganese dioxide LR batteries, but now it is using primary lithium batteries. Do not operate while charging the batteries.

(3) The LEDs on the front panel light up as follows (assuming Vcc2 is ON).

(A) 16MHz LED and 10MHz LED

- When the front POWER switch is ON and both Vcc1 and Vcc2 are ON, the LEDs correspond according to the MPU operation mode.
- If the POWER2 switch is OFF, it does not correspond to the LED. 
- When turning OFF the system with the front POWER switch ON, the LED remains in the state for a few seconds before the 10s internal processing is finished and it turns OFF.
- When Vcc1 is OFF but only Vcc2 is ON, the CLOCK SPEED switching state is shown on the LED as RED.

Vcc2    Vcc1    MPU     CLOCK           10MHz LED     16MHz LED
                    operation  SPEED SW
ON     ON      10MHz   x                 GREEN         OFF
                          16MHz   x                 OFF           GREEN
OFF            10MHz   RED            OFF
OFF            16MHz   OFF            RED
OFF     OFF                            OFF

(B) TIMER LED

- Using RTC and ALARM timer function to set RTC's register address, E8A00H's D04*1 sets "1" and turns the TIMER LED on. Conversely, when using the timer function, writing "0" turns it off. That is, this corresponds to D04*1, D04 is reset, and when Vcc2 is OFF, it is cut off, and the TIMER LED does not light even though the front POWER switch is ON.
 
(C) HD BUSY LED

- Indicating the internal hard disk access. It lights up during read/write operations of the hard disk.

Page - 34 -

(D) Floppy Disk Drive LED

| Front | Activity LED | Eject LED |
| - | - | - |
| POWER Switch | | |
| ON State | - When media is in the FDD<br>Green lights up<br>- When there is no media in the FDD and the LED flashing function is ON<br>Green blinks<br>- When there is no media in the FDD and the LED flashing function is OFF<br>Turns off<br>↓<br>If the FDD is read/written (drive present ON, read/write ON)<br>Green changes to red | - When the eject switch mask function is ON<br>Turns off<br>- When there is media in the FDD and the eject switch mask function is OFF<br>Green lights up |

| OFF State | - When there is media in the FDD<br>Green lights up<br>- When there is no media in the FDD<br>Turns off | - When there is media in the FDD<br>Green lights up<br>- When there is no media in the FDD<br>Turns off |

(4) This machine uses ports A and B of the 8255 as input ports for two joysticks, and also uses port C as a switching port for controlling the two joysticks, controlling the sound synthesis output and sampling rate switching. Therefore, by using the control word register of this 8255, it is necessary to specify port A and B as input and port C as output.  
<8255 Control Word Register (E9A007H)>

| D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 |
| - | - | - | - | - | - | - | - |
| 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

```
0 - Port C (lower 4 bits) output (sound synthesis)  
1 - Port B input (joystick No.2)  
0 - Port C (upper 4 bits) output (joystick control)  
1 - Port A input (joystick No.1)
```

Page 35

# 6. Keyboard and Mouse
This device uses the keyboard and mouse in the following block configuration.

<Main Body>
SCC
Data Bus
Control Bus
Address Bus
RTSB
RxDB
Vcc2
GND
GND
RDY

CPU System Board (EBE007H) 
Data Bus
Control Bus
Address Bus

MFP
RR
SO
SI
GND
TV Controller Remote Signal
Dedicated Disk Display

<Keyboard>
MSCTRL
Mouse Control
MSDATA
Mouse Data
MSDATA
Mouse Data
MSCTRL
Mouse Control

80C51
Vcc2
GND
TO
RxD
TxD
T1
<MFP->80C51 Send Data>
<80C51->MFP Receive Data>

GND
Vcc2

(CPU System Board (EBE003H))

Notes:
Regarding the control of the mouse and TV control, please use either control on the main unit or control on the keyboard side, or use them independently.

Figure 6-1 Keyboard and Mouse Surrounding Block Diagram

<Keyboard>
This keyboard uses the 80C51 as the sub-CPU, and performs the following roles:

(1) Transformation and transmission of key scan data to MFPA (refer to Table 1-3)
Unlike the X18&X1turbo series, this keyboard transmits the scanned key data to the sub-CPU without converting it to ASCII code. The serial data of one byte is then sent with information on whether the key was pressed or released. Regarding repeat functionality, this keyboard has the capability to control the start time (Delay 1) and the repeat interval (Speed), as well as the functionality to send the data of the pressed key (MSB) after the delay. This repeat functionality is valid for all keys (refer to Table 6-2).

(2) Transmission of TV control remote control signals
In the X18&X1turbo series, the TV control remote control signals are output to P27 (pin 38) of the main unit's 80C49 or P27 through 80C51 (port 1 TI). However, this keyboard has two ways to transmit these TV remote control signals from the main unit's MFPA: via software method and 1-byte data transfer from 80C51. Especially for this keyboard’s own TV remote control mode, sending the 1-byte data to MFPA through 80C51 validates the data as a TV control remote command sent from the main unit. Additionally, other system mode management is handled by the system board E8E003HJ D03. By this, the TV control remote signal can be sent through software timers. The commands valid for repeat control are TV Volume Up, Volume Down, Channel Up, and Channel Down.

(3) LED Lighting Control on the Keyboard
The illumination of the seven LEDs on the keyboard can be controlled via software. In other words, it’s possible to turn on, off, or flash arbitrary LEDs based on one-byte data transmitted from MFPA to 80C51. Moreover, LEDs are lit up when a specific key code generated by the keyboard reset signal is received; thus, it is possible to ascertain that the keyboard has been initialized by the main unit. Additionally, when the keyboard is reset (e.g., during power-up reset or keyboard replacement), the key code transmitted to the main unit indicates the LED status which is used to inform that the keyboard has been reset.

(4) Mask Control Signal (MSCTRL) Control
Transmitting one-byte data from the keyboard’s MFPA to 80C51 allows control of the MSCTRL signal. This is significant when the keyboard's mouse connector is used.

(5) Key Scan Data Transmission Error Code
80C51 outputs scan data directly via main and interrupt loops. However, if certain error prevention mechanisms within the MFPA or during the RR signal for data reading are unsuitable (triggering issues such as the system board E8E007HJ D01 becoming inactive), then key data transmission by 80C51 is invalid. In such a case, the keyboard enters an idle state until the data becomes acceptable for system board E8E007HJ D01 acknowledgment. This error state is resolved when the RDY signal transitions from a "0" state, in which 1-byte data transmission is permissible.

Table 6-1 Key Data Transmission Format

Baud Rate: 2400 baud

Key Data Transmission Sequence (Serial Transmission Asynchronous Communication)

| Start Bit  | 1 |
| Data Length | 8 |
| Stop Bit   | 1 |
| Parity None |   |

(6) Key Assignment for X1 Control in Designated TV Control Keys

For the following TV control keys, sending 1-byte data from MFP to 80C51 allows them to be used as TV control keys for X1 punch.

| Operation Key       | CZ-600C                         | X1 Punch Mode           |
|----------------------|--------------------------------|--------------------------|
| TV Control Key ++   | Superimpose/Superimpose Toggle Key | Superimpose                |
| TV Control Key +=   |  TV/External Input Toggle Key       | TV                        |
| TV Control Key +    |  TV/Computer Screen Toggle Key     | Computer Email             |

(7) Control of TV Control Mode and Mouse Control Mode

By sending 1-byte data from this MFP to the 80C51, you can toggle the ON/OFF state of the keyboard's TV control key or mouse control key, respectively. Typically, like the SHIFT key, if you hold down a TV control key or mouse control key while pressing another key, the key will be controlled. In this control mode, these toggle operations retain their state until pressed again for the second time, which cancels the previous key state. In this mode, once the TV control key or mouse control key turns ON, it will remain ON until turned OFF, and it keeps holding the key down functionality. Standard key codes are sent from the MFP.

Table 6-2 Key Scan Data Format:

D7 D6 D5 D4 D3 D2 D1 D0
| Key Scan Code |
```
0 - Key pressed state
1 - Key not pressed state
```

1-byte data from 80C51 to MFP
Key code reference is in figure 3-2

CZ-634C-TN
CZ-644C-TN

7. Sound Function

This machine uses the YM2151 as the FM sound source LSI and the MSM6258 as the voice synthesis LSI.

Fig. 7-1 Sound System Block Diagram

Labels in the diagram:

- Data
- Address
- Control
- Buffer
- Decoder
- FM Sound Source (YM2151)    Vcc1 Vss CLK(4MHz)
- µPD8255 PC    Vcc1 Vss
- ADPCM (MSM6258)    Vcc1 Vss CLK(4MHz)
- PCM PAN
- Built-in Speaker
- Headphone Out
- Amp
- L line Out
- R line Out
- R TV AUDIO
- L TV AUDIO
- line In

7-1. FM Tone Generation

● LSI YM2151
<Features>
(1) Up to 8 tones can be generated. However, for sinusoidal waves, up to a maximum of 32 tones can be generated.
(2) Noise generation.
(3) Pitch and time modulation.
(4) In addition to the fundamental wave, allows irregular modulation of the upper harmonics.
(5) Allows detuning of the 7th harmonic.
(6) Adjustment of pitch with 1.6 cent accuracy.
(7) Vibrato and tremolo operation.
(8) Enables various sound effects due to deep vibrato and frequency modulation as well as detuning of the upper harmonics along with the fundamental wave.
(9) Includes two types of timers.

7-2. Voice Synthesis

This system uses MSM6258 in ADPCM method as the voice synthesis LSI. PCM's output control, sample frequency conversion, and switching are performed by the 8255's ports and Ck. The LSI converts voice input to digital via S&H (Sampling & Hold) and AD converter, and when using the PCM (Pulse Code Modulation) code, the difference between the predicted value and the actual value is quantized using the ADPCM (Adaptive Differential PCM) method, reducing the amount of information. Additionally, through the above process, the resulting output is converted back to its original form using a digital-to-analog converter (DAC).

<Features>
(1) 4-bit straight ADPCM method
(2) ADPCM dedicated memory/voice synthesis capability built-in
(3) Built-in DRAM refresh, MPU interface circuit
(4) Sampling frequency: 3.9, 5.2, 7.8kHz
(5) Reference frequency: 4MHz
(6) Built-in AD converter: 8-bit
(7) Built-in DA converter: 10-bit
(8) DA output format: A class (voltage type)

(End of page 41)

**CZ-634C-TN**  
**CZ-644C-TN**  

**8. Peripheral LSI**  
**8-1. DMAC**

In this book, the 63450 is used as the DMAC. This is an independent 4-channel DMAC, and in this machine, it is allocated as shown in Table 8-1.

**Table 8-1 Allocation of each DMAC channel**

| Channel No. | Allocation      | Transfer Demand   | Block Transfer     |
|-------------|-----------------|-------------------|--------------------|
| 0           | Internal 2HD    | External Transfer Request | Cycle Steal Mode      |
| 1           | SCSI Device     | Auto Request | Full Channel Dual Address Mode  | 
|             |                 | Max Speed   | Full Channel (programmable)   |
| 2           | Memory Memory   | Auto Request | Continue Mode  |
|             |                 | Limited Speed and Max Speed  | Array Chain Mode   |
| 3           | Sound Synthesis | External Transfer Request | Cycle Steal Mode  |
|             |                 |               | Link Array Chain Mode  |

**Figure 8-1 DMAC Block Diagram**

- 68000  
- Address Bus
- Data Bus
- Control Bus
- CLK (10/16MHz)
- Vcc1
- Vss

- 63450  
- CLK (10MHz)
- Vcc1
- Vss
- Ch0 Internal 2HD
- Ch1 SCSI Device
- Ch2 Memory Memory
- Ch3 Sound Synthesis

**<Features>**
This DMAC has the following features. Also, Table 8-2 shows the DMAC transfer request methods, and Table 8-3 shows the DMAC data block transfer.

(1) Equipped with 4 independent DMA channels (priority is programmable).
(2) Enables transfers between memory to memory, and memory to I/O devices.
(3) Supports block transfer functions of Continue Mode, Array Chain Mode, and Link Array Chain Mode.
(4) Programmable transfer using internal registers.
(5) Supports error detection and high-reliability data transfer functions with vector error splitting and exception handling.
(6) Maximum 5 MBytes/sec. (10MHz)
(7) Compatible with the 68000 bus.

**Table 8-2: DMAC Transfer Request Methods**

Transfer Request Methods
- External Transfer Request (using the REQ pin)
```
  - Cycle Steal Mode
    - Transfers at each operation's timing. Releases the bus at each transfer completion.

  - Cycle Steal Burst Hold Mode
    - Transfers at each operation's timing. However, does not release the bus for a fixed period after transfer.

  - Burst Mode
    - Transfers multiple operations consecutively.
```

- Auto Request (not using the REQ pin)
```
  - Fixed Speed
    - Transfers multiple operations consecutively. However, periodically releases the bus during certain intervals and does not monopolize the device.

  - Maximum Speed
    - Transfers multiple operations consecutively. However, releases the bus during certain intervals and monopolizes the device until the transfer is completed.
```

- Auto Request (only transfers the first operand) + External Transfer Request (transfers operand from the 2nd one onward)

**Table 8-3: DMAC Data Block Transfer Methods**

- Single Data Block Transfer
  - Assigns the transfer address and transfer word count to internal DMAC registers.

- Multiple Data Block Transfer
```
  - Continue Mode
    - Assigns the transfer address and transfer word count to internal DMAC registers, and sets the CNT bit to indicate the presence of the next data block.

  - Array Chain Mode
    - Creates an array table in main memory.

  - Link Array Chain Mode
    - Creates a link array table in main memory.
```

8-2. Floating-Point Arithmetic Co-Processor

In this device, it is possible to optionally use the floating-point arithmetic co-processor (hereinafter abbreviated as FPU) MC68881 (16.67MHz).

![Diagram of FPU signal block]
**MC68881 Main Features**
● 8 80-bit floating-point data registers
● 67-bit arithmetic device
● 67-bit barrel shifter and high-speed shifter
● 46 instructions
● Complete compliance with the IEEE 754 standard
● Support for functions not defined by the IEEE standard
  (transcendental functions such as trigonometric and logarithmic functions)
● 7 types of data types
  (byte, word and longword integer, single-precision real number, double-precision real number, extended-precision real number, packed BCD real number)
● Support for 22 constants in on-chip ROM (including π)
● Virtual memory compatible operation
● Efficient handling of exceptions, interrupts, and inserted processing mechanisms
● Parallel execution of main processor commands
● Compatible with hosts with 8-bit, 16-bit, or 32-bit data buses
The IC slots on the FPU-compatible motherboards detect the presence of an FPU or not, and automatically judge whether an FPU is installed in the motherboard IC slot. If the FPU is not installed in the motherboard IC slot, connecting it to the corresponding CPU socket on the CZ-6BP1 expansion slot will enable proper function.
However, if the FPU is installed on both the motherboard and the I/O slot processor board, the system will recognize the FPU on the motherboard as the priority and operate accordingly. Therefore, ensure not to have duplicate installations.

8-3 Expansion Main Memory
(1) Internal Expansion Board (CZ-6BE2A, CZ-6BE2B)
* Expansion by 2MB units up to a maximum of 6MB (Actual maximum with internal extension of 8MB)
Installed on expansion board

* 2MB Memory Install Range
   Installation range: 200000~3FFFFF H

* Connector for 2MB Memory Module
```
   Connector 1: 400000~5FFFFF H
   Connector 2: 600000~7FFFFF H
```

* BIOS ROM Mount IC Socket (2 of 1MB EPROM)
* BIOS ROM Replacement Switch

* The memory controller automatically determines the presence or absence of the above three 2MB memory boards by checking the following three signals (Each signal is enabled when LOW level):
```
   DRAMSENSE1 Signal: 200000~3FFFFF H Memory
   DRAMSENSE2 Signal: 400000~5FFFFF H Memory
   DRAMSENSE3 Signal: 600000~7FFFFF H Memory
```

If this function is not used and the internal expansion board is not used, the previously used IO slot 2.4MB memory board attachment is enabled. (CZ-6BE2,4)

* Accessible in sync wait at both 16/10MHz.

(2) Adding memory on IO slot
```
   Possible to expand memory according to internal switching range
   * In the case of 8MB installed, 4MB can be expanded on the IO slot
   * In the case of 6MB installed, 6MB can be expanded on the IO slot
   * In the case of 4MB installed, 8MB can be expanded on the IO slot
   * In the case of 2MB installed, 10MB can be expanded on the IO slot
```
 
(Note) IO slot memory boards are inaccessible in non-wait state at 16MHz mode. (Possible at 10MHz mode)

# 8-4. MFP

In this unit, we use the 68901 from the 68000 family for data transmission and reception with the keyboard, timer functions, and various interrupt controls.

**CLK RESET Vcc1 Vss (4MHz)**

**Internal Control Logic**

**Timer C, D** (Delay Mode)
- XTAL1 (4MHz)
- XTAL2 (4MHz)
- TCO (N C)
- TDO (N C)

**Timer A** (Event Count Mode)
- TAO (N C)
- TAI (CRT0 V-DISP signal)

**Timer B**, (Delay Mode)
- TBO (USART serial clock)
- TBI (N C)

**USART** (Keyboard)
- Rx (Reception Data)
- SI (Keyboard/Reception Data)
- RC (TBO input)
- SO (Keyboard send data)
- TC (TBO input)
- Tx (Send Data)

**GPIP**
- GPIP0 (RTC Alarm signal based on detection of ON/OFF)
- GPIP1 (EXPWON signal based on detection of ON/OFF)
- GPIP2 (POWER SW signal based on detection of ON/OFF)
- GPIP3(VCC2 drop signal detection)
- GPIP4 (CRT0 V-DISP signal detection)
- GPIP5 (RTC CLKOUT (1Hz) signal)
- GPIP6 (RTC 1QR signal)
- GPIP7 (CRT0 H-SYNC signal)

**Interrupt Control**

- IRQ
- IEI
- IEO
- IACK

**Data** (8)
**Register** select (5)
**CS
R/W
DS
DTACK**

**CPU Bus I/O**

**Figure 8-3 MFP Block Diagram**

Page 46

<Features>
This MFP has the following features:
(1) Control of priority interrupts (interrupt control from various sources)
(2) Internal timer with 4 channels (2 diversification modes, 1 event count mode, 1 Ch)
(3) Contains a 2-channel USART (board-to-board communication reception)

<68901MFP Interrupts, Read Address Channel>

Decoder

68000MPU

| High      | INT7
IPL0       | Priority | INT6
IPL1       | Priority | INT5
IPL2       | Priority | INT4
| Low       | INT3
|           | INT2
|           | INT1

| Priority bits:
High       | 15   | GPIP7 (CRTC's H-SYNC signal)
```
              14   | GPIP6 (CPTC's IRQ signal)
              13   | TimerA (CPTC V-DISP signal)
              12   | Receive Buffer Full (Data reception)
              11   | Receive Error (Data reception error)
              10   | Transmit Buffer Empty (Data transmission)
               9   | Transmit Error (Data transmission error)
               8   | TimerB (USART serial clock)
               7   | GPIP5 (RTC 1Hz clock signal)
               6   | GPIP4 (CRTC V-DISP signal monitor)
               5   | TimerC (General 8-bit timer)
               4   | TimerD (General 8-bit timer)
               3   | GPIP3 (Power supply detection)
               2   | GPIP2 (POWER SW ON/OFF detection)
               1   | GPIP1 (Expansion slot detection or EXPWON signal ON/OFF detection)
```
Low        |  0    | GPIP0 (RTC ALARM signal ON/OFF detection)

Figure 8-4 MFP interrupt block diagram

(TAI)
(CRTC's V-DISP signal)

(4MHz)

Figure 8-5 MFP timer block diagram

CZ-634C-TN
CZ-644C-TN

Inside the main diagram:

TBO terminal
RC terminal
TC terminal

USART (x16)

SI (Keyboard receive data)
SO (Keyboard send data)
RR (Receive status)
TR (Transmit status)

Box on the right side of the diagram:

Asynchronous communication
2400 baud
Start 1 bit,
Data 8 bits
No parity,
Stop 1 bit

Fig. 8-6 MFP USART System Block Diagram

Table 8-4 Details of MFP Channels

| Channel No. | Function Details                                                                            |
|-------------|---------------------------------------------------------------------------------------------|
| QPIP7       | Generates an interrupt when a rising edge of the CRTC H-SYNC signal is detected. (Set "0" to the active edge register bit) H-SYNC |
| QPIP6       | Generates an interrupt when the programmed edge (R09(E80012H)) of the CRTC is detected, or generates an interrupt when the falling edge of the CRTC IRQ signal is detected. (Set "0" to the active edge register bit) |
| TimerA      | Generates an interrupt when the rising edge of the CRTC V-DISP signal is detected. In Pulse Width Count Mode, generates an interrupt when the counter overflows and sets the BCD counter overflow flag. |
| Receive Buffer Full | Generates an interrupt when data is received by the keyboard (when reception data is transferred from the reception shift register to the reception buffer, and D07 of the reception status register is set to 1). |
| Receive Error | Generates an interrupt when an error occurs during data reception by the keyboard (overrun error, parity error, or frame error) and sets D06 to 1, D05 to 1, or D03 to 1 of the reception status register. |
| Transmit Buffer Empty | Generates an interrupt when data is transmitted from the keyboard (when transmission data is transferred from the transmission buffer to the transmission shift register, and D07 of the transmission status register is set to 1). |
| Transmit Error | Generates an interrupt when an error occurs during data transmission by the keyboard (unexpected acknowledgment or completion of asynchronous transmission) and sets D06 to 1 or D04 to 1 of the transmission status register. |
| TimerB      | Generates an interrupt when the internal clock (4MHz) is input (delay mode), and changes the MFP USART (keyboard) input clock from 38400Hz to match. However, it is not used when the keyboard is utilized in serial clock mode. |
| QPIP5       | Generates an interrupt when the state change is detected on the signal of the RTC CLKOUT(1Hz). |
| QPIP4       | Reads the state of the CRTC V-DISP signal. When "1" and "2", it indicates the vertical sync period, and "0" when "L" indicates the vertical display period. (Interrupt cannot be generated) |
| TimerC      | Generates an interrupt when the internal clock (4MHz) is input (delay mode), and uses the arbitrary set prescaler and BCD counter when the BCD counter reaches 00H. |
| TimerD      | Generates an interrupt when the internal clock (4MHz) is input (delay mode), and uses the arbitrary set prescaler and BCD counter when the BCD counter reaches 00H. |

Channel No.  / Function Details

GPIP3
When Vcc2 (secondary main power source) is detected, it reads whether it has been reinserted. An "H" indicates detection of Vcc2, while a "0" indicates "L". When Vcc2 is detected, GPIP3 automatically becomes "0". However, if Vcc2 is detected again after being cut off, GPIP3 will change to "1". If GPIP3 remains "0" even after Vcc2 is detected, it signifies that the front power (POWER switch) is ON. When the POWER switch is ON, all subsequent detections will show "12" on GPIP3 instead of "0". The MPU will determine if Vcc2 is inserted and must set GPIP3 to "1" by writing "12" to E8A0 and D056 registers. Access the RTC registers with the previously saved values. Generally, reading will prevent using the port report.

GPIP2  
The POWER switch reads whether the computer power (Vcc1) is ON or OFF. Normally, the switch state is "0" or "L" (OFF), but pressing it changes it to "1" or "H". When pressing the switch again, it reverts. Ensure the signal step prevents the malfunction.

GPIP1  
Reads whether the computer power (Vcc1) is ON by using the EXPWON signal from the expansion bus slot. When external sources except EXPWON are given, it is "0" or "L". Verify if the computer power is ON by checking GPIP1.

GPIPO  
Uses RTC ALARM timer to generate ALARM signals, and determines if the computer's power (Vcc1) is ON with the ALARM signal. "H" on power ON remains "H" without ALARM signals. After a minute, it goes "L". Monitoring GPIP0 within 1 minute reveals if power was ON or OFF. This signal, combinable with 1Hz and 16Hz clock pulses, can generate any status changes based on the signal power.

Additionally, regarding GPIP0 to GPIP3, it checks from where the computer power was turned ON. The flowchart is shown below.

[Power ON/OFF]

When Vcc1 turns ON Check MFP's GPIP2

```
                    "0"                     "1"
                       ↓                        ↓
```
Power switch is turned ON        Check MFP's GPIP1

```
                         "0"                           "1"
                       ↓                                ↓
```
Turned ON by the EXPWON signal from the expansion I/O slot        Check MFP's GPIP0

```
                         "0"                                              "1"
                       ↓                                                    ↓
```
Turned ON by the ALARM signal from the RTC ALARM timer         Recheck GPIP2, GPIP1, and GPIP0. After final verification, write “00H” to system port E8E00FH to “OFF” and turn off power

The page number at the bottom reads "51." The model numbers mentioned at the top right are CZ-634C-TN and CZ-644C-TN.

Top Left:
CZ-634C-TN
CZ-644C-TN

Middle Right:
RS-232C
Mouse Connector Pinout

Bottom Center:
Fig. 8-7 SCC Block Diagram

Bottom Center:

Other Labels in the Diagram:
TxDA, RTSA, DTRA, D/C, A/B, RxDA, CTSA, DCDA, RxCA, CTCA, CTCS, DCDB, DTRB, CE, RD, WR, DO-D7, PCLK, TRxCA, RTSB, RxDB, IRQ, INT, INT ACK, IEI, GND, Vcc

(5MHz) Vcc2, 4.7 kΩ, Vcc1, GND
RTC, CTS, DSR, ST1, ST2, CI, CD, SG, FG
Mouse
MSCCTRL, MSDATA, GND

75188
+12V, -12V, Vcc, TxD, RTS, DTR, ST1

75189A
(290pF × 4), RxD, CTS, DSR, RT

75189A
(290pF × 3), ST2, CI, CD, SG, FG

Keyboard
MSDATA

**8-5. SCC**

In this manual, the RS-232C serial communication controller is used to support the mouse. We use the Z8530 SCC for the Z8000 family. The block diagram is shown in Fig. 8-7.

<Features>
This SCC has 2 independent full-duplex channels, each with 14 write registers and 7 read registers, and a baud rate generator.

(1) Channel A (RS-232C)
```
  * Asynchronous Mode
    - 5, 6, 7, 8-bit character
    - 1, 1.5, 2 stop bits per character
    - Even parity, odd parity, no parity
    - x1, x16, x32, x64 clock rate
    - Block generation and detection
    - Parity, overrun, and framing error detection

  * Synchronous Mode
    - Byte-oriented synchronous mode: The character synchronization can be internal, external, or either
      1 to 2-character synchronization
      The synchronization character can be 6 to 8 bits
      The automatic insertion or exclusion of synchronization characters
      CRC generation and verification
    - SDLC/HDLC mode: Generation and detection of address field
      Automatic zero insertion and deletion
      Automatic flag insertion between messages
      Detection of address field
      Information field protection
      CRC generation and verification
      EOP detection and escape (online escape) in SDLC loop mode

  * Data Transfer Rate
    - Maximum 1.5 Mbits/sec (NRZ signal mode)
    - Maximum 375 Kbits/sec (FM encoding mode using DPLL)
    - Maximum 187 Kbits/sec (NRZI encoding mode using DPLL)
```

(2) Channel B (Mouse)
```
  * Asynchronous Communication
    - Baud Rate: 4800 baud
    - Start Bit: 1 bit
    - Data Bits: 8 bits
    - Parity: None
    - Stop Bits: 2 bits
    - Data Bus: RXDB
    - Control Bus: RTSB
```

**(3) SCC Register Details**

For the access to each write/read register (write-only register WR3 and read/write register RR8 are excluded), “Command Mode” must be utilized. First, select the register to access using bits D00- D02 of WR0. After designating the accessed register, reading/writing to the data register will allow you to read/write data. Here, access to each register is configured through the reading/writing of the data.

Also, concerning the access to write-only register WR8 and read/write register RR8, you can read/write data by accessing the Data Port. Table 8-5 shows the baud rate generator clock number for each baud rate.

**Table 8-5 Clock number for each baud rate**

| Baud Rate | Clock for 5MHz (in hexadecimal) | Remarks                                    |
|-----------|----------------------------------|--------------------------------------------|
| 9600      | (14(000EH))                      | 5×10^6                                     |
| 4800      | (31(001FH))                      | Clock number = ---------                   |
| 2400      | (63(003FH))                      |                    2                        |
| 1200      | (128(0080H))                     | 2 × (Baud rate × 16)                       |
| 600       | (258(0102H))                     |                                            |
| 300       | (519(0207H))                     | However, when the input clock (PCLK) is 5MHz|
| 150       | (1040(0410H))                    | and data speed uses a 16x clock.           |
| 75        | (2081(0821H))                    |                                            |

**8-6. RTC**
This machine uses RP5C15 as the Real-Time Clock (RTC).

**RTC Block Diagram**

+-----------------------------+
|          RP5C15             |
|                             |
| +-------------------------+ |
| |    Address (4-bit)      | |
| |    Data (4-bit)         | |
| |    Control              | |
| |    Battery Backup/Vcc2  | |
| +-------------------------+ |
|             |               | 
|    +---------------+        |
|    |CKOUT (1Hz) Clock       |
|    +---------------+        |
|             |               |
| ALARM (Alarm signal, 1Hz,   |
|        16Hz Clock)          |
|             |               |
+-------------|---------------+

|                    |
|                    |
|         +------------------------+
|         |      GPI(PF)           |
|         |      Write/Read        |
|         +------------------------+
|                    |
+------- POWER LED & TIMER LED ON/OFF

|                    |
|                    |
|         +------------------------+
|         |      GPI(PF)           |
|         |      Read              |
|         +------------------------+
|                    |
+--------+

**<Features>**

This RP5C15 has the following features with the same READ/WRITE sequence of the memory providing the settings and reading outputs of time using real-time clock.

(1) Possible to connect directly to the 16-bit CPU and allows high-speed access
(2) Address and data bus (D00-D03)
(3) 4-bit address input
(4) Embedded counter (year, month, day, hour, minute, second) calendar (supports until the year 2099)
(5) Internal alarm function
(6) All time data can be displayed in BCD code
(7) Internal 30 seconds adjust function
(8) Battery backup possibility (requires 2.0V)
(9) The alarm signal or 1Hz timing pulse can be output as 16Hz

*Figure 8-9 RTC Block Diagram*

*Page -54-*

(10) 1Hz Clock Output
In particular, this device uses the RP5C15’s alarm feature and clock output as follows.
- Alarm Feature (Alarm Interrupt)
It is used for setting the scheduled timer for turning on the computer's power (Vcc1 ON). When the set date and time match the current date and time, the power to the computer is turned on and the ALARM signal is output, triggering the alarm interrupt. Furthermore, the 1Hz clock output is sent to MFPO/GPIO ● input (used to divide MPFPI). Specifically, the output from ALARM is software selectable and can be executed by capturing the software interrupt signal to divide the MPFP. Also, when setting the alarm timer, the TIMER LED lights up (write “1H” in E8A0**H's D04=1*), additionally, after writing “31H” to the system port EB800DH and enabling WRITE ENABLE, write to SRAM, then turn on the TIMER LED and finally write “0D04=1H” to E8A0**H. Set the system port EB800DH to OFF. Be sure to write SRW=READ ONLY=K, otherwise processing will be needed. (For MPFPK, re-process when Vcc2 is re-inserted).
- 1Hz Clock Output
The 1Hz clock is output from the CLK OUT terminal and connected to the MFPO/GPIO P5 (used to divide the 7-level interrupt input). By doing this, MPFPK division can be performed. This 1Hz signal is also used to turn on the POWER LED and the TIMER LED on the front panel. Normally, the power backup for the RP5C15 internal power is connected to Vcc2, so please make sure the power switch is absolutely OFF when using timing functions.

9. Peripheral
9-1. Disk
The device is equipped with two data-sided FDD (floppy disk drives). This FDD is controlled by FDC and µPD72065 is used. For SCSI interface machines, 80MBHDD is controlled by SCSI controller MB89352. Please refer to figure 9-1.

Table 9-1 Floppy Disk Specifications

| 128, 256, 512, 1,024Bytes/sector | FDCA Input Clock | Formatting Method | 
| 26, 16, 8 Sectors/track           |   2HD(8MHz)      | MFM               | 
| 77Track/side                      |   2DD-2D(4MHz)   | FM                | 
| 154Track/disk                     |                  | Switchable        | 
| (When formatted: 1.28MBytes)      |                  |                   |

<Special Characteristics of FDD>
This machine is equipped with the following unique features.
(1) Auto-eject feature
Automatically ejects media inserted into the specified drive.
(2) Drive activity LED (2-color LED installed)
Automatically lights up the drive activity LED of the designated drive.
Green – Indicates media has been inserted into the specified drive.
Red (lights up when drive select and operation is ON)

CZ-634C-TN CZ-644C-TN

| Front POWER SW | Activity LED | Eject LED |
| --- | --- | --- |
| ON State |  - Green light is on when media is in FDD <br> - Green light blinks when media is not in FDD, and LED blinking feature is ON <br> - Off when media is not in FDD, and LED blinking feature is OFF <br> *Note: When reading/writing to FDD (Drive Select ON, Layer ON), green changes to red | - Off when eject switch masking feature is ON <br> - Green light is on when media is in FDD, and eject switch masking feature is OFF |
| OFF State | - Green light is on when media is in FDD <br> - Off when media is not in FDD | - Green light is on when media is in FDD <br> - Off when media is not in FDD |

3. Eject SW Mask Function
   Eject function masking feature to prevent ejection during access

4. Media Insert/Eject Detection Feature
   Function to constantly monitor insertion and ejection of each drive

5. Media Mis-insertion Detection Feature
   Function to detect mis-insertion of media for each drive

6. Interruption Feature
   Function for interruption during media insertion or ejection

Address Bus
Data Bus
SCSI Controller
Hard Disk Control
Hard Disk Data Bus

HD (Hard Disk)
FD (Floppy Disk)

Address Bus
Data Bus
I/O Controller
FDD Option Control

OPTION SELECT 0~3
EJECT
EJECT MASK
LED BLINK
FDD INT
ERR DISK
DISK IN
TRKO6
WRITE PROTECT
DRIVE SELECT 0~3

FDC (µPD72065)
READY
INDEX
DISK TYPE SELECT
DIRECTION
STEP
WRITE GATE
WRITE DATA
SIDE SELECT

2HD/2DD-2D Switch
Vcc1 Vss 16MHz

VFO Circuit (SED9420AC)
MSN/STD
MOTOR ON
READ DATA

Figure 9-1 FDD/HDD Peripheral Block Diagram

The labels next to specific arrows relate to signals or commands connecting different components in a hard disk and floppy disk drive control system.

Table 9-2 Internal FDD Specifications

| Specification                          | Details                                                                                             |
|----------------------------------------|-----------------------------------------------------------------------------------------------------|
| Memory Capacity (KBytes)               | Unformatted: 1667 <br> Formatted: 1065 <br> Track capacity: 10.42 <br> IBM standard 26 sectors, 256 bytes/density mode |
| Data Transfer Rate (Kbits/sec)         | 500                                                                                                 |
| Access Time (msec)                     | Track Read Time: 3 <br> Seek and Settling Time: 15 <br> Average Access Time: 95 <br> Seek wait time during shifting = Track shift time + Seek and Settling Time <br> Average Access Time = Average Track Shift Time + Seek and Settling Time |
| Media Rotation Speed (rpm)             | 360                                                                                                 |
| Spindle Motor Startup Time (sec)       | 0.5                                                                                                 |
| Maximum Internal Recording Density (BPI)| 9870                                                                                                |
| Number of Tracks                       | TRACK/SIDE: 77 <br> TRACK/DISK: 154                                                                  |
| Track Density (TPI)                    | 96                                                                                                  |
| Number of Heads                        | 2                                                                                                   |
| Encoding Method                        | MFM <br> FM method possible                                                                         |
| External Dimensions (mm)               | 27.0 (H) × 148.0 (W) × 198.0 (D)                                                                     |
| Weight                                 | 900g                                                                                                |
| Others                                 | Auto Clamp Eject Mechanism, Auto Carriage Return Mechanism, VFO (SED9420AC)                          |

Table 9-3 Internal HDD Specifications

Memory Capacity
Formatted: 85,800 (kBytes)
Track Capacity:
  Inner: 20,992 / Outer: 27,648

Data Transfer Speed (Mbits/sec):
  Inner: 10 / Outer: 13

Access Time (msec):
  Average Access Time: 19

Disk Rotation Speed (rpm): 
  2,975 ±1%

Recording Density (BPI): 
  31,500

Number of Tracks:
```
  TRACK/SIDE: 868
  TRACK/DRIVE: 3,472
```

Track Density (TPI): 
  1,300

Number of Heads:

Recording Method:
```
  RLL2-7

Other:
  Built-in Disk Controller
  Interface = SCSI
```

(Page 59)

<CZ-634C-TN
CZ-634C-TN

<FDC Characteristics>
This machine uses the µPD72065 as the FDC to control two FDDs, but it differs from the previously used µPD72065 in the FD controllers utilized in the X1turbo series. Compared to the µPD72065, the points of difference are as follows:

Table 9-4 Comparison of µPD72065 and M88877A

µPD72065                            M88877A
-checks for Read/Write execution result (status)                          -checks for Read/Write execution result (status)
   are performed by polling.                                                               are performed by polling.
-requires I/O ports for driver select, head select                        -requires I/O ports for driver select, head select
  signal output.                                                                                            signal output.
-each drive's current track position is maintained                       -each drive's current track position is maintained
```
   within the FD, making program handling easy.                      in the main RAM, necessitating allocation
                                                                         of track numbers, making program handling
                                                                         slightly more complex.
```

-Formatting is possible simply by giving                                -For formatting, data for one track (6KB~8KB)
```
   a byte of data command to the FDC.                                is needed, making program handling slightly
                                                                           more complex.
```

-Depending on the type of error, command                            -Depending on the type of error, it may not be reset,
```
  may not reset correctly. (e.g. EX) With                             e.g. EX) may not return from hang-up while reading,
  hang-ups in media, the drive may not return                        pulling out the media, etc.
  to normal state if ejected.
```

9-2. Printer
This machine, like the X1&X1turbo series, is equipped with an 8-bit parallel printer I/F according to Centronics standard.

To send a byte of data to the printer from this machine, control signals and BUSY signals use STROBE signals. The BUSY signal is active low, preventing data transmission when the level is "H". That is, it waits until the BUSY signal goes "L" for transmission. Also, the STROBE signal is the output signal to the printer. The printer samples data on the rising edge of this STROBE signal. Therefore, be careful when issuing the STROBE signal as before issuing, it is not possible to guarantee the data will be latched in the ECO011 Data Latch Register.

This machine can accept BUSY signal interrupt requests, allowing software masks. Using this function avoids the need to request BUSY signal checks, knowing printer status through interrupts.

Table 9-5 Printer Register Map

Register Address | D07 | D06 | D05 | D04 | D03 | D02 | D01 | D00 | Remarks
--- | --- | --- | --- | --- | --- | --- | --- | --- | ---
E8C001H | ←-------- Printer Output Data --------→ | Printer Data Register (Write Operation Only)
E8C003H | × | × | × | × | × | × | STRO | Printer Strobe Register (Write Operation Only)
E9C**1H | × | × | × | × | (Write Operation Only)
```
   | | | | | 0 - Printer Busy Interrupt Mask
   | | | | | 1 - Printer Busy Interrupt Mask Disable
   | | | | | 0 - FDD Interrupt Mask
   | | | | | 1 - FDD Interrupt Mask Disable
   | | | | | 0 - FDC Interrupt Mask
   | | | | | 1 - FDC Interrupt Mask Disable
```

E9C**1H | | | | | (Read Operation Only)
```
   | | | | | 0 - Printer Busy Interrupt Mask Enabled
   | | | | | 1 - Printer Busy Interrupt Mask Disabled
   | | | | | 0 - FDD Interrupt Mask Enabled
   | | | | | 1 - FDD Interrupt Mask Disabled
   | | | | | 0 - FDC Interrupt Mask Enabled
   | | | | | 1 - FDC Interrupt Mask Disabled

   | | | | → 0 - Printer Busy Interrupt ON (BUSY=0) - Printer Data Transmission Permitted
   | | | | → 1 - Printer Busy Interrupt OFF (BUSY=1) - Printer Data Transmission Not Permitted
   | | | | → 0 - FDD Interrupt ON
   | | | | → 1 - FDD Interrupt OFF
   | | | | → 0 - FDC Interrupt ON
   | | | | → 1 - FDC Interrupt OFF
```

E9C**3H | Interrupt Vector | → | 1 | 1 | Printer Busy Interrupt Vector

<Printer Access>
(1) Check Printer BUSY signal
```
    • If it is LOW:
        a) To mask printer interrupt before setting, set D00 to "0" at E9C**1H. (Other bits retain the previous state)
        b) Confirm D05 = 0 using E9C**1H.
   • If it is HIGH:
        a) Set the interrupt vector and program to interrupt processing by setting D00 to "1" at E9C**3H with the interrupt vector.
        b) To remove the printer interrupt mask, set D00 to "1" at E9C**1H. (Other bits retain the previous state) If BUSY = 0 (printer is sending data), the interrupt may occur and the channel will be processed.
```
(2) Set the printer output data.
    • Set the printout data from FOX8 at E8C001H.
(3) Send printer data strobe signal (raise the strobe signal)
    • Set D00 to "0" at E8C003H, next set it to "1" and raise the strobe signal.

9-3. Joystick
```
    On X1, X1turbo series, PSG register 14, 15 were used to access two joysticks, but this machine uses the 8255 port and can use two joysticks. Note, if using two joystick inputs, set the upper 4 bits (D04-D07) of E9A005H to "0" as shown below:

              mPD8255
```
Address -------> portA ------------> Joystick No.1
```
                  portB ------------> Joystick No.2
                  portC ------------> Sound Synthesis PCM Control
```

Figure 9-2 Joystick Block Diagram

Register Address  | D7 D6 D5 D4 D3 D2 D1 D0
------------------|------------------------
E9A001H           |  *                     <--- Joystick No.1
                  |
E9A003H           |  *                     <--- Joystick No.2
                  |
E9A005H           | IOC7 IOC6 IOC5 IOC4 Sampling Rate PCM PAN

Table 9-6 Joystick Register Address Map

<Joystick Access>

(1) Set 8255 to mode 92H to specify E9A007H B921.
(2) Set the joystick standard mode A to specify all 0 with E9A005H (Port C) higher 4 bits (D04~D07) as 0.
(3) Read Joystick Input Data No. 1 from E9A001H. Also, if reading Joystick Input Data No. 2, read from E9A003H.

9-4 Expansion I/O Slot

(1) Most of the signals that appear on the expansion I/O slot are signals of the same timing when the MPU operates in 16MHz mode or in 10MHz mode.
```
  - This makes it possible to use peripheral boards for the X68000 even in 16MHz mode.
  - However, depending on the board, subtle timing differences in the hardware and software might cause operational issues, so caution is necessary.
```
(2) If the device on the expansion I/O slot becomes bus master and accesses the system's devices, all signals given by the board to the system must be in the same timing as at the time of 10MHz mode.

Extension I/O Socket Terminal (A)

| Pin No. | Signal Name | I/O | Remarks                            |
|---------|-------------|-----|-----------------------------------|
| 1       | GND         |     | Ground                            |
| 2       | 20M         | Out | 20MHz Clock                      |
| 3       | GND         |     | Ground                            |
| 4       | DB0         | I/O | Data                              |
| 5       | DB1         | "   | "                                 |
| 6       | DB2         | "   | "                                 |
| 7       | DB3         | "   | "                                 |
| 8       | DB4         | "   | "                                 |
| 9       | DB5         | "   | "                                 |
| 10      | DB6         | "   | "                                 |
| 11      | GND         |     | Ground                            |
| 12      | DB7         | I/O | Data                              |
| 13      | DB8         | "   | "                                 |
| 14      | DB9         | "   | "                                 |
| 15      | DB10        | "   | "                                 |
| 16      | DB11        | "   | "                                 |
| 17      | DB12        | "   | "                                 |
| 18      | DB13        | "   | "                                 |
| 19      | DB14        | "   | "                                 |
| 20      | DB15        | "   | "                                 |
| 21      | GND         |     | Ground                            |
| 22      | +12V        |     |                                   |
| 23      | +12V        |     |                                   |
| 24      | FC0         | I/O | Function Code (Indicates the state of MPU execution) |
| 25      | FC1         | "   | "                                 |
| 26      | FC2         | "   | "                                 |
| 27      | AS          | "   | Indicates valid data on address bus |
| 28      | LDS         | "   | Lower data strobe                  |
| 29      | UDS         | "   | Upper data strobe                  |
| 30      | R/W         | "   | Indicates the direction of data transfer based on MPU |
| 31      | -12V        |     |                                   |
| 32      | -12V        |     |                                   |
| 33      | VMA         | I/O | Indicates valid data on address bus |
| 34      | EXVPA       | In  | Indicates address is verified by surrounding 68000 family peripheral devices |
| 35      | DTACK       | I/O | Data transfer acknowledgment complete |
| 36      | EXRESET     | Out | External reset                     |
| 37      | HALT        | I/O | In: MPU halt request, Out: System halt |
| 38      | EXBERR      | I/O | Indicates abnormality on external bus operation |
| 39      | EXPWON     | In  | External bus on                    |
| 40      | GND         |     | Ground                            |
| 41      | Vcc2        | +5V |                                   |
| 42      | Vcc2        | +5V |                                   |
| 43      | Vcc2        | +5V |                                   |
| 44      | SELEN       | Out | Main memory address row/column switch signal |
| 45      | CASRDEN     | Out | Main memory CAS signal (during read) |
| 46      | CASWRL      | Out | Main memory CAS signal (lower data when light) |
| 47      | CASWRU      | Out | Main memory CAS signal (upper data) |
| 48      | INH2        | Out | Main memory refresh cycle          |
| 49      | Vcc1        | +5V |                                   |
| 50      | Vcc1        | +5V |                                   |

(Page - 64 -)

| Terminal No. | Symbol Name | I/O | Remarks                                               |
|--------------|-------------|-----|------------------------------------------------------|
| 1            | GND         |     | Ground                                               |
| 2            | 10M         | Out | 10 MHz clock                                         |
| 3            | 10M         | Out | 10 MHz clock inverted signal                         |
| 4            | E           | Out | Enable (68000 series peripheral control)             |
| 5            | AB1         | I/O | Address                                              |
| 6            | AB2         | "   | "                                                    |
| 7            | AB3         | "   | "                                                    |
| 8            | AB4         | "   | "                                                    |
| 9            | AB5         | "   | "                                                    |
| 10           | AB6         | "   | "                                                    |
| 11           | GND         |     | Ground                                               |
| 12           | AB7         | I/O | Address                                              |
| 13           | AB8         | "   | "                                                    |
| 14           | AB9         | "   | "                                                    |
| 15           | AB10        | "   | "                                                    |
| 16           | AB11        | "   | "                                                    |
| 17           | AB12        | "   | "                                                    |
| 18           | AB13        | "   | "                                                    |
| 19           | AB14        | "   | "                                                    |
| 20           | AB15        | "   | "                                                    |
| 21           | GND         |     | Ground                                               |
| 22           | AB16        | I/O | Address                                              |
| 23           | AB17        | "   | "                                                    |
| 24           | AB18        | "   | "                                                    |
| 25           | AB19        | "   | "                                                    |
| 26           | AB20        | "   | "                                                    |
| 27           | AB21        | "   | "                                                    |
| 28           | AB22        | "   | "                                                    |
| 29           | AB23        | "   | "                                                    |
| 30           | IDDIR       | Out | Data bus transection direction control signal        |
| 31           | -           |     | -                                                    |
| 32           | HSYNC       | Out | Horizontal sync signal                               |
| 33           | VSYNC       | Out | Vertical sync signal                                 |
| 34           | DONE        | I/O | Block data transfer complete (DMA)                   |
| 35           | DTC         | Out | Device data transfer complete (DMA)                  |
| 36           | EXREQ       | In  | External request (DMA)                               |
| 37           | EXACK       | Out | External permission (DMA)                            |
| 38           | EXPCL       | I/O | External peripheral control (DMA)                    |
| 39           | EXOWN       | I/O | External OWN (DMA)                                   |
| 40           | EXNMI       | In  | External NMI                                         |
| 41           | GND         |     | Ground                                               |
| 42           | IRQ2-n      | In  | Interrupt request (n: slot 1 or 2)                   |
| 43           | IRQ4-n      | In  | "                                                    |
| 44           | IACK2-n     | Out | Interrupt acknowledge (n: slot 1 or 2)               |
| 45           | IRCK4-n     | Out | "                                                    |
| 46           | BRn         | Out | Bus request (n: slot 1 or 2)                         |
| 47           | BGn         | Out | Bus grant (n: slot 1 or 2)                           |
| 48           | BGACK       | I/O | Bus grant acknowledge (indicates other devices have bus master) |
| 49           | Vcc1        |     | +5V                                                  |
| 50           | Vcc1        |     | +5V                                                  |

This table appears to reference the pin designations and functions for an expansion I/O slot.

**CZ-634C-TN**
**CZ-644C-TN**

**9-5. Various Connectors (The pin numbers of the connectors represent the view from the part side.)**

◎ Analog RGB Signal Output Connector

| Pin No. | Signal Name  | I/O | Remarks                                 |
|---------|---------------|-----|-----------------------------------------|
| 1       | R OUT         | Out | Analog 0.7Vp-p (75Ω termination)        |
| 2       | GND           | Out | Ground                                  |
| 3       | G OUT         | Out | Analog 0.7Vp-p (75Ω termination)        |
| 4       | GND           | Out | Ground                                  |
| 5       | B OUT         | Out | Analog 0.7Vp-p (75Ω termination)        |
| 6       | GND           | Out | Ground                                  |
| 7       | YS            | Out | Indicates presence of computer data     |
| 8       | GND           | Out | Ground                                  |
| 9       | N.C           | -   | Not connected                           |
| 10      | AUDIO L       | Out | Audio signal left                       |
| 11      | AUDIO R       | Out | Audio signal right                      |
| 12      | GND           | Out | Ground                                  |
| 13      | N.C           | -   | Not connected                           |
| 14      | HSYNC         | Out | Horizontal sync signal TTL level        |
| 15      | VSYNC         | Out | Vertical sync signal TTL level          |

◎ TV Control Connector

| Pin No. | Signal Name    | I/O | Remarks                           |
|---------|----------------|-----|-----------------------------------|
| 1       | EXHSYNC        | In  | External horizontal sync signal TTL level |
| 2       | EXVSYNC        | In  | External vertical sync signal TTL level     |
| 3       | TVPOWERON/OFF  | Out | TV power on/off signal            |
| 4       | TVREMOTE       | Out | TV remote signal                  |
| 5       | Vcc1           | Out | +5V                               |
| 6       | GND            | Out | Ground                            |
| 7       | GND            | Out | Ground                            |
| 8       | N.C            | -   | Not connected                     |

◎ IMAGE IN (Image Input Connector)

| Pin No. | Signal Name | I/O | Remarks                       |
|---------|-------------|-----|-------------------------------|
| 1       | ADD11       | In  | Analog/digital conversion data |
| 2       | ADD10       | In  | "                             |
| 3       | ADD9        | In  | "                             |
| 4       | ADD8        | In  | "                             |
| 5       | ADD7        | In  | "                             |
| 6       | ADD6        | In  | "                             |
| 7       | ADD5        | In  | "                             |
| 8       | ADD4        | In  | "                             |
| 9       | ADD3        | In  | "                             |
| 10      | ADD2        | In  | "                             |
| 11      | ADD1        | In  | "                             |
| 12      | ADD0        | In  | "                             |
| 13      | Q A         | Out | Dot clock                     |
| 14      | Vcc1        | Out | +5V                           |
| 15      | GND         | --  | Ground                        |

(Page - 66)

**Terminal No. | Signal Name | I/O | Remarks | Notes**
```
16 | Vcc3 | Out | +12V
17 | CD4 | Out | Computer control signal
18 | CD3 | Out | Computer control signal
19 | CD2 | Out | Computer control signal
20 | CD1 | Out | Computer control signal
21 | CD1 | Out | Computer control signal
22 | ADD15 | In | Analog/Digital conversion data
23 | ADD14 | In | Analog/Digital conversion data
24 | ADD13 | In | Analog/Digital conversion data
25 | ADD12 | In | Analog/Digital conversion data
```

**Printer Connector**
**(Pins diagram)**

**Terminal No. | Signal Name | I/O | Remarks | Notes**
```
1 | STROBE | Out | Negative polarity print output strobe signal
2 | PA0 | Out | Parallel data bus
3 | PA1 | " | " 
4 | PA2 | " | "
5 | PA3 | " | "
6 | PA4 | " | "
7 | PA5 | " | "
8 | PA6 | " | "
9 | PA7 | " | "
10 | N.C | - | Not connected
11 | BUSY | In | Printer 'LOW' level when ready
12 | N.C | - | Not connected
13 | GND | Out | Ground
14 | GND | Out | Ground
```

**SEE THROUGH COLOR**
**(Pins diagram)**

**Terminal No. | Signal Name | I/O | Remarks | Notes**
```
1 | VHT | Out | Video Half Tone (semi-transparent color)
2 | GND | Out | Ground
```

**LINE IN**
**(Pins diagram)**

**Terminal No. | Signal Name | I/O | Remarks | Notes**
```
1 | GND | Out | Ground
2 | LINEIN | In | Audio synthesis input
3 | N.C | - | Not connected
```

**LINE OUT**
**(Pins diagram)**

**Terminal No. | Signal Name | I/O | Remarks | Notes**
```
1 | GND | Out | Ground
2 | L | Out | Audio (left output)
3 | R | Out | Audio (right output)
```

**Joystick Connector**
**Joystick 1**

| Pin No. | Signal Name | I/O   | Remarks               |
|---------|-------------|-------|-----------------------|
| 1       | IOA0        | In    | 8255 PA0 Pin          |
| 2       | IOA1        | In    | PA1                   |
| 3       | IOA2        | In    | PA2                   |
| 4       | IOA3        | In    | PA3                   |
| 5       | Vcc1        | Out   | +5V                   |
| 6       | IOA5        | I/O   | PA5/PC6               |
| 7       | IOA6        | I/O   | PA6/PC7               |
| 8       | IOC4        | Out   | PC4                   |
| 9       | GND         | Out   | Ground                |

**Joystick 2**

| Pin No. | Signal Name | I/O   | Remarks               |
|---------|-------------|-------|-----------------------|
| 1       | IOB0        | In    | 8255 PB0 Pin          |
| 2       | IOB1        | In    | PB1                   |
| 3       | IOB2        | In    | PB2                   |
| 4       | IOB3        | In    | PB3                   |
| 5       | Vcc1        | Out   | +5V                   |
| 6       | IOB5        | In    | PB5                   |
| 7       | IOB6        | In    | PB6                   |
| 8       | IOC5        | Out   | PC5                   |
| 9       | GND         | Out   | Ground                |

**RS-232C Connector**

| Pin No. | Signal Name | I/O   | Remarks                           | Pin No. | Signal Name | I/O   | Remarks                            |
|---------|-------------|-------|-----------------------------------|---------|-------------|-------|-----------------------------------|
| 1       | FG          | I/O   | Protective Earth                  | 14      | N.C         | -     | Not Connected                     |
| 2       | TXD         | Out   | Transmit Data                     | 15      | ST2         | In    | Transmit Signal Element Timing    |
| 3       | RXD         | In    | Receive Data                      | 16      | N.C         | -     | Not Connected                     |
| 4       | RTS         | Out   | Request to Send                   | 17      | RT          | In    | Receive Signal Element Timing     |
| 5       | CTS         | In    | Clear to Send                     | 18      | N.C         | -     | Not Connected                     |
| 6       | DSR         | In    | Data Set Ready                    | 19      | N.C         | -     | Not Connected                     |
| 7       | SG          | I/O   | Signal Ground                     | 20      | DTR         | Out   | Data Terminal Ready               |
| 8       | CD          | In    | Carrier Detect                    | 21      | N.C         | -     | Not Connected                     |
| 9       | N.C         | -     | Not Connected                     | 22      | CI          | In    | Ring Indicator                    |
| 10      | N.C         | -     | Not Connected                     | 23      | N.C         | -     | Not Connected                     |
| 11      | N.C         | -     | Not Connected                     | 24      | ST1         | Out   | Transmit Signal Element Timing    |
| 12      | N.C         | -     | Not Connected                     | 25      | N.C         | -     | Not Connected                     |
| 13      | N.C         | -     | Not Connected                     |

(Note: "-" denotes that the pin is not used or not connected.)

**Key Jack**

| Pin No. | Signal Name | I/O | Remarks          |
|---------|-------------|-----|------------------|
| 1       | Vcc2        | Out | +5V              |
| 2       | MOUSE DATA  | In  | Mouse Data       |
| 3       | KEYT × D    | In  | Key Receive Data |
| 4       | KEYR × D    | Out | Key Send Data    |
| 5       | READY       | Out | Key Send Permission/Rejection |
| 6       | REMOTE      | In  | Remote Signal    |
| 7       | GND         | Out | Ground           |

**Headphone**

| Pin No. | Signal Name | I/O | Remarks            |
|---------|-------------|-----|--------------------|
| 1       | GND         | Out | Ground             |
| 2       | L           | Out | Audio Signal (Left)|
| 3       | R           | Out | Audio Signal (Right)|

**Mouse Port**

| Pin No. | Signal Name | I/O | Remarks              |
|---------|-------------|-----|----------------------|
| 1       | Vcc1        | Out | Ground               |
| 2       | MS CTRL     | Out | Control Signal       |
| 3       | MS DATA IN  | In  | Mouse Data          |
| 4       | GND         | Out | Ground              |
| 5       | GND         | Out | Ground              |

**3D Terminal**
**External Floppy Disk Connection Connector**

| Pin No. | Signal Name          | I/O | Remarks                |
|---------|----------------------|-----|------------------------|
| 1       | DISK TYPE SELECT     | Out | Disk Type Selection Signal |
| 2       | N.C                  | -   | Not Connected          |
| 3       | DRIVE SELECT 3       | Out | Drive Select Signal 3  |
| 4       | INDEX                | In  | Disk Index Signal      |
| 5       | DRIVE SELECT 0       | Out | Drive Select Signal 0  |
| 6       | DRIVE SELECT 1       | Out | Drive Select Signal 1  |
| 7       | DRIVE SELECT 2       | Out | Drive Select Signal 2  |
| 8       | MOTOR ON             | Out | Motor On Signal        |
| 9       | DIRECTION            | Out | Head Move Direction Signal  |
| 10      | STEP                 | Out | Head Move Signal       |
| 11      | WRITE DATA           | Out | Write Data Signal      |

**(CZ-634C-TN / CZ-644C-TN)**

| Pin No. | Signal Name      | I/O | Notes                                     |
|---------|------------------|-----|-------------------------------------------|
| 12      | WRITE GATE       | Out | Write Gate Signal                         |
| 13      | TRACK 00         | In  | Track 0                                   |
| 14      | WRITE PROTECT    | In  | Write Protect Signal                      |
| 15      | READ DATA        | In  | Read Data Signal                          |
| 16      | SIDE SELECT      | Out | Head Select Signal                        |
| 17      | READY            | In  | Drive Ready Signal                        |
| 18      | N.C              | -   | Not Connected                             |
| 19      | N.C              | -   | Not Connected                             |
| 20      | OPTION SELECT 0  | Out | Option Select 0                           |
| 21      | OPTION SELECT 1  | Out | Option Select 1                           |
| 22      | OPTION SELECT 2  | Out | Option Select 2   CZ-600C dedicated signal|
| 23      | OPTION SELECT 3  | Out | Option Select 3                           |
| 24      | EJECT            | Out | Eject Signal                              |
| 25      | EJECT MASK       | Out | Eject Mask Signal                         |
| 26      | LED BLINK        | Out | LED Blink Signal                          |
| 27      | DISK IN          | In  | Disk Insert Signal                        |
| 28      | ERR DISK         | In  | Disk Insert Error Signal                  |
| 29      | FDD INT          | In  | Disk Interrupt Signal                     |
| 30      | GND              | Out | Ground                                    |
| 31      | GND              | Out | Ground                                    |
| 32      | GND              | Out | Ground                                    |
| 33      | GND              | Out | Ground                                    |
| 34      | GND              | Out | Ground                                    |
| 35      | GND              | Out | Ground                                    |
| 36      | GND              | Out | Ground                                    |
| 37      | N.C              | -   | Not Connected                             |

◎ SCSI Device Connection Connector

| Pin No. | Signal Name | Pin No. | Signal Name | I/O | Notes                  |
|---------|-------------|---------|-------------|-----|------------------------|
| 1       | GND         | 26      | D0          | I/O | Data Signal            |
| 2       | GND         | 27      | D1          | "   | "                      |
| 3       | GND         | 28      | D2          | "   | "                      |
| 4       | GND         | 29      | D3          | "   | "                      |
| 5       | GND         | 30      | D4          | "   | "                      |
| 6       | GND         | 31      | D5          | "   | "                      |
| 7       | GND         | 32      | D6          | "   | "                      |
| 8       | GND         | 33      | D7          | "   | "                      |
| 9       | GND         | 34      | DBP         | -   | "  Data Bus Parity Bit |
| 10      | GND         | 35      | N.C         | -   | Ground                 |
| 11      | GND         | 36      | N.C         | -   | -                      |
| 12      | GND         | 37      | N.C         | -   | -                      |

| Pin | Signal | Pin | Signal |     |      |
|-----|--------|-----|--------|-----|------|
| 13  | NC     | 38  | TMPWR  | Out | Termination circuit use power |
| 14  | GND    | 39  | N.C    | -   | Ground |
| 15  | GND    | 40  | N.C    | -   | Ground |
| 16  | GND    | 41  | ATN    | -   | Attention signal |
| 17  | GND    | 42  | N.C    | -   | Ground |
| 18  | GND    | 43  | BUSY   | In  | Controller active signal |
| 19  | GND    | 44  | ACK    | Out | Data transfer acknowledgment signal |
| 20  | GND    | 45  | RESET  | Out | Reset signal |
| 21  | GND    | 46  | MSG    | In  | Command completion response signal |
| 22  | GND    | 47  | SEL    | Out | Select signal |
| 23  | GND    | 48  | C/D    | In  | Command/data switching signal |
| 24  | GND    | 49  | REQ    | In  | Data transfer request signal |
| 25  | GND    | 50  | I/O    | In  | Input/output switching signal |

CZ-634C-TN
CZ-644C-TN
CZ-644C-TN

10. Main Board

[Main board component-layout diagram]

"11. Main Circuit Diagram (1)"

On the bottom left corner, it says:

"- 75 -"

On the bottom right corner, it says:

"- 78 -"

"12. Main basic wiring diagram (2)"

The numbers at the bottom of the page, "- 77 -" and "- 78 -", probably indicate the page numbers in the document.

"13. Main Basic Circuit Diagram (3)"

"14. Main basic wiring diagram (4)"

"— 81 —" 

"— 82 —"

CZ-634C-TN
CZ-644C-TN
CZ-644C-TN

15. Main Basic Wiring Diagram (5)

[Main board schematic diagram]

16. Control Basic Wiring Diagram

(Schematic diagram — all labels are signal names, component designators, and part numbers in English/alphanumeric.)

"17. Control Board"

18. I/O, FD Connector, SCSI Connector, LED Basic Wiring Diagram

Top right header boxes:
CZ-634C-TN
CZ-644C-TN

(Schematic diagram — all labels are connector pin names, signal names, component designators, and part numbers in English/alphanumeric.)

19. FD, I/O, SCSI Connector, Power LED, Eject, FD-LED Baseboard

[Image 1]

●FD Connector Baseboard

[Image 2]

●I/O Connector Baseboard

[Image 3]

●SCSI Connector Baseboard

(Note: The "FD" in the text likely stands for "Floppy Disk")

CZ-634C-TN
CZ-644C-TN

● Power LED Board

● Eject Board          ● FD-LED Board

(PCB component-layout diagrams — all remaining labels are component designators and part values in English/alphanumeric.)

CZ-634C-TN
CZ-644C-TN

20. Analog Basic Wiring Diagram

(Schematic diagram labeled "ANALOG" — all remaining labels are signal names, pin names, component designators, transistor/IC part numbers, and component values in English/alphanumeric.)

— 93 —    — 94 —

CZ-634C-TN
CZ-644C-TN

21. Analog board

[PCB component layout diagram — Analog board. Component reference designators as silkscreened:]

X7245CE

Capacitors: C401–C418
Resistors: R401–R430
Transistors: Q401–Q409
Diodes: D401–D484
Ferrite beads / fuses: FB400–FB487
Variable resistors: VR401, VR402, VR403
ICs: IC401, IC482
PTC, CE, RM401

Top-left corner:
"22. Power Supply Unit Basic Circuit Diagram"

Below the title:
"The parts marked (triangle mark, square mark) are safety critical parts.
When replacing, please use the specified parts at the specified locations to ensure safety and performance."

(Note: The symbols, "triangle mark, square mark" are substituted for visual symbols in the actual text.)

"23. Circuit Board"

"KYOSAN"

"AQ1716PA011D"

CZ-634C-TN
CZ-644C-TN

24. Keyboard basic wiring diagram

[Keyboard schematic diagram.]

IC1 (microcontroller)
```
  XTAL1, XTAL2
  RESET
  P10–P17, P20–P27, P30–P37 (port lines)
  TXD REMOTE, RXD, STBY, RDY
```

IC2 (LS374)

Key matrix: row/column scan lines to key switches.

LED indicators: RED, RED, RED, RED, RED, GREEN, GREEN

Connector: keyboard cable / mouse connector

-101-          -102-

"25. Keyboard Component Board"

The numbers at the bottom indicate page numbers.

The text located in the upper center of the image reads:

"CZ-634C-TN
CZ-644C-TN
CZ-634C-TN
CZ-644C-TN"

"26. IC Pin Signal (1)

RH-IX0906CEZZ
G/ARRAY
(CYNTHIA)

Legend:
- (dashed line) VDD (+5V)
- (solid circle) VSS (GND)

RH-IX1095CEZZ
G/ARRAY
(VIPS)

Legend:
- (dashed line) VDD (+5V)
- (solid circle) VSS (GND)

- 105 -"

Top left diagram:
CZ-634C-TN
CZ-644C-TN

RH-IX1604CEZZ
G/ARRAY (PEDE/C)

Top pin labels (from left to right):
70, 69, 68, 67, 66, 65, 64, 63, 62, 61, 60, 59, 58, 57, 56, 55, 54, 53, 52, 51

Right pin labels (from top to bottom):
50, 49, 48, 47, 46, 45, 44, 43, 42, 41, 40, 39, 38, 37, 36, 35, 34, 33, 32, 31

Bottom pin labels (from left to right):
1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20

Left pin labels (from top to bottom):
30, 29, 28, 27, 26, 25, 24, 23, 22, 21

Pin functions (clockwise from top left, starting at pin 30):
DQ0, A1, A2, A3, A4, A5, A6, A7, A8, AG, AD, RDQ, OE2, DQ3, DCLK, VO, VP, DO, DE, DF, LVC2, NC, TV

Top right diagram:
RH-IX1603CEZZ
MB89352

Pin functions (clockwise from top left, starting at pin ATN):
ATN, ACK, REQ, MSG, DBC, SE, IO, CD, RD, SD7, SD6, SD5, SD4, SD3, SD2, SD1, SD0, SOF, A7, A6, A5, A4, A3, A2, A1, A0, GND, VCC, RST, WR, RD, INO, OE2, DQ, DRQC, DACK, REG, ADR, FC, CF, ST, RE, ATR2

Middle right diagram:
RH-IXI81CEZZ
MN4464S

Pin top (from left to right):
VCC, CE2, A8, A9, A10, A11, A12, A3, A4, A2, A3, A4, A5, A6, A7, MD9, MD7, MD4, MD2, MD0, IO0/ID0, IO1/ID1

Bottom right diagram:
RH-IX091CEZZ
(74ALS244)

Pin functions (clockwise from left top, starting at VCC):
VCC, CE2, A8, AO, A1, A2, A3, A4, A5, A6, A7, GND, OE1, IO8, IO7, IO6, IO5, IO4, IO3, IO2, IO0, IO1

Bottom middle diagram:
NJM2073D-1
(NJM2073 Dual Power Amplifier)
```
Function:
   1 SS
   2 EO
   3 P1
   4 VS1
   5 SG
   6 OUT2
   7 VCC
   8 SG
   9 OUT1
   10 AB
```

CZ-634C-TN
CZ-644C-TN

IC Terminal Signals (2)

[IC pin assignment diagrams.]

RH-IX1102CEZZ
MSM6258VGS-K

RH-IX1108CEZZ
(SN74LS486N)

RH-IX1146CEZZ
(SN74ALS05)

RH-IX1096CEZZ
G/ARRAY10SC(AN)

RH-IX1094CEZZ
G/ARRAY
(CATHY)

CZ-634C-TN
CZ-644C-TN

RH-IX1093CEZZ
G/ARRAY
(V/CON)

CZ-634C-TN
CZ-644C-TN

27. Set packaging method

[Exploded packaging diagram with item callouts:]

RGB cable
TV control cable
Protective cover
Keyboard
Mouse
I/O board extraction tool
Cushioning material

[Box (upper right):]
System disk
Dictionary disk
Word processor
SX-WINDOW A
SX-WINDOW B

[Box (lower left):]
Function label
Key top label
Poly bag
Instruction manual
Service shop guide
OS manual
Basic manual
Utility manual
SX-WINDOW manual

Poly bag

Warranty certificate
X68000 Exe card
Packing case
NO. label

28. Procedure for Disassembling the Circuit Board

Please remove the screws and connectors marked with circles in the order of the numbers.

CZ-634C-TN
CZ-644C-TN

1. Top case screws
2. Floppy Disk Drive fixing screws
3. Power cable for Floppy Disk Drive
4. Floppy Disk Drive data cable
5. Power Supply Unit fixing screws
6. Power Supply Unit
7. Fan fixing screws
8. CD-ROM Drive fixing screws
9. CD-ROM Drive
10. CD-ROM Drive data cable
11. CD-ROM Drive chassis screws
12. CD-ROM Drive chassis

The document seems to be a disassembly diagram for a computer, specifically for models CZ-634C-TN and CZ-644C-TN.
