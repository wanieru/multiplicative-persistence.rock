# multiplicative-persistence.rock
Function to calculate the multiplicative persistence and each step for any number, implemented in the Rockstar Programming Language. Try running the code on https://codewithrockstar.com/online.

# What does it do?
Multiplicative Persistence means multiplying every digit of a number together. Then, you do the same for the resulting number, and keep doing it until you have until one digit left. The amount of steps it took to get to one digit is that number's "Multiplicate Persistence". `277777788888899` is the currently smallest known number with the highest multiplicative persistence (11).

# The code
```
My life is resistless
The moon is situational
Your love is a ladykiller
The night takes a toll
Put the moon into my anxiety
Put your love into the world
While the world is greater than my anxiety
If a toll over the world is smaller than the moon
Give back my anxiety

Put the world of your love into the world
Build my anxiety up


The end takes my courage
Put your love into my hands
While my courage is as high as your love
Put my hands over your love into my hands
While my hands is as small as my courage
Put my hands of your love into my hands

Put my hands over your love into my hands
Put my courage without my hands into my courage

Give back my courage

My love takes my strength
Your hope is empty
Put the night taking my strength into the sky
Put my life into my anxiety
While my anxiety is smaller than the sky
Put the end taking my strength into your mind
If your mind is my life
Give back your mind

If your hope aint empty
Put your hope of your mind into your hope

If your hope is empty
Put your mind into your hope

Put my strength without your mind into my strength
Put my strength over your love into my strength
Build my anxiety up

Give back your hope

Forever takes a promise
Put my life into my anxiety
While The moon is greater than my life
Shout a promise
Put the night taking a promise into the sun
If the sun is the moon
Shout my anxiety
Give back my anxiety

Put my love taking a promise into a promise
Build my anxiety up


Forever taking 277777788888899
```

# Background
I had been looking for a reasonable program to try out the [Rockstar language](https://github.com/RockstarLang/rockstar). This idea came to me while I was watching [a video from Numberphile on Multiplicative Persistence](https://www.youtube.com/watch?v=Wim9WJeDTHQ). When Matt Parker started implementing the function in Python in the video, I decided I'd give it a shot in Rockstar.

# Digit Extraction and Multiplcation
Rockstar doesn't provide functions to convert integers to strings, or even manipulate strings to begin with. To multiply each digit of a number together I therefore need a function which can get me a single digit from a number's base 10 representation. If I can get the last digit from the number, I could then subtract that from the original number, and divide it by 10 and then repeat the process.
```
number = 2819
digit = lastDigit(number) = 9
number = (number - digit) / 10 = 281
digit = lastDigit(number) = 1
...
```
The easiest way to extract the last digit is with the modulo operator: `2819 % 10 = 9`. The most straight-forward way to implement this operator without the ability to round numbers is by subtracting the divisor over and over until you get a smaller number. But I wanted the program to not take hours to evaluate when using a number like `277777788888899` so I had to find a loop-hole.
Instead, I find the largest power of 10 which is smaller or equal to the number, then subtract that. I can keep doing this until I have a number smaller than 10, which is always the last digit.

# Number Length
In a simlar problem, I need to know how many digits long a number is. This uses a similar technique. Find the smallest power of ten which is greater than the number and count the amount of zeroes (the exponent). That's the length of the number in base 10.
