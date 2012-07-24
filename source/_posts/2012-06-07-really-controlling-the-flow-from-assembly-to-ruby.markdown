---
layout: post
title: "Really Controlling the flow: from Assembly to Ruby"
date: 2012-06-07 13:37
comments: true
categories: [Assembly, Ruby, Cheatsheet]
author: Geoff Tidey
---

I've recently been converting a bunch of [Assembly](http://www.cs.virginia.edu/~evans/cs216/guides/x86.html) code into Ruby.  ZOMG Why, Why, Why?  You may well ask.  Well the Assembly code is [Intel x86 flavoured](http://en.wikipedia.org/wiki/X86_assembly_language), it's never been run on Linux &amp; we want to run on Linux.  I could have converted to C, but everyone in my current team writes Ruby, and most importantly Ruby allows me (and you) to control the machine, rather than the other way around.  [We are the masters. They are the slaves!](http://www.artima.com/intv/ruby4.html)

My main issue with the conversion was figuring out what the JMP type conditional commands equivalent was in Ruby.  From my 2 minutes of google searching I found there doesn't seem to be a resource on the web that has a simple quick reference.

So without further ado, here's my first stab at an Intel x86 Assembly to Ruby for JMP commands cheatsheet.

<table>
  <tr><td colspan='2'> (<i> Given there is a function/method called <b>func0</b> &amp; a register/variable named <b>al</b> </i>)
</td></tr>
  <tr>
    <th>Assembly</th><th>Ruby</th>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}jmp func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}cmp al, 07Bh
jc func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 unless al - 0x7B == 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}cmp al, 07Bh
jnc func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 if al - 0x7B >= 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}cmp al, 07Bh
jnz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 unless al - 0x7B == 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}cmp al, 07Bh
jz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 if al - 0x7B == 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}test al, 07Bh
jnz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 unless al & 0x7B == 0{% endcodeblock %}</td>
  </tr>
 <tr>
    <td>{% codeblock lang:nasm %}test al, 07Bh
jz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 if al & 0x7B == 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}and al, 07Bh
jnz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 unless al &= 0x7B == 0{% endcodeblock %}</td>
  </tr>
 <tr>
    <td>{% codeblock lang:nasm %}and al, 07Bh
jz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 if al &= 0x7B == 0{% endcodeblock %}</td>
  </tr>
 </table>

If you see a mistake, have a query or a suggestion to update or just found this useful, please let me know.
