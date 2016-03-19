---
layout: post
title:  "Python misc"
date:   2016-03-19
author: rossi
categories: Python misc
---

subprocess
----
* You man want to use subprocess.Popen to execute another program. Please notice that every list item in the arguments you passed to Popen will be treated as an single parameter. If you put two parameters in one item and seperated with an whitespace, an quote `"` will added to your argument. Here is the example:

      proc = subprocess.Popen(['ls', '-l', 'css']])

	  -rw-r--r--  1 liuxiaoxi  staff  1063 Feb 19 12:51 main.scss

	  proc = subprocess.Popen(['ls', '-l css']])

	  ls: illegal option --  

  The first will execute cmd `ls -l css` and the second will execute cmd `ls "-l css"`. Because there is an whitespace in the arg and Popen will add an quote to ensure take it as an whole string. Here is the source code from Python

		needquote = (" " in arg) or ("\t" in arg) or not arg
			if needquote:
				result.append('"')
				.....

			if needquote:
				result.append('"')

range vs xrange
-----
* xrange vs range<br>xrange make a little performance optimize based on range. It will not return an int list for iterate, instead it return an new type *PyRange_Type* which has an iterator. Here is what range(*x*) does from python source code:

      v = PyList_New(n);
      if (v == NULL)
        return NULL;
	  for (i = 0; i < n; i++) {
		  PyObject *w = PyInt_FromLong(ilow);
		  if (w == NULL) {
			  Py_DECREF(v);
			  return NULL;
		  }
		  PyList_SET_ITEM(v, i, w);
		  ilow += istep;
	  }
	  return v;

  And here is what xrange does. It will return an object of type PyRange_Type which has an iterator


      PyTypeObject PyRange_Type = {                                                                                        
	    PyObject_HEAD_INIT(&PyType_Type)                                                                                 
	    0,                          /* Number of items for varobject */
	    "xrange",                   /* Name of this type */
	    sizeof(rangeobject),        /* Basic object size */
		..
		..
		range_iter,                 /* tp_iter */

  And this iterator has an next function like this:

      rangeiter_next(rangeiterobject *r)
	  {
        if (r->index < r->len)
		return PyInt_FromLong(r->start + (r->index++) * r->step);
		return NULL;
	  }

  Here we will not deep into all the detail of this source code, just illustrate how the xrange works.
