# OverThewire Bandit - levels 5-8

** objective:** same as before ssh into a linux filesystem and progress 
through the levels.

**Enviornment:** SSH into each level of the Bandit game server; each level's
password unlocks the next account/level

## what I did
-**Level 5-6** Used the find command to find the tile with attributes given
 using command find inhere -type f -size 1033c ! -executable, then cat it.

-**Level 6-7** find / -user bandit7 -group bandit6 -size 33c.

-**Level 7-8** grep millonth data.txt

-**Level 8-9** sort data.txt | uniq -u



## what I learned
Takeaway I got was how to further get info and help with a command other than -help I can use
command man  "manual" to display more information on the help command in this case man find. 
Which advised of how to use the command to use option -user and option -group to narrow down
the search locations, then add what i learned previously using option -type f for file and -size
to find the exact file with file size provided. Can use grep to show output of a file or command
in this case was used to output contents of a file after the word millonth. Found that uniq can be
combined with the command sort with use of a pipe "|" find duplicate entries or unique entires of a text file.
Also learned that the | command outputs the results of one command to be the input of the next in command chain. 
