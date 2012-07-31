---
layout: post
title: "SHRD : A ruby interpretation of the Double Precision Shift Right Assembly instruction"
date: 2012-07-31 20:43
comments: true
categories: [Assembly, Ruby]
author: Geoff Tidey
---

Following on from my [last post on Assembly conversion](http://blog.tidey.net/blog/2012/06/07/really-controlling-the-flow-from-assembly-to-ruby/), I also came across the SHRD instruction.

I already knew about the SHR & SHL command, logical shift right & left respectively, which translates rather easily:

<table>
  <tr>
    <th>Assembly</th><th>Ruby</th>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}shr @ax, 5{% endcodeblock %}</td><td>{% codeblock lang:ruby %}@ax >>= 5{% endcodeblock %}</td>
  </tr>
  <tr>
    <td>{% codeblock lang:nasm %}shl @ax, 5{% endcodeblock %}</td><td>{% codeblock lang:ruby %}@ax <<= 5{% endcodeblock %}</td>
  </tr>
 </table>

But I was initially stumped when I saw {% codeblock lang:nasm %}shrd ax, dl, cl{% endcodeblock %} in the Assembly code listing.

I'd figured out I needed the following test data, from the debugger

{% codeblock lang:ruby %}
def test_shrd
  assert_equal 12927, shrd(40919, 140, 6)
end
{% endcodeblock %}

And then this [link](https://en.wikibooks.org/wiki/X86_Assembly/Shift_and_Rotate#Extended_Shift_Instructions) gave me the insight I needed to code it up.

Voila:

{% gist 3218681 %}

The test went from red to green :)

"[They will not control us](http://www.artima.com/intv/ruby4.html).  We will be victourious!!!!!!"

{% youtube n2I3_196BpI %}

:D

