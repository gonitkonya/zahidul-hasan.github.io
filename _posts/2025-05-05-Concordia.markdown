---
layout: post
title: "Starting MASc at Concordia University"
date: 2024-01-05 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: enemies.webp # Add image post (optional)
---

In the case of stochastic bandits, our estimators such as the sample mean or the upper confidence bound gives a good glimpse of the fixed distributions that the arms are. But in the adversarial setting, we can run into problems if we choose naive algorithms such as $ETC$ or $UCB_{1}$, because in the case of ETC, after the exploration phase, we choose a possible best arm and stick to it. But in the adversial situation, right after we choose that particular arm, we could start getting all zeros. Or in the case of the UCB algorithms, every time we choose the best arm so far, we could get a zero which could in turn decrease it's confidence radius while at the same time reducing it's sample mean. Therefore, we need to re-assess our policies and introduce randomization and reformulate the notion of regret in the case of the adversarial bandits.  

Here we define the adversarial MAB scenario for today's analysis:
<ol>
  <li>The bandit has $k$ arms and there are $n$ rounds to the game. </li>
  <li>The bandit is <strong>deterministic</strong> and <strong>oblivious</strong> to the algorithm's choices, that is, $x \in [0,1]^{n\times k}$ is the reward table that is chosen beforehand.</li>
  <li>In the case of the Hedge algorithm, we will assume that the environment is fully observable. In the case of the Exp3 algorithm, we will assume that the algorithm is partially observable, i.e, the algorithm can only see the reward of the chosen arm.</li>
</ol>


<strong>The weak regret</strong>: It makes sense to define regret in this case in the following manner,  
<center>$R_{n}(\pi, x) = \sum_{t = 1}^{n} ((max_{1 \leq i \leq k} x_{t,i})- x_{t,A_{t}})$    </center>
Each time, comparing the algorithms choice with that of the best choice in round $t$, but this kind of regret is sort of mathematically intractable. So, we define a weaker version of this in the following way: The maximum reward is taken to be the maximum we could achieve if we stuck to one particular arm from the very beginning.    
<center>$R_{n}(\pi, x) = max_{1 \leq i \leq k} (\sum_{t=1}^{n} x_{t,i} - x_{t,A_{t}})$   </center>
This particular arm that maximizes the first summand is called the <strong>best arm in hindsight</strong>. The bandit literature for adversarial situations uses the word "loss" instead of "reward". So, instead of maximizing the reward, we will be minimizing the loss. And since, the maximum reward we can get is 1, we can define loss in the following way: $y_{t,i} = 1 - x_{t,i}$.    

There are various similar approaches to adversarial bandits starting with <strong>Weighted Majority Algorithm(WMA), Hedge, Exp3, Exp4</strong> etc. Here will only discuss Hedge and Exp3.     

<strong>Hedge Algorithm</strong>: We start with $k$ experts for $k$ arms of the bandit, each having equal weight. In each round, according to this weighted probability distribution, we sample one of the arms for exploitation. Then all of the rewards in that round are revealed. From that we calculate the cost of each arm. We decrease the weights of the arms according to this cost. The costlier the arm, the more the decrease.    
<hr>    
$\textbf{Hedge}$:     
$\quad \textbf{parameters}: \epsilon \in (0,\frac{1}{2})$    
$\quad \textbf{Initialization}:$ for each arm $a$, set $W_{1}(a) = 1$   
$\quad$ for each round $t$:    
$\quad\quad$ let, $p_{t}(a) = \frac{w_{t}(a)}{\sum_{a = 1}^{k} w_{t}(a)}$     
$\quad\quad$ sample one arm $a_{t}$ from the given distribution $p_{t}$ and exploit it    
$\quad\quad$ observe the cost for each arm      
$\quad\quad$ update the weight of each arm $a$ as: $w_{t+1}(a) = w_{t}(a) (1-\epsilon)^{cost_{t}(a)}$     
<hr>    
This algorithm seems fairly intuitive. So, is Exp3 except the concept of <strong>Weighted estimators</strong> that are fake estimators of the reward in round $t$, if we chose arm $i$. And it is defined as follows:    
If our algorithm chooses arm $i$ in round $t$, then $\bar X_{t,i} = X_{t}/P_{t,i}$ where $P_{t,i}$ is the probability that having seen the action-reward series $A_{1}, X_{1}, \cdots, A_{t-1}, X_{t-1}$, the algorithm is going to choose arm $i$ in round $t$. Which means $p_{t,i} = P(A_{t} = i| A_{1}, X_{1}, \cdots, A_{t-1}, X_{t-1}$    
If we don't choose arm $i$ in round $t$, then  $\bar X_{t,i} = 0$.  
Notice that $E_{t-1}[\bar X_{t,i}] = x_{t,i}$ because, $E_{t-1}[X_{t,i}] = (\sum_{j \neq i} p_{t,j} 0 \bar X_{t,i}) + p_{t,i} \frac{x_{t,i}}{p_{t,i}}$. So, this $\bar X_{t,i}$ is an unbiased estimator of $x_{t,i}$.
Since, we are talking about losses instead of rewards, let's define $\bar Y_{t,i} = \mathbb{I}$ { $A_{t} = i$ } 
$\frac{y_{t,i}}{p_{t,i}}$, substituting $x_{t,i} = 1 - y_{t,i}$, we get, $\bar X_{t,i} = 1 - \mathbb{I}$ { $A_{t} = i$ } $\frac{1 - x_{t,i}}{p_{t,i}}$.    

There is one more update in the Exp3 algorithm. Instead of using a weighted probability, we use the <strong>softmax</strong> function to weigh the probabilities. That is,    
$p_{t,a} = \frac{e^{\eta w_{t}(a)}}{ \sum_{i = 1}^{k} e^{\eta w_{t}(i)}}$ where $\eta$ is the learning rate. The greater the value of the learning rate, the more the concentration around the largest probability.   
A pseudocode for the algorithm is as follows:    
<hr>    
$\textbf{Exp3}$:     
$\quad \textbf{parameters}: \eta$    
$\quad \textbf{Initialization}:$ for each arm $a$, set $W_{0}(a) = 0$   
$\quad$ for each round $t$:    
$\quad\quad$ let, $p_{t,a} = \frac{e^{\eta w_{t}(a)}}{ \sum_{i = 1}^{k} e^{\eta w_{t-1}(i)}}$    
$\quad\quad$ sample one arm $a_{t}$ from the given distribution $p_{t}$ and exploit it    
$\quad\quad$ observe the cost for each arm      
$\quad\quad$ update the weight of each arm $a$ as: $w_{t}(a) = w_{t-1}(a) + 1 - \mathbb{I}$ { $A_{t} = i$ } $\frac{1 - x_{t,i}}{p_{t,i}}$    
<hr>    


<strong>Regret Analysis</strong>: The regret analysis of Hedge and Exp3 are very much similar and in fact, the case for Hedge is even easier. So, we only provide the regret analysis of Exp3. Define,   
<center>$R_{n,i} = \sum_{t = 1}^{n} X_{t,i} - \mathbb{E} [ \sum_{t = 1}^{n} X_{t}=]$</center>   
So, what we are looking for is $R_{n}(\pi, x) = max_{1 \leq i \leq k} R_{n,i}$ because we want the worst possible regret.  
By using induction on $t$, we prove that, $\mathbb{E}[ W_{n,i}] = \sum_{t = 1}^{n} x_{t,i}$ which easily follows as,     
<center>$\mathbb{E}[ W_{n,i}] = \mathbb{E}[ W_{n-1,i}] + 1 - \mathbb{E}[ \mathbb{I}$ { $ A_{n} = i $ } $] (1-X_{n}) \frac{1}{p_{n,i}}$</center>      
<center>$\mathbb{E}[ W_{n,i}] = \mathbb{E}[ W_{n-1,i}] + 1 - p_{n,i} (1-X_{n}) \frac{1}{p_{n,i}}$</center>     
<center>$\mathbb{E}[ W_{n,i}] = \sum_{t = 1}^{n-1} x_{t,i} + 1 - p_{n,i} (1-X_{n}) \frac{1}{p_{n,i}}$</center>            
<center>$\mathbb{E}[ W_{n,i}] = \sum_{t = 1}^{n-1} x_{t,i} + x_{t,n}$</center>     

We also know that, <center>$X_{t} = \sum_{i = 1}^{k} p_{t,i} \bar X_{t,i}$</center>,     
So, <center>$\mathbb{E} [ \sum_{t = 1}^{n} X_{t} ] = \mathbb{E} [ \sum_{t = 1}^{n} \sum_{i = 1}^{k} p_{t,i} \bar X_{t,i}] $</center>       
So, let's define <center>$W_{n} = \sum_{t = 1}^{n} \sum_{i = 1}^{k} p_{t,i} \bar X_{t,i}$</center>    
Then <center>$R_{n, i} = \mathbb{E} [ W_{n,i} - W_{n}]$</center>        

Let, $T_{t} = \sum_{i = 1}^{k} e^{\eta W_{t,i}}$, So, by definition,$T_{0} = 1$    
Obviously, <center>$e^{\eta W_{n,i}} \leq \sum_{j = 1}^{k} e^{\eta W_{n, j}} = T_{n} = T_{0} \prod_{t = 1}^{n} \frac{T_{t}}{T_{t-1}} = k \prod_{t = 1}^{n} \frac{T_{t}}{T_{t-1}} \cdots (1) $</center>    
Since, <center>$W_{t,i} = W_{t-1,i} + \bar X_{t,i}$,   </center>
So, <center>$e^{W_{t,i}} = e^{W_{t-1,i}}  e^{\bar X_{t,i}}$.    </center> 
Then we get, <center>$\frac{T_{t}}{T_{t-1}} = \sum_{j = 1}^{k} \frac{e^{W_{t-1,i}}}{T_{t-1}}  e^{\bar X_{t,i}} = \sum_{j = 1}^{k} p_{t,j} e^{\bar X_{t,i}} $</center>        
But we know that for all <center> $x \leq 1$, $e^{x} \leq 1 + x + x^{2}$   </center>
Recall the definition,  <center>$\bar X_{t,i} = 1 - \mathbb{I}$ { $A_{t} = i$ } $\frac{1 - x_{t,i}}{p_{t,i}}$</center>  
and it's obvious that $\bar X_{t,i}$ can never be larger than 1. And we also choose $\eta$ in such a way that it $\eta \bar X_{t,i}$ remains less than 1. So,     
 <center>$\frac{T_{t}}{T_{t-1}} \leq \sum_{j = 1}^{n} p_{t,j} +\eta \sum_{j = 1}^{n} p_{t,j} \bar X_{t,j} +\eta^{2} \sum_{j = 1}^{n} p_{t,j} \bar X_{t,j}^{2} \leq e^{\eta \sum_{j = 1}^{n} p_{t,j} \bar X_{t,j} +\eta^{2} \sum_{j = 1}^{n} p_{t,j} \bar X_{t,j}^{2}}$ </center>
  
 The last inequality follows from the fact that, <center>$e^{x} \geq 1 + x$ for all $x$</center>.   
 From inequality $(1)$, we find that,    
 <center>$e^{\eta W_{n,i}} \leq k e^{\eta \sum_{t = 1}^{n} \sum_{j = 1}^{k} p_{t,i}\bar X_{t,j} + \eta^{2} \sum_{t = 1}^{n} \sum_{j = 1}^{k} p_{t,i}\bar X_{t,j}^{2} }$    </center>
  <center>$e^{\eta W_{n,i}} \leq k e^{\eta W_{n} + \eta^{2} \sum_{t = 1}^{n} \sum_{j = 1}^{k} p_{t,j}\bar X_{t,j}^{2} }$    </center>
By taking logarithms and dividing both sides by $\eta > 0$,   
<center>$W_{n,i} - W_{n} \leq \frac{\log{k}}{\eta} + \eta \sum_{t=1}^{n} \sum_{j=1}^{k} p_{t,j} \bar X_{t,j}^{2}$   </center>

Taking expectation on both sides,    
<center>$R_{n,i} = \mathbb{E} [ W_{n,i} - W_{n} ] \leq \frac{\log{k}}{\eta} + \eta \sum_{i=1}^{n} \mathbb{E}[ \sum_{j=1}^{k} p_{t,j} \bar x_{t,j}^{2}]$  </center> 
Since, $\bar x_{t,j}$ and $p_{t,j}$ both are less than 1, so,    
<center> $\mathbb{E}[ \sum_{j=1}^{k} p_{t,j} \bar x_{t,j}^{2}] \leq \mathbb{E}[ \sum_{j=1}^{k} 1] = k$   </center>
So, <center> $R_{n,i} \leq \frac{\log{k}}{\eta} + \eta nk$   </center>
In order to minimize this quantity, we choose, $\eta = \sqrt{\frac{\log{k}}{nk}}$.
So, the regret bound becomes $2\sqrt{nk\log{k}}$  
