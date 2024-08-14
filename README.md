# Modernization-Rules
<h1>Overview</h1>
<h2>Stage 1</h2>

💬 Convert all programs to ILE-RPG
The first step is to get all of your programs into one type of structure, the latest one.
Working from the lowest RPG II program, change it to RPG and put it into QRPGSRC
Compile it and get rid of things that are not working or broken, such as bit manipulations or data areas.
You may have to rename printer output etc.
Once compiled use CVTRPGSRC to get it into QRPGLESRC format.
You can then start using larger fieldnames and take advantage of the debugger.

💬 Convert all flat files to tables
You want to convert all of your flat files to tables and CPYF the data using FMTOPT(*NOCHK) .
Data will be validated and if it does not conform it will either not copy part or all of the file.
Once it has coppied all of the data you know that it has been scrubbed. 

💬 Convert all dates to *ISO dates in tables
All new date manipulation functions work off *iso style dates.
If you have mixed date types the amount of fiddling around you need to do to date math is horrendous. 
Your programmers are forever looking up date transformation commmands MMDDYY to ISO or YYMMDD to ISO, you get the idea. 

<h2>Stage 2</h2>

💬 Convert all ILE-RPG to free format RPG
Might be in your interest to use a commercial program to do the conversion. 
Its not perfect but it will save you a ton of time and effort.

💬 include a copy member for CTL-OPT

💬 get rid of RPG indicators
There is no need for using non named indicators any longer.
This also holds true for 5250 screens. use INDDS(DSPIND_DS) 
// Indicator Data structure for Display file         
d DSPIND_DS       ds            99              
d  dspInds                       1    dim(99)          
d  CustomerNbr_Error...                                  
d                                 n   overlay(dspInd_DS:21)

<h2>Stage 3</h2>

💬 determine if Referential Integrity is necessary and build constraints
While in a perfect world referential integrity is wonderful, in the world of IBM i that has years of program
described rules, it can work against you. Unless you have a mandate to use it not really for conversion.
