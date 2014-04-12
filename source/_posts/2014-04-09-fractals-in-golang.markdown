---
layout: post
title: "Fractals in GoLang"
date: 2014-04-09 23:16:18 -0700
comments: true
categories: 
- fractals
- recursion
- programming
- GoLang
---

I wanted to explore [Fractals](http://en.wikipedia.org/wiki/Fractal) ever since my friend [Avijit](https://github.com/avijitgupta) told me about them. I found them fascinating. Just one equation and you can do wonders with it. It is more fascinating to know how nature uses recursion/fractals in things like trees, leaves, corals and even broccoli !! Here are some interesting fractals I generated using [Mandelbrot Set](http://en.wikipedia.org/wiki/Mandelbrot_set):

{% img https://raw.githubusercontent.com/piyush-kansal/fractals-in-go/master/output/fractal_1000.000000_0.000000_0.000000.png 'zoom=1000, real=0, imag=0' %}

{% img https://raw.githubusercontent.com/piyush-kansal/fractals-in-go/master/output/fractal_100000.000000_-0.710000_-0.250000.png 'zoom=100000, real=-0.71, imag=-0.25' %}

{% img https://raw.githubusercontent.com/piyush-kansal/fractals-in-go/master/output/spiral_10000_0.040000_0.999900.png 'iter=10000, degree=0.04, factor=0.9999' %}

Here is the [implementation](https://github.com/piyush-kansal/fractals-in-go).
