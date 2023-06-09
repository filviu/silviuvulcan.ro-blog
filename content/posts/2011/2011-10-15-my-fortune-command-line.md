---
title: My fortune command line…
author: silviu
type: post
date: 2011-10-15T14:11:48+00:00
url: /2011/10/15/my-fortune-command-line/
categories:
  - old
tags:
  - bash
  - Fortune
  - profile
  - temp_on

---
I take my bash profile very seriously 🙂

I use:

```bash
fortune fortunes fortunes-o fortunes2 forunes2-o 30% startrek
```

The above means to choose fortunes only from the 5 specified files and more it assures that I get startrek fortunes from time to time. Note that because lists are not equal in size it doesnt mean that I get them 30% of the time...

Below is the fortune man page:

## Name

fortune - print a random, hopefully interesting, adage

## Synopsis

**fortune** [**-aefilosw**] [**-n** _length_] [ **-m** _pattern_] [[_n%_] _file/dir/all_]

## Description

When **fortune** is run with no arguments it prints out a random epigram. Epigrams are divided into several categories.

**Options**

The options are as follows:
**-a**

Choose from all lists of maxims.

**-e**

Consider all fortune files to be of equal size (see discussion below on multiple files).

**-f**

Print out the list of files which would be searched, but don't print a fortune.

**-l**

Long dictums only. See **-n** on how "long" is defined in this sense.
**-m** _pattern_
:   Print out all fortunes which match the basic regular expression _pattern_. The syntax of these expressions depends on how your system defines **re_comp**(3) or **regcomp**(3), but it should nevertheless be similar to the syntax used in **grep**(1).
:   The fortunes are output to standard output, while the names of the file from which each fortune comes are printed to standard error. Either or both can be redirected; if standard output is redirected to a file, the result is a valid fortunes database file. If standard error is _also_ redirected to this file, the result is _still valid_, **but there will be "bogus" fortunes**, i.e. the filenames themselves, in parentheses. This can be useful if you wish to remove the gathered matches from their original files, since each filename-record will precede the records from the file it names.

**-n** _length_
:   Set the longest fortune length (in characters) considered to be "short" (the default is 160). All fortunes longer than this are considered "long". Be careful! If you set the length too short and ask for short fortunes, or too long and ask for long ones, fortune goes into a never-ending thrash loop.

**-s**

Short apothegms only. See **-n** on which fortunes are considered "short".

**-i**

Ignore case for _-m_ patterns.

**-w**

Wait before termination for an amount of time calculated from the number of characters in the message. This is useful if it is executed as part of the logout procedure to guarantee that the message can be read before the screen is cleared.
The user may specify alternate sayings. You can specify a specific file, a directory which contains one or more files, or the special word _all_ which says to use all the standard databases. Any of these may be preceded by a percentage, which is a number _n_ between 0 and 100 inclusive, followed by a _%_. If it is, there will be a _n_percent probability that an adage will be picked from that file or directory. If the percentages do not sum to 100, and there are specifications without percentages, the remaining percent will apply to those files and/or directories, in which case the probability of selecting from one of them will be based on their relative sizes.

As an example, given two databases _funny_ and _not-funny_, with _funny_ twice as big (in number of fortunes, not raw file size), saying

:   **fortune** _funny not-funny_

will get you fortunes out of _funny_ two-thirds of the time. The command
:   **fortune** 90% _funny_ 10% _not-funny_

will pick out 90% of its fortunes from _funny_(the "10% not-funny" is unnecessary, since 10% is all that's left).

The **-e** option says to consider all files equal; thus

:   **fortune -e** _funny not-funny_

is equivalent to
:   **fortune** 50% _funny_ 50% _not-funny_

## Files

Note: these are the defaults as defined at compile time.

_/usr/share/games/fortune_
:   Directory for innoffensive fortunes.

_/usr/share/games/fortune/off_
:   Directory for offensive fortunes.

If a particular set of fortunes is particularly unwanted, there is an easy solution: delete the associated _.dat_ file. This leaves the data intact, should the file later be wanted, but since **fortune** no longer finds the pointers file, it ignores the text file.

## Bugs

The division of fortunes into offensive and non-offensive by directory, rather than via the '-o' file infix, is not 100% compatible with original BSD fortune. Although the '-o' infix is recognised as referring to an offensive database, the offensive database files still need to be in a seperate directory. The workaround, of course, is to move the '-o' files into the offensive directory (with or without renaming), and to use the **-a** option.

The supplied fortune databases have been attacked, in order to correct orthographical and grammatical errors, and particularly to reduce redundancy and repetition and redundancy. But especially to avoid repititiousness. This has not been a complete success. In the process, some fortunes may also have been lost.

The fortune databases are now divided into a larger number of smaller files, some organized by format (poetry, definitions), and some by content (religion, politics). There are parallel files in the main directory and in the offensive files directory (e.g., fortunes/definitions and fortunes/off/definitions). Not all the potentially offensive fortunes are in the offensive fortunes files, nor are all the fortunes in the offensive files potentially offensive, probably, though a strong attempt has been made to achieve greater consistency. Also, a better division might be made.

## History

This version of fortune is based on the NetBSD fortune 1.4, but with a number of bug fixes and enhancements.

The original fortune/strfile format used a single file; strfile read the text file and converted it to null-delimited strings, which were stored after the table of pointers in the .dat file. By NetBSD fortune 1.4, this had changed to two separate files: the .dat file was only the header (the table of pointers, plus flags; see _strfile.h_), and the text strings were left in their own file. The potential problem with this is that text file and header file may get out of synch, but the advantage is that the text files can be easily edited without resorting to unstr, and there is a potential savings in disk space (on the assumption that the sysadmin kept both .dat file with strings and the text file).

Many of the enhancements made over the NetBSD version assumed a Linux system, and thus caused it to fail under other platforms, including BSD. The source code has since been made more generic, and currently works on SunOS 4.x as well as Linux, with support for more platforms expected in the future. Note that some bugs were inadvertantly discovered and fixed during this process.

At a guess, a great many people have worked on this program, many without leaving attributions.

## See Also

**re_comp**(3), **regcomp**(3), **strfile**(1), **unstr**(1)

## Referenced By

**random**(6), **rot13**(6), **wtfindex**(6)