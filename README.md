Qvmdis : Quake3 QVM disassembler

Usage:  qvmdis <qvm file> [cgame|game]
  optionally specify cgame or game qvm to match syscalls and function hashes

Features:

* Labels jump locations
* Identifies which other functions call a particular function
* Identifies syscalls
* Identifies references to function arguments
* Adds comments for possible string reference values
* Adds comments for possible data reference values
* Computes function hashes and compares to stock QVM to identify possible matches
* Function names, arguments, and local variables can be labeled in separate functions.dat file
* Symbol names can be labeled using separate symbols.dat file
* Constants can be labeled in constants.dat
* Comments can be added in comments.dat

The .dat files are opened from the current working directory.  Comments in .dat files are specified with ';'.

Format of .dat files:

    ---- functions.dat ----
    0x0000 vmMain
      arg0 command
      local 0x14 commandTmp

    0x1223 CG_DrawAttacker
    0x28ae CG_Draw3DModel
      arg0 x
      local 0x18 0x170 refdef  ; also specifies the size

Local variables can optionally specify a size to identify references within a range.

    ---- symbols.dat ----
    0xab2a3 serverTime
    0xb23fa 0x1000 clientData

Size can optionally be specified to identify references within a range.

    ---- constants.dat ----
    0x3f31 DEFAULT_SPEED 0x0

The last value in the contants.dat entry is used to double check that the value is correct.

    ---- comments.dat ----
    0x5a11 inline This is an inline comment added to the end of the line
    0x5ba1 before

    This is a comment block
    added before the address.

    <<<
    0x6aa2 after 2 2
    This comment is
    after the address.

    <<<

    d 0x30bc inline fullName

Before and after comments are terminated with a line that only has '<<<'.  They can also specify a number of blank lines before and after the comment.  A 'd' before the address specifies it's a data segment comment.