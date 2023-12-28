---
id: 79
title: 'C/C++ Compiler Macros'
date: '2007-11-27T14:21:26-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/software/cc-compiler-macros/'
permalink: /software/cc-compiler-macros/
categories:
    - software
---

[![cityscape_night.png](http://steve.kargs.net/wp-content/uploads/2007/thumbs/cityscape_night.png "cityscape_night.png")](http://steve.kargs.net/wp-content/uploads/2007/cityscape_night.png)

Every once in awhile, I need a macro to work around a difference in a C compiler.

For example, not every compiler for the Win32 platform has implemented C99 integer and boolean types, so I have [stdint.h](http://bacnet.svn.sourceforge.net/viewvc/*checkout*/bacnet/trunk/bacnet-stack/ports/win32/stdint.h) and [stdbool.h](http://bacnet.svn.sourceforge.net/viewvc/*checkout*/bacnet/trunk/bacnet-stack/ports/win32/stdbool.h) files. Fortunately, The Open Group maintains an online definition for [stdint.h](http://www.opengroup.org/onlinepubs/009695399/basedefs/stdint.h.html) and [stdbool.h](http://www.opengroup.org/onlinepubs/009695399/basedefs/stdbool.h.html) so I don’t have to guess about what is supposed to go in there. C99 also defines some new keywords: `restrict`, `inline`, `_Complex`, `_Imaginary`, `_Bool`. Since `_Bool` is used by stdbool.h, it may or may not have been defined by the compiler. What I needed was a macro defined by the compiler that tells me which compiler it is so I can avoid compiler warnings.

Digging up the compiler macros on the internet can be challenging. However, there is a nice project at SourceForge to track [Pre-defined C/C++ Compiler Macros.](http://predef.sourceforge.net/)

That makes things a whole lot easier!