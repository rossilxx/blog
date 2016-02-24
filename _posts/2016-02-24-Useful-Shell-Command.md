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
