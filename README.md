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

# AUDALF (Almost Universal Dictionary And List Format)

AUDALF is binary format specification for (de)serializing dictionaries and lists.

## Why?

Because I needed something like this for my personal project

## Key features

* By default everything is assumed to be 64 bit (8 bytes) little endian
* Every index, structure, element etc. is aligned for 64 bit access
* Most common types for data are predefined (booleans, int64s, strings, byte arrays etc.)
* You can define your own types if needed 

## Implementations 

C# implementation can be found from [here](https://github.com/mcraiha/CSharp-AUDALF)

## What are the negative traits?

There are usually lots of 0x00 bytes because of alignments and making things future proof. So storage space wise this isn't optimal format. Also 64 bit little endian CPU assumption makes things a bit hard for other type of CPUs.

Also dictionaries must have same key type (value types can be different between pairs) and NULL keys are not allowed.

## License

Specifications are licensed under [Unlicense](LICENSE), so you might use these specs as you want.

## Version history

0.1 First working draft

## Sample file

