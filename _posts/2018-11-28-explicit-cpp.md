---
layout:     post
title:      explicit qualifier in cpp
date:       2018-11-28 11:21:29
summary:    This is post acts as note about explicit qualifier in cpp
categories: cpp
---


`explicit` specifies that a constructor or conversion function is explicit, that is,
it cannot be used for implicit conversions and copy-initialization.

The `explicit` specifier *may* only appear within the *decl-specifier-seq* of the declaration
of a constructor or conversion function within constructor.

A constructor with a single non-default parameter that is declared without the function specifier
`explicit` is called a **converting constructor**

Both constructors (other than copy/move) and user-defined conversion functions may be function
template; the meaning of explicit does not change.

### Usage

```cpp
struct S {
  explicit (S)(const S&);     // error in C++20, OK in C++17
  explicit (operator int)();  // error in C++20, OK in C++17
};

struct A {
  A(int) {}       // converting constructor
  A(int, int) {}  // converting constructor (C++11)
  operator bool() const { return true; }
};

struct B {
  explicit B(int) {}
  explicit B(int, int) {}
  explicit operator bool() const { return true; }
};

```

### Notes

In C++, if a class has a constructor which can be called with a single argument, then this
constructor becomes conversion constructor because such a constructor allows conversion of
single argument to the class being constructed

We can avoid such implicit conversions as these may lead to unexpected results. We can make
constructor explicit with the help of explicit keyword

Examples are similar to the ones from cpp reference website

#### References

https://en.cppreference.com/w/cpp/language/explicit
https://www.geeksforgeeks.org/g-fact-93/