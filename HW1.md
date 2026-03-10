### Problem 1
#### (a)
The gap should be defined as the value difference caused by the change of last digit in mantissa. 
##### Case 1: The exponent remains after changing
The value before changing could be expressed as
$$
v= (-1)^{S}\times m \times 2^{e}
$$
where
$$
\begin{align*}
m=&1.M= 1.d_{1}d_{2}\dots d_{23}\\
=& 1+d_{1}2^{-1}+d_{2}2^{-2}+\cdots +d_{23}2^{-23}
\end{align*}
$$
The exponent of the normalized number remains, so that without loss of generality, the value after changing 
$$
v' = (-1)^{S}\times m' \times 2^{e}
$$
where
$$
m'=m\pm 2^{-23}
$$
Therefore
$$
\Delta v = v'- v = \pm 2^{-23}\times 2^{e}
$$
and the relative variance
$$
\begin{align*}
\left| \frac{\Delta v}{v} \right|=& \frac{2^{-23}\times2^{e}}{m\times2^e}\\
=& \frac{2\times2^{-23}}{m}\\
=& \frac{2\times 2^{-23}}{1.d_{1}d_{2}\dots d_{23}}
\end{align*}
$$
so that we can obtain that
$$
\begin{align*}
2\times 2^{-24} \le \left| \frac{\Delta v}{v} \right|\le 2\times 2^{-23}
\end{align*}
$$
##### Case 2: The exponent varies after changing
It's easy to know that when the exponent increases, the difference
$$
\Delta v = 2^{-23}\times 2^{e}
$$
Similar to case 1, the relative variance 
$$
\begin{align*}
2\times 2^{-24} \le \left| \frac{\Delta v}{v} \right|\le 2\times 2^{-23}
\end{align*}
$$
When the exponent decreases, the value before changing
$$
v= (-1)^{S}\times m \times 2^{e}
$$
where
$$
\begin{align*}
m=&1.M= 1.d_{1}d_{2}\dots d_{23}\\
d_{1}=& d_{2}=\dots = d_{23}=0
\end{align*}
$$
Then the value after changing
$$
v' = (-1)^{S}\times m' \times 2^{e-1}
$$
where
$$
\begin{align*}
m' =& 1.d_{1}'d_{2}'\dots d_{23}'\\
d_{1}' =& d_{2}'=\cdots = d_{23}'=1
\end{align*}
$$
The difference
$$
\Delta v = v - v' = 2^{-24}\times 2^{e}
$$
The relative variance
$$
\begin{align*}
\left| \frac{\Delta v}{v} \right|=& \frac{2^{-24}\times2^{e}}{m\times2^e}\\
=& \frac{2\times2^{-23}}{m}\\
=& \frac{2\times 2^{-23}}{1.00\dots 0}=2\times 2^{-23}
\end{align*}
$$
Q.E.D.
#### (b)
It's evident that $0, \pm 1$ could be represented exactly by the single precision floating-point system.
Note that $2^{24}=16777216\approx 16.8\ \rm million$, now let's consider integers between $\pm 2^{24}$. For any integer $-2^{24}< i< 2^{24}$ that could be represented by single precision system, there's a binary decomposition
$$
\begin{align*}
i =& 1.d_{1}\dots d_{23}\times 2^{p}\\
=& \left(1+ d_{1}2^{-1} + \cdots d_{23}2^{23} \right)\times 2^{p}
\end{align*}
$$
It's evident that $p\le 24$. As long as $p\le 23$, the integer before and after $i$ could always be expressed by
$$
i_{\pm}= \left(1+ d_{1}2^{-1} + \cdots d_{23}2^{23} \pm 2^{-p} \right)\times 2^{p}
$$
By induction, each integer $-2^{24}< i_{0} < 2^{24}$ could be represented by single precision system.
When $p=24$, $\pm 2^{24}$ could be represented by
$$
\pm 2^{24}= \pm \left(1+ 0\cdot 2^{-1} + \cdots 0\cdot 2^{23}\right)\times 2^{24}
$$
Now, we've proved that each integer between $\pm 2^{24}$ has an exact representation in single precision floating-point system.

### Problem 2

Let $a= 2^{24},b=c=1$, then we find that in single precision system
$$
\begin{align*}
(a+b)+c =& (2^{24}+1)+1\\
=& 2^{24}+1\\
=& 2^{24}\\
a+(b+c)=& 2^24+(1+1)\\
=& 2^{24}+2
\end{align*}
$$
The reason why the results differs is that in single precision system, $2^{24}$ is represented as
$$
\begin{align*}
2^{24}=& (-1)^{0}\times (1.0\dots 0)\times 2^{24}\\
=& (-1)^{0}\times (1+0\cdot 2^{-1}+\cdots + 0\cdot 2^{-23})\times 2^{24}
\end{align*}
$$
where the last digit represents
$$
\Delta = 2^{-23}\times 2^{24}=2
$$
i.e. the gap here is $2$. Therefore, when calculating $(a+b)+c$, it could not recognize the exact value $2^{24}+1$, while when calculating $a+(b+c)$, the exact values $2$ and $2^{24}+2$ could be recognized correctly, which leads to the difference between the results.

### Problem 3
When it comes to subtraction, we know that:
$\forall x, y \in \mathbb{R}$, $\exists s,t,\mu$ with $\max\{ |s|, |t|,|\mu|\}\le \varepsilon_{machine}$ s.t.
$$
\begin{align*}
fl(x) =& x(1+s)\triangleq X\in F\\
fl(y) =& y(1+t)\triangleq Y\in F\\
X\ominus Y=& fl(X-Y) = (X-Y)(1+\mu)
\end{align*}
$$
The forward error
$$
\begin{align*}
Error_{forward} =& (X-Y)(1+\mu) - (x-y)\\
=& sx - yt +\mu(x(1+s)-y(1+t))\\
=& \mu(x-y) + (sx-yt)(1+\mu)
\end{align*}
$$
Relative error
$$
\begin{align*}
\left| \frac{Error_{forward}}{True\ Value} \right|=&\left|\mu + \frac{(sx-yt)(1+\mu)}{x-y}\right| \\
=& \left| \mu + (1+\mu)(s+\frac{y(s-t)}{x-y}) \right|\\
=&\left| \frac{y(s-t)}{x-y} + O(\varepsilon_{machine}) \right|
\end{align*}
$$
let $|x-y| < \varepsilon\in \mathbb{R}, y>N\in\mathbb{N}$, for any $s,t$ determined, when $\varepsilon$ small enough and $N$ large enough, 
$$
\begin{align*}
\left| \frac{Error_{forward}}{True\ Value} \right|=&\left| \frac{y(s-t)}{x-y} + O(\varepsilon_{machine}) \right|\\
=& |s-t|\left| \frac{y}{x-y} \right|+O(\varepsilon_{machine})\\
\to&\infty \qquad (\varepsilon\to 0, N\to \infty)
\end{align*}
$$
so the accuracy of subtraction might be problematic.

### Problem 4
Similarly, we know that $\forall x, y \in \mathbb{R}$, $\exists s,t,\mu$ with $\max\{ |s|, |t|,|\mu|\}\le \varepsilon_{machine}$ s.t.
$$
\begin{align*}
fl(x) =& x(1+s)\triangleq X\in F\\
fl(y) =& y(1+t)\triangleq Y\in F\\
X\oplus Y=& fl(X+Y) = (X+Y)(1+\mu)
\end{align*}
$$
Considering 
$$
\begin{align*}
f(x,y) =& x+y\\
\tilde{f}(x,y) =& fl(x)\oplus fl(y) = (x(1+s) + y(1+t))(1+\mu)
\end{align*}
$$
from which we find that
$$
\begin{align*}
	\exists \tilde{x} = X(1+\mu), \tilde{y} = Y(1+\mu)
\end{align*}
$$
s.t.
$$
f(\tilde{x},\tilde{y}) = f(x,y)
$$
The backward error could be analyzed as below:
$$
BE\le\|(x,y) - (\tilde{x},\tilde{y}) \|\le O(\varepsilon_{machine})\|(x,y)\|
$$
which shows the backward stability.
Considering
$$
\begin{align*}
f(x) =& x+1\\
\tilde{f}(x)=&fl(x)\oplus1
\end{align*}
$$
when $0<x<\varepsilon_{machine}$, we have
$$
\begin{align*}
\tilde{f}(x) =& fl(x)\oplus 1 = 0\oplus 1= 1\\
f(\tilde{x}) =& \tilde{x}+ 1 = 1\\
\implies\quad \tilde{x} =& 0
\end{align*}
$$
Therefore, the backward error
$$
\begin{align*}
BE =& \frac{\|\tilde{x}-x \|}{\|x \|}\\
=& 1\gg\varepsilon_{machine}
\end{align*}
$$
such we proved that $\tilde{f}(x)=fl(x)\oplus1$ is not backward stable.