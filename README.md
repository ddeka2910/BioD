# BioD [![Build Status](https://travis-ci.org/biod/BioD.svg?branch=master)](https://travis-ci.org/biod/BioD) [![DUB Package](https://img.shields.io/badge/dub-v0.1.0-red.svg)](https://code.dlang.org/packages/biod)

[BioD](https://github.com/biod/BioD) is a fast and memory efficient bioinformatics library written in the [D programming language](http://dlang.org).

BioD aims to:

* Provide a platform for writing high-performance bioinformatics applications in D. BioD achieves this by:
  - automatic parallelization of tasks where possible for example reading and writing BAM files
  - reducing the GC overhead by avoiding unnecessary memory allocations
* Offer support for manipulating common biological data formats

## Why D?

D is a language that suits parallel programming because of guarantees
the compiler provides. D is both a low-level language and a high-level
hybrid OOP/FP language. There is no other programming language that
matches those features. Also, D templating/generics is far easier that
that of C++.

That is not to say that D is an easy language. A powerful toolbox will
be complicated. If you want to do everything with a hammer, maybe
better choose Java instead ;).

For more information about D find Andrei Alexandrecu's D book. It is a
classic. Ali Çehreli's book also is recommended.

## Current development

Our current focus is to simplify the code base and move out material
that is either outdated or specific to sambamba.

We also want to provide a new bamreader and bamwriter that is really
fast and easy to use. We believe the BAM format is here to stay for
the foreseeable future in pipelines. With D we have an good way to
write performance parsers, particularly with three typical scenarios:

1. Go through a BAM file a read at a time
2. Go through a BAM file a nucleotide at a time (pileup)
3. Go through a BAM file with a sliding window

The sliding window is a derivation of the first - a read at a time or
a nucleotide at a time.

At this point this functionality is mostly in BioD, but not in an
intuitive way. We are building up this functionality and will give
examples (WIP).

# Install

The current default is to provide the path to the checked out repo to the D-compiler. For example
in sambamba we use

    DFLAGS = -wi -I. -IBioD -g

## Build environment

It is possible to create a recent build container with GNU Guix

    guix environment  -C guix --ad-hoc meson ninja ldc dub zlib gdb --network

and run meson and ninja (you may need the meson branch of BioD)

    dub
    meson ./build
    ninja -C ./build

to create a debug version

    meson build --buildtype debug --reconfigure

# Debugging

With gdb make sure to switch off the handlers

    handle SIGUSR1 SIGUSR2 nostop noprint

It can be passed in from the command line

    gdb -iex "handle SIGUSR1 SIGUSR2 nostop noprint" biod_test

# Usage

See the [examples directory](https://github.com/biod/BioD/tree/master/examples)
for examples and usage.

BioD is also a crucial part of the [sambamba](https://github.com/biod/sambamba) tool.

# Contributing

Simply clone the repository on github and put in a pull request.

# BioD contributors and support

See
[contributors](https://github.com/biod/BioD/graphs/contributors). For
support use the [issue tracker](https://github.com/biod/BioD/issues) or contact

* [Pjotr Prins](https://github.com/pjotrp)
* [Artem Tarasov](https://github.com/lomereiter)
* [George Githinji](https://github.com/George-Githinji)

# License

BioD is licensed under the liberal MIT (expat) [license](./LICENSE).
