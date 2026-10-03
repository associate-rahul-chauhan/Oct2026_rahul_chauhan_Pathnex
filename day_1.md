## Day 1 Learning [Date: 03-oct]

### Learn about basic command in linux

in web server only **8% are window** system

and **linux** system hold more than 60% 


### permission

ch: change mode

ls: list file

ls -l : list file with long details

ls -a : show hidden file

pwd: present working directory

touch : create a new file


mv: mv file (rename can also it is/ there is no command of rename a file)

rm: remove file 

cd ~ : change directory to home 


### viewing file


cat : content display

head : see head content of a file

less : read file page by page

tail : show footer content of file


### users and permission

whoami:  find the user name

id: show user id and groups

groups: show group


### how to understand permission


*when we do ls -la on a folder we see data something like

drwxr-xr-x  3 rc rc 4096 Oct  3 15:59 Oct2026_rahul_chauhan_Pathnex


what is drwxr-xr-x means

let divide this into 4 category

d: d stand for directory

rwxr: r-read (4) w:write (2) x:execute (1) total count: 7 (total 7) (r:owner first is owner)
xr: r: read (4) , x: 1 (total: 5) (second is group)
-x: x: (1) only 1 (last one the other)

so this directory have only 764 permission, this is how we understand what permission we need to give

so the persmisson flow goes like 

read: 4 less
write: 2 
execute: 1 (hard) 

so the number goes bottom to top

so this is how we give number in this 


--------------------------------------------------------------------------


## create user in linux

by default linux give few users but we need to create a new user


*create a new user

    `sudo adduser rahul`

*check user
    
    `id rahul`

*find all the users

        `sudo /etc/passwd`

this command will show all the user list


*how to change user group, lets suppose some of user dont have the persmisson

add in wheel group: wheel group that gives sudo privileges to users

go to root user or user which have all the wheel group 

         `sudo usermod -aG wheel rahul`


## how to change/switch user
    
    `su rahul`

## how to set password for rahul user

    `passwd`

then it will ask for password


## how to change the owner


`chown <username> <file>`
    
