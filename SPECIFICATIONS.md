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

**Table of Contents**

| Section        | Description | Link |
| ------------- |:-------------:| -----:|
| Common      | Common definitions | [Common](#Common) |
| Types      | List of types of variables that AUDALF supports | [Types](#Types) |
| Header section | Definition of header section of AUDALF | [Header section](#Header-section) |
| Index section | Definition of index section of AUDALF | [Index section](#Index-section) |
| Key and value pairs | Definition of key and value pairs of AUDALT | [Key and value pairs](#Key-and-value-pairs)


## Common

One byte is ALWAYS 8 bits.

Unless said otherwise, all types are assumed [little endian](https://en.wikipedia.org/wiki/Endianness#Little-endian) and [two's complement](https://en.wikipedia.org/wiki/Two%27s_complement)

Unless said otherwise, all sections, indexes, variables etc. SHOULD align to 8 byte (64 bit) sections.

AUDALF allows padding between [Index](#Index-section) and Key + Value pairs, and padding after every Key + Value pair

Padding SHOULD be **0x00** (zeroes).

Whole AUDALF payload is NOT needed for parsing single key and value pair.

&nbsp;

## Types

Every type has own ID which is ALWAYS *unsigned 64 bit integer*

With single variables the actual value starts immediately from location given and there SHOULD be padding after the value in case the value does not end to 8 byte (64 bit) boundary.

With arrays there is ALWAYS count value *unsigned 64 bit integer* that tells how many bytes of data the array contains (in case the type has data length at least 8 bits) or how many values the array contains in case type has data length 7 bits or less (booleans are currently the only ones). Count does not include itself. Actual data is ALWAYS after the count and there SHOULD be padding in case the array does not end to 8 byte (64 bit) boundary.

&nbsp;

### Special types

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Special      | Reserved for special cases | 0 | **0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00**

&nbsp;

### Unsigned integer types

Notice that unsigned 8 bit integer is also byte

#### Single variables

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Unsigned 8 bit integer | Unsigned 8 bit integer, equals byte, range [0 .. 255] |   1 | **0x01 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 16 bit integer | Unsigned 16 bit integer, range [0 .. 65535] |   2 | **0x02 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 32 bit integer | Unsigned 32 bit integer, range [0 .. 4294967295] |   3 | **0x03 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 64 bit integer | Unsigned 64 bit integer, range [0 .. 18446744073709551615] |   4 | **0x04 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 128 bit integer | Unsigned 128 bit integer, range [0 .. 2<sup>128</sup>−1] |   5 | **0x05 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 256 bit integer | Unsigned 256 bit integer, range [0 .. 2<sup>256</sup>−1] |   6 | **0x06 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 512 bit integer | Unsigned 512 bit integer, range [0 .. 2<sup>512</sup>−1] |   7 | **0x07 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 1024 bit integer | Unsigned 1024 bit integer, range [0 .. 2<sup>1024</sup>−1] |   8 | **0x08 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 2048 bit integer | Unsigned 2048 bit integer, range [0 .. 2<sup>2048</sup>−1] |   9 | **0x09 0x00 0x00 0x00 0x00 0x00 0x00 0x00**
| Unsigned 4096 bit integer | Unsigned 4096 bit integer, range [0 .. 2<sup>4096</sup>−1] |   10 | **0x0A 0x00 0x00 0x00 0x00 0x00 0x00 0x00**

&nbsp;

#### Arrays

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of unsigned 8 bit integers | Unsigned 8 bit integer, equals byte, range [0 .. 255] | 65537 | **0x01 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 16 bit integer | Unsigned 16 bit integer, range [0 .. 65535] | 65538 | **0x02 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 32 bit integer | Unsigned 32 bit integer, range [0 .. 4294967295] | 65539 | **0x03 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 64 bit integer | Unsigned 64 bit integer, range [0 .. 18446744073709551615]  | 65540 | **0x04 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 128 bit integer | Unsigned 128 bit integer, range [0 .. 2<sup>128</sup>−1]  | 65541 | **0x05 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 256 bit integer | Unsigned 256 bit integer, range [0 .. 2<sup>256</sup>−1] | 65542 | **0x06 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 512 bit integer | Unsigned 512 bit integer, range [0 .. 2<sup>512</sup>−1]  | 65543 | **0x07 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 1024 bit integer | Unsigned 1024 bit integer, range [0 .. 2<sup>1024</sup>−1]  | 65544 | **0x08 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 2048 bit integer | Unsigned 2048 bit integer, range [0 .. 2<sup>2048</sup>−1]  | 65545 | **0x09 0x00 0x01 0x00 0x00 0x00 0x00 0x00**
| Array of unsigned 4096 bit integer | Unsigned 4096 bit integer, range [0 .. 2<sup>4096</sup>−1]  | 65546 | **0x0A 0x00 0x01 0x00 0x00 0x00 0x00 0x00**

&nbsp;

### Signed integers types

#### Single variables

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

#### Arrays

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of signed 8 bit integers | Signed 8 bit integer, range [-128 .. 127]  | 16842753 | **0x01 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 16 bit integers | Signed 16 bit integer, range [-32768 .. 32767]  | 16842754 | **0x02 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 32 bit integers | Signed 32 bit integer, range [-2147483648 .. 2 147 483 647]  | 16842755 | **0x03 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 64 bit integers | Signed 64 bit integer, range [-9 223 372 036 854 775 808 .. 9 223 372 036 854 775 807] | 16842756 | **0x04 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 128 bit integers | Signed 128 bit integer, range [-2<sup>127</sup> .. 2<sup>127</sup>−1]  | 16842757 | **0x05 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 256 bit integers | Signed 256 bit integer, range [-2<sup>255</sup> .. 2<sup>255</sup>−1]  | 16842758 | **0x06 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 512 bit integers | Signed 512 bit integer, range [-2<sup>511</sup> .. 2<sup>511</sup>−1]  | 16842759 | **0x07 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 1024 bit integers | Signed 1024 bit integer, range [-2<sup>1023</sup> .. 2<sup>1023</sup>−1]  | 16842760 | **0x08 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 2048 bit integers | Signed 2048 bit integer, range [-2<sup>2047</sup> .. 2<sup>2047</sup>−1]   | 16842761 | **0x09 0x00 0x01 0x01 0x00 0x00 0x00 0x00**
| Array of signed 4096 bit integers | Signed 4096 bit integer, range [-2<sup>4095</sup> .. 2<sup>4095</sup>−1]   | 16842762 | **0x0A 0x00 0x01 0x01 0x00 0x00 0x00 0x00**

&nbsp;

### Floating point types

Most of these follow IEEE 754

#### Single variables

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

#### Arrays

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of 8 bit floating points | 8 bit floating point format | 33619969 | **0x01 0x00 0x01 0x02 0x00 0x00 0x00 0x00**
| Array of 16 bit floating points | 16 bit floating point format, binary16 from IEEE 754 | 33619970 | **0x02 0x00 0x01 0x02 0x00 0x00 0x00 0x00**
| Array of 32 bit floating points | 32 bit floating point format, binary32 from IEEE 754 | 33619971 | **0x03 0x00 0x01 0x02 0x00 0x00 0x00 0x00**
| Array of 64 bit floating points | 64 bit floating point format, binary64 from IEEE 754 | 33619972 | **0x04 0x00 0x01 0x02 0x00 0x00 0x00 0x00**
| Array of 128 bit floating points | 128 bit floating point format, binary128 from IEEE 754 | 33619973 | **0x05 0x00 0x01 0x02 0x00 0x00 0x00 0x00**
| Array of 256 bit floating points | 256 bit floating point format, binary256 from IEEE 754 | 33619974 | **0x06 0x00 0x01 0x02 0x00 0x00 0x00 0x00**
| Array of 512 bit floating points | 512 bit floating point format | 33619975 | **0x07 0x00 0x01 0x02 0x00 0x00 0x00 0x00**

&nbsp;

### Unsigned fixed point types

For Q notation see [Q (number format)](https://en.wikipedia.org/wiki/Q_(number_format))

#### Single variables

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

#### Arrays

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of unsigned 8 bit fixed points | Unsigned 8 bit fixed point format, UQ4.4 | 50397185 | **0x01 0x00 0x01 0x03 0x00 0x00 0x00 0x00**
| Array of unsigned 16 bit fixed points | Unsigned 16 bit fixed point format, UQ8.8 | 50397186 | **0x02 0x00 0x01 0x03 0x00 0x00 0x00 0x00**
| Array of unsigned 32 bit fixed points | Unsigned 32 bit fixed point format, UQ16.16 | 50397187 | **0x03 0x00 0x01 0x03 0x00 0x00 0x00 0x00**
| Array of unsigned 64 bit fixed points | Unsigned 64 bit fixed point format, UQ32.32 | 50397188 | **0x04 0x00 0x01 0x03 0x00 0x00 0x00 0x00**
| Array of unsigned 128 bit fixed points | Unsigned 128 bit fixed point format, UQ64.64 | 50397189 | **0x05 0x00 0x01 0x03 0x00 0x00 0x00 0x00**
| Array of unsigned 256 bit fixed points | Unsigned 256 bit fixed point format, UQ128.128 | 50397190 | **0x06 0x00 0x01 0x03 0x00 0x00 0x00 0x00**
| Array of unsigned 512 bit fixed points | Unsigned 512 bit fixed point format, UQ256.256 | 50397191 | **0x07 0x00 0x01 0x03 0x00 0x00 0x00 0x00**

&nbsp;

### Signed fixed point types

For Q notation see [Q (number format)](https://en.wikipedia.org/wiki/Q_(number_format))

#### Single variables

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

#### Arrays

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of signed 8 bit fixed points | Signed 8 bit fixed point format, Q3.4 | 67174401 | **0x01 0x00 0x01 0x04 0x00 0x00 0x00 0x00**
| Array of signed 16 bit fixed points | Signed 16 bit fixed point format, Q7.8 | 67174402 | **0x02 0x00 0x01 0x04 0x00 0x00 0x00 0x00**
| Array of signed 32 bit fixed points | Signed 32 bit fixed point format, Q15.16  | 67174403 | **0x03 0x00 0x01 0x04 0x00 0x00 0x00 0x00**
| Array of signed 64 bit fixed points | Signed 64 bit fixed point format, Q31.32 | 67174404 | **0x04 0x00 0x01 0x04 0x00 0x00 0x00 0x00**
| Array of signed 128 bit fixed points | Signed 128 bit fixed point format, Q63.64 | 67174405 | **0x05 0x00 0x01 0x04 0x00 0x00 0x00 0x00**
| Array of signed 256 bit fixed points | Signed 256 bit fixed point format, Q127.128 | 67174406 | **0x06 0x00 0x01 0x04 0x00 0x00 0x00 0x00**
| Array of signed 512 bit fixed points | Signed 512 bit fixed point format, Q255.256  | 67174407 | **0x07 0x00 0x01 0x04 0x00 0x00 0x00 0x00**

&nbsp;

### String types

Strings are basically stored as byte arrays. See [ASCII](https://en.wikipedia.org/wiki/ASCII), [UTF-8](https://en.wikipedia.org/wiki/UTF-8), [UTF-16](https://en.wikipedia.org/wiki/UTF-16) and [UTF-32](https://en.wikipedia.org/wiki/UTF-32) for definitions.

Only valid strings SHOULD be used, e.g. invalid surrogate pairs SHOULD NOT be stored in AUDALF.

#### Single variables

Single string variables are same as arrays of other types, so there is ALWAYS *unsigned 64 bit integer* that tells how many bytes of data will follow

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| ASCII string  | ASCII string | 83886081 | **0x01 0x00 0x00 0x05 0x00 0x00 0x00 0x00**
| UTF-8 Unicode string | UTF-8 Unicode string | 83886082 | **0x02 0x00 0x00 0x05 0x00 0x00 0x00 0x00**
| UTF-16 Unicode string | UTF-16 Unicode string | 83886083 | **0x03 0x00 0x00 0x05 0x00 0x00 0x00 0x00**
| UTF-32 Unicode string | UTF-32 Unicode string | 83886084 | **0x04 0x00 0x00 0x05 0x00 0x00 0x00 0x00**

&nbsp;

#### Arrays

Array of strings is made from multiple string variables. Section starts with *total count* that tells how many bytes all strings in array will take. After that there is chain of single string variables.

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of ASCII strings | ASCII string | 83951617 | **0x01 0x00 0x01 0x05 0x00 0x00 0x00 0x00**
| Array of UTF-8 Unicode strings | UTF-8 Unicode string | 83951618 | **0x02 0x00 0x01 0x05 0x00 0x00 0x00 0x00**
| Array of UTF-16 Unicode strings | UTF-16 Unicode string | 83951619 | **0x03 0x00 0x01 0x05 0x00 0x00 0x00 0x00**
| Array of UTF-32 Unicode strings | UTF-32 Unicode string | 83951620 | **0x04 0x00 0x01 0x05 0x00 0x00 0x00 0x00**

### Boolean types

#### Single variables

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Common boolean | It is either True (1) or False (0) | 100663297 | **0x01 0x00 0x00 0x06 0x00 0x00 0x00 0x00**

&nbsp;

#### Arrays

Notice that with boolean arrays the count is always bits. So if there are e.g. 15 booleans, you read 2 bytes and ignore one bit from it.

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of common booleans | It is either True (1) or False (0) | 100728833 | **0x01 0x00 0x01 0x06 0x00 0x00 0x00 0x00**

&nbsp;

### Date/time types

For Unix times (seconds and milliseconds), see [Unix time](https://en.wikipedia.org/wiki/Unix_time)  
For ISO 8601, see [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)

#### Single variables

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Unix time in seconds | Aka POSIX time and UNIX Epoch time in seconds, as 64 bit unsigned integer | 117440513 | **0x01 0x00 0x00 0x07 0x00 0x00 0x00 0x00**
| Unix time in milliseconds | Aka POSIX time and UNIX Epoch time in milliseconds, as 64 bit unsigned integer | 117440514 | **0x02 0x00 0x00 0x07 0x00 0x00 0x00 0x00**
| ISO 8601 | ISO 8601, as UTF-8 string | 117440515 | **0x03 0x00 0x00 0x07 0x00 0x00 0x00 0x00**

&nbsp;

#### Arrays

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of Unix time in seconds | Aka POSIX time and UNIX Epoch time in seconds, as 64 bit unsigned integer | 117506049 | **0x01 0x00 0x01 0x07 0x00 0x00 0x00 0x00**
| Array of Unix time in milliseconds | Aka POSIX time and UNIX Epoch time in milliseconds, as 64 bit unsigned integer | 117506050 | **0x02 0x00 0x01 0x07 0x00 0x00 0x00 0x00**
| Array of ISO 8601 | ISO 8601, as UTF-8 string | 117506051 | **0x03 0x00 0x01 0x07 0x00 0x00 0x00 0x00**

### Arbitrarily large signed integer

Large signed integer value that has no bounds (range limits). Also known as BigInteger or BigInt.

#### Single variables

There is ALWAYS *unsigned 64 bit integer* at start that tells how many bytes of data will follow. Then there are the bytes, which follow the [common BitInteger serialization format](https://docs.microsoft.com/en-us/dotnet/api/system.numerics.biginteger.tobytearray?view=netframework-4.8#System_Numerics_BigInteger_ToByteArray). e.g. 120 would be one byte 0x78, but 128 would be two bytes 0x80, 0x00

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Big integer, signed | Signed integer without range limits | 134217729 | **0x01 0x00 0x00 0x08 0x00 0x00 0x00 0x00**

#### Arrays

Array of arbitrarily large signed integers is made from multiple arbitrarily large signed integer variables. Section starts with *total count* that tells how many bytes all arbitrarily large signed integers in array will take. After that there is chain of single string variables.

| Type        | Description | ID as number | ID as bytes  |
| ------------- |:-------------:|:-------------:| -----:|
| Array of Big integers, signed | Array of Signed integers without range limits | 134283265 | **0x01 0x00 0x01 0x08 0x00 0x00 0x00 0x00**

&nbsp;

## Header section

Header section in AUDALF means FourCC + Specification version + byte size of whole data. Header section size is ALWAYS 16 bytes (128 bits).

### FourCC

[FourCC](https://en.wikipedia.org/wiki/FourCC) is ALWAYS '**AUDA**' as ASCII in bytes, so **0x41 0x55 0x44 0x41**

### Specification version

Defines what AUDALF features have been used. Check from [version history](VERSION_HISTORY.md) what features are added in different versions. First release has version number 1, so as bytes it is **0x01 0x00 0x00 0x00**. This can be assumed to be *unsigned 32 bit integer* and it can be read in one 8 byte get with FourCC (so get 8 bytes when reading start of the stream and decode FourCC and spefication version from those 8 bytes).

### Byte size of whole data

Defines how many bytes the whole AUDALF data has (this includes EVERYTHING, meaning that FourCC and Specification version are included). This is ALWAYS *unsigned 64 bit integer*. 

e.g. **0x00 0x04 0x00 0x00 0x00 0x00 0x00 0x00** would mean that AUDALF size is 1024 bytes.

The size DOES NOT mean that every byte has useful info. So you can padd the end of file if you want to do so.

&nbsp;

## Index section

Index section in AUDALF means Index count + Key type + entry definitions. Header section size is at least 16 bytes, most likely more.

### Index count
Defines how many index items there are. This is ALWAYS *unsigned 64 bit integer*. If value is 0, then there aren't any data in [key and value pair](#Key-and-value-pairs) section.

e.g. **0x04 0x00 0x00 0x00 0x00 0x00 0x00 0x00** would mean that there are 4 items

### Key type

Defines what is the type for dictionary keys. Or defines that this is a list where key is the index number of the list. This is ALWAYS *unsigned 64 bit integer*. 

0 means that structure is a list, and key entries are list index values (as 64 bit unsigned integers). 

Other options are defined in [types](#Types) section.

e.g. **0x07 0x00 0x00 0x00 0x00 0x00 0x00 0x00** would mean that every dictionary key is 64 bit unsigned integer

### Entry definitions

There is 64 bit unsigned integer for every index item, so total is **Index count** * 8 bytes of entry points. Entry point is byte address location of [key and value pair](#Key-and-value-pairs) inside AUDALF payload.

e.g. **0x68 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0xC8 0x00 0x00 0x00 0x00 0x00 0x00 0x00** would mean that first entry is at byte address 104 (0x68) and second entry is at byte address 200 (0xC8)

&nbsp;

## Key and value pairs

Order of **Key + value pairs** is not required. So you can reorder items when you serialize data e.g. to get better compression.

### Key

As Key type is defined in [Index section](#Index-section), you just read right amount of bytes (based on type), and that is the value. You might have to read variable amount of total bytes since arrays, strings etc. can be keys.

Every key entry SHOULD be unique. In case of duplicate keys, the implementation can choose freely what to do.

If key type is 0 that means structure is a list, and key entries are zero based index values of that list (as 64 bit unsigned integers). You SHOULD store list entries in ascending order, but that is not required.

e.g. if type is Unsigned 32 bit integer, you read 4 bytes and use those as Unsigned 32 bit integer.

### Value type ID

This is ALWAYS *unsigned 64 bit integer*. Options are defined in types section. If this is 0 (special type) then it means that value is NULL and next 8 bytes (64 bits) is another type ID that defines the format.


### Actual value bytes

Value length amount of bytes that can be used as value for dictionary entry. Since value type ID can be NULL, these bytes might not exist at all.
