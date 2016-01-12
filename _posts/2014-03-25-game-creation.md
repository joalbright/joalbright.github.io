---
layout: post
title: Game Creation
date: '2014-03-25 19:54:52'
---

A little over a week ago, [Team Treehouse](http://teamtreehouse.com/) presented a contest to [build a Tic Tac Toe iOS app](https://teamtreehouse.com/forum/forum-contest-tictactoe-app-for-ios). What most people do not know about me is that I am a [gamer](http://steamcommunity.com/id/redleader-jo/games?tab=all). And one of my habits is to constantly download (sometimes buy) games or apps on my iPhone & iPad that I believe will have good user experiences and/or great story lines.

> To be a game developer, you must play games to understand what a gamer gets out of playing them. 

Now that games are more presentable to the main stream audience through mobile apps, it is easier to discover what users get from playing them. 

A few of the ones that are special to me are :

- Advancement : Time spent in the game is accruing worth and is meaningful.
- Entertainment : Story lines and new ideas excite the user's imagination.
- Quick Fix : A moment of boredom averted by a game that can be played in a few minutes.

As I thought about the contest, I decided this app will easily be a "Quick Fix"... but I also wanted it to show past games and overall stats to give a feel of worth. And the designer side of me wanted the game to be playful and pleasing to the eye.

Next steps?

### Design & Story

All of my ideas start with design, and I thrive on having a good vision of the end product before I move on to development. I tend to consistently question my ideas to expand on them, but also filter out bad any ideas.

- What will be fun and simple to understand?
	- With X's & O's being obvious, I decided to use colors. This created a new world for the user right away.
- How will the user play? Computer or another person?
	- I knew playing against another person is standard and the simple to implement, so I decided to push myself and create a robot.
- What happens to past games?
	- I personally enjoy seeing my history and one of my favorite parts of Treehouse's setup is their point system. So stats and potentially showing past games were on the top of my list.

Since we only had a week to build the app, I chose not to build a story for it. Instead, I figured I could play up the robot as a character rather than a computer program.

ToDo :

- Create a robot character & its AI
- Change between play styles
- View stats of game play
- Scroll through past games to see how they were won
- Design that is simple to use & learn as well as animate
- Highlight who won or stalemate
- Ability to start new game

For the design, I was thinking about the circles from the keypad on the lock screen from iOS 7. You can't get any closer to making something understandable than using key elements from the core design. I almost went with red and blue as a color theme, but again this is another obvious choice. Seeing that red and green are compliments, I just needed to pick some tints that were playful.
<div class="screen_shots">
![Game Play]({{ site.baseurl }}public/content/images/ttt_gameplay.png)
![Win]({{ site.baseurl }}public/content/images/ttt_win.png)
![Stats]({{ site.baseurl }}public/content/images/ttt_stats.png)
</div>

### Architecture

Why do you design before architecting the code?

One of my skills as a hybrid (designer / developer) is the ability to imagine an app in a visual way. So most of my design is created by understanding the structure of how an app can be built. 

First draft outline of needs :

- Game Collection
	- Game
    	- Spot Choices
        - Winner
- Play State
	- Robot : Runs a decision method to chose a spot
    - Person
- Touches
	- New Game : Add a game to the game collection
    - Spot Tap : Change which player's turn it is
    - Stats Tap : Overlay with current totals
    - Play State : Change who you are playing

Many of my apps are built from code only, without touching Interface Builder (which baffles lots of people). But to me Interface Builder does one thing great, gives a visual experience to someone who can't visualize the app through code.

Next I like to build out the Xcode environment for me to easily navigate my classes and resources. I like to group things as they are contained within other elements, allowing me to go deeper as I need.

Below is an example of how I tend to layout my groups :

- Models (can hold singletons or data objects)
- Random (filled with classes I build for all apps normally)
- Controllers
	- Views
    - TableCells
- Images (now controlled by [Asset Catalogs](https://developer.apple.com/library/ios/recipes/xcode_help-image_catalog-1.0/Recipe.html))

### Code & Discovery

>Never go into building an app believing you know every angle. 

You will quickly find things that collide or could be done better, and sometimes you might even discover new features you want to implement.

Once I have an idea of my structure, I will start building top level classes that will manage most of my elements. For this project I built a singleton to manage my games, allowing me to have access to the games anywhere in the app. 

For simplicity and speed I made the game model a mutable dictionary with the spots set to empty :

	NSMutableDicitionary *game = [@{@1:@2,etc} mutableCopy];
    
    // the key @1 is the spot position
    // the value @2 defines it to be empty (as a user selects a spot it will become @0 for red and @1 for green)
    // once the game is won a new key @"winner" will be added with a @0 or @1 depending on who won
    
This could be so much more advanced by creating a specific class for the game model and having properties to set the winner and spots (thinking about it now, I might upgrade this later). Once I decided upon all of the other pieces like how to save whose turn it is, I moved on to the view portion.

I had a vision of a vertical cover flow animation to swipe through past games. Personally I like controlling every aspect of an app that I can, so instead of trying to find a plugin to make this work, I broke it apart and built parts of it as I went. The [UITableView](https://developer.apple.com/library/ios/documentation/uikit/reference/UITableView_Class/Reference/Reference.html) is basically setup for what I was wanting where each cell could be a game. I set the cell to the screen height and enabled pagination, which took care of the main factors. The tricky part came with trying to animate the games in a cover flow fashion. I ran into a few bumps with the animation of the cells based on the scroll position.

- [CGAffineTransform](https://developer.apple.com/library/ios/documentation/graphicsimaging/reference/CGAffineTransform/Reference/reference.html#//apple_ref/c/func/CGAffineTransformMakeScale) : became a huge pain because the cell.transform was acting funny when the scrollview.contentOffset changed (most likely I had unaccounted for some factor).
- [CATransform3D](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/CoreAnimation_functions/Reference/reference.html#//apple_ref/c/func/CATransform3DScale) : is what I ended up using and attaching it to the cell.layer.transform, and it worked flawlessly after that.

Don't give up if something does not work the way you expect it to. There will be cases where something that worked in one instance does not work this time. I have never removed a feature from being unable to make it work.

With animations working and the tableview filling with game cells, next I needed to deal with touching spots and starting a new game. There wil be times when you need a child object to speak to its parent. The best and most structured way of doing this is through [delegates and protocols](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/WorkingwithProtocols/WorkingwithProtocols.html). Think of this as a contract between objects that specifies what can be communicated between them. I have used this method for sending data, calling events, handling callbacks, and more. For this setup, I have it handling the turns played and game won.

### Artificial Intelligence

You created an intelligent robot?

No, not really. It is funny how ominous AI can sound, and make you look really cool when you build one. But really AI is just code and clockwork with a little bit of random thrown in.

The main functions of my AI :

- Check for a winning move : it looks over every possible set of three and sees if two spots are occupied by the robot
- Check for a blocking move : same as above but looking for two spots occupied by the user
- Random open spot: this is the real special sauce that creates variety for the game play (and honestly it has allowed the robot to beat me multiple times)

So are AIs hard to build? Nah. Just need to break them apart like any other puzzle and start on one piece at a time. In this case, I didn't realize how great it would turn out until I started playing against it.

### Learn

I learned that building a game app is no different than any other type of app. It just has a little extra flare, some goals, and a story thrown in. Don't be scared to build a game, because they are currently the most profitable apps in the App Store.

*What kind of game would you build?* 

**Maybe you should first ask yourself, what kind of games would you play?**

Good luck!