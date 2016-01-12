---
layout: post
title: Competition, A Necessary Evil
date: '2014-01-19 02:38:49'
---

When I see an online contest, my first reaction is to run as fast as possible in the opposite direction. This is due partly to bad experiences, but mostly because my reasons for entering contests were misguided. I have learned a lot from both winning and losing competitions. 

Things to remember when entering a contest :

- Be humble, arrogance in competition is ugly
- Don't focus on the prize, there is only one
- Have a passion for the contest
- Don't rush, get it right, half-done never wins

## Calculator App Contest

[Team Treehouse](https://teamtreehouse.com/) just put on a contest, [Calculator App for iOS](https://teamtreehouse.com/forum/forum-contest-calculator-app-for-ios), which sounded like a great way for me to [start giving back to others](http://blog.jo2.co/the-balance-of-creation-consumption/#creationconsumption). I have been impressed with what the Treehouse's team has been doing with their online training service.
<div class="logo_small">
[![Team Treehouse]({{ site.baseurl }}public/content/images/treehouse_logo.jpg)](https://teamtreehouse.com/forum/forum-contest-calculator-app-for-ios)
</div>

The details for the app contest :

- Build an app that is based on Apple's calculator 
- Make the addition button work
- Due by January 19th *(tomorrow as I am writing this)*
- Post it on [Github](https://github.com/) or [Dropbox](https://www.dropbox.com/)

Let the competition ensue. :)

### Research 

Find apps like what you are wanting to build.
<div class="icon">
![Calculator App Icon]({{ site.baseurl }}public/content/images/calc.png)
</div>

I spent a while testing what happens when using the Apple calculator in different ways. Below are a few tests :

*[button] display*

- [3] 3 [+] 3 [5] 5 [=] 8 [=] 13 [=] 18
- [4] 4 [%] 0.04
- [3] 3 [-] 3 [1] 1 [+] 2 [4] 4 [x] 4 [3] 3 [=] 14
- [4] 4 [.] 4. [5] 4.5 [+] 4.5 [3] 3 [=] 7.5

### Functionality

I spent a good chunk of time trying to get it as close to working like the original app. Here is what I was able to get working :

- math operations [+], [-], [x], [/]
- percent ... [4] 4 [%] 0.04
- signing ... [4] 4 [+/-] -4
- clear / all clear ... [4] 4 [c] 0 and [ac] clears last operation
- decimal ... [4] 4 [.] 4. [6] 4.6
- equals after operation ... [4] 4 [+] 4 [4] 4 [=] 8 [=] 12
- operation after operation ... [4] 4 [+] 4 [3] 3 [-] 7 [2] 2 [=] 5

I always get annoyed when I accidentally hit the wrong number while in the middle of a multi-step formula. So I chose to add a "delete" button that removes numbers if they have just been input. It does not delete if the display is a result.

- delete ... [4] 4 [5] 45 [del] 4 [del] 0

### Design & Experience

Specifications I wanted to follow :

- works for both 3.5 & 4 inch displays
- simple iOS 7 look with better touch and selected animations
- resizable font size for display (like the original app)
- design that will be dynamic for future ability to customize
- discover and use original font

My biggest design challenge was the font**(s)**. Yes, that is plural. Apple uses the Helvetica Neue family for most of there thin [fonts in iOS 7](http://iosfonts.com/). But the funny thing is the decimal point in [Helvetica Neue](http://www.myfonts.com/fonts/linotype/neue-helvetica/) is a line, not a circle. So I went about finding a good decimal and I ended up using [Avenir](http://www.myfonts.com/fonts/linotype/avenir/). The button was easy, the display was a little trickier. I setup a simple [NSMutableAttributedString](https://developer.apple.com/library/mac/documentation/cocoa/reference/foundation/classes/NSMutableAttributedString_Class/Reference/Reference.html) to solve the display issue.

I wanted to have a nerdy throwback. So I based the icon on [calculator speak](http://en.wikipedia.org/wiki/Calculator_spelling). When you put 1337 in a calculator and turn it upside down it spells LEEt (as in an elite nerd).
<div class="icon">
![1337 App Icon]({{ site.baseurl }}public/content/images/leet_icon.png)
</div>

Here are the screenshots of the calculator app that I built.
<div class="screen_shots">
![Launch Image]({{ site.baseurl }}public/content/images/leet_launch.jpg)
![Screen Shot]({{ site.baseurl }}public/content/images/leet_ss.jpg)
![Screen Shot]({{ site.baseurl }}public/content/images/leet_ss2.jpg)
</div>

### Project Links

- [Github - 1337 Calc](https://github.com/joalbright/1337-Calc)
- [Treehouse Contest Entry](https://teamtreehouse.com/forum/forum-contest-calculator-app-for-ios#featurette-241)
- [The Iron Yard](http://theironyard.com/)

Wish me luck!