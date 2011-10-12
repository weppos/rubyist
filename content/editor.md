---
title: Editor Conventions
---

# Editor Conventions


## Indentation

Indentation MUST consist of 2 spaces. Tabs are not allowed.

Configure your editor to use Soft Tabs (replace tabs with spaces) or Spaces.
The most part of IDE and editors support this feature. [^w1]


## Whitespaces

Lines MUST have no trailing whitespace at the end.

You SHOULD use blank lines to group statements. It's RECOMMENDED to use only one empty line.


## Maximum Line Length

The target line length SHOULD be 80 characters.

Developers SHOULD strive keep each line of their code under 80 characters where possible and practical. However, longer lines are acceptable in some circumstances.


## Line Termination

Line termination follows the Unix text file convention. Lines MUST end with a single linefeed (LF) character. Linefeed characters are represented as ordinal 10, or hexadecimal 0x0A.

Note: Do not use carriage returns (CR) as is the convention in Apple OS's (0x0D) or the carriage return - linefeed combination (CRLF) as is standard for the Windows OS (0x0D, 0x0A).


[^w1]: [You should never use tab characters in source files](http://boredzo.org/blog/archives/2007-05-07/tabs-vs-spaces). The world will never come to an agreement on whether a tab character indents 8 spaces or 4, especially on the Mac, where lots of Unix tools (and Unix source code) are hard-coded for 8. So since different people will have their tab-width preferences set differently, just don’t use tab characters in your source code if you want everyone to be able to read it.
