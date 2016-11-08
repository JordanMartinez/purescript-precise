# purescript-precise

[![Latest release](http://img.shields.io/github/release/purescript-contrib/purescript-precise.svg)](https://github.com/purescript-contrib/purescript-precise/releases)
[![Build status](https://travis-ci.org/purescript-contrib/purescript-precise.svg?branch=master)](https://travis-ci.org/purescript-contrib/purescript-precise)

This is a library for working with numbers of arbitrarily finite size.

Javascript (and to some extension Purescript) has quite a few drawbacks when it comes to large numbers. For example, Purescript's `Int` primitive [is a member](https://github.com/purescript/purescript-prelude/blob/v0.1.3/src/Prelude.js#L177-L178) of the `Bounded` typeclass, with `top == 2 ^ 31 - 1` and `bottom == - (2 ^ 32)`.

The Purescript `Number` primitive is not `Bounded` in the same way; however, there are problems with manipulating large-enough `Number`s:

```
> import Prelude
> let x = 900000000000000000.0
> :t x
Number

> x + 1.0 == x
true
> x + 1.0
900000000000000000
```

In this library, correctness is prioritized above all else:

```
> import Data.HugeNum
> let x = fromNumber 900000000000000000.0
> let y = fromNumber 1.0
> x + y == x
false

> x + y
HugeNum 900000000000000001.0
```

Addition is implemented using an elementary-school method. Multiplication follows [Karatsuba](https://en.wikipedia.org/wiki/Karatsuba_algorithm).

## Installation

```
bower install purescript-precise
```

## Documentation

Module documentation is [published on Pursuit](https://pursuit.purescript.org/packages/purescript-precise/).
