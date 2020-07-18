---
date: 2020-07-12
type: Blog Post
title: Things to know about P-values
description: lsajldkjaslkdj
weight: 10
draft: true
Summary: What does getting a small p-value really mean? This article post as a reference point.
---


A *p-value* is the probability that, under the null hypothesis, that the result is as or more extreme than what is actually observed. 

But what does that *really* mean?

In order to answer, it's important to understand other concepts.

Statistical power: 

A *p-value threshold* of 0.05 ( p < 0.05)
	
#### Example: Breast cancer detection

The below example is adapted from the book [Statistics Done Wrong](https://www.amazon.com/Statistics-Done-Wrong-Woefully-Complete/dp/1593276206/ref=sr_1_2?dchild=1&keywords=statistics+done+wrong&qid=1594566069&sr=8-2) by Alex Reinhart. 

*Question:* A group of physicians were trying to determine whether the use of mammograms to screen for early breast cancer is worth the dangers of false positive results. Suppose that **prevalence is 0.8%**, meaning that 0.8% of women who get mammograms have breast cancer. The test has a **90% statistical power** meaning that the mammogram will correctly detect breast cancer in 90% of women who actually have breast cancer. However, among women with no breast cancer at all, about 7% will still get a positive reading (in other words, **p < 0.07 is the significance threshold.**) If you get a positive mammogram result, what are the chances you have breast cancer? 

*Answer:* Imagine 1000 randomly selected women chose to get a mammogram. On average, 0.8% of screened women have breast cancer, so about 8 women in our study will. The mammogram correctly detects 90% of breast cancer cases, so about 7 of the 8 will have their cancer discovered. However, there are 992 women without breast cancer and 7% will get a false positive reading. This means about 70 women will be incorrectly told they have cancer. 

In total we have 77 women with positive mammograms, 7 of whom actually have breast cancer. Only 9% of women with positive mammagrams have breast cancer. The answer is 9% (much lower than what one would assume).