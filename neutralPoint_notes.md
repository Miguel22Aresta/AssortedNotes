# Neutral Point Calculations


## General Analysis 
+ There are several ways of deriving this
+ I like to do it in terms of moments because it captures what's really going on with each component and it's clear how we get to the usual derivatives of the plane (the things we *must* calculate)
+ I'll add the drawings at the end
+ Everyhting in SI  (m, kg, N, etc)


I'll make it very general and introduce assumptions (with justification) where needed to simplify the maths.
Let's start with the isolated wing (represented by its MAC $\bar c$), flying at a speed $U_\infty$ and AoA $\alpha_w$. In the linear region, we have an invariant aerodynamic center,  so we will take moments about it and later use this to our advantage.

### Isolated Wing

Taking moments about the CG:

$$M_{CG} = M_{ac} + (L_w\cos\alpha+D\sin\alpha)(h-h_n)\bar c + (L_w\sin\alpha-D_w\cos\alpha)z\bar c$$

where
 
+ ac : wing aero center
+ $M_{ac}$ is the pitching moment about the ac
+ $L_w$ and $D_w$ is the lift and drag force of the wing
+ $\alpha$ is the AoA, in radians
+ $\bar c$ is the mean aerodynamic chord (MAC) 
+ $h_n$ is the nondimensional distance from the MAC leading-edge to the aero center
+ $h$ is the nondimensional distance from the MAC leading-edge to the CG 
+ z is nondimensional the vertical distance between MAC and the CG


Assumption 1:

+  Small angles, this is justified becase we operate in a narrow band of $\alpha$ around zero (in radians)

We will also divide by $\frac{1}{2}\rho V_\infty^2S\bar c$ to nondimensionalize the first equation:

$$C_{M_{CG}}=C_{M_{AC}}+(C_{L_w}+C_{D_w}\alpha)(h-h_n)+(C_{L_w}\alpha-C_{D_w})z$$

At this point, we can expect $C_{D_w}\alpha$ and  $C_{L_w}\alpha$ to be quite small. Also, we don't know what $z$ is for the MRB5 but we also expect it to be small too. So we could write

$$C_{M_{CG}}=C_{M_{AC}}+C_{L_w}(h-h_n)$$

### Wing-Body

If we had a flying wing, we'd be done. So, let's add realism. 
Taking the previous equation, we'll use the same result for a wing-fuselage configuration, with subscript $wb$. We won't split the fuselage and wing contributions because the superposition of their separate effects doesn't work well seeing as they interact with each other (the data almost always says so)

$$C_{M_{CG}}=C_{M_{AC}}+C_{L_{wb}}(h-h_{wb})$$

### Adding a Horizontal Tail

For an isolated tail, the procedure would be the same as the wing but when we combine the previous wing-body with a horizontal tail _downstream_ of it we need to be prepared to account for

+ Different freestream conditions (we also have the cruise prop + blanking from the fuselage)
+ Average downwash from the wing, $\epsilon$

So we'll name $V_t$ the "freestream" at the tail and the Lift and Drag are going to be perpendicular and parallel to this velocity.

DRAWING HERE

Our tail uses a symmetrical section so its $M_{ac_t}$ is zero when the elevator deflection is zero.
Its lift coefficient is $$C_{L_t}=\frac{L_t}{\frac{1}{2}\rho V_\infty^2S_t}$$

Note: $C_{L_t}$ is still based on $q_\infty$. This is where different people do call different things different names :) Here, I'll simply use a tail lift-curve slope, $a_t$, that is reduced compared to the isolated tail, to avoid using "efficiency factors" and other not so clear things.

Taking moments about the CG again, for the tail 


$$M_t = -l_t[L_t\cos(\alpha_\infty-\epsilon)+D_t\sin(\alpha_\infty-\epsilon)]-z_t[D_t\cos(\alpha_\infty-\epsilon)-L_t\sin(\alpha_\infty-\epsilon)]+M_{ac_t}$$

Where $l_t$ is the distance between the CG and the tail's aero center.

From this equation, we can deduct the very first term (lift and tail arm) is the strongest and the others smaller, compared to it (sometimes drag contributions are disregarded since $L>>D$:

$$M_t=-l_tL_t$$

which is equivalent to

$$M_t=-l_tC_{L_t}\frac{1}{2}\rho V_\infty^2S_t$$

(I'm doing this because we will nondimensionalize and clears up what some books/papers/etc don't show clearly)

We will nondimensionalize the above so we can have the familiar parameters/derivatives usually calculated.

So, dividing by $\frac{1}{2}\rho V_\infty^2S\bar c$ (attention - wing MAC and wing area) we get

$$C_{M_t}=-\frac{l_t}{\bar c}\frac{S_t}{S}C_{L_t}$$

This is where the "area ratio" in the books/papers comes from. It's to keep the nondimensionalization consistent! Also, we see that the tail moment, is proportional to a constant related to involving the plane's fixed geometry.
This constant is the well-known tail "volume coefficient"

$$V_H=\frac{l_t}{\bar c}\frac{S_t}{S}$$

$$C_{M_t}=-H_tC_{L_t}$$

Note: $l_t$ is sometimes defined between wing-body AC and tail AC, I'll use that dimension and call it $ l'_t$ (see drawing). Consequently we'll have a slightly different $V_H$ called (yes..) $V'_H$

$$V_H = V'_H-\frac{S_t}{S}(h-h_{wb}) $$

Adn the tail moment about the wing-body aero center is $$C_{M_t}=-V'_HC_{L_t}$$

And about the CG (by substitution)

$$C_{M_t}=-V'_HC_{L_t}+C_{L_t}\frac{S_t}{S}(h-h_{wb})$$

We're almost there, we need to add another contribution we don't know much about yet - the "propulsive moment" from the cruise motor thrust, $C_{M_T}$ and is throttle-dependent.

## Total A/C Pitching-Moment
We can add all the contributions to get the global pitching-moment of the entire A/C about the CG :

$$C_M = C_{M_{AC}}+\left (C_{L_{wb}}+C_{L_t}\frac{S_t}{S}\right)(h-h_{n_{wb}})-V'_HC_{L_t}+C_{M_T}$$

We can simplify the main lift contributions:

$$C_L=C_{L_{wb}}+C_{L_t}\frac{S_t}{S}$$

and rewrite $C_M$ as

$$C_M = C_{M_{AC}}+C_L(h-h_{n_{wb}})-V'_HC_{L_t}+C_{M_T}$$

Finally, we can obtain more useful/familiar parameters by differentiating with respect to $\alpha$ (or $C_L$)



$$\frac{\partial C_M}{\partial \alpha} =\frac{\partial C_{M_{AC}}}{\partial \alpha} + C_{L_\alpha}(h-h_{n_{wb}}) -V'_H\frac{\partial C_{L_t}}{\partial \alpha}+\frac{\partial C_{M_T}}{\partial \alpha}$$

+ Because of the definition of an aerodynamic center, $\frac{\partial C_M}{\partial\alpha}$ (or $\frac{\partial C_M}{\partial C_L}$)  are zero at that point. So the first term vanishes

$$\frac{\partial C_M}{\partial \alpha} = C_{L_\alpha}(h-h_{n_{wb}}) -V'_H\frac{\partial C_{L_t}}{\partial \alpha}+\frac{\partial C_{M_T}}{\partial \alpha}$$


By order of magnitude arguments, the first term is the strongest contributor ($C_{L_\alpha}$ is about 5 for the MRB5 wing alone, with the fuselage addition usually resulting in a  small net increase). Additionally, the magnitude (and sign!) of the first term depends on $h$, the CG position. 

To make the first term negative, $h_{n_{wb}} > h$ and so the CG _must_ be ahead of the neutral point.
For the aircraft to be _statically_ stable, $\frac{\partial C_M}{\partial \alpha} <0$ so that an increase in $\alpha$ leads to a nose-down (negative) moment. Otherwise, we'd have a positive feedback loop of increasing $\alpha$

What about $\frac{\partial C_M}{\partial \alpha} =0$?
That's how we find the neutral point, setting the LHS to zero and solving for $h_{n}$ (we are moving the CG to this location we are about to determine).
If we substitute the rearranged equation back into the original $C_{M_\alpha}$ equation, we simply get*

$$C_{M_\alpha}=C_{L_\alpha}(h-h_n)$$





+ This is how the neutral point is determined from CFD and wind-tunnel tests (from $C_{M_\alpha}$ and $C_{M_\alpha}$ calculation/measurement) and the position of the CG
+ The negative of quantity in brackets is the static margin


*Alternatively, 

$$\frac{\partial C_M}{\partial C_{L}}=-(h-h_n)$$

There a lot more useful relations we could derive but that's it for now. 
This analysis shows:

+ the relative importance of the contributions 
+ how powerful the CG location is and how easy it is to make the plane statically stable (not necessarily trimmable)
+ How important *good* estimates of realistic configurations are. The simplest method that gives good agreement for an arbitrary and realistic configuration is the VLM (Vortex Lattice Method), a linear inviscid method.








































































