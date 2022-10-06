printf—Format and Print Data
Unlike the other commands in this chapter, the printf command is not used 
for pipelines (it does not accept standard input), nor does it find frequent 
application directly on the command line (it’s used mostly in scripts). So 
why is it important? Because it is so widely used.
printf (from the phrase print formatted) was originally developed for the 
C programming language and has been implemented in many programming languages, including the shell. In fact, in bash, printf is a built-in.
printf works like this:
printf "format" arguments
The command is given a string containing a format description, which 
is then applied to a list of arguments. The formatted result is sent to standard output. Here is a trivial example:
[me@linuxbox ~]$ printf "I formatted the string: %s\n" foo 
I formatted the string: foo
The format string may contain literal text (like I formatted the string:); 
escape sequences (such as \n, a newline character); and sequences beginning with the % character, which are called conversion specifications. In the 
example above, the conversion specification %s is used to format the string 
foo and place it in the command’s output. Here it is again:
[me@linuxbox ~]$ printf "I formatted '%s' as a string.\n" foo 
I formatted 'foo' as a string.
As we can see, the %s conversion specification is replaced by the string 
foo in the command’s output. The s conversion is used to format string data. 
There are other specifiers for other kinds of data. Table 21-4 lists the commonly used data types.
Table 21-4: Common printf Data-Type Specifiers
Specifier Description
d Format a number as a signed decimal integer.
f Format and output a floating point number.
Formatting Output 275
(continued)
Table 21-4 (continued )
Specifier Description
o Format an integer as an octal number.
s Format a string.
x Format an integer as a hexadecimal number using lowercase a–f 
where needed.
X Same as x, but use uppercase letters.
% Print a literal % symbol (i.e., specify “%%”).
We’ll demonstrate the effect each of the conversion specifiers on the 
string 380:
[me@linuxbox ~]$ printf "%d, %f, %o, %s, %x, %X\n" 380 380 380 380 380 380 
380, 380.000000, 574, 380, 17c, 17C
Since we specified six conversion specifiers, we must also supply six 
arguments for printf to process. The six results show the effect of each 
specifier.
Several optional components may be added to the conversion specifier 
to adjust its output. A complete conversion specification may consist of the 
following:
%[flags][width][.precision]conversion_specification
Multiple optional components, when used, must appear in the order specified above to be properly interpreted. Table 21-5 describes each component.
Table 21-5: printf Conversion-Specification Components
Component Description
flags There are five different flags:
ì # Use the alternate format for output. This varies by data 
type. For o (octal number) conversion, the output is prefixed 
with 0 (zero). For x and X (hexadecimal number) conversions, 
the output is prefixed with 0x or 0X respectively.
ì 0 (zero) Pad the output with zeros. This means that the field 
will be filled with leading zeros, as in 000380.
ì - (dash) Left-align the output. By default, printf right-aligns 
output.
ì (space) Produce a leading space for positive numbers.
ì + (plus sign) Sign positive numbers. By default, printf signs 
only negative numbers. 
276 Chapter 21
Table 21-5 (continued )
Component Description
width A number specifying the minimum field width
.precision For floating-point numbers, specify the number of digits of 
precision to be output after the decimal point. For string 
conversion, precision specifies the number of characters to 
output.
Table 21-6 lists some examples of different formats in action.
Table 21-6: print Conversion Specification Examples
Argument Format Result Notes
380 "%d" 380 Simple formatting of an integer
380 "%#x" 0x17c Integer formatted as a hexadecimal number using the 
alternate format flag
380 "%05d" 00380 Integer formatted with leading 
zeros (padding) and a minimum 
field width of five characters
380 "%05.5f" 380.00000 Number formatted as a floatingpoint number with padding and 
5 decimal places of precision. 
Since the specified minimum 
field width (5) is less than the 
actual width of the formatted 
number, the padding has no 
effect.
380 "%010.5f" 0380.00000 Increasing the minimum field 
width to 10 makes the padding 
visible.
380 "%+d" +380 The + flag signs a positive 
number.
380 "%-d" 380 The - flag left-aligns the 
formatting.
abcdefghijk "%5s" abcedfghijk A string is formatted with a 
minimum field width.
abcdefghijk "%.5s" abcde By applying precision to a 
string, it is truncated.
Formatting Output 277
Again, printf is used mostly in scripts, where it is employed to format 
tabular data, rather than on the command line directly. But we can still 
show how it can be used to solve various formatting problems. First, let’s 
output some fields separated by tab characters:
[me@linuxbox ~]$ printf "%s\t%s\t%s\n" str1 str2 str3 
str1 str2 str3
By inserting \t (the escape sequence for a tab), we achieve the desired 
effect. Next, some numbers with neat formatting:
[me@linuxbox ~]$ printf "Line: %05d %15.3f Result: %+15d\n" 1071 3.14156295 
32589 
Line: 01071 3.142 Result: +32589
This shows the effect of minimum field width on the spacing of the 
fields. Or how about formatting a tiny web page?
[me@linuxbox ~]$ printf "<html>\n\t<head>\n\t\t<title>%s</title>\n\t</head>
\n\t<body>\n\t\t<p>%s</p>\n\t</body>\n</html>\n" "Page Title" "Page Content" 
<html> 
<head> 
<title>Page Title</title> 
</head> 
<body> 
<p>Page Content</p> 
</body> 
</html>