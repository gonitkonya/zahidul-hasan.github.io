---
layout: post
title: "China Western Math olympiad 2006: Multiple Solutions"
date: 2017-09-11 05:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: china.jpg # Add image post (optional)
---
<strong>Tags: Projective Geometry, Pascal's Theorem, La Hire's Theorem, Harmonic Division, Ceva's Theorem, Manelaus's Theorem, Co-ordinate Geometry</strong>     

<strong>Problem Description:</strong> As in the figure above, $AB$ is a diameter of a circle with center $O$. $C$ is a point on $AB$ extended. A line through $C$ cuts the circle with center $O$ at $D, E. OF$ is a diameter of the circumcircle of $\triangle BOD$ with center $O_{1}$. Line $CF$ intersect the circumcircle again at $G$. Prove that $O,A,E,G$ are concyclic.

<img src = "/assets/img/geogeo.jpg" width = "60%" height = "60%">

<strong>Solution 1 ( Due to WONG Chiu Wai ):</strong>     
<strong>Lemma:</strong> Let $AE \cap BD = P$ and $AD \cap BE = H$. We will prove that, the polar of point $P$ is through $C$ and $H$. If so, then the extension of $CH$ is perpendicular to $OP$.     
From <strong>La Hire's Theorem</strong>, we know that, if $X$ lies on the polar of $Y$, then $Y$ too lies on the polar of $X$.     
In the above diagram, let the tangents at $A$ and $E$ to the larger circle intersect at $X$ and let the tangents at $B$ and $D$ to the larger circle intersect at $Y$. Since, $AE$ is the polar of $X$ and $BD$ is the polar of $Y$, so the polar of $AE \cap BD = P$ goes through $X$ and $Y$.     
Using <strong>Pascal's Theorem</strong> on hexagon $BAADEE$, we find that $C = BA \cap CE$ and $H = AD \cap BE$ and $X = EE \cap AA$ are collinear.     
Using <strong>Pascal's Theorem</strong> on hexagon $ABBEDD$, we find that $C = AB \cap DE$ and $H = AD \cap BE$ and $Y = BB \cap DD$ are collinear.       
So, it turns out that $C, Y, H, X$ are all collinear. So, definitely, $CH$ is the polar of $P$.     


Let $OP \cap CH = Q$. We will prove that $Q = G$. 
To show $Q = G$, note that $\angle PQH, \angle PDH$ and $\angle PEH$ are $90°$, which implies $P, E, Q, H, D$ are concyclic. Then $\angle PQD = ∠ PED = ∠ DBO$, which implies $Q, D, B, O$ are concyclic. Therefore, Q = G since they are both the point of intersection (other than $O$) of the circumcircle of $\triangle BOD$ and the circle with diameter $OC$.
 
<strong> Solution 2 ( Due to Me ):</strong> My solution is almost analogous to the one above. Except I have my personal proof for the Lemma. Let's simply the diagram as below. We just need to prove that $AO \perp IJ$.    
<img src = "/assets/img/Geo.jpg" width = "80%" height = "80%">

We will go for a hybrid solution. This is why it's my favorite. It's a solution where Euclidean geometry meets Cartesian coordinate geometry.    
Let's define the coordinates of the points in the following way:    
$ D = (0, 0)$, $ A = (0, a)$, $ B = (b, 0)$, $ C = (c, 0), H = (0, h), J = (j, 0)$       
From here we can deduce that, $ O = (\frac{b+c}{2}, 0)$. Now, let's find out the coordinates of $H$ and $J$. One would be tempted to solve equations of the lines $BC$ and $EF$ or $BE$ and $CF$. But that would be very cumbersome. Instead, remember that, if we reflect $H$ across $BC$, it's reflection $H'$ falls on the circumcircle of $\triangle ABC$. So using the power of point $D$, 
<center>$|AD| \times |DH'| = |BD| \times |CD|$  </center>
Therefore, 
<center>$|DH| = |DH'| = \frac{|BD| \times |CD|}{AD} = \frac{-bc}{a}$  </center>
So, $H = (0, \frac{-bc}{a})$  
Now, let's find the coordinates of $J$.  
Since the cevians $AD, BE, CF$ are collinear. So using <strong>Ceva's Theorem</strong>,    
<center> $ \frac{AF}{FB} \frac{BD}{DC} \frac{CE}{EA} = 1$ </center>       
And since $E, F, J$ are collinear. Using <strong>Manelaus's Theorem</strong>,     
<center> $ \frac{AF}{FB} \frac{BJ}{JC} \frac{CE}{EA} = -1$ </center>     

Combining both we get,        
<center> $  \frac{BJ}{JC} = -  \frac{BD}{DC}$ </center>
Which means, $J, B, D, C$ are <strong>harmonic conjugates</strong>.   
<center> $  \frac{j-b}{c-j} = -  \frac{d-b}{c-d}$ </center>
Plugging in $d = 0$ and solving for $j$ yeilds that, $j = \frac{2bc}{b+c}$.    
We calculate the slope of $OA$ to be $m_{1} = \frac{a-0}{0 - \frac{b+c}{2}} = - \frac{2a}{b+c}$.    
We calculate the slope of $IJ$ to be $m_{2} = \frac{0-\frac{-bc}{a}}{\frac{2bc}{b+c} - 0} = \frac{b+c}{2a}$.    
And since, $m_{1} \times m_{2} = -1$, $OA$ and $IJ$ are perpendicular.
