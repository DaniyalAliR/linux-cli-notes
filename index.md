---
title: Linux Command Cheatsheet
layout: default
---


# Organized Commands

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## General Concepts and Basic Commands

COMMAND

this is called         | and to see in cli
EXIT CODES:            | $?

0 = stdin   (

1 = stdout  (

2 = stderr  (

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

TYPE OF FILE :

The file type is one of the following characters:

     ‘-’
          regular file
     ‘b’
          block special file
     ‘c’
          character special file
     ‘C’
          high performance (“contiguous data”) file
     ‘d’
          directory
     ‘D’
          door (Solaris)
     ‘l’
          symbolic link
     ‘M’
          off-line (“migrated”) file (Cray DMF)
     ‘n’
          network special file (HP-UX)
     ‘p’
          FIFO (named pipe)
     ‘P’
          port (Solaris)
     ‘s’
          socket
     ‘?’
          some other file type

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## command is to check if the command is built-in or external.
type

## work as logical AND
&&

## work as logical OR
||

## can represent a value; to assign a value use = like ( like=good ) [now u say echo $like ( the result should be like this ( good ) ]
$

## show all variables that you can use with $ this
set

## u can use this to remove variables that you set using =
unset

source ~/.bashrc

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

VARIABLES CONCEPT:

to make a variable just do ( hello=dani ) now u can see this as
echo $hello ( the result should be dani if u dont use $ then it will prite hello )

## for math funtion for that i neet to use a command { expr } that i can do 5 + 5 it will show me the result in the next line
## so main this sgin is for plus is + and for minuse - and for multipition is \* { this is because u need to escape the special character }
expr

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

RULES

## for any arithmetic operations u need to add $(( )) this
## and for variable just like this hello=5 now the variable is ( 5 )
$(( ))

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## File and Directory Management

## to comment out the line in vim
vim ( :'<,'>s/^/# / )

Select the Lines of the Paragraph

Press Shift + V to start Visual Line Mode.
Arrow keys (↑ / ↓) ka use karke paragraph ki saari lines select karein.
Add # to All Selected Lines

When the lines are selected, type:
vbnet

Copy

Edit
:'<,'>s/^/# /
Press Enter.
AND#lag

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## for last few line of code - follows the file as it grows
TAIL -F

## for looking into the file content
CAT

## file editor [ press 'i' for insert mode to edit the file / press ESC for normal mode, then type ':wq!' + enter to save and exit ]
VIM

## if you get in the ( vim) this is the code to exit without saving ( :q!+enter )
:Q!

## if u type pwd and put ' for exit use this - Note: This might be related to specific terminal settings or visual modes, not a standard exit for `pwd` output.
ctrl+v

## standard interrupt signal to stop a running command
ctrl+c

## creating empty files and updating the timestamps of existing files
TOUCH

## tells you the file type and information like page size, etc.
file

## to make a new directory
MKDIR

## is use for create multiple directories including parent directories if they don't exist. Example: ( mkdir -p hellp/hello2/hello3 )
mkdir -p

Same for rmdir to delete multiple directories.

## can list anything from anywhere
ls / --

## ~ represents the home directory
OR ~ isko list karne ke liyee (ls ~)

## this tells you about the file
file

TAR ( struture ) tar [options] [archive-file] [file or directory to be archived]
## difference between tar file compressions [ The gz format provides the best speed but a "regular" compression ratio.
## The bz2 format provides a mid-term between speed and compression, while xz
## is excellent when talking about compression but a little slower.
tar -czvf mysite-backup-030425.tar.gz /path/to/directory
tar -xzvf backup.tar.gz
tar -xzvf mysite-backup-030425.tar.gz
## Create (-c). Create a new archive.
## Extract (-x). Extract files from an archive.
## Verbose (-v). Show the detailed output of the process.
## File (-f). Specify the archive file.
## Compress with gzip (-z). The archive will be compressed using gzip, resulting in a .tar.gz file.
## Compress with bzip2 (-j). Compress the archive using bzip2, resulting in a .tar.bz2 file.
## Compress with xz (-J). Compress the archive using xz, resulting in a .tar.xz file.
tar -cfz application.mysql.tar.gz /mnt/user_data/home/master/applications/wp-addmin/public_html/

## TO CREATE A TAR FOR ALL FILE
tar -czvf archive_name.tar.gz *

## in linux every thing is a file, the directory is a special file and it is also case sensitive. you can navigate through directories using ( cd ) or this file structure.
file :

## Renames all files in the current directory to hello1, hello2, etc.
i=1; for file in *; do mv "$file" "hello$i"; ((i++)); done

## Find files named log* in /home/daniyal/ and empty them
find /home/daniyal/ -name "log*" -exec truncate -s0 {} \;

## Find files named log* in /home/daniyal/ and empty them - more efficient for multiple files
find /home/daniyal/ -name "log*" -exec truncate -s0 {} +

## Find files named log* in /home/daniyal/ accessed more than 1 day ago and empty them
find /home/daniyal/ -name "log*" -atime +1 -exec truncate -s0 {} +

## for testing command u will create new file but to test this file u will change file time by this command [ touch -d "2 days ago" " file name " ]

## Displays a directory tree with hidden files (-a), directories only (-d), colorized output (-C), and a maximum depth of 1 level (-L 1) starting from the root directory (/)).
tree -aCd -L 1 /

## this is use to make a link between files
ln

## for soft link use -s option and for hard link just use ln
## [ soft link = Symbolic Links ] ( ln -s ) use to make a shortcut of a file. with this link you can edit the original file, and if you delete the soft link it does not affect the original file. 
     the original file and this link have different inode numbers. if the original file is deleted then the soft link will also be deleted or will not be accessible.
## [ Hard link ] ( ln ) use as a duplicate but both are connected and can be edited. if the original file is deleted, it will not affect the hard link because it is a hard link and the inode number is the same.

## for transfer the file without the copy like tar
## [ if u put ( / ) this in the end of the source the the files will be in the directory if not this the folder be there not the file in the directory
rsync -avz -e "ssh -p 2222" --progress --debug=all source/files/ username@remote_ip:/destination/files


rsync -avz -e "ssh -p 2222" --progress --debug=all /root/hello/'not me' daniyal001@24.144.93.237:/mnt/user_data/home/master/applications



## Example of using rsync for file transfer between remote servers via SSH
rsync -avzh --dry-run --progress -e 'ssh -p 2222' siddiqui@3.111.15.150:/mnt/user_data/home/master/applications/conversions/public_html/ siddiqui@142.93.216.187:/mnt/user_data/home/master/applications/conversions/public_html/

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

HARD LINK AND SOFT LINK AND LINK COUNT

COMMAND
{ ln passwd itsme
ls -ali passwd
## Find files with a specific inode number
sudo find / -inum 3671931

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Network Commands

## this command is for network Bandwidth

vnstat 

## to check url if it broken or get stutus
## -I shows header, -L follows redirects
curl -I -L [url]

## finds the IP address for a domain name
nslookup [url]

## for copy file to an other server or dives
## Secure Copy Protocol
scp

## FOR S-COPE USE THIS
scp my_backup.tar.gz user@192.168.1.10:/home/user/backups/

## command to download a file from the web
wget https://wordpress-45523016683.devrimsdemo.com/new-one.tar.gz

## Shows IP addresses and network interfaces
ip a : to fils

## A complex pipeline to extract IP addresses - may need adjustment based on `ip a` output format
ip a |cut -d' ' -f6 |sort -k6 | tr '\n' ' ' | cut -d ' ' -f10 | tr "/ *" ' ' |cut -d ' ' -f1

## NR is for row count from up to down and print is for 2 feild or colunm and sed for replacing

## Extracts the IP address from the 9th line of `ip a` output
ip a |awk 'NR==9{ print $2 }' | sed "s'/' ' " | cut -d ' ' -f1

## Finds the line with 'link/ether', gets the next line, extracts the 2nd field, and removes '/'. Likely intended to get MAC address or IP in a different format.
ip a |grep -A1 link/ether | awk 'NR==2{ print $2 }' |cut -d '/' -f1

## Gets geographical and network information for your public IP
curl ipinfo.io

## Finds lines containing 'port' (case-insensitive) in the sshd configuration file
grep -i port /etc/ssh/sshd_config

## Finds lines with 'GatewayPorts no' and comments them out by adding '#' at the beginning of the line
grep -i port /etc/ssh/sshd_config |sed 's/GatewayPorts no/#GatewayPorts no/'

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## SSL/Certificate Commands

## to check the ssl certificate using local cli command
openssl s_client -connect woocommerce-47155189803.devrimsdemo.com:443

## and u can get more detali by use this

## download this script to run the command
wget https://raw.githubusercontent.com/bobbyiliev/bash-ssl-checker-tool/master/ssl

## Then to run the script make it executable:
chmod +x ssl

## now run this command ( and put your site )
./ssl your site.com
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## WordPress Commands

## for creating a new WordPress user with a specified role and password
wp user create <username> <email> --role=<role> --user_pass=<password>

## for changing the password of an existing WordPress user
wp user update <username> --user_pass=<new_password>

## Gets the WordPress site URL from the database
wp option get siteurl

wp option get siteurl

wp cache flush

## get Wordpress Website URL
wp option get siteurl

TO CHANGE DEFAULT ADMIN CREDENTIALS

FIRST DOWNLOAD WPS HIDE LOGIN PLUGIN
## Sets the custom login URL for the WPS Hide Login plugin
wp option update whl_page "my-custom-login"

Set the Redirection URL (Optional)
## Sets the redirection URL for the WPS Hide Login plugin
wp option update whl_redirect "https://example.com/404"

CACHE FLUSH
## Clears the WordPress cache
wp cache flush

## command to retrieve the custom admin login URL if it has been changed by the WPS Hide Login plugin
wp option get whl_page




------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Database Commands

FOR INSTALLING PHPMYADMIN

## Downloads, unzips, renames, and cleans up the phpMyAdmin installation files
wget https://files.phpmyadmin.net/phpMyAdmin/5.2.0/phpMyAdmin-5.2.0-all-languages.zip && unzip phpMyAdmin-5.2.0-all-languages.zip && mv phpMyAdmin-5.2.0-all-languages phpmyadmin && rm -r phpMyAdmin-5.2.0-all-languages.zip
wget https://files.phpmyadmin.net/phpMyAdmin/5.2.0/phpMyAdmin-5.2.0-all-languages.zip && unzip phpMyAdmin-5.2.0-all-languages.zip && mv phpMyAdmin-5.2.0-all-languages phpMyAdmin && rm -r phpMyAdmin-5.2.0-all-languages.zip
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Backs up a MySQL database to a .sql file
mysqldump -u username -p dbname > db.sql

## Restores a MySQL database from a .sql file
mysql -u username -p dbname < db.sql

Configure the Database Server for Remote Connections:

Edit the MariaDB/MySQL configuration file (e.g., /etc/mysql/mariadb.conf.d/50-server.cnf or /etc/mysql/my.cnf).
Locate the line:
ini
Copy code
bind-address = 127.0.0.1
Change it to:
ini
Copy code
bind-address = 0.0.0.0
Restart the database server:
bash
Copy code
## Restarts the MariaDB/MySQL service after changing the bind-address
systemctl restart mariadb

## Command to create a new database user
CREATE USER 'user'@'%' IDENTIFIED BY 'password';
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Permission Management

this command is use for change the permition of a single group or a user.. -
## this is for looking about permissions in a detailed list using Access Control Lists
getfacl

## this command is use for changing permissions using Access Control Lists
setfacl

FOR ADDING PERMISSION FOR USER -
## command to add read, write, and execute permissions for a specific user to a target file
setfacl -m u:user:rwx <target_file> -

FOR ADDING PERMISSION FOR GROUP -
## command to add read, write, and execute permissions for a specific group to a target file
setfacl -m g:group:rwx <target_file> -

TO REMOVE A SPECIFIC ENTRY -
## command to remove a specific ACL entry for a user or group from a target file
setfacl -x u:user:rwx <target_file> -

TO REMOVE ALL ENTRIES                                                     -
## command to remove all ACL entries from a file or directory
setfacl -b -

FOR ADDING PERMISSION FOR USER IN ALL THE FILES INSIDE A FOLDER -
## command to recursively add ACL entries for a user or group to files and folders within a target directory
setfacl -Rm "entry" <target_file/folder> -
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Text Processing and Filtering

grep -rl >word to find<


FIND COMMAND :

## Finds files containing 'h' in /var, ignores errors, and highlights 'h' in the output
find /var -type f -name "*h*" 2>/dev null | GREP_COLORS='ms=05;34' grep --color=always "h"

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## for checking Abusive Ips in logs - extracts IPs, sorts, counts unique IPs, sorts by count, shows the last few (most frequent) IPs
awk '{print $1}' */logs/lsws_access_logs | sort -n | uniq -c | sort -h | tail
this command is use for ckeck the logs

## Filters log file for a specific IP and shows the last lines
cat lsws_access_logs | grep '20.57.56.244' | tail

## Filters LSWS access logs for a specific IP and shows the last 20 lines
cat */logs/lsws_access_logs | grep 196.251.80.244 | tail -n20

## Filters LSWS access logs for a specific IP and follows the output in real-time
tail -f */logs/lsws_access_logs | grep 65.0.89.109

## Filters LSWS access logs for a specific IP and shows the last 20 lines
cat */logs/lsws_access_logs | grep 13.94.89.2 | tail -n20

tail -f */logs/lsws_access_logs | grep -vE "404|403"

awk '$9 != 404 {count[$1]++} 
     END {for (ip in count) print count[ip], ip}' */logs/lsws_access_logs \
| sort -nr \
| head -10 \
| while read hits ip; do
    grep "^$ip " */logs/lsws_access_logs \
    | awk '$9 != 404 {print $7, $9, $NF}' \
    | sort | uniq -c | sort -nr | head -1 \
    | awk -v ip="$ip" -v hits="$hits" '{print hits, ip, $3, $2, $1, $4}'
done


//log command 
tail -f */logs/lsws_access_logs | awk '{
    code=$9;
    red="\033[1;31m"; green="\033[1;32m"; yellow="\033[1;33m"; reset="\033[0m";
    color=(code ~ /^[23]/) ? green : (code ~ /^4/) ? yellow : red;
    $9=color code reset;
    print;
    fflush();
    system("sleep 0.5");
}'
//i use this command to see log and like status code hits are in color 

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## u can use command like ( grep | sort | uniq | wc | wc -l ) to make an output that u want by filtering out from these

## Opens the nano text editor
NANO(

## in nano, this works as search
## to open search ( / ) and to exit search ( Esc, then \ )
/

## replace the text with other text
## Stream Editor
sed

## flags like [ grep --color ( any word u want to find ) or [ wc -l ( to find out how many line in the file ) ] [ and if u want to see line number then use ( -n ) flag ]
cat

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

FILTERS
19.3. ## Filters lines matching a pattern
grep ( ye koi bhi text ko extract karne ke liyee use hota hai koi bhi cheez greb out ) [ and use --help for flag ]

19.4. ## Removes sections from each line of files
CUT ( cut filter can select columns from files ) [ and use --help for flag ]

19.5. ## Translates or deletes characters
TR { tr '\n' ' ' ( new lines ko space se replace karta hai ) }( translate or delete characters ) [ and use --help for flag ]
## this well encrypt or decrypt text using ROT13 format
[ tr 'a-z' 'n-za-m' ]

19.6. ## Prints newline, word, and byte counts for each file
WC { can count words, line bites } [ and use --help for flag ]

19.7. ## Sorts lines of text files
SORT { file ko sort kar ke istamal ma atee hai } { [ by default ye alphabetical order ma sort karta hai ] }
## specify the column you want to sort the file by
{ -k }

19.8. UNIQ
## Reports or omits repeated lines
{ for removing duplicates for files and more } [ and use --help for flag ]
## prefix lines by the number of occurrences
{ -c }

19.9. COMM
## Compares two sorted files line by line
{ compare two sorted files line by line }
{ Options aur Examples:
Options ke zariye aap kuch columns hide kar sakte hain:

-1 – Pehli file ka unique content hide karta hai.
-2 – Doosri file ka unique content hide karta hai.
-3 – Common content hide karta hai.
[ one example ( -12 ka matlab hai:
Column 1 aur 2 hide karo (sirf common lines dikhao). ) ] }

diff
## to check the different
{ to check the different }
## Compares files line by line

AWK
## a powerful text processing tool
{ awk is for selecting certain thing from the file or any command like
## by using ( -F ) you specify the field separator, by default it is space
[ by using ( -F ) what u want as a field seprated by defulte is ( is space ) ]}

FOLD
## for text wrap
{ for text wrap }
## Wraps each input line to a specified width

SEQ
## seq - print a sequence of numbers
{ seq - print a sequence of numbers }
## Prints numbers from first to last, in steps of increment

## This command is for dictionary check that there is some word wrong in your file
## Converts text to lowercase, puts each word on a new line, sorts, removes duplicates, and finds lines unique to the first file (your text) compared to a sorted dictionary file
{ cat text | tr 'A-Z ' 'a-z\n' | sort | uniq | comm -23 - sorted_dict }
and there is bildin dictionary in linux in { /usr/share/dict/dict/words } in this file

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## System and Package Management

## for reinstalling basic commands
## can run anywhere but root is best
SUDO APT-GET INSTALL --REINSTALL COREUTILS

## going to normal to root
su root

## and to normal
ctrl + D

APT COMMAND

## updates the list of available packages when you newly install a linux or regularly
apt-get update

## for installing a new package
apt install >package name<

## for removing an installed package, but not its dependencies
apt remove >package name<

## removes extra packages that were installed as dependencies and are no longer needed
apt autoremove

## checks the status of a systemd service
systemctl status service_name

the line for basic package

## Installs a list of common and useful packages
sudo apt install build-essential curl wget net-tools git unzip zip htop software-properties-common nano vim openssh-server traceroute inetutils-ping baobab gparted python3 python3-pip nodejs npm tmux ufw libreoffice -y

## Reinstalls the openssh client package
sudo apt-get install --reinstall openssh-client

##If you've already installed it with GUI, you can remove the desktop environment:
## Removes packages related to the GNOME desktop environment and automatically removes dependencies that are no longer needed
sudo apt-get remove --purge gnome* && sudo apt-get autoremove

STOP THE GRAPHICAL DESKTOP IN VARIOUS WAYS

## Stops the GNOME Display Manager or switches to runlevel 3, which is typically multi-user command line
$ sudo systemctl stop gdm (or sudo telinit 3)

and restart it (after logging into the console) with:

## Starts the GNOME Display Manager or switches to runlevel 5, which is typically multi-user graphical
$ sudo systemctl start gdm (or sudo telinit 5)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Dangerous Commands

## to remove all the file and the directory at onces
## Dangerous: Attempts to remove parent directory content and hidden files - use with extreme caution!
rm -rf -- ..? .[!.] *

## this is use for (DoS) attack and also know as fork bomb
## Dangerous: Creates processes rapidly, potentially crashing the system. To kill it, find the process ID (PID) and use `kill -9 <PID>`
:(){ :|: & };: to kill this command > kill -9 <PID> <

## for deleting all the file and directory at onces in the current directory - Dangerous!
rm -rf *

## to remove all files, directories, and hidden files in the current directory and potentially parent directories - Dangerous!
rm -rf -- ..?* .[!.]* *

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## TMUX Commands

TMUX COMMAND:

## Starts a new tmux session
tmux

## Lists active tmux sessions
tmux list-sessions

## will reattach to the last used session
tmux attach

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## CMD Commands

CMD COMMAND
## Location of the hosts file in Windows, used to map IP addresses to hostnames
C:\Windows\System32\drivers\etc\hosts

## How to open the hosts file with Notepad as administrator in Windows
to edit file go to the directory and notepad then file name it will open in admintretor

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Learning Topics

LEARN ABOUT :*=)

## System states or modes of operation
51. Run Levels

## Translate or delete characters
52. Tr Command

## Systemd is a system and service manager, systemctl is used to control it
53. What is System D System CTL(Manage krne ka tareeqa h) ()

## A search and analytics engine
54. Elastic search (Index )

## The process of organizing data for faster searching
55. What is Indexing

## Specifies the delimiter used by awk to separate fields
56. awk -F (Field Separator)

## Counts occurrences of unique lines
57. uniq -c (Yeh command)

## Sorts numerically
58. sort -n

## Searches for files in a directory hierarchy
59. find

## Executes a command periodically and displays the output in fullscreen
60. watch command ( Need to monitor real-time changes in the system's status and command outputs)

## A fast, versatile, remote (and local) file-copying tool
61. rsync

## An archiving utility
62. tar

## Regular Expressions - patterns used to match character combinations in strings
63. regex

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Pattern Matching

## Matches any single character
?

## Matches any string of characters
*

## Matches any character in the set of characters, for example [adf] will match any occurrence of a, d, or f
[set]

## Matches any character not in the set of characters
[!set]

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Scripting and Control Operators

SCRIPTING

Common Control Operators
## Command Separator
;

## EXECUTES COMMANDS SEQUENTIALLY, REGARDLESS OF SUCCESS OR FAILURE.
Example:
command1 ; command2

## Logical AND
&&

## Executes the second command only if the first command succeeds (exit status 0).
Example:
command1 && command2

## Logical OR
||

## EXECUTES THE SECOND COMMAND ONLY IF THE FIRST COMMAND FAILS (EXIT STATUS ≠ 0).
Example:
command1 || command2
If command1 fails, command2 will run.

## Background Execution
&

## RUNS A COMMAND IN THE BACKGROUND SO THE TERMINAL REMAINS FREE FOR OTHER COMMANDS.
Example:
command1 &
command1 will run in the background.

## Pipe Operator
|

## SENDS THE OUTPUT OF ONE COMMAND AS INPUT TO ANOTHER COMMAND.
Example:
command1 | command2
The output of command1 is passed to command2.

## Subshell Grouping
()

## RUNS COMMANDS IN A SUBSHELL.
Example:
(command1 ; command2)
Commands inside parentheses are executed in a separate subshell.

## USED FOR CONDITIONAL EXECUTION IN SCRIPTS (LIKE AN IF-ELSE).
&& and || Combined

Example:
command1 && command2 || command3
If command1 succeeds, command2 runs.
If command1 fails, command3 runs.
------------------------------------------------------------------------------------------------------------------------------
SCRIPTIMG

main rules and basic things

## The $? is a special shell variable that stores the exit status of the last executed command.
The $?

## This is a shebang line specifying the script should be executed with bash. The '--' is less common here and might affect how options are handled,
   generally '#!/bin/bash' is sufficient.
u can add thi { #!/bin/bash -- } [ -- ]

## Prints text to the standard output
and when write any line and u want to be print when script run when use { echo "the line" }

## Command substitution: executes the command and substitutes its output
if u want to make a command a variable then u need to add this { $( any command ) } the curl barcket is for understand

## and normal variable be added like normal { anyname=hello }
and normal variable be added like normal { anyname=hello }

## and like u make a variable if i want to run this
## if do echo anyname { it will give me anyname rather then hello } for that reason i need to add $ to tell echo know that is a variable
## now if i use echo $anyname now it will print hello in the next line

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

SOME [ SOME PRATICE Example ]

## test 56 -gt 55 && echo true || echo false
## true ( answer )
## in this this command is testing whether 56 is greater than 55 by [ -gt ] and the && is used so if the first command succeeds (is true), then it will echo true.
   if the first statement is false, the && part is skipped, and the || works as OR, so it will echo false because the first statement failed.
test 56 -gt 55 && echo true || echo false

## The [ is actually a synonym for the test command. { just remove test and add this bracket [] } can also check man test

SAME EXAMPLE BUT WITH AND & OR

[ 66 -gt 55 -a 66 -lt 500 ] && echo true || echo false
true
[ 66 -gt 55 -a 660 -lt 500 ] && echo true || echo false
false
[ 66 -gt 55 -o 660 -lt 500 ] && echo true || echo false
true

COMPARISON OPERATORS

## greater than
-gt =

## less than
-lt =

## equal
-eq =

## not equal
-ne =

## AND (both conditions must be true)
-a =

## OR (only one condition needs to be true) as this u can also use this as well ( [ ... ] && [ ... ] )
-o =

## is use for negating the result of the test
! =

## checks if a file exists and is a regular file
-f =

## checks if a file descriptor is open and refers to a terminal (This is a common use, but `-t` can also check if a file exists and is a character special file depending on context/tool, 
   but in the context of `[ ]` or `test` it usually refers to a file descriptor/terminal).
-t =

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

+-------------------+------------------------------------------------------------+-----------------------------------------------------------+
| Structure | Purpose | Example and Syntax |
+-------------------+------------------------------------------------------------+-----------------------------------------------------------+
| if-then-else | Condition-based execution. | Example: If a file exists, print a message; otherwise, |
| | | print a different message. |
| | | Syntax: |
| | | if [ condition ]; then |
| | | # Code block if condition is true |
| | | else |
| | | # Code block if condition is false |
| | | fi |
| | | Difference: Handles only two cases—true or false. |
+-------------------+------------------------------------------------------------+-----------------------------------------------------------+
| if-then-elif | To handle multiple conditions. | Example: If one condition is true, take a specific action; |
| | | if another is true, take a different action; if neither |
| | | is true, take a default action. |
| | | Syntax: |
| | | if [ condition1 ]; then |
| | | # Code block for condition1 |
| | | elif [ condition2 ]; then |
| | | # Code block for condition2 |
| | | else |
| | | # Code block if no condition is true |
| | | fi |
| | | Difference: Tests multiple conditions, unlike |
| | | `if-then-else` which only handles two conditions. |
+-------------------+------------------------------------------------------------+-----------------------------------------------------------+
| for Loop | Iterate over a fixed range or list of elements. | Example: Execute code for each item in a list (e.g., |
| | | numbers, filenames). |
| | | Syntax: |
| | | for variable in list; do |
| | | # Code block |
| | | done |
| | | Difference: Used for a specific range or values. Can also |
| | | handle file globbing (e.g., `*.txt`). |
+-------------------+------------------------------------------------------------+-----------------------------------------------------------+
| while Loop | Repeats a code block as long as a condition is true. | Example: A countdown or dynamic task continues as long as |
| | | the condition holds true. |
| | | Syntax: |
| | | while [ condition ]; do |
| | | # Code block |
| | | done |
| | | Difference: Executes until the condition becomes false. |
+-------------------+------------------------------------------------------------+-----------------------------------------------------------+
| until Loop | Executes the loop until a condition becomes true. | Example: A countdown continues until the condition is |
| | | satisfied. |
| | | Syntax: |
| | | until [ condition ]; do |
| | | # Code block |
| | | done |
| | | Difference: Works oppositely to the `while` loop. |
| | | `while` runs as long as the condition is true, while |
| | | `until` runs until the condition becomes true. |
+-------------------+------------------------------------------------------------+-----------------------------------------------------------+

Comparison Table

+-------------------+---------------------------------------------------+------------------------------------------+
| Structure | Purpose | Execution Trigger |
+-------------------+---------------------------------------------------+------------------------------------------+
| if-then-else | Execute code based on a true/false condition | One true/false condition |
+-------------------+---------------------------------------------------+------------------------------------------+
| if-then-elif | Execute based on multiple conditions | Multiple true/false conditions |
+-------------------+---------------------------------------------------+------------------------------------------+
| for Loop | Iterate over a list or range | Fixed list or predefined range |
+-------------------+---------------------------------------------------+------------------------------------------+
| while Loop | Repeat while condition is true | Executes until the condition is false |
+-------------------+---------------------------------------------------+------------------------------------------+
| until Loop | Repeat until condition becomes true | Executes until the condition is true |
+-------------------+---------------------------------------------------+------------------------------------------+

Agar kisi specific structure par zyda explanation chahiye ho, bataiye! 🙂

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Fun Commands

FUN IN LINUX :)

## Displays text in large letters, puts a box around it, and adds rainbow colors
toilet -f mono12 'kuch bhi' | boxes -d cat -a hc -p h38 | lolcat
## Shows a Matrix-like screen effect
cmatrix

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Random Commands

RANDOM COMMANDS
##this command tell the login user name
logname

##calander
cal

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Nginx

ENGIX
## If the Nginx web server is running but the site is not working, or the web server crashes, go to the command line interface (CLI) and use `nginx -t`. 
   This command tests the configuration and will show any errors, such as a missing file. Then, create the missing file and set the correct permissions.
agar web server engix hai or site per sub sai hai or nhi chal rahi or phir web server crash hai then go to cli
and use command ( engix -t ) then wo koi error de hai may be file missing or some this buss waha ja kar file create kar lo
us ko wo permition de do

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Storage Commands

STORAGE
## Displays disk space usage in a human-readable format, showing type
df -hT

## Estimates file space usage in a human-readable format for the current directory
du -sh
>
## These commands extract and display total, free, and used disk space from the `df --total` output
echo "total space:" && df -h --total | grep total | awk '{print $2}' && echo "" && \
echo "(free space):" && df -h --total | grep total | awk '{print $4}' && echo "" && \
echo "(used space):" && df -h --total | grep total | awk '{print $3}'
#All to getter
echo "total space:" && df -h --total | grep total | awk '{print $2}' && echo "" && echo "Free space:" && df -h --total | grep total | awk '{print $4}' && echo "" && echo "used space :" && df -h --total | grep total | awk '{print $3}'

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Bad Bot IP Blocking

BAD BOT IP BLOCK
## Extracts IPs from LSWS access logs, sorts them, counts unique IPs, sorts by count, and shows the most frequent IPs. Useful for identifying abusive IPs.
awk '{print $1}' */logs/lsws_access_logs | sort -n | uniq -c | sort -h | tail
this command is use for ckeck the logs

## Filters LSWS access logs for a specific IP and shows the last 20 lines
cat */logs/lsws_access_logs | grep 196.251.80.244 | tail -n20

## Filters LSWS access logs for a specific IP and follows the output in real-time
tail -f */logs/lsws_access_logs | grep 65.0.89.109

## Filters LSWS access logs for a specific IP and shows the last 20 lines
cat */logs/lsws_access_logs | grep 13.94.89.2 | tail -n20

and this is the rule for .htaccess for blocking the ip

To block bad bots:
1)
RewriteEngine on
RewriteCond %{REMOTE_ADDR} ^143\.110\.185\.219$
RewriteRule .* - [F]
## .htaccess rule to block a single specific IP address

(Multiple Ips Blocking)
RewriteEngine On
RewriteCond %{REMOTE_ADDR} ^89\.248\.169\.52$ [OR]
RewriteCond %{REMOTE_ADDR} ^94\.102\.51\.147$
RewriteRule ^ - [F]
## .htaccess rule to block multiple specific IP addresses

## Multiple IPs were blocked that were found abusive.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Quick File Clear

QUICK FILE CLEAR
So what is the quickest way to clear a file ?
## Redirects empty output to the file 'foo', effectively clearing it
>foo

And what is the quickest way to clear a file when the noclobber option is set ?
## Redirects empty output to the file 'bar', clearing it even if noclobber is set (uses the `|` to bypass noclobber)
>|bar

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Links (Soft and Hard)

this is use to make a like between file -
## this is use to make a link between file
## for soft link use -s option and for hard link just use ln
ln

## [ soft link = Symbolic Links ] ( ln -s ) use to make a shortcut of a file. with this link you can edit the original file, and if you delete the soft link it does not affect the original file. 
     the original file and this link have different inode numbers. if the original file is deleted then the soft link will also be deleted or will not be accessible.
## [ Hard link ] ( ln ) use as a duplicate but both are connect and can edit but the original file will delete then it will not affacted on the duplicate file
## cuz it the hard link and the inode number is same.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Web Server Configuration (.htaccess)

RewriteEngine On
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
RewriteBase /
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(wp-(content|admin|includes).*) $2 [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L]
RewriteRule . index.php [L]
## Apache/htaccess rules for URL rewriting and handling WordPress permalinks/requests

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Application/Environment Notes

lc-infinity-bckup application name

Joomla 4.3.4

php 8.1

Maria db 10.6
## Notes about a specific application environment including application name and versions of CMS, PHP, and Database

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Site Migration Steps

## FIRST SITE KA DATA YE FILE CLEAR KAR DE
## Remove all files and directories in the current location (use with caution!)
rm -rf *

## THEN TALE TAR FILE AND THEN OPEN IT
## Extract the contents of a gzipped tar archive
tar -xzvf daniyal.tar.gz

## PHIR IS FILE MA ( DB NAME , USER NAME & PASSWORD CHANGE KAR YEE
## Open the wp-config.php file for editing
nano wp-config.php

## PHIR DEKLE
## Display the contents of wp-config.php and highlight lines containing 'db' (case-insensitive)
cat wp-config.php | grep -i db

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
					way of migration
1 : scp >this will copy file from source and paste at destination< "this command also transfer file from one server to another"
2 : tar >this will make a compress file from the sourse and you can take this at destination by wget"sourse siteurl/file name"<
3 : rsync >this will move the file from one server to another one <				
4 : sftp >putty< "jsut do ssh"

##scp
##from one server to another
scp -P 2222 /path/to/local/file.tar.gz username@remote_host:/path/to/remote/destination/

## in the server
cp /path/to/source/file.tar.gz /path/to/destination/



##tar
##sorces
tar -czvf archive_name.tar.gz *
>but to move this tar.gz file you need to wget <
##distination
tar -xzvf archive_name.tar.gz

##rsync
rsync -avzh --dry-run --progress -e 'ssh -p 2222' siddiqui@3.111.15.150:/mnt/user_data/home/master/applications/conversions/public_html/ siddiqui@142.93.216.187:/mnt/user_data/home/master/applications/conversions/public_html/
				
					
					
				
					
					
					
					
					Site Migration COMMAND
## for data base backup & for open 

## backup
mysqldump -u username -p dbname > db.sql

## Restores
mysql -u username -p dbname < db.sql

					migration command things

TAR ( struture ) tar [options] [archive-file] [file or directory to be archived]
## difference between tar file compressions [ The gz format provides the best speed but a "regular" compression ratio.
## The bz2 format provides a mid-term between speed and compression, while xz
## is excellent when talking about compression but a little slower.
tar -czvf mysite-backup-030425.tar.gz /path/to/directory
tar -xzvf backup.tar.gz
tar -xzvf mysite-backup-030425.tar.gz
## Create (-c). Create a new archive.
## Extract (-x). Extract files from an archive.
## Verbose (-v). Show the detailed output of the process.
## File (-f). Specify the archive file.
## Compress with gzip (-z). The archive will be compressed using gzip, resulting in a .tar.gz file.
## Compress with bzip2 (-j). Compress the archive using bzip2, resulting in a .tar.bz2 file.
## Compress with xz (-J). Compress the archive using xz, resulting in a .tar.xz file.
tar -cfz application.mysql.tar.gz /mnt/user_data/home/master/applications/wp-addmin/public_html/

## TO CREATE A TAR FOR ALL FILE
tar -czvf archive_name.tar.gz *


## for transfer the file without the copy like tar
## [ if u put ( / ) this in the end of the source the the files will be in the directory if not this the folder be there not the file in the directory
rsync -avz -e "ssh -p 2222" --progress --debug=all source/files/ username@remote_ip:/destination/files

## Example of using rsync for file transfer between remote servers via SSH
rsync -avzh --dry-run --progress -e 'ssh -p 2222' siddiqui@3.111.15.150:/mnt/user_data/home/master/applications/conversions/public_html/ siddiqui@142.93.216.187:/mnt/user_data/home/master/applications/conversions/public_html/


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Other Notes

FARRUKH TASK

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
##other file paths 

#here all the rule site for lsws server site

/usr/local/lsws/conf$ cat httpd_config.conf




This new account is standardized immediately upon signup. For now, it remains active but must be suspended if any suspicious activity is detected.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## REPORT COMMAND

vnstat -m

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## RULE'S

//to block xmlrpc file that it give 403
RewriteEngine On
RewriteRule ^xmlrpc\.php$ - [F,L]

	
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## CMD COMMAND

netsh wlan show profiles

netsh wlan show profile name="WiFiName" key=clear


SELECT
    SUM(data_length + index_length) / 1024 / 1024 / 1024 AS "Total Size (GB)"
FROM
    information_schema.TABLES;
==============================================================================================================
command 

watch du -sh
