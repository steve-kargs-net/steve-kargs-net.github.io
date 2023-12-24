---
id: 116
title: 'Interrupt Safe Ring Buffer Library'
date: '2008-10-25T10:35:21-05:00'
author: skarg
layout: post
guid: 'http://steve.kargs.net/?p=116'
permalink: /software/interrupt-safe-ring-buffer-library/
categories:
    - software
---

[![Christoper looks through a circular tube](http://steve.kargs.net/wp-content/uploads/2008/10/christhoper_circular-150x150.jpg "Christoper looks through a circular tube")](http://steve.kargs.net/wp-content/uploads/2008/10/christhoper_circular.jpg)

I created a [ring buffer](http://en.wikipedia.org/wiki/Circular_buffer) library for embedded systems in C some years ago and have been using it when I need to add a simple queue to my software. I knew it worked correctly since I [created unit tests](http://kargs.net/docs/simplest_unit_test.pdf) to validate the code. However, I noticed that it wasn’t interrupt safe since one of the consumer variables is shared by the producer (the count). This library requires disabling interrupts when consuming. Not what I wanted.

There are a [number of difficulties](http://en.wikipedia.org/wiki/Circular_buffer) when designing ring buffers, mostly dealing with efficiencies of code or data, or the struggle between consumers and producers. My generic ringbuf library had used a single fill count, but the count had to be updated by the [interrupt service routine](http://en.wikipedia.org/wiki/Interrupt_handler) (producer) and by the routine that retrieved the data (consumer). I tried to use read and write offset indices, but that required that I always keep an element open since the you can’t tell if the ring is empty or full when the head and tail are the same.

Absolute indices appeared to be interrupt safe, although they require that the buffer length be a power of two. That seemed to be flexible enough for most embedded work. I modified and tested my ring buffer library using that method, but my ringbuf, which allowed for a fixed length element, seemed to be overkill for what I was using it for – gathering bytes from a serial interrupt service routine. Its [API](http://en.wikipedia.org/wiki/API) also had a slight flaw such that if the consumer retrieved the data (via [Pop](http://en.wikipedia.org/wiki/Push_and_pop) rather than just viewing the first element), the producer was free to put new data into the buffer, overwriting the data just retrieved.

I had started my ring buffer library as a simple character (one byte) [FIFO](http://en.wikipedia.org/wiki/FIFO) – first in, first out. So, I revisited that code, and modified it to use absolute indices. A simple byte ring buffer, first in, first out. Now I had interrupt safe code that would work in my serial interrupt service routine.

Why go to the trouble to make a library module to handle a ring buffer when slapping the following [quick and dirty ring buffer code](http://www.embeddedrelated.com/usenet/embedded/show/77084-1.php) (from Stefan) into the serial module would have worked as well?

```
   #define N 128
   volatile unsigned int head, tail;
   volatile char buffer[N];
   unsigned int inuse() { return head - tail; }
   void put(char c) { if (inuse() != N) { buffer[head++%N] = c; } }
   void get(char* c) { if (inuse() != 0) { *c = buffer[tail++%N]; } }
```

Because I needed to know that it worked correctly, and I like reusable library modules. Especially high quality reusable modules. Especially high quality reusable modules that include unit tests to validate functionality. Unit tests that also serve as guides for implementers.

The new module files are [ringbuf.c](http://kargs.net/code/ringbuf.c) and [ringbuf.h](http://kargs.net/code/ringbuf.h) for the ring buffer with fixed sized elements, and [fifo.c](http://kargs.net/code/fifo.c) and [fifo.h](http://kargs.net/code/fifo.h) for the ring buffer with byte sized elements. All my versions of the ring buffer and the [unit testing framework](http://kargs.net/docs/simplest_unit_test.pdf) can be found in the [ringbuf.zip](http://kargs.net/code/ringbuf.zip) file.

One of my original non-interrupt safe ringbuffer libraries that uses a count can be found in the [ringbuf.tgz](http://www.kargs.net/code/ringbuf.tgz) file archive. Another buffer library I wrote is a linked list that is sorted by key as elements are added, and the elements can be retrieved by key, index, or FIFO. This [keylist library](http://www.kargs.net/code/keylist.tgz) is useful for caching dynamic data by key.