---
layout: post
title:  "A Man's First App"
date:   2017-01-30 04:35:37 +0000
---


First, I want to address why this post is mere hours after my first.  I had been sitting on my initial post for quite some time and had finally gotten enough courage to actually complete it.  With that being cleared up...


## The English Premier League CLI

I just recently finished building my first app, which is now also a ruby gem.  I believe it's fairly well written for a beginner but I'll let others be the judge of that.  As to its practicality, I'm not so sure, but hey, this is a learning process.

I named my app the English Premier League CLI and built it in Ruby.  it provides a CLI version of the current English Premier League (that's the top flight of English football/soccer for the uninitiated) table.  A user can then choose to learn more about a particular club by providing input.  
I have always been a fan of football/soccer to the point that even as an American, I call the sport football.  

I was told that the best way to build your first app, if you're strapped for ideas, is to work on something you're passionate about so that's what I did.  Conception to initial publishment took me a little under a week.

I was taught to write out what you expect your code to do in pseudocode or even just plain English, then stub out the code with fake data slowly adding on functionality until you have your final product.  It works like a dream.  For example, let's say I have a method called `#ask_for_team`; I might start out with:

```
def ask_for_team
  # gets user input
    # it evaluates the input
    # if the input == 'exit' then exit program
    # if input == team.name then display team
    # if input == team.rank then display team
    # else puts "Invalid Entry" then re-prompts the user for input
end
```

You might not even have the idea of adding all that functionality, it'll just come to you as you build it.  In regards to the code above, I just built a fake teams array and pushed fake teams into that array.  When I mean "fake" I mean data not imported from an API or scraped from a website, fake data == hardcoded data.  This allowed me to build out the method and other methods this one depended on without having the worry of getting the data right, that will come later.  Eventually, I ended up with this:

```
def ask_for_team(input)

    if input.downcase == 'exit'
      bye

    elsif input.to_i == 0
      team = @teams.find{|team| team.name.downcase == input.downcase}
      team != nil ? print_team(team) : spell_check

    elsif input.to_i.between?(1, 20)
      team = @teams.find{|team| team.rank == input}
      print_team(team)

    else
      spell_check
    end
  end
```

I'll link the source code at the end because I know that the code above has a lot of unknowns for someone that isn't familiar with the app. Nevertheless,  what I'm trying to essentially get across is that from my initial pseudocode I already knew how I wanted my code to work. Also, by doing that, I had typed it out so I don't forget it.  

I then hardcoded data so that I could turn the pseudocode into actual code. I made `team_1.name = "Chelsea"   team_1.rank = "1" team_2.name = "Arsenal" etc...` then I made `@teams = []` and shovelled all that hardcoded data into the array so I could build out this method.  That pseudocode and stubbing out data had helped immensely when building the app.  I could just replace the fake data with actual data and still have the method work.  It's an invaluable tool I can see myself using for a long time.

As a said earlier the build process took me about a week.  The scraping was the most tasking part, but it always is.  However is also the most rewarding, and seeing everything come together is just pure bliss.

The source code is [available on github](https://github.com/jilustrisimo/epl-cli-gem) which also has a link to the gem in RubyGems.org.
