---
layout: post
title: "What's new in C++11"
date: 2014-07-30 18:47:52 -0700
comments: true
categories: 
- C++11
- programming
---

I heard a lot of cool things about the new features and here is what I came across so far:

## New Keywords

* #### "long long"

   C++11 defines a new integer type "long long", which is guaranteed to be at least 64 bits in length. The largest integer type "long" defined in C++03 is platform specific, so can be 32 or 64 bits in length. Just a heads up, C99 and other compliers already supported it even before C++11.

* #### "auto"

  Automatic type inteference has been introduced using "auto" keyword.

  {% codeblock Previously in C++03 lang:c++ %}
  int a = 10;
  float b = 20.5;
  int c = a;
  string s = "test";
  vector<int> v;
  v.push_back(1);
  v.push_back(2);
  for (vector<int>::iterator itr = v.begin(); itr != v.end(); itr++) {...}
  {% endcodeblock %}

  {% codeblock New in C++11 lang:c++ %}
  auto a = 10;                 // a is infered to be of type int
  float b = 20.5;              // b is infered to be of type float
  int c = a;                   // c is infered to be of type int
  string s = "test";           // s is infered to be of type const char *
  vector<int> v;
  v.push_back(1);
  v.push_back(2);
  auto d = v[0];               // d is infered to be of type int
  for (auto itr = v.begin(); itr != v.end(); itr++) {...}	// itr is infered to be of type vector<int>::iterator
  {% endcodeblock %}

* #### "decltype"

  To know the type of an expression at the compile time. For eg,

  {% codeblock New in C++11 lang:c++ %}
  decltype(a) a2;              // a2's type is int since a is of type int (above)
  const int&& fun();
  decltype(fun()) e;           // e's type is const int&&
  decltype(b) b2 = 0.5;        // b2's type is float since b is of type float (above)
  {% endcodeblock %}

* #### "nullptr"

  No more initializing pointers with NULL which can both act as an int or int * leading to oddity.

  {% codeblock New in C++11 lang:c++ %}
  int *f = nullptr;
  auto g = NULL;
  {% endcodeblock %}

* #### "enum class"

  enums have got an upgrade too and now they are type safe

  {% codeblock Previously in C++03 lang:c++ %}
  enum SPORTS {BADMINTON, TENNIS};
  enum PERSON {EMILY, BOB};
  if (BADMINTON == EMILY) {}   // if condition will evaluate to true
  {% endcodeblock %}

  {% codeblock New in C++11 lang:c++ %}
  enum class SPORTS {BADMINTON, TENNIS};
  enum class PERSON {EMILY, BOB};
  if (SPORT::BADMINTON == PERSON::EMILY) {}   // if condition will evaluate to false
  {% endcodeblock %}

