# Sharp Hard Disk Unit IT-X640 / IT-X680 — User's Manual

*English translation from the Japanese original*

SHARP X68000 supported
HARD DISK UNIT
IT-X640/IT-X680

User's Manual
itec
i-tec Co., Ltd.

**HARD DISK UNIT**
40MB/80MB Hard Disk

IT-X640/IT-X680

**User's Manual**

1. It is prohibited to reproduce any part or all of this document without permission.
2. The contents of this document may be changed without notice.
3. We have taken great care to ensure the accuracy of the contents of this document; however, if you notice any errors or omissions, please contact the store where you purchased the product or our customer support.
4. We do not assume responsibility for any consequential impact resulting from the use of this product, so please acknowledge this in advance.

**Introduction**

Thank you very much for purchasing the I-Tech hard disk unit TX series.

This product is an external hard disk unit (40MB, 80MB) compatible with the Sharp Corporation PC-X68000 series personal computers.

Handling the hard disk unit TX series requires careful attention, and there are certain things that must be done. Please read this manual thoroughly and use this product effectively. Before using the TX series, please acquire sufficient knowledge of the OS.

This manual does not explain the usage of application programs related to the TX series. Please refer to their respective manuals for the application programs.

**Product Contents**

| No | Item Name                |
|----|--------------------------|
| 1  | Hard Disk Unit           |
| 2  | Connection Cable         |
| 3  | User Manual              |
| 4  | Warranty Card            |
| 5  | User Registration Card   |

* Note: The external terminator (terminator resistor) is sold separately.

*(Blank page in the original.)*

**Table of Contents**

Chapter 1: Features and Precautions
1. ITX Series Features ........................................................... 1
2. Precautions for Use ........................................................... 3

Chapter 2: Names and Roles of Each Part ...................................... 5

Chapter 3: Connecting to the Computer ......................................... 7
- Configuration Diagram of Hard Disk for X68000 ............................. 7
- Relationship between ID Number and Device Number of Hard Disk for X68000... 7

Chapter 4: Formatting .............................................................. 9
1. Human68K Ver 2.0 .......................................................... 9
2. OS-9/X68000 .......................................................... 18
```
   (1) Procedures for Initializing Hard Disk with Device Number “0” .......... 18
   (2) Procedures for Initializing Hard Disk with Device Numbers “1” to “3” ... 23
```
3. MSX2 HD Interface ......................................................... 25

Chapter 5: Troubleshooting ....................................................... 27
1. When ITX Series Does Not Operate Even When Phone Is On .............. 27
2. When Power Supply Is Provided to ITX Series but It Does Not Operate ... 27

Chapter 6: Basic Specifications of ITX Series ................................... 29

Chapter 7: Maintenance Guide ...................................................... 31

Appendix: OS-9/X68000 Supplemental User Manual

*(Blank page in the original.)*

**Chapter 1 Characteristics and Precautions**

**1. Characteristics of the ITX Series**

1. Human68k Ver 2.0 or higher:
   - You can use the IT-X640 and IT-X680 by installing them additionally.
2. It can be used with OS-9.
3. From one to eight units, the ID number can be easily set with the switch.
4. It can also be connected to internal hard disk types.
5. There are two new designs in black and gray.
6. IT-X640 can be used with the MSX2 HD Interface connection.

**Notes:**

- External terminator (termination resistor) is sold separately.
- Human68k (Ver2.0 or higher) only supports up to 40MB on a single drive. With the IT-X680, it is fixed to a 40MB setting.
- IT-X403 can be used as a single unit.

**Remarks:**

- IT-X403 has a built-in terminator, so an external terminator is not required.

**◆ Hard Disk Configuration Diagram for X68000 ◆**

X68000
│
├── IT-X680
│   │
│   ├── HDD
│   └── Additional HDD
│
├── IT-X640
│   │
│   ├── HDD
│   └── Additional HDD
│
└── HDD
    └── Additional HDD

In the X68000 series, it is possible to connect up to 16 hard disks. (Using Human68k Ver. 2.0)

By changing the ID numbers of the master to 0-7, you can connect up to 8 hard disks, and further increase the number by adding one slave (additional hard disk) to each master.

IT-X640 is dedicated for master use only. IT-X680 (40MB x 2 units) will use 1 unit as master and 2nd unit as slave.

In X68000, when formatting a hard disk, you specify the disk by device number, so below, the relationship between ID number and device number is documented.

Relation between ID number and Device number of hard disks for X68000
X68000

Master Side:
ID Number = 0
Device Number = 0

ID Number = 1
Device Number = 2

ID Number = 2
Device Number = 4

ID Number = 3
Device Number = 6

ID Number = 4
Device Number = 8

ID Number = 5
Device Number = 10

ID Number = 6
Device Number = 12

ID Number = 7
Device Number = 14

Slave Side:
Additional HDD
Device Number = 1

Additional HDD
Device Number = 3

Additional HDD
Device Number = 5

Additional HDD
Device Number = 7

Additional HDD
Device Number = 9

Additional HDD
Device Number = 11

Additional HDD
Device Number = 13

Additional HDD
Device Number = 15

2. Precautions for Use

1. When taking the box out of storage, please confirm immediately that there are no missing items against the accessory list. Delays in checking may cause issues later. If you discover any missing items upon confirmation, please contact the store where you purchased the product without delay.

2. Do not dispose of the packaging material. It will be necessary for repairs or shipping. Hard disks are extremely vulnerable to vibration and shock. So please store the packaging material safely as shock can cause faults.

3. Before connecting the ITX series to a computer, confirm that all equipment is in an off state.

4. Please strictly avoid placing it in the following environments:
```
   ★ Places exposed to direct sunlight 
   ★ Hot and humid places
   ★ Places with extreme temperature changes
   ★ Places with poor ventilation 
   ★ Places with a lot of movement 
   ★ Places with a lot of dust 
   ★ Near heating appliances 
   ★ Near equipment that generates strong magnetic fields
   ★ Installations on tilted surfaces 
```

5. The ITX series contains precision electronic parts, so do not allow it to be subjected to vibration or shock.

6. Do not block the fan and ventilation holes on the back. This will trap heat and can cause trouble due to overheating.

7. Do not use the product in areas where pharmaceuticals emit steam or chemicals are in the air.

8. Never remove the ITX series cover or front panel while the power is on. Doing so can void the warranty.

9. Do not place it near radios or televisions as it can cause noise. Likewise, placing it near equipment that generates strong magnetic fields can damage the ITX series through interference.

10. For storage of the ITX series, observe the same precautions as for use.

※ To clean the ITX series, use a soft cloth with neutral detergent and wipe gently. Do not use benzene or thinner as it may cause discoloration or deformation.

"MEMO"

Chapter 2     Names and Functions of Each Part

Names and Functions of Each Part of the ITX Series

Front and Rear of the ITX Series

1 Power Lamp (Green)
    Lights up when the power (electricity) switch is turned on.
2 Access Lamp (Red)
    Blinks when accessing the ITX series.
3 Ventilation Hole
    Air intake/exhaust to prevent temperature rise.
4 Connection Connector
    Connects to the X68000 main unit's hard disk connector.
5 Expansion Connector
    Connect cables when installing on another unit.
6 Changeover Switch
    Switches the setup from Unit 1 to Unit 8.
7 Power Cable
    Supplies power to the ITX series.
8 Cooling Fan
    Fan for cooling the drive and power supply.

It says: 

"M E M O"

and at the bottom:

"- 6 -"

Chapter 3: Connecting to a Computer

This section explains important points necessary to connect the ITX series to a computer. If the connection is made incorrectly, it could cause trouble, so please be careful.

Connecting to a Computer

1. Turn off the power to all devices (including the computer).
2. Connect the hard disk drive connector on the main computer unit to the ITX series connector using the connection cable.
3. Plug the power cable into an outlet.
4. Set the switch. Refer to the diagram below and set the ID number.

* Connection Diagram

● When connecting a single unit
```
  X68000
      |
      |———— IT-X640 OR IT-X680 (ID Number = 0)
      |
```
External Terminator 

● When connecting additional units
```
  X68000
      |
      |———— IT-X640 OR IT-X680 (ID Number = 0)
      |
      |———— IT-X640 OR IT-X680 (ID Number = 1)
      |
      |———— IT-X640 OR IT-X680 (ID Number = 2-7)
      |
```
External Terminator 

● When connecting with IT-X403 mixed in

```
                                    IT-X640       ID number = 1
                                    OR
```
X68000                      IT-X680

```
                                    IT-X640       ID number = 2
                                     OR
                                    IT-X680
```

```
                                    IT-X640        ID number = 3~7
                                     OR
                                   IT-X680

                                   IT-X403     ID number = 0
                         (built-in terminator)
```

※ Notes

• In the case of a built-in hard disk type of the X68000, the ID number of the built-in hard disk is fixed at "0", so if you add IT-X640 or IT-X680, please set the ID number to "1".

• The IT-X403 has its ID number fixed at "0", so if you add IT-X640 or IT-X680 as described above, please set the ID number to "1".

• Be careful not to set the same ID number.

• The external terminator (sold separately for 4,000 yen) is attached to the last connected device. However, the IT-X403 has a built-in terminator.

• Human68K Ver 2.0 only supports up to 40MB per drive, so the IT-X680 is fixed to a setting of 2 x 40MB drives.

* If 80MB will be supported in the future, the setting will be changed to 80MB if the short jumper plug for Drive JP1 is removed. 

Chapter 4  Format

The ITX series cannot be used without performing a process called formatting. Here, we will explain the basics for using Human 68K Ver 2.0 on OS-9.

1. Human 68K Ver 2.0

◎Procedure
```
1 Turn on the power to the peripheral devices, then turn on the power to the computer itself.
2 Start Human 68K Ver 2.0.
3 When the window is displayed, match the mouse cursor to "COMMAND. X" and click (press) the left button twice.
4 When prompted, enter "SWITCH" and press the key.
```

A> SWITCH

When a hard disk is connected to the X68000, set the number of connected hard disks with this "SWITCH" command.

※ One important thing to note here is that the number of hard disks connected with the SWITCH command refers to the maximum device number + 1.

◆How to obtain device numbers

* For the main machine

Device number = ID number x 2

* For sub-machines

Device number = main machine's ID number x 2 + 1

**SWITCH for X68000 Version 2.01 Copyright 1989 SHARP / Hudson**

| Keyword   | Current Value                        | Setting Range                                  |
|-----------|--------------------------------------|------------------------------------------------|
| RS232C    | [AUX] 9600 baud 8-bit parity none    | [AUXn] 9600 baud 8-bit parity none             |
|           | Stop 1 Xon                           | Stop 1 Xon [AUXn] = (1,2,3,4,5)                |
| MEMORY    | 1024 KB                              | 1024 KB (1024KB~12288KB)                       |
| BOOT      | STD                                  | STD (STD/HD?/2HD?/ROM?$ /RAM?$)               |
| EJECT     | Off                                  | Off (Off/On)                                   |
| OPT2KEY   | Tvctrl                               | Tvctrl (TvCTRL/Normal)                         |
| CONTRAST  | 14                                   | 14 (5~15)                                      |
| KANA      | Jis                                  | Jis (Jis/Aiu)                                  |
| TV.CTRL   | Off                                  | Off (Tv/Off/1~$3F)                             |
| LCD.MODE  | Lcd                                  | Lcd (Lcd/Normal)                               |
| SRAM      | No.use                               | No.use (No.use/Ramdisk/Program)                |
| P0        | $0       G-$0  R-$0  B-$0            | $0         G-$0  R-$0  B-$0                   |
| P1        | $F38E  G-$1F  R-$0  B-$1F             | $F38E  G-$1F  R-$0  B-$1F                      |
| P2        | $FFC0  G-$1F  R-$1F  B-$0             | $FFC0  G-$1F  R-$1F  B-$0                      |
| P3        | $FFFE  G-$1F  R-$1F  B-$1F            | $FFFE  G-$1F  R-$1F  B-$1F                     |
| P4        | $DF30  G-$1B  R-$1C  B-$18            | $DF30  G-$1B  R-$19  B-$16                     |
| P8        | $806    G-$1  R-$0  B-$3              | $806       G-$8  R-$0  B-$11                   |
| XCHG      | 0                                    | 0 (0~7)                                        |
| HD.MAX    | 1                                    | 1 (0~16)                                       |
| WAIT.PRN  | 5 sec                                | 5 sec  5 sec~$80000                            |
| FIRST.KY  | 3 500ms                              | 3 (0~15) ms=200ms+100×n                        |
| NEXT.KEY  | 2 50ms                               | 2 (0~15) ms=30ms+5×n 2                         |
| END       |                                      |                                                |

You can set the number of connected hard disks.

(Select) (Confirm) ESC (Exit without registration)

Since it is displayed as above, move the cursor to HD.MAX with the cursor keys and press the return key.

HD.MAX:

Please specify the number of connected hard disks (maximum device number + 1).

(Select) (Confirm) ESC (Go back)

The cursor will move as above, so use the cursor keys (↑↓) to set the value to the connected hard disk's maximum device number + 1.

Press the Return key, then move the cursor to the next point and press the Return key.

Do you want to save the changes to the memory switch? Is this okay?
`Y`: (Save and Exit) `N`: (Exit without Saving) `ESC`: (Go back)

If you press `Y`, the content of the memory switch will be changed and saved, and a prompt will be displayed.

5. Since we will initialize the hard disk, please enter "FORMAT".

A>FORMAT

● Hard Disk Format

FORMAT for X68000 Version 2.01 Copyright 1989 SHARP/Hudson

Floppy Disk
*Floppy Disk*
End

Please specify the item
* (Select) ●(Confirm) ESC (End)

Use the cursor key to move the cursor to "Hard Disk" and press the Return key.

* In the case of device number 0, the first device (ID number = 0) is IT-X640, and the second device (ID number = 1) is IT-X640. If the device number 1 is not connected here, it will be an error if selected for initialization.

6Select "Device Initialization"

FORMAT for X68000  Version 2.01 Copyright 1989 SHARP/Hudson

Device Name: Hard Disk
Device Number: 0

Confirm Area
Release Area
Select Area
*Initialize Device
Change Device
End

Management information is corrupted.
Please initialize the device.

Please specify an item.

(Select) (OK) ESC (Return)

Use the cursor key to align the cursor to "Initialize Device" and press the return key.

10M
20M
40M

Use the cursor key to align the cursor to "40M" and press the return key.

Initialize the entire device. Is this okay?
(Execute) (N: Return) ESC (Return)

Press "Y" here to start initialization. To cancel, press the "ESC" key. You will return to the previous screen.

FORMAT for X68000 Version 2.01 Copyright 1989 SHARP/Hudson

Device Name: Hard Disk
Device Number: 0

[Box]
Area Confirmation
Area Release
Area Selection
Device Initialization
Device Change
End

Total Capacity of Device: 40 MB
Maximum Capacity Ensured: 40 MB
Free Capacity: 40 MB

0 10 20 30 40 50 60 70 80 90 100 %

40 MB Initializing...

A horizontal graph will be displayed, and a message will appear during initialization. Initialization ends when it reaches 100%.

7. Select Area Confirmation.

FORMAT for X68000 Version 2.01 Copyright 1989 SHARP/Hudson

Device Name: Hard Disk
Device Number: 0

[Box]
Area Confirmation
Area Release
Area Selection
Device Initialization
Device Change
End

Total Capacity of Device: 40 MB
Maximum Capacity Ensured: 40 MB
Free Capacity: 40 MB

Specify Item
(Select) (Confirm) (ESC: Go Back)

Move the cursor with the cursor key and press the return key to select "Domain Secure".

● Specify the Capacity

Capacity                             Overall Device Capacity              40MB 
Volume Name                  Maximum Secured Capacity       40MB
System Transfer              Available Capacity                            40MB
Execute
End

Move the cursor with the cursor key and press the return key to select "Capacity".

Specify the capacity to secure.

ESC: (Return to previous)

If you want to secure the entire hard disk capacity as a domain, enter "40" and press the return key. If you want to partition the domain, enter the capacity to partition.

● Specify the Volume Name

Capacity                             Overall Device Capacity              40MB 
Volume Name                  Maximum Secured Capacity       40MB
System Transfer              Available Capacity                            40MB
Execute
End

Move the cursor with the cursor key and press the return key to select "Volume Name". If the volume name is not required, select "System Transfer".

Specify the volume name.

ESC: (Return to previous)

Enter the volume name and press the return key.

● Specifying System Transfer

Capacity            Total Capacity of Device             40 MB
Volume Name         Maximum Capacity Available           40 MB
:: System Transfer  Available Capacity                   40 MB
Execute
Finish

Use the cursor key to select "System Transfer" and press the return key.

                Don't

If you are transferring the Human68K system, place the cursor on "Do". If you are not transferring the system, place the cursor on "Don't" and press the return key.

● Execution

Capacity            Total Capacity of Device             40 MB
Volume Name         Maximum Capacity Available           40 MB
System Transfer     Available Capacity                   40 MB
Execute
Finish

Use the cursor key to select "Execute" and press the return key.

Are you sure you want to secure the area? Is that okay?
:: Execute: (Y) ESC: (Go back)
Confirmation message will appear. Press the "Y" key. 

**FORMAT for X68000 Version 2.01 Copyright 1989 SHARP/Hudson**

Device Name: Hard Disk
Device Number: 0

Capacity: 40
Volume Name:  
System Transfer: Yes
Execute
End

Total Device Capacity: 40 MB
Maximum Usable Capacity: 40 MB
Free Capacity: 40 MB

0 10 20 30 40 50 60 70 80 90 100 %

[Area confirmation in progress...]

A message will be displayed with a horizontal bar graph during area confirmation. It will be completed if it reaches 100%.

**FORMAT for X68000 Version 2.01 Copyright 1989 SHARP/Hudson**

Device Name: Hard Disk
Device Number: 0

Capacity: 40
Volume Name:
System Transfer: Yes
Execute
End

Total Device Capacity: 40 MB
(1) Autostart: Human68K 40 MB
Maximum Usable Capacity: 0 MB
Free Capacity: 0 MB

Please specify an item
↑↓(Select) ¥(Confirm) ESC(Return to previous)

As mentioned above, "(1) Auto-boot: Human68K" will be ensured. 

Select 9 Finish.

[Box Content]
FORMAT for X68000 Version 2.01 Copyright 1989 SHARP/Hudson

Floppy Disk
Hard Disk
* [Blank]

Please specify an item
(Select) *: (Confirm) ESC: (Exit)

Use the cursor key to align the cursor with "Finish" and press the return key.

Using the hard disk requires a reboot. Do you want to reset?
Y: (Execute) N: (Go Back) ESC: (Go Back)

You cannot use the hard disk immediately after formatting it. When the above message is displayed, press the 'Y' key.

* After booting with the system disk again, copy the system to the hard disk, and from the next time, you can boot "Human68K" from the hard disk.

Note:
If you want to change the boot device number, change the BOOT in the SWITCH command.

Page 17

2. OS-9/X68000

Notes:
The hard disk supported by OS-9/X68000 is up to device numbers 0 to 3.
If it is a built-in type hard disk, it will be as follows:

Device number 0  ····· Built-in hard disk
Device number 1  ····· Cannot be used
Device number 2  ····· External hard disk (ID number=1)
Device number 3  ····· External expansion hard disk

(1) Procedure for initializing hard disk of device number “0”
1. Turn on the power of peripheral devices and then turn on the power of the computer itself.
2. Start OS-9/X68000.
3. When “Your name?:” is displayed, press the return key. The prompt “$” will be displayed as shown below.

■shell            win0
Japanese front processor A S K 6 8 K for X68000 version 1.10
Copyright 1987,88 SHARP Corp. / ACCESS CO., LTD. 

$

4. Initialize the hard disk of device number “0”. Please input and enter “init-hd-40m” as shown below.

■shell            win0
Japanese front processor A S K 6 8 K for X68000 version 1.10
Copyright 1987,88 SHARP Corp. / ACCESS CO., LTD.

$ init-hd-40m

**If not yet initialized**

**shell      win0**

Japanese Front Processor ASK68K for X68000 version 1.10  
Copyright 1987,88 SHARP Corp. / ACCESS CO., LTD.

$ init-hd-40m
tmode nopause -w=1
chd CMDS./BOOTOBJS
load -d rrhbd0.40m
hpu \/win0

Partition data is not initialized.  
Do you want to initialize?  Y  
Enter the IPL file name.  :

★★★  System area management information is as follows ★★★  
Total installation capacity: 40 MB  
Free space: 39 MB  

1: Secure area  2: Release area  3: Create descriptor  4: Exit  :

For a newly purchased hard disk, it is not initialized yet. As shown above, enter "Y" and press the return key twice, then proceed to (1) Secure area.

**If already used with Human68K**

**shell      win0**

★★★  System area management information is as follows ★★★  
Total installation capacity: 40 MB  
Block (1): Human68k  39 MB  
Free space: 0 MB  

1: Secure area  2: Release area  3: Create descriptor  4: Exit  :

If it has already been used with Human68K, the allocated area will be displayed as shown above. Release the area as shown below.

Page 19

1: Domain Confirmation  2: Domain Release  3: Disk Reap Creation  4: End  : 2

Please enter the partition number. (1,2,3,4..15) : 1

★★★★ System domain management information is as follows ★★★★
Total device capacity 40 MB
Free domain 39 MB

1: Domain Confirmation  2: Domain Release  3: Disk Reap Creation  4: End  : 

When you enter '2' and press the return key, "Domain Release" will be selected, and it will ask for the partition number. When you enter '1' and press the return key, the domain of 'Block (1): Human68k' will be released.

Confirm domain: Enter '1' as shown below and press the return key, "Domain Confirmation" will be selected, and it will ask for the capacity to confirm. Enter '39' and press the return key if using with OS-9.

* When sharing with Human68k, enter the capacity to be used with OS-9.

1: Domain Confirmation  2: Domain Release  3: Disk Reap Creation  4: End  : 1
How many MB to confirm?  : 39

★★★★ System domain management information is as follows ★★★★
Total device capacity 40 MB
Block (1) : OS-9/68k 39 MB
Free domain 0 MB

1: Domain Confirmation  2: Domain Release  3: Disk Reap Creation  4: End  :

6. Create a disk script. Enter '3' and press the return key to select 'Create Disk Script', then enter the partition number to create and the disk script file name as shown in the diagram below.

1: Confirm Region 2: Release Region 3: Create Disk Script 4: End : 3

Please enter the partition number. (1, 2, 3, 4..15) : 1
Enter the name of the original disk script file. : h0.40m
Enter the name of the disk script file to be created. : h0.p1

★★★ Management information for the system region is as follows ★★★
Total device capacity: 40 MB
Block (1): OS-9/68k 39 MB
Free region: 0 MB

1: Confirm Region 2: Release Region 3: Create Disk Script 4: End : 

#####

7 Finally, enter "4: End" and press the return key. The hard disk with device number "0" will be automatically formatted.

1: Protect area  2: Release area  3: Create descriptor  4: End   : 4

unlink h0
load -d h0.p1
format /h0 -rv=OS-9/68000
Disk format command
OS-9/68000 V2.2R1 SHARP X68000
.................Format data.................

Fixed values:
Disk type: Hard
Sector/track: 33
Segment allocation size: 8

Variable values:
Cylinders: 604
Recording surface heads: 8
Sector interleave offset: 1

Formatting device: /h0
Is this ok? Hard disk. Is this ok? Perform physical format? Verify physically? 000 001 002 003 ....

Normal sectors: $00026ee0  159456
Bad sectors:  $00000000  0
Verify sectors:  $00026ee0  159456
Writing root directory.

※ For using the hard disk with device number "0" as a data disk, please enter the following commands.

$ chd /d0/CMDS/BOOTOBJS
$ load -d rbhddrv h0.pl
$ iniz h0

— Page 22 —

※If you want to boot the OS-9 system from the hard disk with device number "0," please input the following.

$ make.h0.xxx

Here, "xxx" is as follows.

avs    Creates a system for the AV-RIDER environment.
txt    Creates a system for the multi-screen environment.
wnd    Creates a system for the personal window environment.

For more details, please refer to "6.14 System Reconstruction" in the OS-9/X68000 user manual.

(2) Procedure for initializing hard disks with device numbers "1 to 3."

※ In the OS-9/X68000, a procedure file like "init_hd.40m" is not provided for initializing hard disks with device numbers "1 to 3," so the following steps are necessary.

■Procedure to create a procedure file

1. Change the current data directory to PROC.

$ chd PROC

2. Copy the original procedure file.

※ If device number is 1, it's h1; if 2, it's h2; and if 3, it's h3. For example, if it's device number 1:

$ copy init_hd.40m init_h1.40m

3. Use EDT (line editor) to change the device number in init_h1.40m.

$ EDT init_h1.40m

4) Use the string replacement command to change the device number. Please enter "c* h0 hl".

*0001	-t
E: c* h0 hl
*0004	load -d rbhddrv hl1.40m
*0006	unlink hl
*0007	load -d hl1.p1
*0008	format /hl1 -rv=OS-9/68000
E:

5) Move the pointer of the line editor back to 0001 and use the string replacement command again to change the device number. Please enter "0001" and "c* hpu hpu /hl1".

E: 0001
*0001	-t
E: c* hpu hpu /hl1
*0005	hpu /hl1 </win0
E:

6) Confirm if the device number has been correctly changed. Please enter "0001" and "/13".

E: 0001
*0001	-t
E: /13
*0001	-t
```
0002	tmode nopause -w=1
0003	chd CMDS/BOOTOBJS
0004	load -d rbhddrv h1.40m
0005	hpu /hl1 </win0
0006	unlink hl
0007	load -d hl1.p1
0008	format /hl1 -rv=OS-9/68000
0009	y
0010	y
0011	y
0012	y
```
E:

7) If the device number has been correctly changed, please enter "Q". init.hl1.40m is saved and restored to the original prompt state.

E: Q

8) Return to the original current data directory.

$ chd ..

Page 24

Above, by executing "init.h1.40m", it is possible to initialize the hard disk of device number 1.

* If you use the hard disk of device number "1 - 3" as data disks, please change the device number h0 as below.

$ cd CMDS/BOOTOBJS
$ load -d rbhddrv h0.pl
$ iniz h0

Notes:

If you need to boot the OS-9 system from the hard disks of device numbers 1 to 3, you must change the device number of the "make.h0.xxx" project file, but if the device number is attached inside the procedure file in "make.h0.xxx", you must also change the device number there.

In OS-9/X68000, there are many procedure files prepared for using device number "0" for the hard disk, but there are not many procedure files regarding device numbers "1 - 3".

For beginners of OS-9/X68000, it is recommended to use device number "0" for the hard disk. Please use device numbers "1 - 3" as data disks.

3. MSX2 HD Interface

By purchasing the ASCII-made MSX2 HD Interface IT-X640, it is possible to use with MSX2 and MSX2+.

* For hard disk initialization and handling methods, please refer to the user manual of the MSX2 HD Interface.

Important Notes:
- When using the IT-X640 with MSX2 HD Interface, make sure to always set the ID number of IT-X640 to "0".
- IT-X680 cannot be connected to and used with MSX2 HD Interface.

"M E M O"

And at the bottom of the page:

"— 26 —"

Chapter 5: Steps to Take During Troubles

In case of trouble, please carefully read this chapter and re-confirm the issue. If the trouble cannot be resolved, please consult with the store where you purchased the product or our user support.

1. If the ITX series does not operate even when the power is turned on:
- Is the power plug properly connected to the AC outlet?

2. If power is supplied to the ITX series but it does not operate:

1 System does not start
- Is the computer's power supply normal?
- Is the system disk correctly set in the drive you are trying to start?

2 ITX series is not recognized
- Are you using Human 68K Ver 2.0 or later?
- Is the memory switch setting correct?
- Are the connection cables correctly and securely connected?
- Is the ID switching switch setting correct?
- Did you correctly perform the format?
- Did you restart after formatting?
- Are the terminators correctly attached?
- Is the memory switch setting correct?

The text is:

MEMO

This text does not appear to be in Japanese; it is in English.

Chapter 6 Basic Specifications of the ITX Series

* Performance Specifications

| Item Name    | IT-X640 | IT-X680 |
|--------------|--------|--------|
| Storage Capacity (When formatted) |        |        |
| Device (MB)  | 42.0   | 85.8   |
| Cylinder (KB)  | 65,536 | 92,160 |
| Track (KB)  | 8,192    | 18,432 |
| Sector (KB)  | 256     | 512    |
| Disk Configuration   |        |        |
| Number of Disks   | 4      | 3      |
| Number of Heads  | 8      | 5      |
| Total Cylinders    | 642    | 932    |
| Total Tracks   | 5,136  | 4,660  |
| Data Transfer Rate (Mbit/s) | 5      | 10     |
| Access Time    |        |        |
| Between tracks (ms) | 8      | 7      |
| Average Seek Time (ms) | 28     | 20     |
| Maximum Seek Time (ms) | 54     | 39     |
| Disk Rotation Speed (rpm) | 3,600  | 3,600  |
| Average Rotational Latency (ms) | 8.33   | 8.33   |
| Recording Media Type | MFM    | 2-7 RLL|
| Recording Density   |        |        |
| Bit Density (BPI)   | 14,000 | 28,000 |
| Track Density (TPI) | 850    | 1,175  |
| Interface      | SASI   | SASI   |

**External Specifications**

| Product Name | IT-X640 | IT-X680 |
|--------------|---------|---------|
| External Dimensions (W×H×D mm) | 87×142×260 | 87×142×260 |
| Weight (Kg)  | 2.4     | 2.3     |
| Power Consumption (W) | 28      | 35      |

**Environmental Conditions**

| Product Name | IT-X640 |            | IT-X680 |            |
|--------------|---------|------------|---------|------------|
|              | Operating | Non-operating | Operating | Non-operating |
| Temperature  | 5~45°C  | -40~60°C   | 5~45°C  | -20~60°C   |
| Temperature Gradient | 10°C/H | No condensation | 10°C/H | 10°C/H |
| Relative Humidity | 8~80% | No condensation | 5~80% | 5~90% |
| Shock        | 2G      | 40G        | 2G      | 50G        |

**Chapter 7: Maintenance Information**

Thank you for purchasing our product from Aitek Corporation. We take every measure to ensure the quality of our products, but in the event that repairs are needed due to an accident, we offer repair services. The details are as follows:

1. **Bringing in Repairs**
   If damage occurs, you can bring the malfunctioning unit to the shop where you purchased it to fulfill the conditions for repair.

2. **Repairs by Courier**
   If damage occurs and it is inconvenient for you to bring the malfunctioning unit to the shop where you purchased it, you can send it to us by courier. In this case, you are responsible for the shipping cost. Please consult with the shop where you purchased the unit about packaging for shipment. 

3. **Repair Time**
   Repair time varies depending on the extent and content of the damage, but generally, it will be completed within 2 weeks.

4. **Warranty Repairs**
   If the repair is within the warranty period of one year, it will be done free of charge. However, even within the warranty period, some cases may incur charges depending on the warranty terms.

5. **Important Warranty Notice**
   Keep the warranty card in a safe place. If you do not have the warranty card, the warranty repair may not be provided even within the warranty period.

6. **Repairs After Warranty**
   After the warranty period, repairs will be charged. The basic repair fees are shown in the table below.

**Please note that the prices listed below do not include consumption tax.**

| **Simple Repair (Technical Fee)** | **3,000 Yen** |
| **General Repair (Technical Fee)** | **5,000 Yen** |
| **Parts Charges** | **Actual Cost** |
| **Shipping Cost** | **Customer's Responsibility** |

※ The ownership rights of defective parts replaced during the repair will belong to Aitec Co., Ltd.

7. For those who wish to receive a replacement machine due to the convenience of the customer, we have prepared a 40MB hard disk as follows.

| Within the Warranty Period | Up to 1 week after the repaired product arrives at the customer's place is free After that, an additional 1500 yen per day |
| Outside the Warranty Period | The first week is 5,000 yen. After that, an additional 1,500 yen per day |

Appendix

User's Manual
OS-9/X68000 Supplement Edition

(blank page)

**Introduction**

The basic handling method is explained in the IT-X640 / IT-X680 user manual, but this book is a supplementary user manual for handling OS-9 / X68000 and IT-X640 · IT-X680.

The main contents are as follows:
- How to initialize the additional hard disk
- How to register an additional hard disk to the system
- How to coexist with Human68K (Ver2.0)
- How to reconfigure the system

**Caution**

Within OS-9 Version 2.2, there are cases where initialization cannot be done when using IT-X680. (There is no problem with the IT-X640)

According to our research, this version covers serial numbers up to SS13000; from SS13001 onwards it can be used with IT-X680 without any problems.

If you are using OS-9 with serial numbers up to SS13000, please contact the address below.

**Contact Information**
Postal code 162  8 Ichigaya-Yawatacho, Shinjuku-ku, Tokyo
Sharp Corporation, TV Business Division, Product Planning Department 4 
Phone: (03) 260-1161

(blank page)

Table of Contents

Chapter 1: Precautions for Using OS-9/X68000 .......................................... 1
1.1 Relationship Between ITX Series and Device Number ............ 1
■ When connecting the ITX series to the X68000 series .......... 1
● IT-X640 connecting two units ............................................ 1
● IT-X640.IT
X680 connecting .................................................................. 1
● IT-X680 connecting two units ............................................. 2
■ When connecting the internal hard disk type ITX68000 series .... 2
ITX series connecting .............................................................. 2
● IT-X640 connecting ..................................................... 2
● IT-X680 connecting ..................................................... 2

Chapter 2: How to Initialize the Additional Hard Disk ..................... 3
2.1 Precautions (for device number "0") .......................................... 3
◎ When the ITX series is connected to the X68000 series ................ 3
◎ Hard Disk (20 MB) Internal Type X68000 series ............................ 3
2.2 How to Initialize for Device Number "1" ...................................... 3
2.3 How to Initialize for Device Number "2" ..................................... 5
2.4 How to Initialize for Device Number "3" ...................................... 7

Chapter 3: Registering the Additional Hard Disk to the System ...... 10
3.1 Changing the StartUp File .......................................................... 10
3.2 Creating the InitHD File .............................................................. 11

Chapter 4: How to Manage When Mixed with Human68K (Ver 2.0) ... 15
4.1 Startup Menu ...................................................................... 15

Chapter 5: System Reconfiguration ............................................ 16
5.1 How to Reconfigure the System ......................................... 16
5.2 When the Device Number is "1" or More and Hard Disk Devices .... 16
■Precautions When Creating a Project File .................................. 16
■How to Execute a Project File .................................................. 17

*(Blank page in the original.)*

Chapter 1  Precautions for Using OS-9/X68000

In OS-9, there are no concepts such as logical drives (A: B: C: D:) like Human68K, but rather, fixed drives are specified. Up to 4 hard disk devices supported by OS-9 can be used, h0 through h3. (Device numbers "0" to "3")

The procedure files related to hard disk devices provided on the OS-9 system disk, such as [init_hd_40m] and [make_h0_wnd], are prepared only for device number "0"; device numbers "1" to "3" must be created independently.

1.1 Relationship between ITX Series and Device Numbers

■ When connecting the ITX series to the X68000 series
● In case of connecting two IT-X640 units

```
                      ID Number "0"              ID Number "1"
  X68000 ——— IT-X640 ——— IT-X640
                      Device Number "0"          Device Number "2"
                      No Device Number "1"       No Device Number "3"
```

● When connecting IT-X640/IT-X680

```
                      ID Number "0"              ID Number "1"
  X68000 ——— IT-X640 ——— IT-X680
                      Device Number "0"          Device Number "2"
                      No Device Number "1"       Device Number "3"

                      ID Number "0"              ID Number "1"
  X68000 ——— IT-X680 ——— IT-X640
                      Device Number "0"          Device Number "2"
                      Device Number "1"          No Device Number "3"
```

● When connecting two IT-X680 units

```
                                        ID number = "0"                                                                   ID number = "1"

                                   IT-X680                                                                                   IT-X680
```
X68000                            Device number "0"                     X68000                                        Device number "2"
                                   Device number "1"                                                                       Device number "3"

● When connecting the ITX series to the X68000 series with built-in hard disk type
■ When connecting IT-X640

```
                                        ID number = "1"

                              IT-X640
```
X68000 (Built-in HDD)     Device number "0"                           X68000 (Built-in HDD)                     Device number "2"
                              Device number "1" absent                Device number "3" absent

● When connecting IT-X680

```
                                        ID number = "1"

                           IT-X680
```
X68000 (Built-in HDD)   Device number "0"                    X68000 (Built-in HDD)                    Device number "2"
                           Device number "1" absent        Device number "3" absent

When connecting IT-X640, please note that the next device number will be empty.
Even if the device number is empty for logical drive purposes in Human68K (Ver. 2.0), it will automatically become A, B, C, etc. in order. However, in OS-9, empty device numbers cannot be used for specifying fixed drives. 

# Chapter 2: How to Initialize the Additional Hard Disk

When initializing a hard disk (device number "0"), use `init_hd_xx.x`. 
(For detailed instructions, refer to the IT-X640/IT-X680 User Manual.)

# 2.1 Precautions (For device number "0")

**1. If connected to the ITX series in the X68000 series:**

- Perform initialization using `init_hd_40m`.
- Input the disk descriptor file `h0_40mh0_p1`.

**2. For a 20MB internal type hard disk in the X68000 series:**

- Perform initialization using `init_hd_20m`.
- Input the disk descriptor file `h0_20mh0_p1`.

# 2.2 How to Initialize a Device Numbered "1"

**Note:** When connected with IT-X680 and ID number is "0" in the X68000 series. Internal type hard disks in the X68000 series do not include a "1" device number.

1. First, create an initial project file for device number "1".
```
   Change the current data directory to PROC.
   $ chd PROC
```

2. Copy the original project file.
   $ copy init-hd_40m init-h1_40m

3. In EDT (Line Editor), change the device number of `init_h1_40m`.
   $ EDT init_h1_40m

4 Convert the device number using the string substitution command. Please enter "0 0 0 1", "c:* " h0" h1" ".
*0001 - t
```
 E: c:* " h0" h1"
 *0004 load -d rbhddrv h1_40m
 *0006 unlink h1
 *0007 load h1_p1
 *0008 format /h1 -rv = OS-9 / 68000
 E:
```
5 Return the pointer of the line editor to 0 0 0 1, and convert the device number again using the string substitution command. Please enter "0 0 0 1", "c:* " hpu" / h1 " ".
```
 E: 0 0 0 1
 *0001 -t
 E: c:* " hpu" hpu / h1"
 *0005 hpu /h1 </ win0
 E:
```
6 Check that the device number has been converted correctly. Please enter "0 0 0 1", "113".
```
 E: 0 0 0 1
 *0001 -t
 E: 113
 *0001 -t
 0002 tmode nopause - w=1
 0003 chd CMDS / BOOTOBJS
 0004 load -d rbhddrv h1_40m
 0005 hpu / h1 </ win0
 0006 unlink h1
 0007 load -d h1_p1
 0008 format / h1 -rv= OS-9 / 68000
 0009 y
 0010 y
 0011 y
 0012 y
 E:
```

7 If the device number has been changed correctly, please enter "q". init_h1_40m will be saved and will return to the original prompt state.

    E: q

8 Return to the current data directory.

    $ chd ..

9 Initialize the hard disk with device number "1".

    $ init_h1_40m

10 The operation method is the same as for device number "0". However, for descriptor creation, enter "h1_40m2h1_p1".

2.3 How to initialize device number "2"

* When connected with ITX series using ID number "1" for X68000 series (including hard disk embedded type).

1 First, create the initialization procedure file for device number "2". Change the current data directory to PROC.

    $ chd PROC

2 Copy the original procedure file.

    $ copy init_hd_40m init_h2_40m

3 Using EDT (line editor), change the device number in init_h2_40m.

    $ EDT init_h2_40m

4 Use the string substitution command to replace the device number. Enter "fc* h0" h2".

*0001 -t
E: c* "h0" h2"
*0004 load -d rbhddrv h2_40m
*0006 unlink h2
*0007 load -d h2_p1
*0008 format /h2 -rv=OS-9/68000
E:

5 Return the line editor pointer to 0001, and use the string substitution command again to replace the device number. Enter "0001 fc* hpu" hpu /h2".

E:0001
*0001 -t
E: c* "hpu" hpu /h2"
*0005 hpu /h2 < /win0
E:

6 Confirm that the device number has been correctly replaced. Enter "0001" and "113".

E:0001
*0001 -t
E:113
*0001 -t
```
0002 tmode nopause -w=1
0003 chd CMDS/BOOTOBJS
0004 load -d rbhddrv h2_40m
0005 hpu /h2 < /win0
0006 unlink h2
0007 load -d h2_p1
0008 format /h2 -rv=OS-9/68000
0009 y
0010 y
0011 y
0012 y
```
E:

Page 6

7 If the device number has been correctly replaced, input 'q' and press enter. init_h2_40m will be saved, and the state will be returned to the original prompt.
E: q

8 Return to the original current data directory.
$ chd ..

9 Initialize the hard disk with device number "2".
$ init_h2_40m

10 The operation method is the same as for device number "0". However, when creating a descriptor, input "h2_40meh2_p1" as shown.

2.4  Initialization Method for Device Number "3"

※ For X68000 Series (including the internal hard disk type), when connecting IT-X680 to ID Number="1", follow the instructions from point 2.

1 First, create an initialization procedure file for device number "3". Change the current data directory to PROC.
$ chd PROC

2 Copy the original procedure file.
$ copy init_hd_40m init_h3_40m

3 Edit (line editor) init_h3_40m to change the device number.
$ EDT init_h3_40m

4. Use the string replacement command to change the device number. Enter "fc* "h0" "h3"".

```
 * 0001     -t
  E: c* ”h0” “h3”
 * 0004     load -d rbhddrv h3_40m
 * 0006     unlink h3
 * 0007     load -d h3_p1
 * 0008     format /h3 -rv=OS-9/68000
 E:
```

5. Return the line editor pointer to 0001, and again use the string replacement command to change the device number. Enter "fc* "hpu" hpu /h3"".

```
 E: 0001
 * 0001     -t
  E: c* ”hpu” hpu /h3 ”
 * 0005     hpu /h3 </win0
 E:
```

6. Confirm that the device number has been changed correctly. Enter "0001" and "113".

```
 E: 0001
 * 0001     -t
  E: 113
 * 0001     -t
  0002      tmode nopause -w=1
  0003      chd CMDS/BOOTOBJS
  0004      load -d rbhddrv h3_40m
  0005      hpu /h3 </win0
  0006      unlink h3
  0007      load -d h3_p1
  0008      format /h3 -rv=OS-9/68000
  0009      y
  0010      y
  0011      y
  0012      y
 E:
```

7 If the device number has been correctly changed, enter "q". init_h3_40m will be saved and return to the original prompt state.
```
Example: 
    E: q
```
8 Return to the original current data directory.
    $ chd ..
9 Execute hard disk initialization for device number "3".
    $ init_h3_40m
10 The operation method is the same as for device number "0". However, when creating a disk script, enter "h3_40m & h3_p1".

Note:

If you add -np to the format within init_h3_40m, physical formatting will not be performed, so it will save time for reinitialization. (In this case, remove "0009 to 0012" options)
*0008   format   /h3    -rv=OS-9/68000    -np

If you add -nv to the format within init_h3_40m, verify (bad sector detection) will not be performed, so reinitialization will be processed quite quickly. However, if the number of bad sectors is displayed during initialization with the verify function, be sure to perform initialization with this option. (In this case, remove "0009 to 0012" options)
*0008   format   /h3    -rv=OS-9/68000    -nv

When rebuilding the system, it is necessary to perform reinitialization, so the above options are convenient.

Chapter 3: How to Register the Additional Hard Disk System

After initializing the hard disk device, it can recognize the hard disk device as there are drivers in the memory, but if you reboot OS-9, the hard disk device will not be recognized. Therefore, it is necessary to register the hard disk device in the system.

In the case of Device Number "0", if you execute "make_h0_xxx", h0 will be registered automatically, but if you start up from the OS-9 system floppy disk, h0 will not be recognized, so please change it as follows.

3.1 StartUp File Changes

※When starting from a hard disk device with device number "0", change the StartUp file to /h0/SYS/StartUp.
※When starting from an OS-9 system floppy disk, change the StartUp file to /d0/SYS/StartUp.

1Change the current data directory of the startup drive to SYS.
   $ chd SYS

2Change the StartUp file with the EDT (Line Editor).
```
   $ EDT StartUp
     *0001   -xt
     E:
```

3Enter the next keys in the E: state. ["0020" • " SYS/InitHD" • " *" • "0023" • "q"]
```
    (Enter a space at the beginning for [" SYS/InitHD" • " *"])

   E: 0020
   *0020     * END OF STARTUP
   E: SYS/InitHD
   *0021     * END OF STARTUP
   E: *
   *0022     * END OF STARTUP
   E: 0023
   *0023
   E: q
```

4 Check the modified StartUp file with the list command.

$ list StartUp
-xt
* 
* OS-9 / 68000 Level I V2.2
* Copyright 1984 by Microware Systems Corporation
*
* OS-9 / X68000
* Copyright 1988 by Microware Japan, LTD.
*
* The commands in this file are highly system dependent and should
* be modified by the user.
*
link shell cio
load math
*
iniz syscon
setime -s
*
SYS/InitDD
*
SYS/InitHD
*
* END OF STARTUP

3.2 Creating the InitHD File

*If you are booting from the hard disk system with device number "0",
create the /h0/SYS/InitHD file.

*If you are booting from an OS-9 system floppy disk,
create the /d0/SYS/InitHD file.

1 Set the current data directory of the boot drive to SYS.

$ chd SYS

2 Create the InitHD file using EDT (line editor).

$ EDT InitHD

*Please enter the initial line.*

chd C:\MDS\BOOTOBOJS

*If booting from the OS-9 system floppy disk, /h0 is not recognized, so include /d0 /SYS/InitHD file.
*It is not necessary when booting from /h0 /SYS/InitHD file.*

load  -d rbhddrv h0=_p1
iniz h0

*When the hard disk built-in type is the 68000 series, /h1 does not exist.*
*If IT-X680 is connected with ID number "0" on the second unit with an OS-9 area, please enter it.*

load  -d rbhddrv h1=_p1
iniz h1

*If ITX series is connected with ID number "1" on the second unit with an OS-9 area, please enter it.*

load  -d rbhddrv h2=_p1
iniz h2

*If IT-X680 is connected with ID number "1" on the second unit with an OS-9 area, please enter it.*

load  -d rbhddrv h3=_p1
iniz h3

Example 1

When connecting two IT-X640 units (ID numbers "0" and "1") in the X68000 series and booting from the OS-9 system floppy disk
(When inserting a new line with a line editor, be sure to insert a space first)

● The current data directory is /d0/SYS.
$ EDT InitHD
*0001
E: chd CMDS/BOOTOBJS
*0002
E: load -d rbhddrv h0_p1
*0003
E: iniz h0
*0004
E: load -d rbhddrv h2_p1
*0005
E: iniz h2
E: q

Example 2

When connecting two IT-X680 units (ID numbers "0" and "1") in the X68000 series and booting OS-9 from the hard disk device with device number "0"

● The current data directory is /h0/SYS.
$ EDT InitHD
*0001
E: chd CMDS/BOOTOBJS
*0002
E: load -d rbhddrv h1_p1
*0003
E: iniz h1
E: load -d rbhddrv h2_p1
*0004
E: iniz h2
*0005
E: load -d rbhddrv h3_p1
*0006
E: iniz h3
*0007
E: q

**Example 3**

※ When connecting IT-X640 (ID number is "1") to the built-in hard disk type X68000 series and booting OS-9 from the built-in hard disk device

● The current data directory is /h0/SYS.

$ EDT InitHD
* 0001
E: : chd CMDS/BOOTOBJS
* 0002
E: : load -d rbhddrv h2_p1
* 0003
E: : iniz h2
* 0004
E: q

**Example 4**

※ When connecting IT-X680 (ID number is "1") to the built-in hard disk type X68000 series and booting from the OS-9 system floppy disk

● The current data directory is /d0/SYS.

$ EDT InitHD
* 0001
E: : chd CMDS/BOOTOBJS
* 0002
E: : load -d rbhddrv h0_p1
* 0003
E: : iniz h0
* 0004
E: : load -d rbhddrv h2_p1
* 0005
E: : iniz h2
* 0006
E: : load -d rbhddrv h3_p1
* 0007
E: : iniz h3
* 0008
E: q

Please make sure to copy the file h×_p1 created when running init_h×_40m to the device's CMDS/BOOTOBJS where InitHD is located.

Chapter 4: How to Handle Mixing Human 68K (Ver2.0)

If you prioritize Human 68K area verification first and then prioritize OS-9 area verification, the following message may be displayed, indicating that OS-9 area verification cannot be performed. In that case, please perform the area verification with OS-9 first, then verify the area with Human 68K later.

『"×××" MB cannot be allocated. The starting cylinder is too large.』

The initialization method is the same as “Chapter 2: Initialization Method for Expanded Hard Disk.”

Please enter the capacity you are verifying when you select “1: Area Verification.”

If “3: Create Disk Script” is selected and a disk script file name ending in “_p1” is specified, you will be asked whether to overwrite the h0_p1 created during the previous initialization, if one exists.

If you overwrite h0_p1, make sure to copy CMD S/BOOTOBJS from the device with InitHD.

The disk script file h0_p1 contains hard disk device information, if this disk script file is incorrect, you may face problems, so please handle it carefully.

4.1 Boot Menu

When OS-9 and Human 68K are mixed, a menu screen will be displayed during boot, allowing you to select which OS to boot from.

X68000 HARD DISK IPL MENU

```
1 OS-9/68K
2 Human 68K
```

Select with the cursor key and press the return key

# Chapter 5: Method for System Reconstruction

**5.1 Method for System Reconstruction**

The files for reconstructing the system for hard disk device number "0" are prepared as follows:

- make_h0_wnd: Create a system for the personal window environment.
- make_h0_txt: Create a system for the multi-screen environment.
- make_h0_avs: Create a system for the AV-RIDER environment.

**5.2 In the Case of Hard Disk Device Number "1" or Above**

The reconstruction procedure files for the system for hard disk are specifically for device number "0"; there are no files prepared for device numbers "1" through "3".

Because OS-9 fixes the device drive, you cannot reconstruct the system simply for device numbers "1" through "3". We recommend using the method described below.

Typically, you can copy the procedure file operating on device number "0" and run it on device number "1".

**Notes When Creating Procedure Files**

You can execute procedure files by removing the drive specification and including only the current data directory, so if you are creating a new procedure file, ensure that no drive specification is included.

**Example: In the Case of InitHD**

The floppy drive is fixed at “0”.

$ list InitHD
chd /d0/CMDS/BOOTOBJS
load -d rbhddrv h2_p1
iniz h2

Page: 16

● The hard disk device is fixed to "0".

```
  $ list InitHD
  chd /h0/CMDS_/BOOTOBOJS
  load -d rbhddrv h2 _p1
  iniz h2
```

● Both floppy drive "0" and hard disk device "0" can be used.  
```
  (However, the current data directory needs to be changed)

  $ list InitHD
  chd CMDS_/BOOTOBOJS
  load -d rbhddrv h2 _p1
  iniz h2
```

■ How to run the procedure file

After reconstructing the system with the hard disk of device number "0", secure the free space to execute the procedure file.

When executing the newly created procedure file from a hard disk device other than device number "1", copy it to the hard disk device "0" and run it on the device number "0".

In this way, there is no need to prepare several types of procedure files for device number "0" and device number "1" that perform the same task.

Furthermore, data such as utilization data can be used commonly by specifying a fixed data area in the hard disk device of device number "0" and assigning a drive, even for more than one hard disk device with device number "1".

This usage method explained in the OS-9/X68000 supplementary manual is explained for beginners, so it does not mean that there is a predetermined usage method.

In practical use with the OS-9 hard disk environment: The use of OS-9 to facilitate the management of files and data is encouraged.

*(Blank page in the original.)*

itec

Aitec Co., Ltd.

Postal code 550  1-25-14 Shinmachi, Nishi-ku, Osaka-shi

TEL 06-532-0120

FAX 06-532-0543

User Support 06-532-0320

"i tec
Itec Corporation"
