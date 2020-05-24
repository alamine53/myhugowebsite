---
author:
  name: "Ramzy Al-Amine"
date: 2019-03-01
linktitle: Measuring the Contribution of Coaches in the NBA
type:
- post 
- posts
title: Measuring the Contribution of Coaches in the NBA
draft: true
weight: 10
series:
- Hugo 101
---



# Introduction

![Popovich spurs] (/images/posts/post2_webimage2_popovich.png)

Tweeting in May 2018, Isaiah Thomas called Brad Stevens “by far the best coach in the NBA” after leading a short-handed Celtics to consecutive playoff runs. But given the lack of relevant metrics, how is one to judge whether this statement is true? If anything, the NBA's coaching award went to Dwayne Casey that year, who was ironically fired weeks after.

![Isiah Thomas' tweet about Stevens] (/images/posts/tweet_thomas_stevens.png)

The debate as to whether coaches matter that much for team performance continues to linger among armchair analysts and those in the sports business. For the average fan, it may be excrutiatingly difficult to question their impact. Some coaches, like Phil Jackson and Red Auerbach, have won too many trophies to deny their importance. But could they have benefitted from exceptional players? 

Some head coaches accomplish eye-cataching statistical features that for some may put to rest the question of their impact. Some coaches seem to do well consistently on different teams and regardless of the cards they are dealt. Greg Popovich is now going into his 22nd season as the head coach of the San Antonio Spurs while failing to miss the post-season a single time over the course of his tenure. Phil Jackson's career win percentage is 70 percent, and this spans X seasons and 2 teams. Steve Kerr has reached the NBA finals 5 times in has first 5 seasons.

In soccer, names like Pep Guardiola, Jose Mourinho, and Jurgen Klopp come to mind when the discussion on legendary coache is brought up. They seem to deliver results wherever they go. In football, Sean McVay

Granted, coaching is dependent on talent. A superior raster may give one coach the edge over another, which complicates the task of estimating their contribution.  play a hand in their success, yet coaches who are great consistently outperform expectations. Popovich has had years where his best player was X. But other coaches have also had talent and faired much worse. In addition,that is not always the case. More tuned-in fans may notice that some coaches do more with less.

 such sought after names are likely to benefit from bigger bugets that can attract superior talent. But that is only after they showed promise in lesser teams with more modest budgets. In other words, they became great coaches before they took on the giants, then grew even more after. There are a few names that come to mind when one thinks of promising names in the coaching sphere today. 


Many great coaches are ignored in that conversation because of a lack of rings. In order for a coach to enter the “greatness” conversation, they must be championship winners. All others are automatically removed from the conversation. They might be highly impactful, yet since we have no other way to measure their impact other than by the ultimate price, they go by unnoticed. But winning a championship is very daunting task that only a select few ever get to experience. Only 1 coach out 20 or 30 (depending on the league) can win each season. Does this mean that all others have not done a good enough job?

The degree to which coaching impacts the outcome of a sports season is much-debated among armchair analysts and anecdotally by those in the sports business, but has been subject to little systematic study. Historically, coaching ability is approximated by the number of championships: Those with most silverware are considered all-time greats. But this approach fails to capture the extent to which a particular head coach plays a role in their team's success. Superior talent may provide some coaches a head start while others may over-achieve given a set of players. 

My paper proposes a new, statistically-robust approach to measuring the relative contribution of head coaches in professional sports. Using data from the NBA, it disentangles their impact as they move across teams while controlling for roster quality and injuries. The NBA is unique in its high frequency of front office changes, with around 60 percent of its coaches being observed on more than one team. Econometrically, this enhances the accuracy of the estimates and efficiently captures the coaching effect.

The resulting estimates allow for identifying excellent coaches, including those who are over-looked by the lack of accolades. They also help compare the contribution of coaches from different eras. For example, changing from the mean head coach to Rick Carlisle generates an estimate 10.5 additional wins when roster characteristics are held at their means [Table 1], while changing to Don Nelson generates 3.8 additional wins.

More importantly, this quantification exercise allows to investigate observable characteristics that shape excellent coaches. For example, the notion that ex-players make for good coaches is debunked in the data. On the contrary, coaches with more diverse backgrounds seem to be better-suited to lead an NBA franchise. Moreover, playoff-seasoned coaches display better results on average.

# Data Analysis

The main estimation strategy follows from the literature on managerial contribution in organizational settings. It consists in a coach-fixed effect regression model that is tweaked to fit the context of the NBA. The model is supplemented by performance-based metrics that capture players' relative ability level at the start of the season. It can be represented by the following equation. 

For coach $i$ in season $t$ (with players $p$ = 1, ..., 5):

\begin{equation}
\text{Wins}_{i,t} = \sum_{p=1}^{5}(\alpha_{p}\text{Talent}_{p,t} + \beta_{p}\text{Injuries}_{p,t}) + \lambda_{i} + \epsilon_{i,t}
\end{equation}

where the dependent variable is the number of wins for team $i$ in season $t$ = {1,2,3}.  Coach fixed effects are captured by $\lambda_{i}$, the variable of interest. ${Talent}_{p,t}$ represents player $p$'s overall contribution from the previous season.

The research provided in this paper sheds light on an aspect of team play that is under-emphasized. In addition to setting strategy, coaches motivate, inspire, and establish a culture. Identifying the right head coach is crucial to maximizing on a team's potential and accentuating its players' relative strengths. The sports world has seen many memorable figures, including the likes Pep Guardiola, Bill Belichik, Phil Jackson, and Greg Popovich. Motivated by their success, this paper views coaching as source of value rather than just a seat to fill. 


# Results

# Conclusion

