# Setting Up TRISA and TRISB

During Lab 3, I noticed that a lot of you initially had `TRISB = 0x00`. Setting up your TRISA and TRISB values correctly is important. Otherwise, your circuit will not work. This guide will explain what these two bits actually do and how to find the correct values for them. If you need more information on ports and TRIS values, check out <a href="http://www.islavici.ro/cursuriold/conducere%20sist%20cu%20calculatorul/PICbook/2_05chapter.htm">this page on Microchip's website.</a>

## What is TRISA and TRISB?

There are two 'ports' on the 16F648A, port A and port B. Each pin corresponds to one bit on that port. For example, RB0 and RB1 are bit 0 and bit 1 for port B, respectively. Each RB and RA pin on the 16F648A can act as either an input or output, but you have to specify their roles first. If you're connecting RB0 to a button, then it's an input (bit value 1). If you're connecting RB0 to an LED, then it's an output (bit value 0). TRISB tells the 16F648A which bit is an input or output, and programs the pins accordingly. 

## How to Set Up TRISA and TRISB

Let's go over an example:

We want to hook up RB0 and RB1 to an LED, and RB2 to a button. In other words, we want RB0 and RB1 to be outputs, while RB2 is an input. The rest of the bits we don't care about, but we'll just set them as outputs.
Therefore, the bit value will be as follows:

```
RB0 = 0 // output
RB1 = 0 // output
RB2 = 1 // input
RB3 = 0 // dont care 
RB4 = 0 // dont care
RB5 = 0 // dont care
RB6 = 0 // dont care
RB7 = 0 // dont care

```
Thus, to make RB0 and RB1 outputs, while setting RB2 to an input, we have to set TRISB a binary value of `00000100`. You can assign TRISB this value by prepending with `0b`, so the compiler knows that the numbers represent a binary number. The code would then look like:
```
TRISB = 0b00000100;
```
You could also declare it as a hex value. To convert, you can use <a href="https://www.rapidtables.com/convert/number/binary-to-hex.html">this online hex converter.</a>

Using that, we get `00000100 => 4`, and we prefix the hex value with `0x` to denote that it's a hex value. Therefore, our final line of code in our program will be:

```
TRISB = 0x04;
```

This will set RB0 and RB1 to outputs, and RB2 to an input. This will ensure that our LEDs and buttons will work as intended. The same process applies when setting up port A (RA0, RA1, etc.).
