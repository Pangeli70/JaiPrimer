
# Behind and Beyond Jai

## Friction in modern OOP C++

Modern C++ has arisen as the "de facto" standard for many of the most complex software like videogames. But it isn't the best possible choice as it is cumbersome, heavy and overcomplicated. It is a general-purpose "big agenda" language used everywhere from embedded microsystems till server farms, that pretends to remain somewhat consistent with its C language heritage. It evolved in many years stratifying decisions taken to mitigate problems that "game developers don't have" (cit.). Using this language for big complex tasks becomes rapidly a stressful and tedious activity. The coders have to express themselves in terms forced by the language and so even simple tasks become boring error-prone activities that may lead to poor performance products. Many people are perfectly comfortable using it but some still use it because they don't have better alternatives.

The tools involved in modern C++ programming sometimes have a tremendous lack of effectiveness: compilers sometimes give obscure messages, compilation time on serious programs becomes rapidly an issue, debugging can be very hard on complex situations, build process involves several connected tools, etc..  

All of these problems can be expressed in terms of _friction_: the difficulty to get a constant fluid flow of improvement in the code till the scheduled release. 
Having deadlines and a list of todos that shrink slowly is stressful and painful for everyone.
Moreover, friction limits the coder in terms of the exploration of alternatives and new ideas because of their time cost. This reduces the effectiveness, performance, and security of the code. 

In the end, friction not only reduces enthusiasm, and freedom of the coding teams but also heavily reduces the quality of life of the programmers so their productivity. It wipes away the *joy* from the creation process and makes the "programmers feel like living a miserable life" (cit.).

Writing software is an activity that involves creativity. To be productive the programmers need to stay motivated and focused for large periods. They have to load the software and make it run in their brain entering in [the zone](https://en.wikipedia.org/wiki/Flow_(psychology)) where all the magic happens. Fred Books stated a famous phrase [cit.](https://en.wikiquote.org/wiki/Fred_Brooks) that sais that no matter what kind of tools the programmer uses, about 70% of software development happens in the mind, thanks to the correct way of thinking about the problems. Friction keeps programmers away from this mental state.  

All of these are very big problems for the software industry. Imagine if it would be possible to gain only  20% or even 10% in friction reduction, this could lead to an enormous amount of overall improvement. And this possibility alone justifies the idea of the creation of a new language even if Jai won't pretend to be the magic [siver bullet](http://worrydream.com/refs/Brooks-NoSilverBullet.pdf) that will solve all the problems.


## Data-oriented programming

The author of the language stated that "video games are machines that fill memory". Most of the time, coders are thinking about how to fill memory with huge reams of data in ways that allow the data to be efficiently accessed and processed. Hundreds of megabytes of memory must be moved from the hard disk into the main memory, and from there into the video card or the processor cache to be processed and returned to the main memory.

Because of the nature of video games often the overall user's experience is bounded to the 1/60th-second frame-rate, and so is driven by the complexity of the simulations, the quality of visuals and the responsiveness to the user's input. This means that everything must be accomplished by the hardware as fast as it is possible.
This kind of problem goes beyond the capabilities of many modern programming languages, which may allow the programmers to _write code faster_ but will prevent them from writing _fast code_. And even C++ that should produce really fast machine code may fail at it if it is not used properly or if the coder won't use tricky workarounds.

Almost all modern languages are designed to allow "average experienced" programmers to produce "almost safe", "almost effective code" in a "reasonable amount of time". But most of them prevent experienced senior programmers to deal directly and easily with the data at the lower levels of the machine code to squeeze out from the CPU and the GPU all the available elaboration power. Especially in C++ sometimes the programmer has the sensation to chase the compiler instead of the hardware [cit.](https://www.youtube.com/watch?v=IAdLwUXRUvg&feature=youtu.be&t=1624).

Game programmers are not afraid to deal with manual memory management, different OS and hardware nuances, and low-level data optimizations to pack pieces of information in smaller spaces. They know that mistakes may cause crashes, but crashes are not bad at all if caught at development and testing time. Subtle defects that appear weeks after the release that may corrupt save-files, or make unstable the network transfer-rate and compromise multiplayer experience are some of the real problems.

Game programmers should reason about code’s behavior on the range of machines targeted for shipping on, and design the data to use efficiently the available hardware capabilities. Mike Acton’s states these concepts in his famous talk on [“Data-Oriented Design” methodology](https://www.youtube.com/watch?v=rX0ItVEVjHc).). Now he is developing these ideas as a principal engineer in the development of the [DOTS](https://unity.com/dots) stack in Unity.

Programmers who care about the performance of their software on their target hardware are inhibited by programming languages that sit between them and the hardware.
In the years because of the availability of more and more powerful hardware, the academic culture about software development has moved away from the real Information Technology concerns (the data) toward the tools used by the programmers (the software).
The attention was driven toward safety and patterns instead than on the matter of fact of the problems: how to transform data effectively, that should be the true purpose of the software. 
This is nothing new, instead was really clear years ago. Fred Books stated a famous phrase [cit.](https://en.wikiquote.org/wiki/Fred_Brooks) resembled in this brief [intervention](https://youtu.be/rX0ItVEVjHc?t=4543).

The overall result of this culture is that at present time we have super "beefy" hardware, almost everywhere filled with over-bloated Operative systems, that run super-complex user interfaces with very poor performances, assembled using a stack of layers of services, built upon almost unmaintainable aged inherited code.

Jai tries to give to the programmers a more data-oriented approach to software development removing all the abstractions typical of the OOP culture implemented in many years by the modern languages like garbage collection, RAII, constructors and destructors, multiple-inheritance and deep hierarchies, polymorphism based on abstract classes, exceptions and so on.

---
### Navigate 
* [Home](./) 
* [Back: Introduction](./Introduction) 
* [Next: Why jay?](./Why-Jai%3F)