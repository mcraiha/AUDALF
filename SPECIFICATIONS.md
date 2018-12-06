```
 __          __        _       _                                                  
 \ \        / /       | |     (_)                                                 
  \ \  /\  / /__  _ __| | __   _ _ __     _ __  _ __ ___   __ _ _ __ ___  ___ ___ 
   \ \/  \/ / _ \| '__| |/ /  | | '_ \   | '_ \| '__/ _ \ / _` | '__/ _ \/ __/ __|
    \  /\  / (_) | |  |   <   | | | | |  | |_) | | | (_) | (_| | | |  __/\__ \__ \
     \/  \/ \___/|_|  |_|\_\  |_|_| |_|  | .__/|_|  \___/ \__, |_|  \___||___/___/
                                         | |               __/ |                  
                                         |_|              |___/                   
```

# Specification for AUDALF

## Common

Unless said otherwise, all types are assumed [little endian](https://en.wikipedia.org/wiki/Endianness#Little-endian) and [two's complement](https://en.wikipedia.org/wiki/Two%27s_complement)

Unless said otherwise, all sections, indexes, variables etc. SHOULD align to 8 byte sections.

Format allows padding between [Index](Index) and Key + Value pairs, and padding after every Key + Value pair

## Types

Every type has own ID which is ALWAYS *unsigned 64 bit integer*

### Special types
| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Special      | Reserved for special cases | 0 | **0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00**

&nbsp;

### Unsigned integer types

Notice that unsigned 8 bit integer is also byte

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Unsigned 8 bit integer      | Unsigned 8 bit integer, equals byte, range [0 .. 255]      |   1 | **0x01 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 16 bit integer      | Unsigned 16 bit integer, range [0 .. 65535]      |   2 | **0x02 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 32 bit integer      | Unsigned 32 bit integer, range [0 .. 4294967295]  |   3 | **0x03 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 64 bit integer      | Unsigned 64 bit integer, range [0 .. 18446744073709551615]  |   4 | **0x04 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 128 bit integer      | Unsigned 128 bit integer, range [0 .. 2<sup>128</sup>−1]  |   5 | **0x05 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 256 bit integer      | Unsigned 256 bit integer, range [0 .. 2<sup>256</sup>−1] |   6 | **0x06 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 512 bit integer      | Unsigned 512 bit integer, range [0 .. 2<sup>512</sup>−1]  |   7 | **0x07 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 1024 bit integer      | Unsigned 1024 bit integer, range [0 .. 2<sup>1024</sup>−1]  |   8 | **0x08 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 2048 bit integer      | Unsigned 2048 bit integer, range [0 .. 2<sup>2048</sup>−1]  |   9 | **0x09 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 4096 bit integer      | Unsigned 4096 bit integer, range [0 .. 2<sup>4096</sup>−1]  |   10 | **0x0A 0x00 0x00 0x00 0x00 0x00 0x00 0x00**

&nbsp;

### Signed integers types

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Signed 8 bit integer | Signed 8 bit integer, range [-128 .. 127]  | 16777217 | **0x01 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 16 bit integer | Signed 16 bit integer, range [-32768 .. 32767]  | 16777218 | **0x02 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 32 bit integer | Signed 32 bit integer, range [-2147483648 .. 2 147 483 647]  | 16777219 | **0x03 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 64 bit integer | Signed 64 bit integer, range [-9 223 372 036 854 775 808 .. 9 223 372 036 854 775 807] | 16777220 | **0x04 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 128 bit integer | Signed 128 bit integer, range [-2<sup>127</sup> .. 2<sup>127</sup>−1]  | 16777221 | **0x05 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 256 bit integer | Signed 256 bit integer, range [-2<sup>255</sup> .. 2<sup>255</sup>−1]  | 16777222 | **0x06 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 512 bit integer | Signed 512 bit integer, range [-2<sup>511</sup> .. 2<sup>511</sup>−1]  | 16777223 | **0x07 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 1024 bit integer | Signed 1024 bit integer, range [-2<sup>1023</sup> .. 2<sup>1023</sup>−1]  | 16777224 | **0x08 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 2048 bit integer | Signed 2048 bit integer, range [-2<sup>2047</sup> .. 2<sup>2047</sup>−1]   | 16777225 | **0x09 0x00 0x00 0x01 0x00 0x00 0x00 0x00**
| Signed 4096 bit integer | Signed 4096 bit integer, range [-2<sup>4095</sup> .. 2<sup>4095</sup>−1]   | 16777226 | **0x0A 0x00 0x00 0x01 0x00 0x00 0x00 0x00**

&nbsp;

### Floating point types

Most of these follow IEEE 754

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| 8 bit floating point | 8 bit floating point format | 33554433 | **0x01 0x00 0x00 0x02 0x00 0x00 0x00 0x00**
| 16 bit floating point | 16 bit floating point format, binary16 from IEEE 754 | 33554434 | **0x02 0x00 0x00 0x02 0x00 0x00 0x00 0x00**
| 32 bit floating point | 32 bit floating point format, binary32 from IEEE 754 | 33554435 | **0x03 0x00 0x00 0x02 0x00 0x00 0x00 0x00**
| 64 bit floating point | 64 bit floating point format, binary64 from IEEE 754 | 33554436 | **0x04 0x00 0x00 0x02 0x00 0x00 0x00 0x00**
| 128 bit floating point | 128 bit floating point format, binary128 from IEEE 754 | 33554437 | **0x05 0x00 0x00 0x02 0x00 0x00 0x00 0x00**
| 256 bit floating point | 256 bit floating point format, binary256 from IEEE 754 | 33554438 | **0x06 0x00 0x00 0x02 0x00 0x00 0x00 0x00**
| 512 bit floating point | 512 bit floating point format | 33554439 | **0x07 0x00 0x00 0x02 0x00 0x00 0x00 0x00**

&nbsp;

### Unsigned fixed point types

For Q notation see [Q (number format)](https://en.wikipedia.org/wiki/Q_(number_format))

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Unsigned 8 bit fixed point | Unsigned 8 bit fixed point format, UQ4.4 | 50331649 | **0x01 0x00 0x00 0x03 0x00 0x00 0x00 0x00**
| Unsigned 16 bit fixed point | Unsigned 16 bit fixed point format, UQ8.8 | 50331650 | **0x02 0x00 0x00 0x03 0x00 0x00 0x00 0x00**
| Unsigned 32 bit fixed point | Unsigned 32 bit fixed point format, UQ16.16 | 50331651 | **0x03 0x00 0x00 0x03 0x00 0x00 0x00 0x00**
| Unsigned 64 bit fixed point | Unsigned 64 bit fixed point format, UQ32.32 | 50331652 | **0x04 0x00 0x00 0x03 0x00 0x00 0x00 0x00**
| Unsigned 128 bit fixed point | Unsigned 128 bit fixed point format, UQ64.64 | 50331653 | **0x05 0x00 0x00 0x03 0x00 0x00 0x00 0x00**
| Unsigned 256 bit fixed point | Unsigned 256 bit fixed point format, UQ128.128 | 50331654 | **0x06 0x00 0x00 0x03 0x00 0x00 0x00 0x00**
| Unsigned 512 bit fixed point | Unsigned 512 bit fixed point format, UQ256.256 | 50331655 | **0x07 0x00 0x00 0x03 0x00 0x00 0x00 0x00**

&nbsp;

### Signed fixed point types

For Q notation see [Q (number format)](https://en.wikipedia.org/wiki/Q_(number_format))

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Signed 8 bit fixed point | Signed 8 bit fixed point format, Q3.4 | 67108865 | **0x01 0x00 0x00 0x04 0x00 0x00 0x00 0x00**
| Signed 16 bit fixed point | Signed 16 bit fixed point format, Q7.8 | 67108866 | **0x02 0x00 0x00 0x04 0x00 0x00 0x00 0x00**
| Signed 32 bit fixed point | Signed 32 bit fixed point format, Q15.16  | 67108867 | **0x03 0x00 0x00 0x04 0x00 0x00 0x00 0x00**
| Signed 64 bit fixed point | Signed 64 bit fixed point format, Q31.32 | 67108868 | **0x04 0x00 0x00 0x04 0x00 0x00 0x00 0x00**
| Signed 128 bit fixed point | Signed 128 bit fixed point format, Q63.64 | 67108869 | **0x05 0x00 0x00 0x04 0x00 0x00 0x00 0x00**
| Signed 256 bit fixed point | Signed 256 bit fixed point format, Q127.128 | 67108870 | **0x06 0x00 0x00 0x04 0x00 0x00 0x00 0x00**
| Signed 512 bit fixed point | Signed 512 bit fixed point format, Q255.256  | 67108871 | **0x07 0x00 0x00 0x04 0x00 0x00 0x00 0x00**

&nbsp;

### String types

Strings are stored as bytes

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| ASCII   | ASCII | 83886081 | **0x01 0x00 0x00 0x05 0x00 0x00 0x00 0x00**
| UTF-8 Unicode | UTF-8 Unicode | 83886082 | **0x02 0x00 0x00 0x05 0x00 0x00 0x00 0x00**
| UTF-16 Unicode | UTF-16 Unicode | 83886083 | **0x03 0x00 0x00 0x05 0x00 0x00 0x00 0x00**
| UTF-32 Unicode | UTF-32 Unicode | 83886084 | **0x04 0x00 0x00 0x05 0x00 0x00 0x00 0x00**

&nbsp;

### Boolean types

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Common boolean | It is either True (1) or False (0) | 100663297 | **0x01 0x00 0x00 0x06 0x00 0x00 0x00 0x00**

## Header section

Header section in AUDALF means FourCC + Specification version + byte size of whole data

### FourCC

[FourCC](https://en.wikipedia.org/wiki/FourCC) is ALWAYS '**AUDA**' as ACII in bytes, so **0x41 0x55 0x44 0x41**

### Specification version

Defines what AUDALF features have been used. Check from [version history](VERSION_HISTORY.md) what features are added in different versions. First release has version number 1, so as bytes it is **0x01 0x00 0x00 0x00**. This can be assumed to be *unsigned 32 bit integer* and it can be read in one 8 byte get with FourCC (so get 8 bytes when reading start of the stream and decode FourCC and spefication version from those 8 bytes).

### Byte size of whole data

Defines how many bytes the whole AUDALF data has (this includes EVERYTHING, meaning that FourCC and Specification version are included). This is ALWAYS *unsigned 64 bit integer*. 

e.g. **0x00 0x04 0x00 0x00 0x00 0x00 0x00 0x00** would mean that AUDALF size is 1024 bytes.

The size DOES NOT mean that every byte has useful info. So you can padd the end of file if you want to do so.

## Index section

Index section in AUDALF means Index count + Key type + entry definitions

### Index count
Defines how many index items there are. This is ALWAYS *unsigned 64 bit integer*. 

e.g. **0x04 0x00 0x00 0x00 0x00 0x00 0x00 0x00** would mean that there are 4 items

### Key type

Defines what is the type for dictionary keys. Or defines that this is a list where key is the index number of the list. This is ALWAYS *unsigned 64 bit integer*. 

0 means that structure is a list, and key entries are list index values (as 64 unsigned integers). 

Other options are defined in types section.

e.g. **0x07 0x00 0x00 0x00 0x00 0x00 0x00 0x00** would mean that every dictionary key is 64 bit unsigned integer

###  Entry definitions

There is 64 bit unsigned integer for every index item, so total is Index count * 8 bytes of entry points. Entry point is byte address location of key + value pair.

e.g. **0x68 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0xC8 0x00 0x00 0x00 0x00 0x00 0x00 0x00** would mean that first entry is at byte address 104 (0x68) and second entry is at byte address 200 (0xC8)

## Key + value pairs

### Key

As Key type is defined in Index section, you just read right amount of bytes, and that is the value. 

If key type is 0 that means structure is a list, and key entries are list index values (as 64 unsigned integers). You SHOULD store list entries in ascending order, but that is not required.

e.g. if type is Unsigned 32 bit integer, you read 4 bytes and use those as Unsigned 32 bit integer.

### Value type ID

This is ALWAYS *unsigned 64 bit integer*. Options are defined in types section.

### Value length

This is ALWAYS 64 bit unsigned integer that tells how many bytes the value takes. Can be 0 in certain cases, e.g. with empty string. Value length max (0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF 0xFF) means that value is NULL.

### Actual value bytes

Value length amount of bytes that can be used as value for dictionary entry. Since length can be 0 or NULL, these bytes might not exist at all
