# OverTheWire: Bandit Writeup

## Level 0

Going through the *Helpful Reading Material* given on the OTW website is more than enough to understand how SSH works and work out the command to remotely connect to and access the game from our local terminal.

- Address given: **bandit.labs.overthewire.org**
- port: **2220**
- username: **bandit0**
- password: **bandit0**

The command required is:

`ssh bandit0@bandit.labs.overthewire.org -p 2220`

followed by entering the password `bandit0` when prompted.  

## Level 0 -> Level 1

1. In the home directory using command `ls` (to list the contents), we find a single file titled '**readme**'.   
2. Using `file readme` (to get the file type) shows that it is ASCII text.
3. Using `du readme` (to get the file space usage), shows that it takes up an estimated storage space of 4.   
4. Finally command `cat readme` (to output the contained text), we receive the password **ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If** for accessing the next level.   

## Level 1 -> Level 2

1. Using `ls` we find a file titled '**-**'.  
However this time running any of the other commands to read the file don't work directly as using the '-' character as an argument refers to *STDIN/STDOUT*.  
So, to run those commands we need to specify the full location of the file, which would here be **./-**.  
2. Using `file ./-` shows us it is ASCII text.
3. `cat ./-` gives the password **263JGJPfgU6LtdEvgfWU1XP5yac29mFx** for the next level.  

Alternatively, we can also use commands `cat < -` (causes it to check for the content within '-'), or `more -`.  

## Level 2 -> Level 3

1. Listing the home directory's contents using `ls` shows us a file '**spaces in this filename**'.   
Trying all of the other commands don't work for the file as the terminal considers the file's name as multiple arguments rather than just one.  
To get past this we can either enclose the file's name within quotes (**'spaces in this filename'** or **"spaces in this filename"**) or use the backslash key to escape all the space characters (**spaces\ in\ this\ filename**).  
2. Entering `file spaces\ in\ this\ filename` we find out it is ASCII text.
3. `cat spaces\ in\ this\ filename` gives us the password **MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx**.  

## Level 3 -> Level 4

1. `ls` shows us that the home directory contains a directory '**inhere**'.  
2. We navigate into it using `cd inhere`, but using `ls` within that directory doesn't show us anything- the file we need is a hidden file.  
To see all the files, even those starting with '.' (i.e. hidden files), we must use the argument '**-a**' or '**--all**' (which according to the manual `man ls` instructs not to ignore entries starting with '.').  
3. So, `ls -a` shows us a file '**...Hiding-From-You**'.
4. We find out its ASCII text using `file ...Hiding-From-you`.
5. Output the file using `cat ...Hiding-From-You` to get the password **2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ**.  

Viewing hidden files can also be achieved using the arguments '**-A**' or '**--almost-all**' (which will just not list '.' and '..', the current and parent directories respectively).  

## Level 4 -> Level 5

1. `ls` shows us that the home directory contains a directory '**inhere**'.
2. We navigate into it using `cd inhere`.
3. Check the contents using `ls`, and find 10 files titled '**-file00**', '**-file01**', '**-file02**', and so on till '**-file09**'.  
4. Checking the filetype of all the files using `file ./-*` shows that all of them are simply data (which also then give us strings of random unreadable characters when read using `cat`) except for '**-file07**', which is ASCII text.
5. On reading the file using `cat ./-file07` we get the password **4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw**.  

If the terminal gets messed up at any point, we can use `reset` to clean it up.  
[//]: # (Or use `find -type f | xargs file | grep text`)   

## Level 5 -> Level 6

1. `ls` shows us the directory '**inhere**', which we navigate into using `cd inhere`.  
2. Using `file ./*` shows 20 sub-directories.
3. `ls -lR` (lists in long format (-l) and recursively through all sub-directories (-R) ) now gives us a list of all of the files contained, but its still not easy to locate the one we need.  
4. Using `find -type f ! -executable -size 1033c` (i.e. a file that is not executable and exactly 1033 bytes in size) gives us the file **"./maybehere07/.file2"**, which is the one we need.  
5. Finding its contents using `cat maybehere07/.file2`, gives us the password **HWasnPhtq9AVKe0dmk45nxy20cvUa6EG**.  

Alternatively for listing we could've also used `ls -lAh`.  

## Level 6 -> Level 7

1. `ls` this time isn't of any use as the file could be anywhere on the server rather than just the home directory.  
2. To locate it using the info given, we can use the command `find /. -type f -group bandit6 -user bandit7 -size 33c`.  
However, this gives a large list of inaccessible files that are tedious to parse through to find the one required.  
3. We know that the one we are looking for must be accessible to us, so we redirect all the inaccessible files causing errors (*STDERR* (2)) to wherever the standard output (*STDOUT* (1)) is being directed, and not display wherever we're getting "Permission denied" using the command `find /. -type f -group bandit6 -user bandit7 -size 33c 2>&1 | grep -v "Permission denied"`.  
This gives us the file **/./var/lib/dpkg/info/bandit7.password**.  
4. Gettings its contents using `cat /./var/lib/dpkg/info/bandit7.password` gives us the password **morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj**.  


## Level 7 -> Level 8

1. `ls` shows **data.txt**.  
2. But simply using `cat data.txt` won't be useful as it gives a huge amount of data that we can't manually search through.  
So we first sort the content using `sort data.txt` (in alphabetical order).
3. Then we search for the line containing "millionth" using `grep "millionth" data.txt`. We can also perform both commands together using `sort data.txt | grep "millionth"`. (Or just use 'grep', sorting isn't necessary here).  
4. Next to the word "millionth" we get the password **dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc**.  

## Level 8 -> Level 9

1. `ls` shows **data.txt**.  
2. But `cat data.txt` isn't feasible as it gives all the data and we only require a single line of text (the one that occurs just once).  
We can find it using `uniq -u data.txt` but it doesn't work directly as 'uniq' only detects repeated lines if they're adjacent. We must sort the data first, we use the command `sort data.txt | uniq -u`.   
3. We get the password **4CKMh1JI91bUIZZPXDqGanal4xvAg0JM**.   

## Level 9 -> Level 10

1. `ls` shows **data.txt**.  
2. Checking the content using `cat data.txt` gives a large number of unreadable characters, out of which we need to find the human-readable ones.   
3. `strings data.txt` lists all the human-readable strings. 
4. Modifying it to `strings data.txt | grep -E '==+'` will narrow the list down further to just those strings preceded by several '=' characters. 
5. From the strings left we end up getting the password **FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey**.  

## Level 10 -> Level 11

1. Using `ls` to find **data.txt** and `cat data.txt` we get the base64 encoded data contained within the file.  
2. We can decode the contents using `base64 -d data.txt` or `base64 --decode data.txt`.  
3. On decoding we get: The password is **dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr**.    

## Level 11 -> Level 12

1. Using `ls` to find **data.txt** and `cat data.txt` we get the file's contents which have been encoded using the Rot13 cipher.  
2. To decode, we use the 'tr' command to shift the letters back to their original position; the command is `cat data.txt | tr '[a-z][A-Z]' '[n-za-m][N-ZA-M]'`.  
The 'tr' part can also be written as `tr 'a-zA-Z' 'n-za-mN-ZA-M'` or  `tr [A-Za-z] [N-ZA-Mn-za-m]`.
3. On decoding we get: The password is **7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4**.   

## Level 12 -> Level 13

1. `ls` shows **data.txt**.
2. We create a temporary directory under /tmp using `mktemp -d` (something like **/tmp/tmp.Q80omD3Kcx**), which we then copy the file into using `cp data.txt /tmp/tmp.Q80omD3Kcx` and navigate to using `cd ../../tmp/tmp.Q80omD3Kcx`.  
/tmp/tmp.f3VzEnD1Hg  
3. We rename the file using `mv data.txt file.txt` and can check the contents with `cat file1.txt`.  
4. As we know the file currently consists of a hexdump of some other file, we decipher and get the original data in another file using `xxd -r file1.txt > file2`.  
5. Checking the filetype of the new file using `file file2` gives us this:  

*file2: gzip compressed data, was "data2.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 574*  

6. As we know the file was compressed into a gzip file, we can reverse the compression using either of the following commands,  
    - `mv file2 file3.gz` followed by either `gzip -d file3.gz` or `gunzip file3.gz`  
    - `zcat -d file2 > file3`

7. Now, `file file3` gives us:  

*file3: bzip2 compressed data, block size = 900k*  

8. To decompress this we use `bzip2 -d file3`, which changes it to **file3.out**.  
10. Checking the new file's type with `file file3.out` shows:  

*file3.out: gzip compressed data, was "data4.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 20480*  

11. `zcat -d file3.out > file4` decompresses and move the data to another file, and checking its type with `file file4` gives:  

*file4: POSIX tar archive (GNU)*  

12. To decompress the tar archive we must use the 'tar' command as `tar -xvf file4` (extracts file from archive (-x), lists the files being extracted (-v, 'verbose mode')). This extracts **data5.bin**, and `file data5.bin` gives:  

*data5.bin: POSIX tar archive (GNU)*  

13. Using `tar -xvf data5.bin` extracts the decompressed content to **data6.bin**, which on checking filetype `file data6.bin` shows:  

*data6.bin: bzip2 compressed data, block size = 900k*  

14. `bzip2 -d data6.bin` modifies the file to **data6.bin.out** containing the decompressed data, which we check `file data6.bin.out` giving us:  

*data6.bin.out: POSIX tar archive (GNU)*  

15. `tar -xvf data6.bin.out` extracts the uncompressed data to **data8.bin**, and `file data8.bin` gives:  

*data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Sep 19 07:08:15 2024, max compression, from Unix, original size modulo 2^32 49*   

16. To decompress the gzip file we use the command `zcat -d data8.bin > file5`, and checking the new file's filetype `file file5`, we get:  

*file5: ASCII text*  


17. On reading this file using `cat file5`, we finally get: The password is **FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn**.  

## Level 13 -> Level 14

1. Using `ls` shows a file **sshkey.private** (which we can see is the (RSA) private key file we need from the extension).  
We can also use `ls -la`, which shows that it is accessible by the users *bandit13* and *bandit14*.
3. To get the key itself, we can use `cat sshkey.private`, which gives us:  
```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```
4. After this, we close the connection to the bandir server (using `exit`).
5. To copy the private key file onto our own local system, we use the `scp` command (which stands for 'Secure Copy'), as `scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .`  
(where `-P` specifices the port, `bandit13` the user, `bandit.labs.overthewire.org` the source host, `sskhey.private` the path of the file required, and `.` the location to which we're copying in our local system (here, the current location)).  

Even though what was asked in the level has been achieved, here is how we can use the key for logging in:
- For using a private key with ssh, we use the `-i` option. So the command should be `ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`. However, it doesn't work and we get this instead:
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for 'sshkey.private' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "sshkey.private": bad permissions
```
- To get past this, we can use one of two methods:  
    1. Run the command with `sudo` (which gives root/superuser priveleges) as `sudo ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220` (which would prompt the user to enter the password set before connecting).
    2. Copy the private key file to the *.ssh* directory (which gets created on the first use of `ssh`) using `cp sshkey.private ~/.ssh/sshkey.private`. Then change the permissions of the file so that only the owner of the file (and no other user) can read and write into it using `sudo chmod 600 ~/.ssh/sshkey.private`.  
    After this run the `ssh` command with `-i` (and the path of the updated file) as `ssh -i ~/.ssh/sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`.