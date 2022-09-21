---
layout: post
title: "Stochastic Bandits: The Epsilon Greedy Algorithm"
date: 2022-04-04 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: eps.png # Add image post (optional)
tags: [Js, Conference] # add tag
---

Previously, we saw that in the ETC algorithm, we first explore all of the arms $m$ times for some $m$, then we choose the best arm from our exploration and use this arm for all the subsequent rounds. But we could severely underperform in the initial exploration phase. So, instead of blindly exploring in the first $km$ rounds, we can spread the uniform exploration over all of the rounds using a coin toss model. For each round $t$, with a probability $\epsilon_{t}$, we explore any arm with a uniform probability of $\frac{1}{k}$, otherwise, we choose the best possible arm from our experience of explorations so far. In this way, we do not run the risk of incurring a heavy regret in the exploration phase and also, eventually our algorithm succeeds to determine the truly optimal arm.

$\textbf{for}$ round $t = 1, 2, \cdots , n$ $\textbf{do}$   
$\quad$ Toss a coin with probability $\epsilon_{t}$   
$\quad\quad$ if $\textbf{success:}$   
$\quad\quad\quad$ Explore any with uniform probability   
$\quad\quad$ if $\textbf{failure:}$   
$\quad\quad\quad$ Exploit the best arm so far

Let's look at the simple regret of a particular round $t$. If $n$ is sufficiently large, then at some point, in an exploitation round, only the optimal arm will be used. So, a suboptimal arm being exploited is unlikely. So, most arms are used in the algorithm in the random exploration rounds. Let's say in an exploitation round, a suboptimal arm $a_{i}$ is being used. So, definitely, $\bar u_{i}(t-1) \geq max_{j = 1}^{k} \bar u_{j}(t-1)$.
Let's define the good event $G$. In the good event, for all of the arms, the mean reward stays within the confidence bound of the sample mean reward. That is, for all rounds $t$ and for all arms $i$, $|\bar \mu_{i}(t-1) - \mu_{i}| \leq \sqrt{\frac{2}{n_{i}(t-1)} log(n)}$
We know that, $Pr(G) \geq 1 - \frac{1}{n^{2}}$.  
In the good event, let's say at round $t$, arm $i$ is the apparently best arm and arm $j$ is the truly optimal arm. We know for sure that,  
$$\mu_{j} \leq \bar \mu_{j}(t-1) + \sqrt{\frac{2}{n_{j}(t-1)} log(n)}$$  
$$\mu_{i} \geq \bar \mu_{i}(t-1) - \sqrt{\frac{2}{n_{i}(t-1)} log(n)}$$  
so, $$\mu_{j} - \mu_{i} \leq \bar \mu_{j}(t-1) - \bar \mu_{i}(t-1) + \sqrt{\frac{2}{n_{j}(t-1)} log(n)} + \sqrt{\frac{2}{n_{i}(t-1)} log(n)}$$  
Since, $i$ is the chosen arm at round $t$, so $\bar \mu_{j}(t-1) - \bar \mu_{i}(t-1) \leq 0$, so we have,  
$$\delta_{i} = \mu_{j} - \mu_{i} \leq \sqrt{\frac{2}{n_{j}(t-1)} log(n)} + \sqrt{\frac{2}{n_{i}(t-1)} log(n)}$$     
Now, let's try to find an upper bound for the expected value of this $\delta_{i}$.    
$$E[\Delta_{i}] \leq \sqrt{\frac{2}{ E[n_{j}(t-1)]} log(n)} + \sqrt{\frac{2}{E[n_{i}(t-1)]} log(n)}$$  
$$E[n_{i}(t-1)] = \sum_{t}^{} Pr(exploration) \frac{1}{k} + Pr(exploitation) Pr(i\space being\space the\space best\space arm\space at\space round\space t) \geq t\epsilon_{t}/k$$   
so, $$E[\Delta_{i}] \leq \sqrt{\frac{8k}{t\epsilon_{t}} log(n)}$$  
So, the expected regret per round in the good event is, $$E[R_{i}] \leq Pr(exploration)1 + Pr(exploitation)\sqrt{\frac{8k}{t\epsilon_{t}} log(n)}$$    
$$= \epsilon_{t} + (1-\epsilon_{t}) \sqrt{\frac{8k}{t\epsilon_{t}} log(n)}$$    
$$\leq  \epsilon_{t} + \sqrt{\frac{8k}{t\epsilon_{t}} log(n)}$$   
The above bound is minimized by the choice $\epsilon_{t} = 2^{\frac{1}{3}} k^{\frac{1}{3}} t^{\frac{-1}{3}} log(n)^{\frac{1}{3}}$.   
Then we get, $$E[R_{i}] \leq (2^{\frac{1}{3}} + 2^{\frac{1}{3}}) k^{\frac{1}{3}} t^{\frac{-1}{3}} log(n)^{\frac{1}{3}} $$  
So, the expected simple regret over both good and bad events is,  
$$E[R(t)] = Pr(G) E[R(t)|G] + Pr(G^{c}) E[R(t)|G^{c}]$$   
$$\leq (1-\frac{1}{n^2}) k^{\frac{1}{3}} t^{\frac{-1}{3}} log(n)^{\frac{1}{3}} + \frac{1}{n^2} 1$$   
$$\leq k^{\frac{1}{3}} t^{\frac{-1}{3}} log(n)^{\frac{1}{3}}$$    

So, now we find the expected regret over all rounds,  
$$E[R(n)] = E[\sum_{1\leq t\leq n} R(t)]$$   
$$\leq n E[R(n)]$$  
$$= k^{\frac{1}{3}} n^{\frac{2}{3}} log(n)^{\frac{1}{3}}$$  

So, the epsilon-greedy algorithm has an asymptotic complexity of $\mathcal{O}(k^{\frac{1}{3}} n^{\frac{2}{3}} log(n)^{\frac{1}{3}})$  


