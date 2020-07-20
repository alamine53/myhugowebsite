---
date: 2020-04-01
type: Sports Economics
title: Quantifying the Coaching Effect in the NBA
summary: I estimate the relative added-value of NBA head coaches in light of roster characteristics and injuries. I find that the top coaches (e.g. Steve Kerr, K.C. Jones, Phil Jackson, and Greg Popovich), elevate team performance by as much as 20 wins per season. These estimated fixed effects are also useful in predicting team wins for future coach-team pairings. 
featured_image: "/images/posts/coaches/scatter_plot.png"
draft: false
weight: 1
---
![bar_chart] (/images/posts/coaches/thumbnail.png)

### Introduction

At the 2017 Sloan Sports Analytic Conference, Zach Lowe raised a question that had been on my mind for a while: "When will we have metrics that capture coaches' contribution?" Like many basketball enthusiasts, it's quite evident to me, from watching and [playing professionally](https://www.asia-basket.com/Lebanon/basketball-National-Team.asp?Age=18&Year=2010), that some coaches are able to elevate team performance more than others. But the analytics community has yet to come up with a metric that systematically captures that. So, I've set out to fill this gap. 

The project started as I was completing my Master's in Applied Economics, during which I happened to read a number of academic papers on sports economics. I came across [a paper on the impact of managers in the German Bundesliga](https://journals.sagepub.com/doi/abs/10.1177/1527002516674760) and decided to replicate the analysis on NBA coaches. I soon realized that the NBA is an ideal environment for two main reasons:

1. **We are able to capture player quality pretty well**: Thanks to advanced performance metrics such as Win Shares, VORP, BPM.. etc,  we can control for roster quality, which is not the case in soccer. 

2. **The turnover rate of coaches is high**. Most NBA coaches are observed on more than one team, with some on as many as 11 (Larry Brown). This reduces standard errors, allowing to trace their impact accurately as they move across teams.

The project continued to evolve as I gathered feedback from professors and later on from colleagues at the IMF. The code was originally built in Stata, but I've redone it in Python in order to incorporate some additional features. Here's the [Github repo](https://github.com/alamine53/nba_coach_FixedEffects). 

For the sake of clarity, I will leave out some details from this article. If you're interested in the technicalities, I encourage you to check [my working paper](https://www.ramzyalamine.com/files/alamine_coaches.pdf). 



### Controlling for Roster Quality

The main challenge in assessing the impact of coaches is accounting for roster quality. This is why looking at winning records alone can be misleading. For example, Phil Jackson has an astonishing 70% win record over his career, but some could argue he benefited from superior talent (Michael Jordan, Kobe Bryant, Shaquille O'Neal, to a name a few). So, how do we account for that? How do we know whether it the coach who benefited from the players and not the other way around?

Some coaches fly under the radar despite outperforming with lesser rosters. Many would consider Brad Stevens as one of the league's best coaches, especially after taking a roster led by Isaiah Thomas to the top seed in the Eastern Conference in [2016-17](https://www.basketball-reference.com/teams/BOS/2017.html). To Stevens' credit, Thomas has had nowhere near this kind of individual or team success on any of [the other 7 teams he's played on]((https://www.basketball-reference.com/players/t/thomais02.html)). It could have been luck, but Stevens seems to consistently derive the most out of his players (think of Jae Crowder, Kelly Olynyk, Aaron Baynes). It's impossible to put in numbers the size of Stevens' impact simply because there are no metrics for that. The current analytics landscape lacks any systemic quantification of the coaching effect.

### 'Fixed Effects' as Metrics for Coaches

The model I develop generates metrics that capture a coach's average impact on team wins while controlling for roster quality. I use a regression model called 'Fixed Effects' that includes players' performance in the previous season as a proxy for quality. The analysis covers 209 head coaches across all NBA teams since 1985. 

I obtain a nice distribution of fixed effects. As shown in the below histogram, the range of values is from -25 to +28 (Steve Kerr). The mean fixed effect is 0, which means that a value of +10.0 indicates that a coach generates 10 additional wins per season relative to the mean. 

![histogram] (/images/posts/coaches/histogram.png)


### Top Coaches

The top 15th percentile of coaches are shown in the below figure. Changing from the mean head coach to Steve Kerr generates an additional 28 wins when roster quality is held at its mean. Kerr is by far the most impactful, followed by Phil Jackson and Gregg Popvich with 20 wins each. It is important to note that the data set stops at 2018, therefore the recent Warriors struggles are not captured in this model. 


These metrics are point estimates, therefore they are accompanied with [confidence intervals](https://en.wikipedia.org/wiki/Confidence_interval). Coaches with fewer observations are subject to higher standard errors (and wider confidence intervals). Since Nick Nurse, for example, is only observed on 3 seasons, his Fixed Effect has a high degree of uncertainty. Meanwhile, Phil Jackson and Gregg Popovich, who have considerably more observations, have lower standard errors. 

![bar_chart] (/images/posts/coaches/top10_barchart.png)


### Underrated Coaches

One of the main advantages of this model is identifying coaches whose impact is overlooked by their team's winning record. Each dot in the chart represents one NBA head coach according to his estimated fixed effect (y-axis) and career win percentage (x-axis). The further the dot from the 45 degree line, the larger the mis-representation between both measures. Observations in yellow correspond to coaches who outperform expectations on a consistent basis, while observations in purple represent coaches who underperform given a threshold of roster quality.

The point is to show that, despite those being closely related, they are not exactly identical. 
![scatter] (/images/posts/coaches/scatter_plot.png)

### Predictive Power

To determine whether these estimated fixed effects have any usefulness for the real world, I investigate their predictive power. I ask the following question: Knowing a coach's performance up to season *t*, does that tell me anything about his future performance on season *t+1*? 


The line chart below compares the RMSE for my fixed effect model against a model of just roster quality. The RMSE is calculated based on a cross-validation exercise (see working paper for full details). I find that fixed effects improve forecast accuracy of team wins by as much as 15 percent. 

![rmse] (/images/posts/coaches/forecast_error_per_season.png)


### Coverage  

My dataset covers all NBA teams between 1985 and 2018. The unit of observation is a team-season, which leads to about 900 observations (~ 30 teams x 35 seasons). I source all of the data, including coach and roster information, team wins, and player metrics, from [Basketball Reference](https://www.basketball-reference.com/).

### How Fixed Effects are Calculated  

For a given coach in a given season *t*, I take into account the players' performance in season *t-1*. Specifically, I compute the roster's mean Value Over Replacement Player (VORP) from that season as a measure of its "quality".

Using a 'fixed effect' regression model, I estimate the correlation between head coach identity and team wins for 209 head coaches (since 1985), while controlling for roster quality. What this produces is the [fixed effect](https://en.wikipedia.org/wiki/Fixed_effects_model) for each head coach. The resulting metric, which I am calling 'Coach Fixed Effect', measures the additional wins contributed, on average, while controlling for roster quality. 
