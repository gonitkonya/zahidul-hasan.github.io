---
layout: post
title: "Stochastic Bandits: The Epsilon Greedy Algorithm"
date: 2022-04-04 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: eps.png # Add image post (optional)
tags: [Js, Conference] # add tag
---

Previously, we saw that in the ETC algorithm, we first explore all of the arms $m$ times for some $m$, then we choose the best arm from our exploration and use this arm for all the subsequent rounds. But we could severely underperform in the initial exploration phase. So, instead of blindly exploring in the first $km$ rounds, we can spread the uniform exploration over all of the rounds using a coin toss model. For each round $t$, with a probability $\epsilon_{t}$, we explore any arm with a uniform probability of $\frac{1}{k}$, otherwise, we choose the best possible arm from our experience of explorations so far. In this way, we do not run the risk of incurring a heavy regret in the exploration phase and also, eventually our algorithm succeeds to determine the truly optimal arm.

<img src = "https://github.com/Zahidul-Hasan/zahidul-hasan.github.io/tree/master/assets/img/etc.jpg" >
![alt text](https://github.com/Zahidul-Hasan/zahidul-hasan.github.io/tree/master/assets/img/etc.jpg?raw=true)
