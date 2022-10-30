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

<strong>Solution 1:</strong> 
<strong>Lemma:</strong> Let $AE \cap BD = P$ and $AD \cap BE = H$. We will prove that, the polar of point $P$ is through $C$ and $H$. If so, then the extension of $CH$ is perpendicular to $OP$.     
From <strong>La Hire's Theorem</strong>, we know that, if $X$ lies on the polar of $Y$, then $Y$ too lies on the polar of $X$.     
In the above diagram, let the tangents at $A$ and $E$ to the larger circle intersect at $X$ and let the tangents at $B$ and $D$ to the larger circle intersect at $Y$. Since, $AE$ is the polar of $X$ and $BD$ is the polar of $Y$, so the polar of $AE \cap BD = P$ goes through $X$ and $Y$.
Using <strong>Pascal's Theorem</strong> on hexagon $BAADEE$, we find that $C = BA \cap CE$ and $H = AD \cap BE$ and $X = EE \cap AA$ are collinear.    
Using <strong>Pascal's Theorem</strong> on hexagon $ABBEDD$, we find that $C = AB \cap DE$ and $H = AD \cap BE$ and $Y = BB \cap DD$ are collinear. 
So, it turns out that $C, Y, H, X$ are all collinear. So, definitely, $CH$ is the polar of $P$. 
 

<img src = "/assets/img/Geo.jpg" width = "80%" height = "80%">

