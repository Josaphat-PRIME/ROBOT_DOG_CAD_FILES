# There is all CAD files and the mechanical explenations behind this project
Disclaimer /!\ this project was not made by using AI ! 

When i was working on this project, i was just a robotics student passionate about big challenges. Because of that, there may be some imperfections or misatkes in this project so If you spot any issues or have ideas for improvements, please feel free to open an issue or submit a pull request. Contributions and feedback are always welcome!

> "A robot may not harm a human being or, through inaction, allow that human being to come to harm" *ISAAC ASIMOV*.

## INVERSE KINEMATICS : PART ONE
This part of the project is the most important . The robot's entire locomotion depends on it and the goal of this part is to find the relation between the robot end leg and motor rotation angle. 

![IK of one leg](/Pictures/IK.png)

According to the picture bellow, **$e$ is equal to the length of the shin and $d$ the length of thigh** . Our next step is to find the expression of $\theta_{1}$ and $\theta_{2}$ for that we'll use few geometric formulas. 

 ### 1 - Let's find $\theta_{2} $
According to Pythagoras's formula we found that

$$\boxed {r^2 = x^2+z^2}$$

And with the cosine law we found that

$$ 
\boxed {r^2 = e^2 + d^2 -2ed\cos(\theta_{2})} 
$$

After equating these two equations, we obtain this.

$$ 
x^2+z^2 = e^2 + d^2 -2ed\cos(\theta_2) 
$$

$$  
2ed\cos(\theta_2)  = (e^2 + d^2)-(x^2+z^2) 
$$

$$  
\cos(\theta_2)  = \frac {(e^2 + d^2)-(x^2+z^2)}{2ed} 
$$

and at the end we found that 

$$ 
\boxed{\theta_2  = \arccos \frac {(e^2 + d^2)-(x^2+z^2)}{2ed}} 
$$

### 2 - Let's find $\theta_{1} $
$\theta_{1}$ is angle between the x-axis and the Thigh. According to our schematics,


$$
\theta_{1} = \alpha + \beta
$$

let's find  $\alpha$  &  $\beta$

$$ 
\tan(\alpha) = \frac{z}{x} \Leftrightarrow \alpha = \arctan(\frac{z}{x} )
$$

and again with cosine law we can write

$$
e^2 = r^2 + d^2 - 2dr\cos(\beta)
$$

$$
 2dr\cos(\beta)= r^2 + d^2 - e^2 
$$

$$
 \cos(\beta)= \frac{r^2 + d^2 - e^2 }{2dr} \Leftrightarrow \beta= \arccos\frac{r^2 + d^2 - e^2 }{2dr}
$$

$$
\theta_{1} = \alpha + \beta \Leftrightarrow \boxed {\theta_{1} =  \arccos\frac{r^2 + d^2 - e^2 }{2dr} + \arctan(\frac{z}{x})}
$$

At this step, it should be noted that the `arctan` function does not allow us to determine the quadrant of the target point based on the signs of the coordinates $x$ and $z$ ; to do this, we will use the `atan2(x,z)` function instead. Typically, `atan2` is used as `atan2(z, x)`, but as you may have noticed, my coordinate system has the positive x-axis pointing to the left. That is why I use `atan2(x, z)` and then subtract π/2 to align with my servo motors origin positions. The final equations become something like that. 

$$
\boxed {\theta_{1} =  \arccos\frac{r^2 + d^2 - e^2 }{2dr} + \arctan2(\frac{z}{x}) - 90^0}
$$

## INVERSE KINEMATICS : PART TWO
In the first part bellow our main task was to find the relation between the sesired position ($x$ , $y$) and the angle($\theta_1$,$\theta_2$ ) to give to the servo. But in practice it's more complicated than that; because the angles aren't sent directly to the servomotors . instead they follow the following diagram.

![IK_Full Diagram](/Pictures/IK_chart.png) 

so we need to add some other equation.
### Four-bar linkage Mechanism : Freudenstein's equation
Formulated by Ferdinand Freudenstein in 1954, it relates the input angle ($\phi$) and output the angle ($\theta_2$) of a four-bar mechanism to the lengths of its four links ($a,b,c,d$)


![IK_Full Diagram](/Pictures/IK_Four-bar_linkage_Mechanism.png) 

It gives an implicit relation between the position variables $\theta_2$ and $\phi$ . In order to obtain an explicit expression for $\theta_2$ and $\phi$ , Freudenstein's equation can be written in the form:, 

$$\boxed{K_1\cos(\theta_2)-K_2\cos(\phi)+K_3=\cos(\theta_2-\phi)}$$

where 

$$
\boxed{K_1 = \frac{d}{a} \ \ , \ \ K_2 = \frac{d}{c} \ \ ,\ \  K_3 = \frac {a^2-b^2+c^2-d^2}{2ac}}
$$

In the last part, we found expression of $\theta_2$ so our goal now is to find the expression of $\phi$ 

