# Advanced Meeting

- In general, for writeups you want to provide a summary of the challenge from a high-level upfront, but also go low level to make a purposeful writeup.

- Remember to screenshot flags!

**Eavesdrop PicoCTF**

- Analyze network traffic on port 9002. (Follow TCP stream in wireshark)
- Gives a command with the secretkey to decrypt it.
- Downloading the file found on port 9002 and running the command provided decrypts and gives me file.txt.

***Bbbbloat**

- Binary generally is the hardest category of CTFs.

- Reverse engineering a binary - first download the file, and run `file` on it to know more about the file.

- From this, we can tell it is a ELF 64 bit binary.

- To do static [analysis] reverse engineering we will use Ghidra, and import the binary file.

- Ghidra will try to decompile the binary, and produce pseudocode that is close to the actual [C] code.

- After running the pseudocode, we will be asked for a favorite number.

- Looking at the ghidra output, we can see that local_48 is likely the scanf input that we gave it. 
  - Proceeds to compare local_48 with 0x86187.
  - Right click, and change that hex to decimal, and you will get something like 529687.
