---
title: "Regular Expressions"
author: "Shawnzoom"
date: "October 26, 2015"
output: html_document
---

```
R Markdown format of slides from the Coursera Data Science Specialization course. RegEx lectures
https://www.coursera.org/course/getdata
```


#### Regular Expressions
```
We need a way to express

whitespace word boundaries
sets of literals
the beginning and end of a line
alternatives ("war" or "peace") Metacharacters to the rescue!
```


#### Metacharacters

**Some metacharacters represent the start of a line**

**^i think** **means, match any line beginning with "i think"**

```
will match the lines

i think we all rule for participating
i think i have been outed
i think this will be quite fun actually
i think i need to go to work
i think i first saw zombo in 1999.
```

#### $ represents the end of a line

**morning$** **"means, match any line ending with "morning""**
```
will match the lines

well they had something this morning
then had to catch a tram home in the morning
dog obedience school in the morning
and yes happy birthday i forgot to say it earlier this morning
I walked in the rain this morning
good morning
```



#### Character Classes with []

**We can list a set of characters we will accept at a given point in the match**

**[Bb][Uu][Ss][Hh]** **means. match lowercase or uppercase letters**
```
will match the lines 


The democrats are playing, "Name the worst thing about Bush!"
I smelled the desert creosote bush, brownies, BBQ chicken
BBQ and bushwalking at Molonglo Gorge
Bush TOLD you that North Korea is part of the Axis of Evil
I'm listening to Bush - Hurricane (Album Version)
```

#### Character Classes with []

**\^[Ii] am** **maens, match "I am or i am" at thebeginning of line, lowercase i, or uppercase I**
```
will match

i am so angry at my boyfriend i can't even bear to
look at him

i am boycotting the apple store

I am twittering from iPhone

I am a very vengeful person when you ruin my sweetheart.

I am so over this. I need food. Mmmm bacon...
```


**Similarly, you can specify a range of letters [a-z] or [a-zA-Z]; notice that the order doesn't matter**

**\^[0-9][a-zA-Z] match a number at the beginning of a line followed by either an uppercase or lowercase letter**
```
will match the lines

7th inning stretch
2nd half soon to begin. OSU did just win something
3am - cant sleep - too hot still.. :(
5ft 7 sent from heaven
1st sign of starvagtion
```



**When used at the beginning of a character class, the "^" is also a metacharacter and indicates matching characters NOT in the indicated class**

**[^?.]$ Match any at the end of the line that is not a '?' or a "."**
```
will match the lines

i like basketballs
6 and 9
dont worry... we all die anyway!
Not in Baghdad
helicopter under water? hmmm
```


### More Metacharacters

**"." is used to refer to any character. So**

**9.11** **means, match 9 followed by\<any character\>follwed by 11**

```
will match the lines

its stupid the post 9-11 rules
if any 1 of us did 9/11 we would have been caught in days.
NetBios: scanning ip 203.169.114.66
Front Door 9:11:46 AM
Sings: 0118999881999119725...3 !
```

**\"\|" This does not mean "pipe" in the context of regular expressions; instead it translates to "or"; we can use it to combine two expressions, the subexpressions being called alternatives**

**flood|fire** **means. match "flood" or "fire"**

```
will match the lines

is firewire like usb on none macs?
the global flood makes sense within the context of the bible
yeah ive had the fire on tonight
... and the floods, hurricanes, killer heatwaves, rednecks, gun nuts, etc.
```


#### We can include any number of alternatives...

**flood|earthquake|hurricane|coldfire** **means, match any of those words**

```
will match the lines

Not a whole lot of hurricanes in the Arctic.
We do have earthquakes nearly every day somewhere in our State
hurricanes swirl in the other direction
coldfire is STRAIGHT!
'cause we keep getting earthquakes
```

#### The alternatives can be real expressions and not just literals

**\^[Gg]ood|[Bb]ad** **means, match at beginning of line "Good" or "good" or match "Bad" or "bad" anywhere**

```
will match the lines

good to hear some good knews from someone here
Good afternoon fellow american infidels!
good on you-what do you drive?
Katie... guess they had bad experiences...
my middle name is trouble, Miss Bad News
```


#### Subexpressions are often contained in parentheses to constrain the alternatives

**\^([Gg]ood|[Bb]ad)** **means, match at beginning of line,only, "Good" or "good" or match "Bad" or "bad"**
```
will match the lines

bad habbit
bad coordination today
good, becuase there is nothing worse than a man in kinky underwear
Badcop, its because people want to use drugs
Good Monday Holiday
Good riddance to Limey
```


#### The question mark indicates that the indicated expression is optional

**[Gg]eorge( [Ww]\.)? [Bb]ush** **means, match "George/george", optional match for "W./w." and match "Bush/bush"**
```
will match the lines

i bet i can spell better than you and george bush combined
BBC reported that President George W. Bush claimed God told him to invade I
a bird in the hand is worth two george bushes
```



#### The "*" and "+"" signs are metacharacters used to indicate repetition; * means "any number, including none, of the item" and + means "at least one of the item"**


**(.\*)** **means, match parenthesies and any character in the parenthesies that appears zero or more times**
```
will match the lines

anyone wanna chat? (24, m, germany)
hello, 20.m here... ( east area + drives + webcam )
(he means older men)
()
```

#### The * and + signs are metacharacters used to indicate repetition; * means "any number, including none, of the item" and + means "at least one of the item"

**[0-9]+ (.\*)[0-9]+** **means, match at least one digit "0-9" followed by any number of characters, followed by at least one digit "0 to 9"**
```
will match the lines

working as MP here 720 MP battallion, 42nd birgade
so say 2 or 3 years at colleage and 4 at uni makes us 23 when and if we fin
it went down on several occasions for like, 3 or 4 *days*
Mmmm its time 4 me 2 go 2 bed
```

#### "{" and "}" are referred to as interval quantifiers; they let us specify the minimum and maximum number of matches of an expression

-m,n means at least m but not more than n matches

-m means exactly m matches

-m, means at least m matches

**[Bb]ush( +[^ ]+ +){1,5} debate** **means, match "Bush/bush", followed by a "space", followed by something that is not a "space", followed by at least one "space", 1-5 times, followed by "debate"**
```
will match the lines

Bush has historically won all major debates he's done.
in my view, Bush doesn't need these debates..
bush doesn't need the debates? maybe you are right
That's what Bush supporters are doing about the debate.
Felix, I don't disagree that Bush was poorly prepared for the debate.
indeed, but still, Bush should have taken the debate more seriously.
Keep repeating that Bush smirked and scowled during the debate
```


#### More metacharacters: ( and ) revisited
```
In most implementations of regular expressions, the parentheses not only limit the scope of alternatives divided by a "|", but also can be used to "remember" text matched by the subexpression enclosed

We refer to the matched text with \\1, \\2, etc.
```
So the expression

** +([a-zA-Z]+) +\\1 +** **means, match a "space", followed by at least one character, followed by at leaset one "space", followed by the same pattern we matched before, followed by a "space"**
```
will match the lines

time for bed, night night twitter!
blah blah blah blah
my tattoo is so so itchy today
i was standing all all alone against the world outside...
hi anybody anybody at home
estudiando css css css css.... que desastritooooo
```


#### The * is "greedy" so it always matches the longest possible string that satisfies the regular expression. So

**\^s(.\*)s** **means, match a lowercase "s" at the beginning, followed by some number of characters, followed by an lowercase "s" at the end**
```
matches

sitting at starbucks
setting up mysql and rails
studying stuff for the exams
spaghetti with marshmallows
stop fighting with crackers
sore shoulders, stupid ergonomics
```



#### The greediness of * can be turned off with the ?, as in

**\^s(.\*?)s$**


#### Summary

-Regular expressions are used in many different languages; not unique to R.

-Regular expressions are composed of literals and metacharacters that represent sets or classes of characters/words

-Text processing via regular expressions is a very powerful way to extract data from "unfriendly" sources (not all data comes as a CSV file)

-Used with the functions grep,grepl,sub,gsub and others that involve searching for text strings (Thanks to Mark Hansen for some material in this lecture.)







