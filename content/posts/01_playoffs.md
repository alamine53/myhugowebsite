---
author:
  name: "Ramzy Al-Amine"
date: 2019-06-01
linktitle: My Favorite Music Albums
type:
- post 
- posts
title: The Top 10 Albums That Have Influenced My Taste in Music
weight: 10
draft: false
series:
- Hugo 101
---

Despite a positive showing in Game 1, the Brooklyn Nets were eliminated just five games into their 2018-19 playoff campaign. Given their rather unimpressive roster, some might argue that they were better off tanking. Instead, they marked their first playoff appearance since 2013 and looked to be on the verge of turning a corner as an organization. 

Just below them in the rankings, the Charlotte Hornets witnessed a very different fate going into the next season. While the Nets added superstars Kyrie Irving and Kevin Durant, the Hornets lost their primary scorer and all-star Kemba Walker. Despite finishing only 2 wins apart from each other, these teams witnessed diverging paths.

The NBA tends to follow the championship-or-bust model: If a team doesn't have what it takes to compete for a chip, they're probably better off tanking for a higher draft pick. It might seem like a trivial choice for those at the bottom but should those who are middle-of-the-pack also give in to the power of the ping pong balls? In this post, I use the concept of regression discontinuity to see whether those around the playoff admission threshold have more to gain from making the playoffs or missing it.

Regression discontinuity consists of focusing on observations around a certain admission threshold. The idea is that, over a large enough sample, those observations would be identical in every way other than whether or not they were admitted. This method is used to numerically measure the returns of a certain *treatment* effect whose assignment is based on a continuous variable.

Applying this to the NBA, a trip to the playoffs can be viewed as a $treatment$ for which we are interested in measuring the returns. In other words, what is the true effect of making the playoffs in a given year? For that, we would need to focus our analysis on those just around the playoff admission threshold ~ i.e. 8-seeds and 9-seeds, rather than the whole sample. The reason is that those at the top are systematically better than those at the bottom, therefore they cannot be compared against each other. 

Given that they are close in end-of-season seeding, we can infer that teams around the cutoff point are *very* close in ability levels. The only thing that separates them is that some (8th seeds) *happened* to make the playoffs. Otherwise, they are basically identical. As a result, any difference in outcome can be attributed to the treatment effect ~ i.e. making the playoffs. 

The dependent variable is performance in the following season. In other words, the *treatment effect* is measured in terms of the difference in win percentage (in season *t+1*) for those who barely make the playoffs versus those who barely miss it. 

Note that peformance *during* the playoffs is completely irrelevenat. Whether a team witnesses a first round sweep or makes it all the way to the finals is the same for the sake of the analysis. Either way, 8-seeds typically fare miserably in the post-season. Only 5 times in the last 35 years has an 8-seed been able to get past the first round, and neither of those has lead to a championship. 

Those who finish 9th don’t participate in the post-season at all. Instead, they earn a spot in the lottery which gives them a first-hand shot at improving their long-term future throught the draft. Although it’s rare than a 9-seed wins the first overall pick (it happened once in 1993), a top-5 position is not out of the picture. In the last X years, they have earned a top-6 pick X times and a top-10 pick X+5 times. 

So, one could argue that 9-seeds have at least *something* to gain from missing the playoffs. As such, there is no reason to believe than 8-seeds are in a better position going forward, unless a few playoff games can make a difference. But what does the data say? How do 8-seeds perform, on average, relative to 9-seeds in the following season?

This is an interesting question because, given their ranking, both teams are fairly close in ability level, so unless the playoff provides some sort of benefit, one should expect them to progress uniformly.

However, the data suggests that 8th seeds are much more likely to improve in the following season than 9th seeds. In fact, 9th seeds are more likely to regress. On average, 8th seeds experience a 2.1 percent improvement while 9th seeds experience a 5.9 percent drop. The difference between the average outcomes – which is 8.0 percent – can be thought of as the average treatment effect, or the returns from playoff experience. 


![RD Chart] (/images/posts/post1_chart1.png)

The question then becomes, where is this difference in future performance coming from? 

The benefits from being in a playoff series are many, especially for teams with promising but unpolished players. For one, the incredibly competitive environment is are great for learning and provides tremendous growth opportunities for players at their start of their careers. The 2017-18 season witnessed the come-up of Jayson Tatum who put the short-handed Celtics team on his back during the playoffs. Tatum now looks to be the centerpiece for the Celtics’ future as the team looks to build around them.

Most playoff games are nationally-televised, providing a chance for players to make a name for themselves at the biggest stage. This year was the turn for players like Jamal Murray, D’Angelo Russell, and Derrick White – whose names seemed to echo in every Sports Center highlight. With such wide recognition, these players are more likely to become stars and earn interest from the big teams around the league. Russell is a proof of that as the Golden State Warrior sought him in return for losing their primary scorer – Kevin Durant. Before his brief stunt with the Nets, which was solidified in the playoffs, Russell was a loosely traded commodity around the league.

The playoffs also makes teams more attractive as a destination for good coaches and star players around the league. Teams competing in the playoffs give signs of seriousness when it comes to the desire to win. It sends a signal that they will do what it takes to get closer to a championship. Indeed, a perfect illustration of this is the Brooklyn Nets who had an incredible off-season attracting two of the league’s biggest names versus the New York Knicks who failed to make any meaningful signing despite their desparate needs for that. Both teams had both the cap space and the intent to bring-in Durant and Irving, yet the Brooklyn side was a clear favorite for the star duo.

The playoffs also does wonders to team chemistry. There’s no question that a first-round exit from the 2017-18 playoffs has brought the Milwaukee Bucks closer to being a contender in the East. They are now a couple of games away from their first Finals appearance since 1974. It would be no surprise to see the Brooklyn Nets take a similar leap next year.

All of these factors provide tangible benefits team more attractive as a destination for good coaches and free agents during the off-season. When exploring the market, more talented players are likely to choose teams where they are certain to play at the big stage, so having recently been in the post-season improves a team’s chances of landing big names.

Even with little chance of going all the way, teams who make the playoffs are in for a treat. 8th seeds typically exit from the first round because they face the top seed, yet despite this, we see a significant difference in their future performance relative to the 9th seed. This can be traced to the “playoffs effect.”

This is an important finding because it shows that teams can build on their roster without needing to go through the lottery. The playoffs provide a valuable stepping stone for that. Sure, the lottery may have something out there, but only by going through the trials and tribulations does a team eventually become a serious contender.