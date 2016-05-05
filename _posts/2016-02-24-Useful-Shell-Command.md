---
layout: post
title:  "Useful Shell Commands"
date:   2016-02-24
author: rossi
categories: Python Compiler
---

Some Useful Command

* xargs

xargs
------
+ Execute utility to take every line as an input parameter

      cat <fileName> | xargs -L 1 <command>

  The -L number options from man page:

  __*Call utility for every number non-empty lines read.  A line ending with a space continues to the next non-empty line.*__

  Examples :

      echo "hello" > test.txt
      echo "world" >> test.txt
      echo "hahaha" >> test.txt
      cat test.txt | xargs -L 1 echo

  The result is :

      hello
      world
      hahaha

  If you change the line numbers:

      cat test.txt | xargs -L 2 echo

  The result is :

      hello world
      hahaha

  __*If EOF is reached and fewer lines have been read than number then utility will be called with the available lines.*__
  
+ Replace the parameter (read from pipeline stdout) to a placeholder

      cat <fileName> | xargs -L 1 -I 'placeholder' stat 'placeholder' >statfile.txt
      # truncate log files
      ls | grep XXX.log | xargs -I 'log' truncate -s 0 'log'

  If there's too much `'` the command may break. For example, if we want to clean the log as below:

      ls | grep XXX.log | xargs -I 'log' echo '' > 'log'

  Will create an empty file named `log` instead truncate it. But you can use `sh -c "COMMAND"` to do this

      ls | grep XXX.log | xargs -I 'log' sh -c "echo '' > log"


