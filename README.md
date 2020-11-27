# PeekPoke::FFI [![Build Status](https://travis-ci.org/PerlFFI/PeekPoke-FFI.svg)](http://travis-ci.org/PerlFFI/PeekPoke-FFI) ![windows](https://github.com/PerlFFI/PeekPoke-FFI/workflows/windows/badge.svg) ![macos](https://github.com/PerlFFI/PeekPoke-FFI/workflows/macos/badge.svg)

Perl extension for reading and writing to arbitrary memory locations

# SYNOPSIS

```perl
# function interface
use PeekPoke::FFI qw( peek poke );
my $value = peek( 0xdeadbeaf );
poke( 0xdeadbeaf, $value + 1 );

# OO-interface
use PeekPoke::FFI;
my $pp = PeekPoke::FFI->new( type => 'sint32', base => 0xdeadbeaf );
my $value = $pp->peek( 0xdeadbeaf );
$pp->poke( 0xdeadbeaf, 0 - $value );
```

# DESCRIPTION

Very occasionally I need to get/set bytes from arbitrary bits of memory
from a Perl script or module.  If you know what you are doing it isn't
too tricky to get an arbitrary byte from Perl.  Setting one is a little
harder, but can be done with tricks.  This module implements these tricks
so that I don't have to remind myself of how to do it the next time I
need to reach for this particular tool.

# CONSTRUCTOR

## new

```perl
my $pp = PeekPoke::FFI->new(%opts);
```

Create a [PeekPoke::FFI](https://metacpan.org/pod/PeekPoke::FFI) instance.  If you need to get/set values other than bytes, or
if you want to set a base address, then you will want to create

- type

    The [FFI::Platypus](https://metacpan.org/pod/FFI::Platypus) type to use for peeking and poking.  Defaults to `uint8`.
    Only integer and floating point types are supported.

- base

    The base address to use.  The offset will be added to this value.

# METHODS

## peek

```perl
my $value = $pp->peek($offset);
my $value = peek($offset);
```

Get the value at the given offset.

## poke

```
$pp->poke($offset, $value);
poke($offset, $value);
```

Set the value at the given offset.

# CAVEATS

Most of the time you shouldn't be peeking and poking at random bits of memory.
Sometimes during development it can be useful for various reasons.  Use with
extreme caution in production.

# SEE ALSO

- [PeekPoke](https://metacpan.org/pod/PeekPoke)

    This is an XS module that has been around for donkey's years.  It only works
    with the native Perl integer values (IV) which is not usually what I want.

- [Proc::Memory](https://metacpan.org/pod/Proc::Memory)

    BASIC style Peek/Poke via [Alien::libvas](https://metacpan.org/pod/Alien::libvas).

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2020 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
