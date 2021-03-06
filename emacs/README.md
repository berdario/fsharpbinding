# Experimental support for Intellisense in Emacs

## December 2012

Removed old intellisense approach. File manifest now as follows:

intelli_tip.el             - old tooltip generation, currently disabled
intellisense2.el           - new intellisense, uses autocomplete
readme-intellisense.txt    - this file
test.fs                    - simple small test script, to be moved
test.py                    - python script for feeding in test scripts

-- Robin Neatherway


## October 2012

This code has been imported with minor changes from Sourceforge. There are some caveats.

1. There are dependencies on esense, and tooltip-help.el. Modified versions are present in this directory (intellisense.el and intelli_tip.el respectively).

2. Communication between emacs and the fsintellisense.exe subprocess are working, but the results are not always interpreted correctly.

I intend to update the code to remove the dependencies above, using autocomplete instead of esense, and emacs' builtin tooltips. In the fullness of time, multi-file projects should also be supported.

-- Robin Neatherway


## February 2011



## Getting started


1. fsintellisense.exe is a program which communicates with F# compiler to
get all the Intellisense information. The first step is to make sure you
can run it. When you execute it, it should read commands on standard
input. Enter a random line and you should get "ERROR: Unknown command or
wrong arguments".

If you get an exception, you can copy FSharp.Compiler.dll and
FSharp.Compiler.Server.Shared.dll from F# (November release) into current
directory.

2. Edit intellisense.el and edit the intellisense-wrapper value to the actual
path.

3. Load intellisense.el <kbd>M-x load-file</kbd>

4. Open a F# buffer. Then <kbd>M-x start-intellisense</kbd> will run
fsintellisense.exe in background. You can play with those (temporary)
bindings:
  F1: display a tool-tip at point
  F2: do completion (also appears when you enter a dot)
  F4: display error messages from compiler


## Recompiling fsintellisense.exe

Here is the command-line I use:
  `fsc.exe fsharpcompiler.fs tipFormatter.fs parser.fs program.fs -r "FSharp.Powerpack.dll"`



## Documentation

fsintellisense.exe is a modified version of the Compiler example you can
get here:

    http://fsxplat.codeplex.com

In particular, this documentation is very useful:

   http://fsxplat.codeplex.com/wikipage?title=fsharp%20intellisense%20tool&referringTitle=Home



## Bugs / Limitations / TODO

- It's not yet possible to add references (external dll files). I think
  the fsintellisense already handles it, so it should be easy to add.

- Completion works only on current buffer. We need a way to specify a
  project and give a list of source files.

- Error messages are not reported. We should display them in the code
  (underline errors in the buffer?)

