---
layout: default
title:  "Bash Cheatsheet"
date:   Thu, Aug 12, 2021 12:00:35
categories: Bash
---

<hr/>

  _Do the easy tasks first._

<hr/>

- [1. Shortcuts](#1-shortcuts)
  - [1.1. Navigation](#11-navigation)
  - [1.2. Editing](#12-editing)
  - [1.3. History](#13-history)
  - [1.4. Process control](#14-process-control)
  - [1.5. Bang(!)](#15-bang)
- [2. if](#2-if)
- [3. Checks](#3-checks)
  - [3.1. Boolean operators](#31-boolean-operators)
  - [3.2. Checking files:](#32-checking-files)
  - [3.3. Check strings](#33-check-strings)
  - [3.4. Check numbers](#34-check-numbers)
- [4. Snippets](#4-snippets)
  - [4.1. Get current script directory](#41-get-current-script-directory)
  - [4.2. Check if running as root](#42-check-if-running-as-root)
- [5. References](#5-references)

# 1. Shortcuts

## 1.1. Navigation

| | |
|-|-|
| Ctrl + a | Go to the beginning of the line (Home) |
| Ctrl + e | Go to the End of the line (End) |
| Alt + b | Back (left) one word |
| Alt + f | Forward (right) one word |
| Ctrl + f | Forward one character |
| Ctrl + b | Backward one character |
| Ctrl + xx | Toggle between the start of line and current cursor position |

## 1.2. Editing

| | |
|-|-|
| Ctrl + u | Cut the line before the cursor position |
| Alt + Del | Delete the Word before the cursor |
| Alt + d | Delete the Word after the cursor |
| Ctrl + d | Delete character under the cursor |
| Ctrl + h | Delete character before the cursor (backspace) |
| Ctrl + w | Cut the Word before the cursor to the clipboard |
| Ctrl + k | Cut the Line after the cursor to the clipboard |
| Alt + t | Swap current word with previous |
| Ctrl + t | Swap the last two characters before the cursor (typo) |
| Esc + t | Swap the last two words before the cursor. |
| Ctrl + y | Paste the last thing to be cut (yank) |
| Alt + u | UPPER capitalize every character from the cursor to the end of the current word. |
| Alt + l | Lower the case of every character from the cursor to the end of the current word. |
| Alt + c | Capitalize the character under the cursor and move to the end of the word. |
| Alt + r | Cancel the changes and put back the line as it was in the history (revert) |
| ?trl + _ | Undo |

## 1.3. History

| | |
|-|-|
| Ctrl + r | Recall the last command including the specified character(s)(equivalent to : vim ~/.bash_history).  |
| Ctrl + p | Previous command in history (i.e. walk back through the command history) |
| Ctrl + n | Next command in history (i.e. walk forward through the command history) |
| Ctrl + s | Go back to the next most recent command. |
| Ctrl + o | Execute the command found via Ctrl+r or Ctrl+s |
| Ctrl + g | Escape from history searching mode |
| Alt + . | Use the last word of the previous command |

## 1.4. Process control

TODO

## 1.5. Bang(!)

Bash also has some handy features that use the ! (bang) to allow you to do some funky stuff with bash commands.

| | |
|-|-|
| !! | run last command |
| !blah | run the most recent command that starts with ‘blah’ (e.g. !ls) |
| !blah:p | print out the command that !blah would run (also adds it as the latest command in the command history) |
| !$ | the last word of the previous command (same as Alt + .) |
| !$:p | print out the word that !$ would substitute |
| !* | the previous command except for the last word (e.g. if you type ‘find some_file.txt /‘, then !* would give you ‘find some_file.txt‘) |
| !*:p | print out what !* would substitute |

# 2. if

```sh
if [ $num -lt 10 -o $num -gt 100 ]; then
    echo "Number $num is out of range"
elif [ ! -w $filename ]
then
    echo "Cannot write to $filename"
else
    echo "Something else"
fi
```

# 3. Checks

## 3.1. Boolean operators

| Operator | Meaning |
| -- | -- |
| ! |  not |
| -a | and |
| -o | or |

## 3.2. Checking files:

Check | Meaning
-- | --
-r file | Check if file is readable.
-w file | Check if file is writable.
-x file | Check if we have execute access to file.
-f file | Check if file is an ordinary file (as opposed to a directory, a device special file, etc.)
-s file | Check if file has size greater than 0.
-d file | Check if file is a directory.
-e file | Check if file exists. Is true even if file is a directory.

## 3.3. Check strings

| Check | Meaning |
| -- | -- |
| s1 = s2 |  Check if s1 equals s2 |
| s1 != s2  |  Check if s1  doesn't equal s2 |
| -z s1  |  Check if s1  has size 0 |
| -n s1  |  Check if s1  has nonzero size |
| s1  |  Check if s1  is not the empty string |

## 3.4. Check numbers

| Check | Meaning |
| -- | -- |
| n1 -eq n2 | Check to see if n1 equals n2. |
| n1 -ne n2 | Check to see if n1 is not equal to n2. |
| n1 -lt n2 | Check to see if n1 < n2. |
| n1 -le n2 | Check to see if n1 <= n2. |
| n1 -gt n2 | Check to see if n1 > n2. |
| n1 -ge n2 | Check to see if n1 >= n2. |

# 4. Snippets

## 4.1. Get current script directory

```sh
SCRIPT_DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
```

## 4.2. Check if running as root

```sh
if [ "$EUID" -eq 0 ]; then
fi
```

# 5. References

- [Bash Shortcuts For Maximum Productivity](http://www.skorks.com/2009/09/bash-shortcuts-for-maximum-productivity/)
- [Syntax Bashkeyboard](http://ss64.com/osx/syntax-bashkeyboard.html)
- [Moving efficiently in the CLI](https://clementc.github.io/blog/2018/01/25/moving_cli/)
