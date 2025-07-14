---
title: Linux入门
date: 2022-05-15 18:34:12
tags:
- 操作系统
- Linux
categories:
- 学习
- 操作系统
---

## 1.Linux Manual

#### > command  --help

to see the  usage of the command.

PS : `man command ` is more specific.

EX:  `date  --help`  、`man  date`

<!-- more -->

#### > command  [options1|options2 ]  <SOMETHING>...

`[options1|options2 ]` means optional , but can't  be both.

`<SOMETHING>` means things mandatory(required).

`...`   means repeatable.

*`SOMETHING`* means things should be replaced with whatever is appropriate.

ex:  `which   [-a|-f ]   date cal`



----



## 2.Standard Input And Output

> cat  1> /dev/output.txt   2>&1  

**/dev/output.txt  represents output files**
` > `   means redirection ，ex ：echo "123" > /home/123.txt
`1`   means standard output. The system default value is 1, therefore ">/dev/null" equals "1>/dev/null"
`2`   means standard error.
`&`   means equal.

`2>&1` means the  redirection of 2 is the same as 1.



> cat  1>>  /dev/output.txt   2>&1 

  `>>`  means appending，`>`  means override



> cat < output.txt

`<`   means outputting the contents of ourput.txt 



---



## 3.Piping

> date | cut  --delimiter " " --fields 1

It means :  A. date 1>date.txt   B. cut <date.txt --delimiter " " --fields 1

The date.txt was piped from A  to B .



> date | tee date.txt |cut  --delimiter " " --fields 1

`tee`  add a intermediate output in piping.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/2/24/Tee.svg/400px-Tee.svg.png)

> date | xargs echo

`xargs` convert the data from standard output into command  arguments



---

## 

## 10.Unique commands

| commands  | meanings                           |
| --------- | ---------------------------------- |
| history 4 | list the latest 4 command history. |
|           |                                    |
|           |                                    |

