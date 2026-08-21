# There is all CAD files and the mechanical explenations behind this project
Disclaimer /!\ this project was not made by using AI ! 

When i was working on this project, i was just a robotics student passionate about big challenges. Because of that, there may be some imperfections or misatkes in this project so If you spot any issues or have ideas for improvements, please feel free to open an issue or submit a pull request. Contributions and feedback are always welcome!

> "A robot may not harm a human being or, through inaction, allow that human being to come to harm" *ISAAC ASIMOV*.

## INVERSE KINEMATICS
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

