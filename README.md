# There is all CAD files and the mechanical explenations behind this project
Disclaimer /!\ this project was not made by using AI ! 

When i was working on this project, i was just a robotics student passionate about big challenges. Because of that, there may be some imperfections or misatkes in this project so If you spot any issues or have ideas for improvements, please feel free to open an issue or submit a pull request. Contributions and feedback are always welcome!

> "A robot may not harm a human being or, through inaction, allow that human being to come to harm" *ISAAC ASIMOV*.

## INVERSE KINEMATICS
This part of the project is the most important . The robot's entire locomotion depends on it and the goal of this part is to find the relation between the robot end leg and motor rotation angle. 

![IK of one leg](/Pictures/IK.png)

According to the picture bellow, **$e$ is equal to the length of the shin and $d$ the length of thigh** . Our next step is to find the expression of $ \theta_1 $ and $ \theta_2 $ for that we'll use few geometric formulas. 

 ### 1 - Let's find $\theta_2 $
According to Pythagoras's formula we found that

$$ 
\boxed {r^2 = x^2+z^2} \\ 
$$

And with the cosin law we found that

$$ 
\boxed {r^2 = e^2 + d^2 -2*e*d*\cos(\theta_2)} 
$$

After equating these two equations, we obtain this.

$$ 
x^2+z^2 = e^2 + d^2 -2*e*d*\cos(\theta_2) 
$$

$$  2*e*d*\cos(\theta_2)  = (e^2 + d^2)-(x^2+z^2) $$
$$  \cos(\theta_2)  = \frac {(e^2 + d^2)-(x^2+z^2)}{2*e*d} $$
and at the end we found that 

$$ \boxed{\theta_2  = \cos^{-1}\frac {(e^2 + d^2)-(x^2+z^2)}{2*e*d}} 
$$