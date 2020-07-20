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

At a 2017 Sloan Sports Analytic Conference panel, Zach Lowe raised a question that had been on my mind for a while: "When will we have metrics that capture coaches' contribution?" Like many basketball enthusiasts, it's quite evident to me, from watching and [playing professionally](https://www.asia-basket.com/Lebanon/basketball-National-Team.asp?Age=18&Year=2010) for so long, that some coaches are able to elevate team performance more than others. But the analytics community has yet to come up with a metric that systematically captures that. So, I set out to fill this gap. 

The project started while I was completing my Master's in Applied Economics, during which I happened to read a number of academic papers on sports economics. I came across [a paper on the impact of managers in the German Bundesliga](https://journals.sagepub.com/doi/abs/10.1177/1527002516674760) and decided to replicate the methodology on NBA coaches. I soon realized that the NBA is an ideal environment for two main reasons:

1. **We are able to capture player quality pretty well**, thanks to advanced performance metrics such as Win Shares, VORP, BPM.. etc. This has yet to be the case in soccer. 

2. **The turnover rate of coaches is quite high**. Most NBA coaches are observed on more than one team, with some on as many as 11 (Larry Brown). This reduces standard errors, allowing to trace their impact accurately as they move across teams.

The project continued to evolve as I gathered feedback from professors and later on from colleagues at the IMF. The code was originally built in Stata, but I've redone it in Python in order to incorporate some additional features. You can find it [this](https://github.com/alamine53/nba_coach_FixedEffects) Github repo. For the sake of clarity, I will leave out some important details from this article. If you're interested in the technicalities, I encourage you to check out [my working paper](https://www.ramzyalamine.com/files/alamine_coaches.pdf). 



### Controlling for Roster Quality

The main challenge in assessing the impact of coaches is accounting for roster quality. This is why looking at winning records alone can be misleading. For example, Phil Jackson is an astonishing 70% over his career, but some could argue he benefited from superior talent (Michael Jordan, Kobe Bryant, Shaquille O'Neal, to a name a few). So, how do we account for that? How do we know whether it wasn't the other way around, that it's the players who benefitted from his coaching?

Other coaches fly under the radar despite outperforming with lesser rosters. Many would consider Brad Stevens as one of the league's best coaches, especially after taking a roster led by Isaiah Thomas to the top of the Eastern Conference in [2016-17](https://www.basketball-reference.com/teams/BOS/2017.html). To Stevens' credit, Thomas has not had anywhere near this kind of individual or team success on any of [the other 7 teams he's played on]((https://www.basketball-reference.com/players/t/thomais02.html)). Of course, it could have been a lucky match. Either way, it's impossible to put in numbers the size of Stevens' impact as the current analytics landscape lacks any systemic quantification of the coaching effect.

The model I develop here tackles these issues. It controls for roster quality by including the players' performance in the previous season. For a given coach in a given season *t*, I take into account the players' performance in season *t-1*. Specifically, I compute the roster's mean Value Over Replacement Player (VORP) from that season as a measure of its "quality".

### 'Fixed Effects' as a Metric for Coaches

Using a 'fixed effect' regression model, I estimate the correlation between head coach identity and team wins for 209 head coaches (since 1985), while controlling for roster quality. What this produces is the [fixed effect](https://en.wikipedia.org/wiki/Fixed_effects_model) for each head coach. The resulting metric, which I am calling 'Coach Fixed Effect', measures the additional wins contributed, on average, while controlling for roster quality. 

As shown in the below histogram, I obtain a nice distribution of fixed effects. The range of values is from -25 to +21, resulting in a range of 46 wins per season. The mean fixed effect is 0, which is a nice property because it simplifies interpretation. A value of +10.0 means the coach generates 10 additional wins per season relative to the mean historical head coach. 

![histogram] (/images/posts/coaches/histogram.png)


### Top Coaches

The top 15th percentile of coaches are shown in the below figure. Changing from the mean head coach to Steve Kerr generates an additional 28 wins when roster quality is held at its mean. Kerr is by far the most impactful, followed by Phil Jackson and Gregg Popvich with 20 wins each. It is important to note that the data set stops at 2018, therefore the recent Warriors struggles are not captured in this model. 


These metrics are point estimates, therefore they are accompanied with [confidence intervals](https://en.wikipedia.org/wiki/Confidence_interval). Coaches with fewer observations are subject to higher standard errors. For example, Nick Nurse is only observed on 3 seasons in the dataset - therefore the error bar is significantly higher than Phil Jackson or Gregg Popovich who are observed on 15+ seasons. In other words, the error margin is reduced as a coach's career unfolds.

![bar_chart] (/images/posts/coaches/top10_barchart.png)


### Underrated Coaches

The scatter plot below places all of the coaches in terms fixed effect (y-axis) versus the "traditional" measure of career win percentage. The point is to show that, despite those being closely related, they are not exactly identical. The further a coach is from the 45 degree line, the more his actual impact is misrepresented by his winning record. Observations in yellow correspond to the fixed effect rank being larger than the win rank, therefore they represent underrated coaches. Vice versa, observations in purple represent overrated coaches (or, more accurately, those whose success was driven heavily by superior player quality).

![scatter] (/images/posts/coaches/scatter_plot.png)

### Predictive Power

To determine whether these estimated fixed effects have any usefulness for the real world, I investigate their predictive power. I ask the following question: Knowing a coach's performance up to season *t*, does that tell me anything about his future performance on season *t+1*? 


The line chart below compares the RMSE for my fixed effect model against a model of just roster quality. The RMSE is calculated based on a cross-validation exercise (see working paper for full details). I find that fixed effects improve forecast accuracy of team wins by as much as 15 percent. 

![rmse] (/images/posts/coaches/forecast_error_per_season.png)


### Coverage  

My dataset covers all NBA teams between 1985 and 2018. The unit of observation is a team-season, which leads to about 900 observations (~ 30 teams x 35 seasons). I source all of the data, including coach and roster information, team wins, and player metrics (for the sake of robustness, I try VORP, WS, BPM... etc as roster quality measures), from the [BBRef website](https://www.basketball-reference.com/)

### How Fixed Effects are Calculated  

