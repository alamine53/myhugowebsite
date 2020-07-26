---
date: 2020-04-01
type: Sports Economics
title: Quantifying the Coaching Effect in the NBA
summary: Using a coach-fixed effect regression model, I find that the top NBA coaches elevate team performance by as much as 20 additional wins per season. 
featured_image: /images/posts/coaches/scatter_plot_notitle.png
images: /images/posts/coaches/scatter_plot_notitle.png
thumbnail: /images/posts/coaches/scatter_plot_notitle.png
draft: false
weight: 1
---
![coach_faces] (/images/posts/coaches/thumbnail.png)


### Introduction

Coaching analysis remains largely a black box in the NBA. Despite being heavily debated by armchair analysts and those in the sports business, the degree to which coaches impact the outcome of a basketball season continues lack any systematic study. At the same time, it can be quite evident---even to the casual observer---that some coaches elevate team performance *much more* than others. In this article, I propose an econometrically-robust methodology to measure that.

The project started during my graduate studies in economics, where I happened to read a number of academic papers on sports economics (having played basketball professionally, this was an effective way to learn about economic research while being geniunely interested in the content matter). I came across [a paper](https://journals.sagepub.com/doi/abs/10.1177/1527002516674760) that studied the impact of managers in the German Bundesliga, and decided to replicate the analysis on NBA coaches. I soon realized that the NBA was an ideal environment for two main reasons:

1. **Player quality can be captured fairly accurately,** thanks to advanced performance metrics such as Win Shares, Value Over Replacement (VORP), Real Plus-Minus... etc. 

2. **The turnover rate of coaches is high.** Most NBA coaches are observed on more than one team (with some on as many as 11), therefore reducing standard errors.

I've always been interested in the question of coaching. The project continued to evolve as I gathered feedback from professors and later on from colleagues at the IMF. The code was originally built in Stata, but I've redone it in Python in order to incorporate some additional features. Here's the [Github repo](https://github.com/alamine53/nba_coach_FixedEffects). 

For the sake of clarity, I will leave out some details from this article. If you're interested in the technicalities, I encourage you to check [my working paper](https://www.ramzyalamine.com/files/alamine_coaches.pdf). If you'd like to jump straight to the ratings, they are at the bottom of the page. 



### Controlling for Roster Quality

The main challenge in systematically assessing the impact of coaches is accounting for roster quality. Some coaches may benefit from stronger lineups for achieving good winning records. This is why looking at the winning record for someone like Phil Jackson can be misleading. While he maintained an astonishing 70% win record over his career, some could argue that much of it is due to coaching superior talent (Michael Jordan, Kobe Bryant, Shaquille O'Neal, to a name a few). So, how do we account for that? How do we know whether it's the coach who benefited from the players and not the other way around?

Some coaches fly under the radar despite outperforming with lesser rosters. Many would consider Brad Stevens as one of the league's best young coaches, especially after taking a roster led by Isaiah Thomas to the top seed of the Eastern Conference in [2016-17](https://www.basketball-reference.com/teams/BOS/2017.html). To Stevens' credit, Thomas has had nowhere near this kind of individual or team success on any of [the other 7 teams he's played on]((https://www.basketball-reference.com/players/t/thomais02.html)). It could have been luck, of course, but Stevens seems to consistently derive the most out of even secondary players (think Jae Crowder, Kelly Olynyk, Aaron Baynes) and outperform expectations. 

If one is to measure the pure coaching effect, then one needs to take into considerations that Jackson and Stevens have had different starting points. 

### 'Fixed Effects' as Metrics for Coaches

Coach Fixed Effects (Coach FE) capture the average additional wins contributed while controlling for roster quality. I take into account the players' performance in the previous season as a proxy for quality. The analysis covers 159 head coaches across all teams from 1985 to 2018. 

Here's a look at the distribution of Coach FE estimates. Values range from -25 to +21. The mean fixed effect is close to 0, which means that a value of +10.0 generates about 10 additional wins per season relative to the mean. 

![histogram] (/images/posts/coaches/histogram.png)


### Top Coaches

The top 15th percentile of coaches are shown in the below figure. Changing from the mean head coach to Nick Nurse generates an additional 21 wins when roster quality is held at its mean. Similarly, changing to Steve Kerr generates 18 wins on average. 

These metrics are point estimates, therefore they are accompanied with [confidence intervals](https://en.wikipedia.org/wiki/Confidence_interval). As shown by the error bars in the below chart, coaches with fewer observations are subject to higher standard errors (and wider confidence intervals). Since Nick Nurse, for example, is only observed on just 1 season, his Fixed Effect could be anywhere from +7 to +40. This margin will decrease as he coaches more seasons. Phil Jackson and Gregg Popovich, meanwhile, have much higher certainty because they have more decorated careers.

![bar_chart] (/images/posts/coaches/top10_barchart.png)


### Underrated Coaches

One of the main advantages is identifying coaches whose impact is overlooked by their team's winning record. Each dot in the below chart represents a head coach. On the y-axis would be on his percentile rank based on estimated fixed effect and on the x-axis is his percentile rank based on win percentage. The further the dot from the 45 degree line, the larger the difference between the two approaches. For example, observations in yellow are ranked higher in fixed effect relative to win percentage, therefore they correspond to coaches who are under-rated given team performance. Observations in purple represent those whose success record is largely due to superior players.

Based on this comparison, the most "over-rated" head coach would be David Blatt, who ranks around the top in win percentage but below average in fixed effect. This suggests that Blatt, who coached for only one full season with the Cavs, did not necessarily outperform given how his players had performed in prior seasons. The most "under-rated" head coach would be J.B. Bickerstaff, who despite ranking around the center in win percentage, had done considerably well given the quality of his roster. Note that the estimates for both these coaches are associated with high standard errors due to low observations. 

![scatter] (/images/posts/coaches/scatter_plot.png)

### Predictive Power

To determine whether these estimated fixed effects have any usefulness for the real world, I investigate their predictive power. I ask the following question: Knowing a coach's performance up to season *t*, does that tell me anything about his future performance on season *t+1*? 


The line chart below compares the RMSE for my fixed effect model against a model of just roster quality. The RMSE is calculated based on a cross-validation exercise (see working paper for full details). I find that fixed effects improve forecast accuracy of team wins by as much as 15 percent. 

![rmse] (/images/posts/coaches/forecast_error_per_season.png)


### How Fixed Effects are Calculated  

First, I calculate the 'roster quality' variable for each team since the beginning of the dataset. For each roster at time *t*, I sort players by descending number of minutes played and keep only the top 5 players with most usage (this helps eliminate those with significant injuries). Using VORP, I calculate the players' cumulative performance in season *t-1* as a proxy for roster quality in season *t*.

Note that what you see here is one specification (VORP for 5-player roster) out of hundreds. For robustness, I also consider rosters of 3 and 7 players but I find optimal results with 5. In addition, I repeat the same calculations using a number of other metrics instead VORP (computing means instead of sums where necessary), including Win Shares, Box Plus-Minus, and Player Efficiency Rating. Once again, I find highest forecasting accuracy with VORP. You can find more robustness checks in [the paper](https://www.ramzyalamine.com/files/alamine_coaches.pdf).

Using a 'fixed effect' regression model, I estimate the correlation between head coach identity and team wins for 209 head coaches (since 1985), while controlling for roster quality. What this produces is the [fixed effect](https://en.wikipedia.org/wiki/Fixed_effects_model) for each head coach. The resulting metric, which I am calling 'Coach Fixed Effect', measures the additional wins contributed, on average, while controlling for roster quality. 

### Potential Shortcomings

1. **Player development being credited to the coach.** Since performance at t-1 is used as a proxy for player quality, season-to-season growth is not accurately accounted for as an independent variable, leading to upward bias on the fixed effect. In other words, the model could favor coaches with budding superstars, such as Scott Brooks with the Oklahoma City Thunder. I foresee two ways of addressing this. First is using a weighted average of the prior X seasons, not just t-1, with weights assigned by proximity. Second is incorporating posterior seasons in the player variable. 

2. **High Uncertainty for coaches with few observations.** Low observations can be due either to the coach being relatively recent (Nick Nurse) or having had a short career as a head coach. For example, both Larry Bird and Danny Ainge moved on to the General Manager positions after just three seasons as head coach. It's not surprising, given their promotion, that they both appear in the top 10th percentile of coaches. 


### Coverage  

The dataset covers all NBA teams between 1985 and 2018. The unit of observation is a team-season, which leads to about 900 observations (~ 30 teams x 35 seasons). I source all of the data, including coach and roster information, team wins, and player metrics, from [Basketball Reference](https://www.basketball-reference.com/).

### Full Metrics

Click [here](/files/results.csv) for a csv version of the below table.

|     | Name               |Coach FE |    t_stat | Pct Rk (FE) | Pct Rk (Wins) |   Career Win% |
|----:|:-------------------|--------:|----------:|------------:|--------------:|--------------:|
|   0 | Nick Nurse         |   22.33 |      2.64 |           1 |          0.98 |          0.71 |
|   1 | Danny Ainge        |   21.47 |      2.54 |        0.99 |          0.96 |          0.64 |
|   2 | Steve Kerr         |   16.77 |      3.9  |        0.99 |          1    |          0.79 |
|   3 | Gregg Popovich     |   16.65 |      8.53 |        0.98 |          0.97 |          0.69 |
|   4 | Larry Bird         |   14.66 |      2.45 |        0.98 |          0.99 |          0.74 |
|   5 | Tom Thibodeau      |   11.84 |      3.41 |        0.97 |          0.93 |          0.59 |
|   6 | Billy Cunningham   |   11.63 |      1.37 |        0.96 |          0.99 |          0.72 |
|   7 | Phil Jackson       |   11.35 |      5.65 |        0.96 |          0.98 |          0.7  |
|   8 | Scott Brooks       |   11.11 |      3.68 |        0.95 |          0.91 |          0.59 |
|   9 | Del Harris         |   10.99 |      3.64 |        0.94 |          0.85 |          0.55 |
|  10 | Mike Budenholzer   |   10.7  |      2.82 |        0.94 |          0.86 |          0.55 |
|  11 | Frank Layden       |   10.48 |      2.47 |        0.93 |          0.68 |          0.49 |
|  12 | Kevin McHale       |   10.11 |      2.38 |        0.92 |          0.86 |          0.55 |
|  13 | Pat Riley          |    9.75 |      4.87 |        0.92 |          0.95 |          0.64 |
|  14 | Butch Carter       |    9.62 |      1.14 |        0.91 |          0.71 |          0.5  |
|  15 | Scott Skiles       |    9.56 |      3.34 |        0.91 |          0.72 |          0.5  |
|  16 | Frank Vogel        |    9.2  |      2.42 |        0.9  |          0.75 |          0.51 |
|  17 | Jeff Van Gundy     |    9.11 |      3.02 |        0.89 |          0.91 |          0.59 |
|  18 | Brad Stevens       |    8.66 |      2.28 |        0.89 |          0.84 |          0.55 |
|  19 | Chuck Daly         |    8.64 |      3.33 |        0.88 |          0.93 |          0.61 |
|  20 | K.C. Jones         |    8.59 |      2.22 |        0.88 |          0.97 |          0.7  |
|  21 | Erik Spoelstra     |    8.46 |      3.12 |        0.87 |          0.92 |          0.59 |
|  22 | Billy Donovan      |    8.32 |      1.7  |        0.86 |          0.94 |          0.61 |
|  23 | Quin Snyder        |    8.28 |      1.95 |        0.86 |          0.85 |          0.55 |
|  24 | Rick Pitino        |    8.13 |      1.91 |        0.85 |          0.67 |          0.48 |
|  25 | Stan Van Gundy     |    8.11 |      2.99 |        0.84 |          0.9  |          0.58 |
|  26 | Lionel Hollins     |    8.1  |      2.13 |        0.84 |          0.7  |          0.49 |
|  27 | Rick Adelman       |    7.13 |      3.74 |        0.83 |          0.9  |          0.59 |
|  28 | Dave Joerger       |    7.04 |      1.85 |        0.82 |          0.72 |          0.5  |
|  29 | Rick Carlisle      |    7    |      3.24 |        0.82 |          0.82 |          0.55 |
|  30 | George Karl        |    6.67 |      3.46 |        0.81 |          0.92 |          0.59 |
|  31 | Mike Brown         |    6.66 |      2.05 |        0.81 |          0.95 |          0.62 |
|  32 | Mike Schuler       |    6.61 |      1.35 |        0.8  |          0.77 |          0.53 |
|  33 | Flip Saunders      |    6.19 |      2.6  |        0.79 |          0.78 |          0.53 |
|  34 | Larry Brown        |    5.86 |      2.87 |        0.79 |          0.84 |          0.55 |
|  35 | Doug Collins       |    5.82 |      2.15 |        0.78 |          0.76 |          0.52 |
|  36 | Doc Rivers         |    5.81 |      2.75 |        0.78 |          0.89 |          0.58 |
|  37 | Steve Clifford     |    5.68 |      1.49 |        0.77 |          0.67 |          0.48 |
|  38 | J.B. Bickerstaff   |    5.62 |      0.66 |        0.76 |          0.4  |          0.39 |
|  39 | Mike Fratello      |    5.47 |      2.2  |        0.76 |          0.87 |          0.56 |
|  40 | Rudy Tomjanovich   |    5.39 |      1.99 |        0.75 |          0.89 |          0.57 |
|  41 | Cotton Fitzsimmons |    5.26 |      1.5  |        0.74 |          0.81 |          0.54 |
|  42 | Frank Johnson      |    5.21 |      0.62 |        0.74 |          0.64 |          0.47 |
|  43 | Paul Westphal      |    5.17 |      1.49 |        0.73 |          0.83 |          0.55 |
|  44 | Vinny Del Negro    |    5.01 |      1.32 |        0.72 |          0.79 |          0.54 |
|  45 | Jim O'Brien        |    4.89 |      1.41 |        0.72 |          0.66 |          0.48 |
|  46 | Jerry Sloan        |    4.7  |      2.34 |        0.71 |          0.94 |          0.61 |
|  47 | Don Nelson         |    4.65 |      2.26 |        0.71 |          0.88 |          0.57 |
|  48 | Jason Kidd         |    4.55 |      1.07 |        0.7  |          0.69 |          0.49 |
|  49 | Tyronn Lue         |    4.54 |      0.54 |        0.69 |          0.94 |          0.61 |
|  50 | Doug Moe           |    4.3  |      1.23 |        0.69 |          0.78 |          0.53 |
|  51 | Mike Malone        |    4.17 |      0.98 |        0.68 |          0.69 |          0.49 |
|  52 | Lenny Wilkens      |    3.94 |      1.88 |        0.68 |          0.83 |          0.55 |
|  53 | Jeff Hornacek      |    3.82 |      0.78 |        0.67 |          0.5  |          0.43 |
|  54 | Mike D'Antoni      |    3.7  |      1.36 |        0.66 |          0.87 |          0.56 |
|  55 | Mark Jackson       |    3.56 |      0.73 |        0.66 |          0.76 |          0.51 |
|  56 | Maurice Cheeks     |    3.07 |      0.88 |        0.65 |          0.7  |          0.49 |
|  57 | Nate McMillan      |    2.97 |      1.2  |        0.64 |          0.77 |          0.52 |
|  58 | Kevin Loughery     |    2.95 |      0.77 |        0.64 |          0.56 |          0.45 |
|  59 | Dwane Casey        |    2.68 |      0.89 |        0.63 |          0.81 |          0.54 |
|  60 | Brian Hill         |    2.22 |      0.64 |        0.62 |          0.68 |          0.48 |
|  61 | Paul Silas         |    2.14 |      0.62 |        0.62 |          0.56 |          0.45 |
|  62 | Randy Wittman      |    2.02 |      0.62 |        0.61 |          0.45 |          0.41 |
|  63 | Dan Issel          |    1.87 |      0.44 |        0.61 |          0.62 |          0.46 |
|  64 | Chris Ford         |    1.83 |      0.57 |        0.6  |          0.62 |          0.46 |
|  65 | Avery Johnson      |    1.75 |      0.46 |        0.59 |          0.88 |          0.57 |
|  66 | Dick Versace       |    1.69 |      0.2  |        0.59 |          0.61 |          0.46 |
|  67 | Terry Stotts       |    1.34 |      0.44 |        0.58 |          0.75 |          0.51 |
|  68 | Larry Drew         |    1.13 |      0.27 |        0.57 |          0.49 |          0.42 |
|  69 | Fred Hoiberg       |    1.05 |      0.18 |        0.57 |          0.49 |          0.43 |
|  70 | Dick Motta         |    0.87 |      0.25 |        0.56 |          0.46 |          0.41 |
|  71 | Eric Musselman     |    0.84 |      0.17 |        0.56 |          0.55 |          0.44 |
|  72 | Monty Williams     |    0.77 |      0.2  |        0.55 |          0.54 |          0.43 |
|  73 | Stu Jackson        |    0.62 |      0.07 |        0.54 |          0.5  |          0.43 |
|  74 | David Fizdale      |    0.25 |      0.04 |        0.54 |          0.35 |          0.37 |
|  75 | Lloyd Pierce       |    0.06 |      0.01 |        0.53 |          0.31 |          0.35 |
|  76 | Tyrone Corbin      |    0.05 |      0.01 |        0.52 |          0.48 |          0.42 |
|  77 | P.J. Carlesimo     |    0.04 |      0.01 |        0.52 |          0.56 |          0.45 |
|  78 | John Lucas         |    0.02 |      0.01 |        0.51 |          0.43 |          0.4  |
|  79 | Dave Cowens        |    0.01 |      0    |        0.51 |          0.65 |          0.47 |
|  80 | Bill Fitch         |   -0    |     -0    |        0.5  |          0.69 |          0.49 |
|  81 | Jack Ramsay        |   -0.27 |     -0.06 |        0.49 |          0.74 |          0.51 |
|  82 | Isiah Thomas       |   -0.28 |     -0.07 |        0.49 |          0.61 |          0.46 |
|  83 | Mike Montgomery    |   -0.44 |     -0.07 |        0.48 |          0.47 |          0.41 |
|  84 | Lawrence Frank     |   -0.5  |     -0.16 |        0.48 |          0.59 |          0.45 |
|  85 | Bob Weiss          |   -0.51 |     -0.15 |        0.47 |          0.5  |          0.43 |
|  86 | Allan Bristow      |   -0.56 |     -0.15 |        0.46 |          0.74 |          0.5  |
|  87 | Mike Woodson       |   -0.8  |     -0.27 |        0.46 |          0.63 |          0.47 |
|  88 | Stan Albeck        |   -0.8  |     -0.13 |        0.45 |          0.79 |          0.53 |
|  89 | Gene Shue          |   -0.92 |     -0.15 |        0.44 |          0.52 |          0.43 |
|  90 | Jeff Bzdelik       |   -0.98 |     -0.16 |        0.44 |          0.37 |          0.38 |
|  91 | Randy Pfund        |   -1.02 |     -0.12 |        0.43 |          0.58 |          0.45 |
|  92 | Bernie Bickerstaff |   -1.18 |     -0.44 |        0.42 |          0.59 |          0.45 |
|  93 | Alvin Gentry       |   -1.21 |     -0.4  |        0.42 |          0.66 |          0.48 |
|  94 | Mike Dunleavy      |   -1.34 |     -0.6  |        0.41 |          0.64 |          0.47 |
|  95 | Luke Walton        |   -1.61 |     -0.27 |        0.41 |          0.42 |          0.4  |
|  96 | Matt Guokas        |   -1.76 |     -0.51 |        0.4  |          0.51 |          0.43 |
|  97 | Bob Hill           |   -1.82 |     -0.47 |        0.39 |          0.75 |          0.51 |
|  98 | Don Casey          |   -1.85 |     -0.31 |        0.39 |          0.37 |          0.38 |
|  99 | Sam Mitchell       |   -1.92 |     -0.5  |        0.38 |          0.53 |          0.43 |
| 100 | Byron Scott        |   -1.97 |     -0.83 |        0.38 |          0.46 |          0.41 |
| 101 | Don Chaney         |   -2.1  |     -0.7  |        0.37 |          0.45 |          0.41 |
| 102 | Kenny Atkinson     |   -2.11 |     -0.35 |        0.36 |          0.34 |          0.37 |
| 103 | Garry St. Jean     |   -2.11 |     -0.5  |        0.36 |          0.38 |          0.38 |
| 104 | John Calipari      |   -2.59 |     -0.43 |        0.35 |          0.4  |          0.39 |
| 105 | James Borrego      |   -2.63 |     -0.31 |        0.34 |          0.55 |          0.44 |
| 106 | Jim Lynam          |   -2.74 |     -0.79 |        0.34 |          0.6  |          0.46 |
| 107 | Gene Littles       |   -2.94 |     -0.35 |        0.33 |          0.14 |          0.28 |
| 108 | Ron Rothstein      |   -3.15 |     -0.74 |        0.32 |          0.19 |          0.3  |
| 109 | John MacLeod       |   -3.19 |     -0.75 |        0.32 |          0.8  |          0.54 |
| 110 | David Blatt        |   -3.31 |     -0.39 |        0.31 |          0.96 |          0.67 |
| 111 | Jimmy Rodgers      |   -3.47 |     -0.71 |        0.31 |          0.48 |          0.42 |
| 112 | Eddie Jordan       |   -3.66 |     -1.14 |        0.3  |          0.51 |          0.43 |
| 113 | Bill Cartwright    |   -3.68 |     -0.44 |        0.29 |          0.27 |          0.34 |
| 114 | Darrell Walker     |   -3.77 |     -0.45 |        0.29 |          0.25 |          0.33 |
| 115 | Reggie Theus       |   -4.11 |     -0.49 |        0.28 |          0.47 |          0.42 |
| 116 | Wes Unseld         |   -4.13 |     -1.19 |        0.28 |          0.36 |          0.37 |
| 117 | Kevin O'Neill      |   -4.47 |     -0.53 |        0.27 |          0.44 |          0.4  |
| 118 | George Irvine      |   -4.71 |     -0.96 |        0.26 |          0.28 |          0.34 |
| 119 | Brett Brown        |   -4.8  |     -1.26 |        0.26 |          0.33 |          0.36 |
| 120 | Keith Smart        |   -4.85 |     -0.81 |        0.25 |          0.31 |          0.35 |
| 121 | Hubie Brown        |   -4.91 |     -1    |        0.24 |          0.6  |          0.45 |
| 122 | Terry Porter       |   -4.95 |     -0.83 |        0.24 |          0.62 |          0.46 |
| 123 | Sam Vincent        |   -4.99 |     -0.59 |        0.23 |          0.39 |          0.39 |
| 124 | Michael Curry      |   -5.48 |     -0.65 |        0.22 |          0.65 |          0.48 |
| 125 | Phil Johnson       |   -5.68 |     -0.67 |        0.22 |          0.43 |          0.4  |
| 126 | Dick Harter        |   -5.82 |     -0.69 |        0.21 |          0.06 |          0.23 |
| 127 | Dave Wohl          |   -5.87 |     -0.98 |        0.21 |          0.34 |          0.36 |
| 128 | John Wetzel        |   -6.06 |     -0.72 |        0.2  |          0.28 |          0.34 |
| 129 | Paul Westhead      |   -6.14 |     -1.02 |        0.19 |          0.57 |          0.45 |
| 130 | Butch Beard        |   -6.14 |     -1.03 |        0.19 |          0.34 |          0.37 |
| 131 | Willis Reed        |   -6.35 |     -0.75 |        0.18 |          0.2  |          0.3  |
| 132 | Earl Watson        |   -6.65 |     -0.79 |        0.18 |          0.14 |          0.28 |
| 133 | Jerry Reynolds     |   -6.68 |     -0.79 |        0.17 |          0.25 |          0.33 |
| 134 | Lon Kruger         |   -6.76 |     -1.13 |        0.16 |          0.32 |          0.36 |
| 135 | Brian Shaw         |   -6.96 |     -0.82 |        0.16 |          0.42 |          0.4  |
| 136 | John Kuester       |   -7.17 |     -1.2  |        0.15 |          0.29 |          0.35 |
| 137 | Mike Dunlap        |   -7.56 |     -0.89 |        0.14 |          0.11 |          0.26 |
| 138 | Jacque Vaughn      |   -8.25 |     -1.37 |        0.14 |          0.12 |          0.27 |
| 139 | Johnny Davis       |   -8.46 |     -1    |        0.13 |          0.26 |          0.33 |
| 140 | Larry Krystkowiak  |   -8.72 |     -1.03 |        0.12 |          0.22 |          0.31 |
| 141 | Fred Carter        |   -9.06 |     -1.07 |        0.12 |          0.2  |          0.3  |
| 142 | Bill Blair         |   -9.36 |     -1.11 |        0.11 |          0.12 |          0.27 |
| 143 | Brendan Malone     |   -9.36 |     -1.11 |        0.11 |          0.16 |          0.29 |
| 144 | Igor Kokoskov      |   -9.61 |     -1.14 |        0.1  |          0.07 |          0.23 |
| 145 | Bill Musselman     |   -9.65 |     -1.61 |        0.09 |          0.21 |          0.3  |
| 146 | Tim Floyd          |   -9.88 |     -2.02 |        0.09 |          0.19 |          0.3  |
| 147 | Jay Triano         |  -10.59 |     -1.77 |        0.08 |          0.3  |          0.35 |
| 148 | Quinn Buckner      |  -10.73 |     -1.26 |        0.08 |          0.04 |          0.16 |
| 149 | Johnny Bach        |  -11.18 |     -1.87 |        0.07 |          0.32 |          0.36 |
| 150 | Marc Iavaroni      |  -11.77 |     -1.39 |        0.06 |          0.12 |          0.27 |
| 151 | M.L. Carr          |  -13.04 |     -2.18 |        0.06 |          0.17 |          0.29 |
| 152 | Leonard Hamilton   |  -13.07 |     -1.55 |        0.05 |          0.07 |          0.23 |
| 153 | Brian Winters      |  -13.28 |     -1.57 |        0.04 |          0.06 |          0.2  |
| 154 | Sidney Lowe        |  -14.43 |     -2.95 |        0.04 |          0.11 |          0.26 |
| 155 | Richie Adubato     |  -14.5  |     -2.42 |        0.03 |          0.29 |          0.35 |
| 156 | Kurt Rambis        |  -16.21 |     -2.71 |        0.02 |          0.27 |          0.34 |
| 157 | Derek Fisher       |  -18.67 |     -2.21 |        0.02 |          0.19 |          0.29 |
| 158 | Jim Cleamons       |  -18.96 |     -2.24 |        0.01 |          0.15 |          0.29 |
| 159 | Bill Hanzlik       |  -21.35 |     -2.53 |        0.01 |          0.03 |          0.13 |