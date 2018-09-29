# Port Specification
Port Specification is used when you're specifying the inputs and outputs of a sub-module that you created. More information can be found on page 47 of *Logic Design and Verification Using SystemVerilog* by Donald Thomas.

## Introduction
Let's say you want to implement a sub-module called myModule in your top .sv file. In this example, we will use the module described below. It has one output called `out`, and three inputs named `in1`, `in2`, and `in3`. What the module does isn't important for this example, so we can ignore it for now.

```sv
module myModule
	(output out,
	input logic in1, in2, in3);
	
	// we dont care about what this actually does
	
endmodule: myModule
```
How would you implement it in the top .sv file? Most of you use something called *ordered port specification*, but there are other ways! Which one should you use? Well, it comes down to preference, but please be consistent and use only one specification style throughout a project.

## Ordered Port Specification
You all are probably familiar with this one. If we were to implement `myModule` in a top file using ordered port specification, it would look something like this:

```sv
// Ordered Port Specification

module Top 
	(output OUT,
	input logic IN1, IN2, IN3);
	
	myModule m1(OUT, IN1, IN2, IN3);
	
endmodule: Top
```

Notice that in this specification, you have to list your inputs and outputs **in the same order** that you specified in the sub-modules declaration. In this case, since we specified the output first, and the three inputs afterwards, we have to pass in the output as the first argument in `m1`'s declaration. Also note that the variable names in the top declaration **have to be different that the variable names in the sub-module's declaration.**

But what if you want to have the same variable names? And what if you don't like being orderly!? What if you don't want to worry about the order of your arguments. Well, you can use something called *named port specification!*

## Named Port Specification

Using named port specification, we don't have to worry about the order that we pass our arguments into `m1`! Here's what it looks like:

```sv
// Named Port Specification

module Top 
	(output out,
	input logic in1, foo, bar);
	
	myModule m1(.in2(foo), .out(out), .in1(in1), .in3(bar));
	
endmodule: Top
```
Now, I admit, this looks really confusing at first. But essentially, all you have to do is state which port you want to map a signal to by prepending a '.' to the port name. In this example, we want to map the signal `foo` to `m1`'s `in2` port. So, we prepend `in2` with a '.', and wrap `foo` in parenthesis next to it. Using this, we don't have to worry about which order we declare our arguments! 

Also, notice that we can use the same variable name in our `Top` module as the variable names in our `myModule` declaration! If you so happen to have this, then you can use the `.*` shorthand to *automatically map signals to any and every port with the same name.* It'll look something like this:

```sv
// Named Port Specification with '.*'

module Top 
	(output out,
	input logic in1, foo, bar);
	
	myModule m1(.in2(foo), in3(bar),  .*));
	
endmodule: Top
```

You see how we don't have to even declare what we're mapping `m1`s `in1` and `out` port to? The `.*` will automatically map `in1` and `out` to the Top module's `in1` and `out`, since they share the same name! 

## Conclusion
Which specification you use is up to you, but it's good to know that other ways to specify ports exist, and how to do it. That way, if you come across code written differently, you'll be able to understand it. Just remember that the second most important thing when writing code is that it's *concise and easy to read* (and the most important thing is to write code that actually works).
