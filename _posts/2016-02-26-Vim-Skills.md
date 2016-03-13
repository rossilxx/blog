---
layout: post
title:  "Vim Skills"
date:   2016-02-24
author: rossi
categories: vim tools 
---

# Plugins #

# Commands #

## Delete ##

+ Delete inside quotes.
  
       di"
  
  This will 'd'elete everythin 'i'nside the `'"'` quote. You can use this command when the cursor is in the `"` quote.

## Indent ##

+ Enable auto indent
  Add this in your ~/.vimrc
  
      filetype plugin indent on
  
+ Disable auto indent when pasting
  
  Sometimes when we paste already indented code, we want to disable auto indent, you can use these commands:
  
      :set paste
  
  And you can enable it after you finish your pasting
  
      :set nopaste
  
+ Indent blocks manually
  
  1st, select block through Visual block command `<C-v>`, or use `V` to select the first line, and press `j` to select the rest
  
  2nd, press `>` to increast the indent and press `<` to decrease the indent
