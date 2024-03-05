+++
title = "Write Bugs, Use Python"
date = "2023-02-16"
draft = true
+++

One of the common misconceptions of many beginners is that they can write great performant code from start. Myself, of course was a victim of this line of thinking and now I am starting to understand how dumb it was. So, I want this blog post to be a piece of advice for my older self.

## Write bugs


### Practice

When I started learning programming, I used to look at my mentors and think "Man, I would never be as good as them. How can they come up with such elegant solutions. It really does take a genius to write great code". But, what I did not take into account was their experience. Practice really does make perfect. Rome was not built in a day. If anyone thinks they can come into writing software and can build big things, no one could be more mistaken.


Consistent effort is very important to become a good programmer. Let me give you an example. Let us assume someone started learning to code a month before and practiced 10 hours each day. So today, they have an experience of 300 hours. Let us assume another person who started learning to code 6 months before and they practiced 1 hour per day. So, today, they have an experience of 180 hours. Who do you think would be better? The person who has been practiciing for 6 months would be miles ahead of the other person. 

Programming is a skill and you just can't shoehorn it into someone's brain in a said amount of hours. It takes time for our brains to get acquainted with programming concepts.

Write as much code as possible. May it be wrong code, inefficient algorithms, do not care about them, write code.

It is really important to set our expectations low. Don't start out to build the next big kernel or game engine. Write small, simple programs to get comfortable with the programming patterns. See how structuring code is helpful over procedural code. Writing real world applications show us how different real world code is to the code we wrote in DSA problems or textbook examples. 

Writing these insignificant, small programs strengthen our fundamentals. They give us practice to think / write software. They serve as the stepping stones to writing bigger, better and more significant software.

### Correctness don't matter

My mentor used to have a rule, "No usage of global variables". When learning to code, I remember solving questions faster than my peers, but he would not accept my solution because I was using global variables. It was a big deal to me back then. His intention was to make my code better, but my frustation was that I did not get the appreciation I deserved. This incident made me lose interest in writing code. Now I can easily do the question following all good principles. This is one of the few places I don't agree with my mentor. 

Correctness can be learnt with experience. But where do you get the experience? Writing incorrect code. 

## Use Python

### Speed, go brrrr...

Another trap many fall into is using the "fastest" programming language. This is probably the most obvious sign of an inexperienced programmer. It really does not matter.

To put it into perspective, python can generate a million pairs of random numbers, add them in about a second. We hear the words million, billion, trillion etc and lose sense of their scale. Try counting to 1000 and see how long it takes. A million is a 1000 1000s. Python is very fast compared to human scales. Yeah, the same program written in C++ takes about 50 milli seconds, which is about 20 times faster, but does it really matter? Considering the comfort python offers, it is no brainer to choose an easy language over something "fast". 

To give another example, let us say you built a website, it took off and now you have 1000 concurrent users. A flask server running on a $50 server can very easily handle all 1000 users concurrently. The same website written in rust using actix-web or some fast framework can probably handle the same 1000 concurrent users on a $35 server. Considering the development overhead, it is no brainer to choose the python version. And above all, in most cases, the limitation is the network or database access or some other parameter and not CPU. In real life applications python's speed is very rarely a limitation. 

In places where numerical calculations speed is required, `numpy`, `tensorflow` and many other fast C/C++ libraries can be used. They contain optimized, vectorized or GPU code which will be faster than any code we can come up with in pure C++ or rust. 

So, if I were to start over, I would just learn python and stop worrying. 

## Write bugs, but finish them
Well, I am guessing we are all guilt about this one, incomplete projects. It is better to complete small projects, deploy them rather than incomplete huge projects. Always strive to complete projects before starting a new one. 

## Experience is the best teacher

I fell for all the traps above, eventhough I have heard most of the advice in this post, especially choosing the "fastest" programming language. At that time I was unconvinced when many said to write software in an easier language, but now I know better. I guess experience **is** the best teacher. 
