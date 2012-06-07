---
layout: post
title: "Control flow: from Assembly to Ruby"
date: 2012-04-28 00:59
comments: true
categories: [Assembly, Ruby, Cheatsheet]
published: false
author: Geoff Tidey
---

I've recently been converting a bunch of Assembly [1] code into Ruby.  Why you may ask?  Well the Assembly code is [Intel x86 flavoured](http://en.wikipedia.org/wiki/X86_assembly_language), it's never been run on Linux &amp; we want to run on Linux.  I could have converted to C, but everyone in my current team writes Ruby, and most importantly Ruby allows me (and you) to control the machine, rather than the other way around [2].

My main issue with the conversion was figuring out what the JMP type conditional commands equivalent was in Ruby.  From my 2 minutes of google searching I found there doesn't seem to be a resource on the web that has a simple quick reference.

So without further ado, here's my first stab at an Assembly to Ruby for JMP commands cheatsheet.

(Given there is a function/method called **func0** &amp; a register/variable named **al**)


<table>
  <tr>
    <th>Assembly</th><th>Ruby</th>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}jmp func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}cmp al, 01Ah
jc func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 if al - 0x1A > 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}cmp al, 01Ah
jnc func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 unless al - 0x1A > 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}cmp al, 01Ah
jz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 if al - 0x1A == 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}cmp al, 01Ah
jnz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 unless al - 0x1A == 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}test al, 01Ah
jnz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 unless al & 0x1A == 0{% endcodeblock %}</td>
  </tr>
 <tr>
    <td>{% codeblock lang:nasm %}test al, 01Ah
jz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 if al & 0x1A == 0{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}and al, 01Ah
jnz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 unless al & 0x1A == 0{% endcodeblock %}</td>
  </tr>
 <tr>
    <td>{% codeblock lang:nasm %}and al, 01Ah
jz func0{% endcodeblock %}</td><td>{% codeblock lang:ruby %}func0 if al & 0x1A == 0{% endcodeblock %}</td>
  </tr>
 </table>

If you see a mistake or have a suggestion to update, please let me know.


[1] http://www.cs.virginia.edu/~evans/cs216/guides/x86.html

[2] http://www.artima.com/intv/ruby4.html

