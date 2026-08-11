# OverThewire Bandit - Levels 9-12

** objective:** same as before ssh into a linux filesystem and progress
through the levels.

**Enviornment:** SSH into each level of the Bandit game server; each level's
password unlocks the next account/level

## What I did
-**level 9-10** First I used man sort to refresh with sort and same with strings,
where i learned string prints printable characters 4 characters or longer. Used 
Strings command to find 4 printable charecters in a row, Used a pipe to output results to grep which was advised to show what is adjacent to "==" so the command 
that was used to find the password was strings data.txt | grep "==="

-**level 10-11** First thing I did was used the man command for base64 by using man base64 , determined need to use the
-d flag to decode since we need to find the alphanumeric characters in the password. Noticed the -i flag when decoding, ignore non-alphabetic characters
 so I tried base64 -d -i data.txt and got password as the result

**level 11-12** Used info provided by wikipedia to have the output of the cat command output
piped to tr to decode the cesear cypher using cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

## what I learned
Learned how to decode base64 files by using the -d option to decode and i also used -i to ignore all
junk as it states in the manual file, to ignore non printable characters.  Learned that strings prints printable 
 characters 4 characters or longer in a row or string, so used strings to find section of file with multiple "=" , so output strings command to grep using pipe |grep "==" to narrow down results with multiple "=" and it found the section of the data.txt file that contained the password.   Used info provided by wikipedia to have the output of the cat command output
piped to tr to decode the cesear cypher using cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
