---
layout: post
title: "String concatenation the right way; the fast and furious way"
date: 2012-10-09 23:15
comments: true
categories: 
---
<p>One of the greatest parts of programming is learning something that blows your mind, a moment where <a href="http://youtu.be/ZKh68YfQYkE?t=5s">this</a> happens. It's one of those moments that you realize you are a programming n00b, and that there is always a better way to do things. I had one of these moments recently when I was going through the <a href="http://rubykoans.com">Ruby Koans</a>. In one of the introductory tests that cover strings you are told to think about string concatenation, and in particular which method is faster when building strings: "+" or "<<". 
</p>
<p>The great part about leading questions like that is that you pretty much already know what the answer is going to be. So I went ahead and proved it, just so I could write this blog post. Awesome. There's a really handy Benchmark class in Ruby that lets you time to execution of blocks of code, so I used that to scientifically prove what we all now know is true: "<<" is faster than "+".<p>
``` ruby
require "benchmark"

Benchmark.bm(6) do |x|
	x.report("a << b") {
		second_a = "a"
		100000.times do
			second_a << "b"
		end
	}
	x.report("a + b") { 
		first_a = "a"
		100000.times do 
			first_a + "b"
		end
	}
	x.report("\#{ab}") {
		third_a = "a"
		third_b = "b"
		100000.times do
			"#{third_a}#{third_b}"
		end
	}

end

```
Here are the results:
```
             user     system      total        real
a << b   0.040000   0.000000   0.040000 (  0.036503)
a + b    0.040000   0.000000   0.040000 (  0.042027)
#{ab}    0.040000   0.000000   0.040000 (  0.040516)
```
<p>As you can see, the "<<" operator is a whole lot faster. It's faster because "<<" alters the original string, whereas "+" has to create a new string, and creation is a more costly operation. This is something that seems really small and insignificant, but performance matters. Like Vin Diesel said, "It doesn't matter if you win by an inch or a mile. Winning's winning. Unless you're not using '<<' to build Ruby strings. Then you are losing."</p>