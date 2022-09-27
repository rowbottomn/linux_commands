# ls Options  

Option |Long Option | Description
---|---|---
`-a `|`--all` |List all files, even those with names that begin with a period, which are normally not listed (i.e., hidden).
`-d` |`--directory` | Ordinarily, if a directory is specified, ls will list the contents of the directory, not the directory itself. Use this option in conjunction with the -l option to see details about the directory rather than its contents.
`-F` | `--classify` | This option will append an indicator character to the end of each listed name (for example, a forward slash if the name is a directory).
`-h` |`--human-readable` |In long format listings, display file sizes in human-readable format rather than in bytes.
`-l` ||Display results in long format.
`-r` |`--reverse` |Display the results in reverse order. Normally, ls displays its results in ascending alphabetical order.
`-S` ||Sort results by file size.
`-t` ||Sort by modification time
----------------------------------------------------------------
## Long Field Meanings
Run the command `ls -l` in a Repl directory in the Linux shell.
Below is an example of a possible output.  
`-rw-r--r-- 1 runner runner  46 Aug  9 03:31 style.css`
Field | Meaning
---|---
`-rw-r—r--` |Access rights to the file. The first character indicates the type of file. Among the different types, a leading dash means a regular file, while a d indicates a directory. The next three characters are the access rights for the file’s owner, the next three are for members of the file’s group, and the final three are for everyone else. 
`1` | File’s number of hard links.
`runner` |The user name of the file’s owner.
`runner` |The name of the group that owns the file.
`46` |Size of the file in bytes.
`Aug  9 03:31`| Date and time of the file’s last modification.
`style.css`| Name of the file.