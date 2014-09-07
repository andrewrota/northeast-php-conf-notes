# Under the Hood of the HHVM JIT Compiler
**By Ed Smith**

Facebook switched to a C++ Cross Compiler in 2009-2012 timeframe and cut CPU use in half

But the problem with the cross compiler is that it takes a long time to compile your binary

2011-2012 they had already started working on a PHP virtual machine w/ JIT

Virtual machine gives you best of both worlds.  High CPU performance becuase you can watch the code as it runs, and that happens very quickly

The overall plan of HHVM is to load up the code and run it and see what it's doing.  If you don't watch what a dynamically typed language does you have to look at every step and see what it does.  So we want to fire up the code, watch it run.  In HHVM this is done with traclets, which are small pieces of code which watches what types are being passed into it and you can generate optimized code from that.

Use static single assignment at each of these levels.  It's taking your PHP program and turning it into a functional program, where each assignment only happens once.

Traclets --> HHIR high level representation --> VASM low level representation --> LLVM more low level virtual machine --> machine code into X64 asm tracelet cache

Using Hack reduces the time to discover type changes during dev but doesn't speed up compiliation (yet).

If you were designing the system from scratch you wouldn't have VASM in the process.  They were able to get VASM up and running fairly quick and it turned out that those changes that had to be made were the sames one made to use LLVM.  SO they made one stage to another.  More software engineering problem then compiler problem.

HHVM cannot yet do tail recursion optimization.

Safari webkit JIT for JavaScript has four compilers in it (last one is LLVM)

