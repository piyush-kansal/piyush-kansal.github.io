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
  for (auto itr: v) {cout << itr;}                              // Another easier way to do the same, called range-based 
                                                                // for statement. itr is read only here
  for (auto& itr: v) {cout << ++itr;}                           // Another easier way to do the same, called range-based 
                                                                // for statement. itr is writable here
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

* #### "static_assert"

  C++11 defines a new compile time assert.

  {% codeblock New in C++11 lang:c++ %}
  static_assert(sizeof(int) == 4, "This program cannot be run on machines not supporting integer to be 4 bytes long");
  {% endcodeblock %}

* #### "default", "delete", "final" and "override"

  All of these 4 new additions are w.r.t. to the inheritance constructs:

##### "default"

  To explicity tell the compiler to provide the default constructor. The only use I see is the enhanced readability.

  {% codeblock New in C++11 lang:c++ %}
  class Temp {
     public:
        Temp() {}            // Own implementation of the default constructor
        Temp() = default;    // Explicitly ask compiler to provide the implementation
  };
  {% endcodeblock %}

##### "delete"

  To not to allow anyone call a function. It is definitely very useful.

  {% codeblock New in C++11 lang:c++ %}
  class Temp {
     public:
        Temp() {}
        Temp(const Temp&) = delete;          // Does not allow copy construction
        Temp& Temp(const Temp&) = delete;    // Does not allow assignment operation
  };
  {% endcodeblock %}

##### "final"

  To not to allow anyone override a virtual function or inherit from class. Looks kind of odd :)

  {% codeblock New in C++11 lang:c++ %}
  class B {
     public:
        virtual f() final;     // Overriding not allowed
  };

  class D {
     public:
        virtual f();           // Compiler error
  };

  class B2 final {};           // Inheriting not allowed
  class D2 : public B2 {};     // Compiler error
  {% endcodeblock %}

##### "override"

  To explicity tag functions we intend to override in a derived class class. Definitely useful.

  {% codeblock New in C++11 lang:c++ %}
  class B {
     public:
        virtual void f();
        virtual void g();
        void h();
  };

  class D {
     public:
        virtual void f(int) override;    // Compiler error
        virtual void g() override;       // Okay
        void h() override;               // Compiler error
  };
  {% endcodeblock %}

## Initializer Lists

  C++11 patches up the inconsistency between initializing simple data types and containers:

  {% codeblock Previously in C++03 lang:c++ %}
  int v[3] = {0, 1, 2};
  struct PERSON {int id; string name};
  PERSON p = {1, "EMILY"};
  vector<int> v2[3] = {0, 1, 2};          // Not possible in C++03
  {% endcodeblock %}

  {% codeblock New in C++11 lang:c++ %}
  vector<int> v2[3] = {0, 1, 2};          // Possible in C++11
  {% endcodeblock %}

  The way it works is that it calls the constructor std::vector<int>(std::initializer_list<int>). std::initializer_list is a new template class. So, you can add this into your container classes as well:

  {% codeblock New in C++11 lang:c++ %}
  class MyVector {
     vector<int> v;

     public:
        MyVector() {}
        MyVector(std::initializer_list<int>& l) {
           for(auto i: l) v.push_back(i);
        }
  };
  {% endcodeblock %}

## Uniform Initialization

  {% codeblock New in C++11 lang:c++ %}
  vector<int> v(3);         // Creates a vector of size 3 with uninitialized elements
  vector<int> v{3, 2, 1};   // Creates a vector of size 3 with elements 3, 2, 1. This is called uniform initialization
  {% endcodeblock %}

  This concept can be used during the function calls and while returning from the functions too:

  {% codeblock New in C++11 lang:c++ %}
  vector<int> myfunc(vector<int> v) {
     return {1, 2, 3};
  }

  myfunc({3, 2, 1});
  {% endcodeblock %}

## Delegating Constructors

  It is now possible to call an another constructor from the first one i.e we can chain constructors:

  {% codeblock New in C++11 lang:c++ %}
  class MyVector {
     public:
        MyVector() {
           // accomplishes task A
        }
        MyVector(int a): MyVector() {
           // accomplishes task A and B
        }
        MyVector(int a, int b): MyVector(a) {
           // accomplishes task A, B and C
        }
  };
  {% endcodeblock %}
