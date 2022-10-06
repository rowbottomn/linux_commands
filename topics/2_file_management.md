# Manipulating Files and Directories
### Introduce the following
commands:
- `cp` – Copy files and directories  
- `mv` – Move/rename files and directories
- `mkdir` – Create directories  
- `rm` – Remove files and directories  
- `ln` – Create hard and symbolic links  

These five commands are among the most frequently used Linux commands. They are used for manipulating both files and directories.  
While it is easy to perform simple file manipulations with a graphical file manager, complicated tasks can be easier with the command line programs. For example, how could we copy all the HTML files from one directory to another but only copy files that do not exist in the destination directory or are newer than the versions in the destination directory? It's pretty hard with a file manager but pretty easy with the command line.  
`cp -u *.html destination`

### Wildcards  
Before we begin using our commands, we need to talk about a shell feature that makes these commands so powerful. Since the shell uses filenames so much, it provides special characters to help us rapidly specify groups of filenames. These special characters are called wildcards. Using wildcards (which is also known as **globbing**) allows us to select filenames based on patterns of characters. 

Wildcard |Meanings
---|---
`*`| Matches any characters
`?`| Matches any single character
`[characters]`| Matches any character that is a member of the set characters
`[!characters]`| Matches any character that is not a member of the set characters
`[[:class:]]`| Matches any character that is a member of the specified class

### Character Classes
Character Class |Meaning
---|---
`[:alnum:]`| Matches any alphanumeric character
`[:alpha:]`| Matches any alphabetic character
`[:digit:]`| Matches any numeral
`[:lower:]`| Matches any lowercase letter
`[:upper:]`| Matches any uppercase letter

Using wildcards makes it possible to construct sophisticated selection criteria for filenames. 

### Wildcard Patterns
Pattern |Matches 
---|---
`*`| All files
`g*`| Any file beginning with “g”
`b*.txt`| Any file beginning with “b” followed by any characters and ending with “.txt”
`Data???` |Any file beginning with “Data” followed by exactly three characters
`[abc]*`| Any file beginning with either an “a”, a “b”, or a “c”
`BACKUP.[0-9][0-9][0-9]`| Any file beginning with “BACKUP.” followed by exactly three numerals
`[[:upper:]]*` |Any file beginning with an uppercase letter
`[![:digit:]]*` |Any file not beginning with a numeral
`*[[:lower:]123]`| Any file ending with a lowercase letter or the numerals “1”, “2”, or “3”



## mkdir – Create Directories
The `mkdir` command is used to create directories. It works like this:  
`mkdir directory ...`

    A note on notation: When three periods follow an argument in the description of a command (as above), it means that the argument can be repeated, thus the following command: `mkdir dir1` would create a single directory named dir1, while the following: `mkdir dir1 dir2 dir3` would create three directories named dir1, dir2, and dir3.
## cp – Copy Files and Directories
The cp command copies files or directories. It can be used two different ways. The following:  
`cp item1 item2`  
copies the single file or directory item1 to the file or directory item2 and the following:

`cp item... directory`  
copies multiple items (either files or directories) into a directory.
### Useful Options and Examples
Option |Long Option |Meaning
---|---|---
`-a` |`--archive` | Copy the files and directories and all of their attributes, including ownerships and permissions. Normally, copies take on the default attributes of the user performing the copy. 
`-i` |`--interactive` |Before overwriting an existing file, prompt the user for confirmation. If this option is not specified, cp will silently (meaning there will be no warning) overwrite files.  
`-r` |`--recursive`| Recursively copy directories and their contents. This option (or the -a option) is required when copying directories.
`-u` |`--update`| When copying files from one directory to another, only copy files that either don't exist or are newer than the existing corresponding files, in the destination directory. This is useful when copying large numbers of files as it skips files that don't need to be copied.
`-v`| `--verbose`| Display informative messages as the copy is performed.

### cp Examples
Command | Results  
---|---
`cp file1 file2`| Copy file1 to file2. If file2 exists, it is overwritten with the contents of file1. If file2 does not exist, it is created.
`cp -i file1 file2`| Same as previous command, except that if file2 exists, the user is prompted before it is overwritten.
`cp file1 file2 dir1`| Copy file1 and file2 into directory dir1. The directory dir1 must already exist.
`cp dir1/* dir2`| Using a wildcard, copy all the files in dir1 into
dir2. The directory dir2 must already exist.
`cp -r dir1 dir2`| Copy the contents of directory dir1 to directory dir2. If directory dir2 does not exist, it is created and, after the copy, will contain the same contents as directory dir1.  If directory dir2 does exist, then directory dir1 (and its contents) will be copied into dir2.
## mv – Move and Rename Files
The mv command performs both file moving and file renaming, depending on how it is used. In either case, the original filename no longer exists after the operation. mv is used in much the same way as cp, as shown here:   
`mv item1 item2`   
to move or rename the file or directory item1 to item2 or:  
`mv item... directory`  
to move one or more items from one directory to another.  
### Useful Options and Examples
mv shares many of the same above options as cp 
Option |Long Option |Meaning
---|----------------------|---
`-i` |`--interactive` |Before overwriting an existing file, prompt the user for confirmation. If this option is not specified, mv will silently overwrite files.
`-u` |`--update` |When moving files from one directory to another, only move files that either don't exist, or are newer than the existing corresponding files in the destination directory.
`-v`| `--verbose`| Display informative messages as the move is performed.

### mv Examples
Command| Results
---|---
`mv file1 file2`| Move file1 to file2. If file2 exists, it is overwritten with the contents of file1. If file2 does not exist, it is created. In either case, file1 ceases to exist.
`mv -i file1 file2`| Same as the previous command, except that if file2 exists, the user is prompted before it is overwritten.
`mv file1 file2 dir1`| Move file1 and file2 into directory dir1. The directory dir1 must already exist.
`mv dir1 dir2`| If directory dir2 does not exist, create directory dir2 and move the contents of directory dir1 into dir2 and delete  irectory dir1.  If directory dir2 does exist, move directory dir1  and its contents) into directory dir2.
## rm – Remove Files and Directories
The rm command is used to remove (delete) files and directories, as shown here:  
`rm item...`  
where item is one or more files or directories.  

### Useful Options and Examples
Option | Long Option |Meaning
---|---|---
`-i`| `--interactive`| Before deleting an existing file, prompt the user for confirmation. If this option is not specified, rm will silently delete files.
`-r `|`--recursive `|Recursively delete directories. This means that if a directory being deleted has subdirectories, delete them too. To delete a non-empty directory, this option must be specified.
`-f`| `--force`| Ignore nonexistent files and do not prompt. This overrides the --interactive option.
`-v`| `--verbose`| Display informative messages as the deletion is
performed.
### rm Examples
Command |Results
`rm file1`| Delete file1 silently.
`rm -i`| file1 Same as the previous command, except that the user is prompted for confirmation before the deletion is performed.
`rm -r file1 dir1`| Delete file1 and dir1 and its contents.
`rm -rf file1 dir1`| Same as the previous command, except that if either file1 or dir1 do not exist, rm will continue silently.  
    **Be Careful with rm!**  
Unix-like operating systems such as Linux do not have an undelete command.  Once you delete something with rm, it's gone. Linux  assumes you're smart and you know what you're doing.
Be particularly careful with wildcards. Consider this classic example. Let's say you want to delete just the HTML files in a directory. To do this, you type the following:   
`rm *.html`  
This is correct, but if you accidentally place a space between the * and the .html like so:  
`rm * .html`  
the rm command will delete all the files in the directory and then complain that there is no file called .html!!!  
Here is a useful tip: whenever you use wildcards with rm (besides carefully checking your typing!), test the wildcard first with ls. This will let you see the files that will be deleted. Then press the up arrow key to recall the command and replace ls with rm.
## ln – Create Links
The ln command is used to create either hard or symbolic links. It is used in one of two ways. The following creates a hard link:  
`ln file link`  
The following creates a symbolic link:  
`ln -s item link`  
to create a symbolic link where item is either a file or a directory.
### Hard Links
Hard links are the original Unix way of creating links, compared to symbolic links, which are more modern. By default, every file has a single hard link that gives the file its name.  
When we create a hard link, we create an additional directory entry for a file. Hard links have two important limitations:  
1. A hard link cannot reference a file outside its own file system. This means a link cannot reference a file that is not on the same disk partition as the link itself.  
2. A hard link may not reference a directory.  
   
A hard link is indistinguishable from the file itself. Unlike a symbolic link, when we list a directory containing a hard link we will see no special indication of the link. When a hard link is deleted, the link is removed but the contents of the file itself continue to exist (that is, its space is not deallocated) until all links to the file are deleted.  
It is important to be aware of hard links because you might encounter them from time to time, but modern practice prefers  symbolic links, which we will cover next.  
### Symbolic Links
Symbolic links were created to overcome the limitations of hard links. Symbolic links work by creating a special type of file that contains a text pointer to the referenced file or directory. In this regard, they operate in much the same way as a Windows shortcut,
though of course they predate the Windows feature by many years.
A file pointed to by a symbolic link, and the symbolic link itself are largely indistinguishable from one another.  
For example, if we write something to the symbolic link, the referenced file is written to. However when we delete a symbolic link, only the link is deleted,
not the file itself. If the file is deleted before the symbolic link, the link will continue to exist but will point to nothing. In this case, the link is said to be broken.  
In many implementations, the ls command will display broken links in a distinguishing color, such as red, to reveal their presence.  
The concept of links can seem confusing, but hang in there. We're going to try all this stuff and it will, hopefully, become clear.
## Let's Build a Playground
Since we are going to do some real file manipulation, let's build a safe place to “play” with our file manipulation commands. 
1. First we need a directory to work in. Create one in our home directory and call it playground.
### Creating Directories
The mkdir command is used to create a directory. To create our playground directory we will first make sure we are in our home directory and will then create the new directory.  
`[me@linuxbox ~]$ cd ~`    
`[me@linuxbox ~]$ mkdir playground`  
To make our playground a little more interesting, let's create a couple of directories inside it called dir1 and dir2. To do this, we will change our current working directory to playground and execute another mkdir.
`[me@linuxbox ~]$ cd playground`  
`[me@linuxbox playground]$ mkdir dir1 dir2`  
Notice that the mkdir command will accept multiple arguments allowing us to create both directories with a single command.
### Copying Files
Next, let's get some data into our playground. We'll do this by copying a file. Using the cp command, we'll copy the passwd file from the /etc directory to the current working directory.  
`[me@linuxbox playground]$ cp /etc/passwd .`  
Notice how we used shorthand for the current working directory, the single trailing period. So now if we perform an ls, we will see our file.  
`[me@linuxbox playground]$ ls -l`  
`total 12`  
`drwxrwxr-x 2 me me 4096 2022-09-20 16:40 dir1`  
`drwxrwxr-x 2 me me 4096 2022-09-20 16:40 dir2`  
`-rw-r--r-- 1 me me 1650 2022-09-20 16:07 passwd`   
Now, just for fun, let's repeat the copy using the “-v” option (verbose) to see what it does.  
`[me@linuxbox playground]$ cp -v /etc/passwd .`  
```/etc/passwd' -> `./passwd'```   
The cp command performed the copy again, but this time displayed a concise message indicating what operation it was performing. Notice that cp overwrote the first copy without any warning. Again this is a case of cp assuming that we know what we're doing.  
To get a warning, we'll include the “-i” (interactive) option.  
`[me@linuxbox playground]$ cp -i /etc/passwd .`  
```cp: overwrite `./passwd'?```  
Responding to the prompt by entering a y will cause the file to be overwritten, any other character (for example, n) will cause cp to leave the file alone. 
`cp /etc/os-release/` 
### Moving and Renaming Files
Now, the name passwd doesn't seem very playful and this is a playground, so let's change it to something else.
`[me@linuxbox playground]$ mv passwd fun`
Let's pass the fun around a little by moving our renamed file to each of the directories and back again. The following moves it first to the directory dir1:   
`[me@linuxbox playground]$ mv fun dir1`  
The following then moves it from dir1 to dir2:  
`[me@linuxbox playground]$ mv dir1/fun dir2`  
Finally, the following brings it back to the current working directory:  
`[me@linuxbox playground]$ mv dir2/fun .`  
Next, let's see the effect of mv on directories. First we will move our data file into dir1 again, like this:  
`[me@linuxbox playground]$ mv fun dir1`  
Then we move dir1 into dir2 and confirm it with ls.  
`[me@linuxbox playground]$ mv dir1 dir2`  
`[me@linuxbox playground]$ ls -l dir2`  
```total 4```  
```drwxrwxr-x 2 me me 4096 2022-09-20 06:06 dir1```  
`[me@linuxbox playground]$ ls -l dir2/dir1`  
```total 4```  
```-rw-r--r-- 1 me me 1650 2022-09-20 16:33 fun```  
Note that since dir2 already existed, mv moved dir1 into dir2. If dir2 had not existed, mv would have renamed dir1 to dir2. Lastly, let's put everything back.  
`[me@linuxbox playground]$ mv dir2/dir1 .`  
`[me@linuxbox playground]$ mv dir1/fun .`  
### Creating Hard Links
Now we'll try some links. We’ll first create some hard links to our data file like so:
`[me@linuxbox playground]$ ln fun fun-hard`  
`[me@linuxbox playground]$ ln fun dir1/fun-hard`  
`[me@linuxbox playground]$ ln fun dir2/fun-hard`  
So now we have four instances of the file fun. Let's take a look at our playground directory.  
`[me@linuxbox playground]$ ls -l`  
```total 16```  
```drwxrwxr-x 2 me me 4096 2022-09-20 16:17 dir1```  
```drwxrwxr-x 2 me me 4096 2022-09-20 16:17 dir2```  
```-rw-r--r-- 4 me me 1650 2022-09-20 16:33 fun```  
```-rw-r--r-- 4 me me 1650 2022-09-20 16:33 fun-hard```   
One thing we notice is that both the second fields in the listings for fun and fun-hard contain a 4 which is the number of hard links that now exist for the file. Remember that a file will always have at least one link because the file's name is created by a link. So, how do we know that fun and fun-hard are, in fact, the same file? In this case, ls is not very helpful. While we can see that fun and fun-hard are both the same size (field 5), our listing provides no way to be sure. To solve this problem, we're going to have to dig a
little deeper.  
When thinking about hard links, it is helpful to imagine that files are made up of two parts:  
1. The data part containing the file's contents.
2. The name part that holds the file's name.  
   
When we create hard links, we are actually creating additional name parts that all refer to the same data part. The system assigns a chain of disk blocks to what is called an **inode**, which is then associated with the name part. Each hard link therefore refers to a specific inode containing the file's contents.  
The ls command has a way to reveal this information. It is invoked with the -i option.  
`[me@linuxbox playground]$ ls -li`  
```total 16```  
```12353539 drwxrwxr-x 2 me me 4096 2022-09-20 16:17 dir1```  
```12353540 drwxrwxr-x 2 me me 4096 2022-09-20 16:17 dir2```  
```12353538 -rw-r--r-- 4 me me 1650 2022-09-20 16:33 fun```  
```12353538 -rw-r--r-- 4 me me 1650 2022-09-20 16:33 fun-hard```  
In this version of the listing, the first field is the inode number and, as we can see, both fun and fun-hard share the same inode number, which confirms they are the same file.
###Creating Symbolic Links
Symbolic links were created to overcome the two disadvantages of hard links.  
1. Hard links cannot span physical devices.  
2. Hard links cannot reference directories, only files.  
* Symbolic links are a special type of file that contains a text pointer to the target file or directory.
* Creating symbolic links is similar to creating hard links.  
  
`[me@linuxbox playground]$ ln -s fun fun-sym`  
`[me@linuxbox playground]$ ln -s ../fun dir1/fun-sym`  
`[me@linuxbox playground]$ ln -s ../fun dir2/fun-sym`  
The first example is pretty straightforward; we simply add the “-s” option to create a symbolic link rather than a hard link. But what about the next two? Remember, when we create a symbolic link, we are creating a text description of where the target file is relative to the symbolic link. It's easier to see if we look at the ls output shown here:  
`[me@linuxbox playground]$ ls -l dir1`  
```total 4```  
```-rw-r--r-- 4 me me 1650 2022-09-20 16:33 fun-hard```  
```lrwxrwxrwx 1 me me 6 2022-09-20 15:17 fun-sym -> ../fun```  
The listing for fun-sym in dir1 shows that it is a symbolic link by the leading l in the first field and that it points to ../fun, which is correct. Relative to the location of funsym, fun is in the directory above it.   
Notice too, that the length of the symbolic link file is 6, the number of characters in the string ../fun rather than the length of the file to which it is pointing.  
When creating symbolic links, we can either use absolute pathnames, as shown here:  
`[me@linuxbox playground]$ ln -s /home/me/playground/fun dir1/fun-sym`  
or relative pathnames, as we did in our earlier example.  
In most cases, using relative pathnames is more desirable because it allows a directory tree containing symbolic links and their referenced files to be renamed and/or moved without breaking the links.
In addition to regular files, symbolic links can also reference directories.  
`[me@linuxbox playground]$ ln -s dir1 dir1-sym`  
`[me@linuxbox playground]$ ls -l`  
```total 16```  
```drwxrwxr-x 2 me me 4096 2022-09-20 15:17 dir1```  
```lrwxrwxrwx 1 me me 4    2022-09-20 14:45 dir1-sym -> dir1```  
```drwxrwxr-x 2 me me 4096 2022-09-20 15:17 dir2```  
```-rw-r--r-- 4 me me 1650 2022-09-20 16:33 fun```  
```-rw-r--r-- 4 me me 1650 2022-09-20 16:33 fun-hard```  
```lrwxrwxrwx 1 me me 3    2022-09-20 15:15 fun-sym -> fun```  
### Removing Files and Directories
As we covered earlier, the rm command is used to delete files and directories. We are going to use it to clean up our playground a little bit. First, let's delete one of our hard links.
`[me@linuxbox playground]$ rm fun-hard`  
`[me@linuxbox playground]$ ls -l`  
```total 12```
```drwxrwxr-x 2 me me 4096 2022-09-20 15:17 dir1```  
```lrwxrwxrwx 1 me me 4 2022-09-20 14:45 dir1-sym -> dir1```  
```drwxrwxr-x 2 me me 4096 2022-09-20 15:17 dir2```  
```-rw-r--r-- 3 me me 1650 2022-09-20 16:33 fun```  
```lrwxrwxrwx 1 me me 3 2022-09-20 15:15 fun-sym -> fun```  
That worked as expected.  
The file fun-hard is gone and the link count shown for fun is reduced from four to three, as indicated in the second field of the directory listing.  
Next, we'll delete the file fun, and just for enjoyment, we'll  include the -i option to show what that does.  
`[me@linuxbox playground]$ rm -i fun`  
```rm: remove regular file `fun'?```  
Enter y at the prompt and the file is deleted.   
But let's look at the output of ls now. Notice what happened to fun-sym? Since it's a symbolic link pointing to a now-nonexistent file, the link is broken.  
`[me@linuxbox playground]$ ls -l`  
```total 8```  
```drwxrwxr-x 2 me me 4096 2022-09-20 15:17 dir1```  
```lrwxrwxrwx 1 me me 4 2022-09-20 14:45 dir1-sym -> dir1```  
```drwxrwxr-x 2 me me 4096 2022-09-20 15:17 dir2```  
```lrwxrwxrwx 1 me me 3 2022-09-20 15:15 fun-sym -> fun```  
Most Linux distributions configure ls to display broken links. The presence of a broken link is not in and of itself dangerous, but it is rather messy.   
If we try to use a broken link
we will see this:  
`[me@linuxbox playground]$ less fun-sym`  
```fun-sym: No such file or directory```  
Let's clean up a little. We'll delete the symbolic links here:  
`[me@linuxbox playground]$ rm fun-sym dir1-sym`  
`[me@linuxbox playground]$ ls -l`  
```total 8```  
```drwxrwxr-x 2 me me 4096 2022-09-20 15:17 dir1```  
```drwxrwxr-x 2 me me 4096 2022-09-20 15:17 dir2```  
One thing to remember about symbolic links is that most file operations are carried out on the link's target, not the link itself. rm is an exception. When we delete a link, it is the link that is deleted, not the target.  
Finally, we will remove our playground. To do this, we will return to our home directory and use rm with the recursive option (-r) to delete playground and all of its contents, including its subdirectories.  
`[me@linuxbox playground]$ cd`  
`[me@linuxbox ~]$ rm -r playground`  
