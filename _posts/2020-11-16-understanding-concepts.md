---
layout: post
title: "Understanding Computers in a Nutshell"
description: "a short blog that helps understand how computer work"
date: 2020-11-16
tags: [blog, computer, hardware, software]
comments: true
share: true
---

![What is a computer?](https://raw.githubusercontent.com/szikaria961/szikaria961.github.io/master/computer.png)

###### _desktop computer by David Christensen from the Noun Project_

---

## Building A Love For Software

I am writing this blog to keep a record of my own learning as well as making an effort to really care about software. This is my attempt to research and document my learnings from the ground up so that I don't have an excuse to not feel confident. I feel embarrassed to acknowledge my abilities around not knowing enough, I lack a deep understanding of computer science concepts and I frankly haven't put effort into changing that. I have come to an understanding that the first thing I need to change in my life is to remove insecurities that I have built around my career and competence; it has become an unhealthy response to not excel in software. I hope by making changes to my lifestyle like writing more brutally honest blogs, keeping a record of anything I don't understand and digging deeper, not running away from my problems and doing more projects in my own time, I feel excited to learn.

So, let's learn!

## What is a Computer?
It is an electronic device that manipulates information. Computers see  information or data as `1's` and `0's` known as binary, but it knows how to combine them into much more complex things; an image, a video, a game etc. Computers use a combination of hardware and software. Hardware can be anything that's physical; like the internal components and the external parts of a computer. Hardware takes a set of instructions from a software.

## What is Binary?
System of Counting, just like tally marks and base ten positional. Binary works the exact same as Base Ten (regular counting). Instead of each digit going from `0-9`, it goes from `0-1`. Counting upwards in binary is like this: `0, 1, 10, 11, 100, 101, 110, 111, 1000 and 1001`, that's us counting from `1-9` in binary. Because each digit of the binary has only `2` values and not `10`, each additional digit increases in power of `2` rather than an increasing power of `10`. Binary falls between the Tally Mark and Base Ten counting system, in terms of efficiency. So, why don't we use Base Ten as our counting system for computers, when it's clearly much more efficient than binary. That's because of the physical limitations on how computers were created back then. Everything a computer does comes down to Micro Transistors. Micro Transistors are tiny switches that can be flipped on or off with a very weak electrical charge. Remember when I mentioned that the computers were first created to just count, well micro transistors were used with the binary counting system to represent numbers; where an on switch means `1` and an off switch is a `0`. A single transistor is a __bit__ (binary digit) and `8` bits makes up of a single byte. Which means that any number from `0 - 255` can be encapsulated in `8` bits or `1` byte.

### What does it mean to spell in Binary?
It just means to spell it in __ASCII__ (American Standard Code Information Interchange). ASCII is a way to convert computer data (binary) into letters for us humans to have an easier time to work with. My name in binary can be represented in `4` bytes; each byte per letter. To reduce the amount of transistors required to calculate massive values, new computers are designed to recognize `2` bytes as one single number. Instead of referencing one line of `8` transistors, the computer could reference two lines giving `16` digits worth of binary. This increased the amount of numbers that could be represented from `255` to `65535`.

A server is another example of a computer that sends information to other computers on a network. For example, a quick google search of your favorite poutine place will go to a web server that delivers pages that you want to see on your computer. Computers were essentially created to manipulate information. They initially started out as basic calculators and were only used to manipulate numbers.

The computer system is divided into input and output devices. Input devices are devices that send information into your computer and output devices is where information is coming from your computer. For example: A keyboard sends input into the computer, therefore it's an input device; you type your keys and send the signal inside your computer, giving it some direction. A mouse is another example of an input device, we're sending information into the system. A monitor is an example of an output device, this is because the computer system is sending information out to the monitor for us to see.

Let's compare a computer to a toaster. I give a CPU `2+2` it returns `4` to me just like if I give a toaster a piece of bread and it returns toast to me.

## Components of a Computer:

### 7 essential parts:

#### Simple:
1. __Case__: Plastic box that stores all the parts and keeps the inside safe.
2. __Power Supply__: Plugs into the wall, take power from the electrical outlet and provide all the other parts with the electricity needed to do their thing
3. __MotherBoard__: circuit board that all the other components plug into. Allows all of the components to send electrical currents with data between each other. __BIOS__ (Basic Input Output System) is the first software (small piece of code) contained on a chip on your Motherboard. When you start your computer, BIOS is the first software that runs; identifies your computer's hardware, configures it, tests it and connects it to the Operating System for further process. This is called the boot process.

#### Complex (Deal with data):
4. __CPU__ (Central Processing Unit): Processor. It's basic job is to receive input and provide output. Handles all the system instructions. Very good at doing things with data; reading it, arranging it. This is essentially where most of our programs run from. Center part of the computer's brain. Two main companies that make CPUs; intel and AMD. The CPU has no memory, it's very smart and can process information very quickly but it can't remember anything (like me).
5. __RAM__ (Random Access Memory): Another form of storage that stores the exact same data as your Hard Drive but has small storage space but has nearly instant access to it. This is where you'll store the data that you are using and need to get to quickly.
6. __Hard drive__ (Storage): Where all of the data is stored. Although they're good at storing lots of data, they're really bad at accessing all that data quickly. This is where you'll store data that you own but you aren't currently using.
7. Graphics card or __GPU__ (Graphics Processing Unit): Standalone computer. Dedicated to figure out what pixels on the screen need to light up on the screen, what color and at what time.

## In Summary:
- The Case stores everything in a physical box
- The Power Supply gives electricity to what needs it
- The MotherBoard is the body that everything plugs into
- The CPU handles all the system and does everything
- The RAM stores data that is needed for quick access
- Hard Drive stores everything that you have installed
- Graphics Card figures out how it's all supposed to look on your monitor/screen

### Real World Example:
- Case is your skin
- Motherboard is your skeleton
- CPU is your brain
- Hard drive is your long-term memory
- Ram is your short-term memory
- Power supply is your stomach / heart and
- GPU is your eyes
- Cooling is your sweat

Relationship between our computers Hard Drive and RAM. Imagine the kitchen cabinet as the symbolic representation of our computers hard drive and imagine our kitchen countertop as the representation of our computers RAM. At any time we can grab a bowl from our kitchen cabinet. We can put it on the countertop and use it. When we use the bowl we use it on the countertop and when we're done with it (after washing it) we can put it back in the cabinet. The bigger my countertop, the more things I can do simultaneously. We can maybe have a plate on the countertop while we have a bowl on it as well.

When you run a program or a project file. Your CPU identifies what parts of data are needed for that program to run, pulls them from your Hard Drive, stores them in your RAM sticks for quick accessibility. This is why for instance when you load a new level in a game, it has to load; anytime we see loading it's loading the data that composes that level from the bulky hard drive to RAM.

### How does a CPU work?
In every CPU there's a particular wire, that turns on and off at a steady rate to help keep everything in sync. That wire is called the clock. Modern CPUs are measured in GHz; giga meaning billion and hertz meaning times per second so the clock in modern CPUs turns on several billion times per second. That speed is what allows CPUs to do very complicated things very quickly.

### How does the CPU and RAM interact?
Ram consists of a list of addresses and at each of those addresses is a piece of data. The CPU normally requests and processes each piece of data from RAM in order, one after the other. However, if the CPU is instructed to pull data out of order it can do so, that is why it's called Random Access Memory. The data can be accessed randomly if it needs to be although normally it's accessed in order. When the computer first starts running a program it sends an address to RAM to begin retrieving that program. The RAM address just consists of a series of ones and zeros representing on and off wires. If the enable wire is turned on, Ram automatically sends whatever piece of data is at that address back to the CPU. That data is then processed by the CPU accordingly. Once the CPU is finished processing that piece of data it then sends another address to Ram, turns on the enable wire and gets the next piece of data from Ram, this process happens over and over again inside the computer.

### But what is that data inside Ram? (it just looks like a bunch of ones and zeros)
Data in RAM are the instructions; instructions just tell the CPU to do different things.

As soon as the power to the computer is turned off all the data and RAM is lost so you have to have a way to store it more permanently for that we use a hard drive. Inside the hard drive is a spinning disk covered in tiny magnets with a small metal arm floating above it. The arm moves around to the different parts of the disk where a different data can be stored and retrieved. The disk and the arm generally move very very quickly, but nowhere near as fast as the CPU can process data. For this reason all the data from the hard drive must first be moved to RAM before it can be processed.

