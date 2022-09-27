---
layout: post
title: "Stochastic Bandits: Optimism In The Face of Uncertainty"
date: 2022-03-07 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: ucb.webp # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Holidays, Hawaii]
---

The previous two algorithms had regret bounds in the order of $\mathcal{O}(n^{\frac{2}{3}} (k\log{n})^{\frac{1}{3}})$. But with a bit of optimism, we can get smaller regret bounds. We explore each of the arms at least once. Then choose the arm with the highest upper bound. There are mainly two reasons for doing that:
<ul>
  <li>This arm probably has a large sample mean which makes it a very good choice</li>
  <li>Or this arm probably has a wider confidence radius which means this arm is largely unexplored. So, we better explore this arm more.</li>
</ul>
Let the upper bound of arm $i$ at round $t$ be called $UCB_{i}(t-1) = \bar \mu_{i}(t-1) + \sqrt{\frac{2}{T_{i}(t-1)} \log{n}}$. 

$\textbf{UCB1 Algorithm}$   
Explore each arm once   
$\textbf{for}$ round $t = 1, 2, \cdots , n$ $\textbf{do}$   
$\quad$ pick the arm $i$ that maximizes $UCB_{i}(t-1)$    
$\quad$ update it's sample mean reward and confidence radius   
$\textbf{end}$   

<strong style="color:red;">Crude Instance Independent Regret Analysis</strong>: Since, at round $t$, arm $i$, is chosen, so, $UCB_{i}(t-1) \geq max_{1 \leq j \leq k} UCB_{j}(t-1)$. Let's say, arm $j$ is the optimal arm. And like the previous algorithms in the good event, $\mu_{j} \leq \bar \mu_{j}(t-1) + \sqrt{\frac{2}{T_{j}(t-1)} \log{n}}$ and $\mu_{i} \geq \bar \mu_{i}(t-1) - \sqrt{\frac{2}{T_{i}(t-1)} \log{n}}$   
So, $\mu_{j} - \mu_{i} \leq \bar \mu_{j}(t-1) -  \bar \mu_{i}(t-1) + \sqrt{\frac{2}{T_{i}(t-1)} \log{n}} + \sqrt{\frac{2}{T_{j}(t-1)} \log{n}}$   
But since, $UCB_{i}(t-1) \geq UCB_{j}(t-1)$, so, $\bar \mu_{j}(t-1) -  \bar \mu_{i}(t-1) \leq \sqrt{\frac{2}{T_{i}(t-1)} \log{n}} - \sqrt{\frac{2}{T_{j}(t-1)} \log{n}}$   
Adding them up, we get $\Delta_{i} = \mu_{j} - \mu_{i} \leq 2\sqrt{\frac{2}{T_{i}(t-1)} \log{n}}$   
So, for any round $t$, the regret upto round $t$, due to arm $i$, is $R(t:i) \leq \Delta_{i} T_{i}(t-1) \leq \sqrt{8T_{i}(t-1) \log{n}}$  
So, for all arms, the total regret is $R(t) \leq \sum_{i = 1}^{k} \sqrt{8T_{i}(t-1) \log{n}}$    
Since, $f(x) = \sqrt{x}$ is concave, so, using Jensen's Inequality, we have, $\frac{1}{k} \sum_{i=1}^{k} \sqrt{T_{i}(t-1)} \leq \sqrt{\frac{1}{k} \sum_{i=1}^{k} T_{i}(t-1)} = \sqrt{\frac{t}{k}}$   
So, the upper bound for $R(t)$ is $R(t) \leq \sqrt{8 t k \log{n}}$   
So, $R(n) \approx \mathcal{O}(\sqrt{nk\log{n}})$
