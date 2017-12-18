# os-malloc
This directory contains:

myAllocator.c: a first-fit allocator
myAllocator.h: its header file

myAllocatorTest1.c: a test program for my allocator

malloc.c: a replacement for malloc that uses my allocator
test1.c: a test program that uses this replacement malloc

There are two different testers as some implementations of printf
call malloc to allocate buffer space. This causes test1 to behave
improperly as it uses myAllocator as a malloc replacement. In this
case myAllocatorTest1 will function correctly. The only difference
between the programs is that test1 uses myAllocator as a malloc
replacement and myAllocatorTest1 uses myAllocator directly.

Makefile: a fairly portable "makefile", targets "all" and "clean"

To compile:
 $ make
To clean:
 $ make clean
To run:
 $ ./myAllocatorTest1

The cygwin runtime uses malloc() and brk() extensively.  It is
interesting to compare the output of test1 & myAllocatorTest1.  All
those extra allocated regions are being used by cygwin's libraries!

# Source Code by Ana J. Garcia

I added a function called findBestFit(size_t s) that finds the "best fit" in the
arena in which a memory block of size s would fit.

findBestFit(size_t s) will search the arena for a region of size at least s, and
compute the remaining space (if any) in this block of memory and save it
to spaceDiff. After traversing the arena, findBestFit will return a prefix to
the block of memory that wastes the least space. (See the function's comments
for more detail under the file myAllocator.c).

I added some modifications to resizeRegion() that allow for resizing an already
allocated region to the requested size when possible, instead of just allocating
a new (larger) region and copying the entire contents of the old region into
the new one.

I received help from Jose Cabrera in understanding how resizeRegion works and we
went over the algorithm to follow in order to modify it.

I received help from Hector Cervantes in implementing findBestFit() and fixing
a bug in that function.
