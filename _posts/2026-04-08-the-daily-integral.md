---
layout: post
title: "The Daily Integral, 8 April 2026"
date: 2026-04-08T16:34:30-04:00
categories:
  - Calculus
tags:
  - daily-integral
---
Today's integral is an elegant combination of complex exponentials, an infinite Taylor series, and the Dirichlet integral.

$$
\int_{0}^{\infty} \frac{sin(sin(x))}{x} e^{cos(x)} dx
$$

<a href="https://dailyintegral.com/archive/205/hard">Link to today's hard daily integral</a>

The first thing we notice about this problem is the inclusion of both sine and cosine terms. Whenever we see the inclusion of both, we think, "how can I simplify my problem to include only one of these terms?" An easy first thought is a U-substitution, but as you could prove for yourself that won't get you very far.

Before moving forwards with any type of substitutions, we also note the strange structure of where the sine and cosine terms are: the left term has nested sines, and the cosine is found on the exponential. Why would this be the case? Is there something we can exploit from this strange placement of problems? As is with all puzzle problems, the answer is of course yes!

We want to simplify the number of terms in the integrand. If we can convert one of our terms into an exponential, we would be able to combine the powers from properties of exponents. Luckily for us, we notice that the nested sine functions are the imaginary part of a complex exponential,

$$
\sin(\sin(x)) = \operatorname{Im}(\cos(\sin(x)) + i\sin(\sin(x))) = \operatorname{Im}(e^{i\sin(x)})
$$

Using this, we can replace the left term's numerator in our integrand with the complex exponential,

$$
\int_{0}^{\infty} \frac{sin(sin(x))}{x} e^{cos(x)} dx = \int_{0}^{\infty} \frac{\operatorname{Im}(e^{i\sin(x)})}{x} e^{cos(x)} dx
$$

We can pull out the imaginary operator, since the variable of integration and bounds are real valued,

$$
\operatorname{Im}\left(\int_{0}^{\infty} \frac{(e^{i\sin(x)})}{x} e^{cos(x)}dx\right)
$$

Now that the nested sine was rewritten as a complex exponential, we can combine the powers of the two exponentials to simplify the integrand,

$$
\operatorname{Im}\left(\int_{0}^{\infty} \frac{(e^{\cos(x) + i\sin(x)})}{x} dx\right)
$$

But now, we notice something interesting! The power attached to the complex exponential is itself the definition of <i>another</i> complex exponential! This allows us to simplify the power,

$$
\cos(x) + i\sin(x) = e^{ix}
$$

$$
\operatorname{Im}\left(\int_{0}^{\infty} \frac{(e^{e^{ix}})}{x} dx\right)
$$

Does this get us anywhere though? Now it just looks like we have some crazy double exponential... What we can do to reduce this power-tower is replace the exponential with its infinite Taylor series. This way (although we do introduce an infinite summation) we have a slightly simpler term

$$
\operatorname{Im}\left(\int_{0}^{\infty} \frac{ \sum_{0}^{\infty}\frac{e^{ixn}}{n!}}{x} dx\right) = \operatorname{Im}\left(\int_{0}^{\infty} \sum_{0}^{\infty} \frac{e^{ixn}}{xn!} dx\right)
$$

We can swap the order of the integral and the summation

$$
\operatorname{Im}\left(\sum_{0}^{\infty} \int_{0}^{\infty} \frac{e^{ixn}}{xn!} dx\right)
$$

From here, we expand back out the complex exponential using Euler's identity. We do so in order to get us towards the Dirichlet integral, which has a known solution over the bounds $$(0, \infty)$$. Granted, we did not need to combine the terms in the original complex exponential into this term we are expanding out again, we could have just left the original expression as is. However, for the sake of brevity in my expressions, I simplified it when carrying it through the last few steps.

$$
\operatorname{Im}\left(\sum_{0}^{\infty} \left(\frac{1}{n!}\right) \int_{0}^{\infty} \frac{cos(nx) + isin(nx)}{x} dx\right)
$$

$$
\sum_{0}^{\infty} \left(\frac{1}{n!}\right) \operatorname{Im}\left( \int_{0}^{\infty} \frac{cos(nx)}{x} dx + i\int_{0}^{\infty}\frac{sin(nx)}{x}dx\right)
$$

Since we pulled out the imaginary operator at the very beginning, we can drop the real component of our integral, which works out great! The first term does not have a bounded solution, so we are happy to only use the sine component (the Dirichlet integral)

$$
\sum_{0}^{\infty} \left(\frac{1}{n!}\right) \int_{0}^{\infty}\frac{sin(nx)}{x} dx
= \frac{\pi}{2} \sum_{1}^{\infty} \left(\frac{1}{n!}\right)
$$

In the previous step, we are able to change the summation starting term from 0 to 1 from the fact that when $$n = 0$$, the Dirichlet integral is $$0$$, and when $$n > 0$$, the Dirichlet integral is $$\frac{\pi}{2}$$.

Finally, we need to solve the infinite sum. We notice that this is simply the Taylor series of $$e^x$$ evaluated at $$x = 1$$ (if we modify the starting bound of the sum to be 0).

$$
1 + \sum_{0}^{\infty} \left(\frac{1}{n!}\right) = e - 1
$$

Therefore, the final answer for the integral is

$$
\frac{\pi}{2} (e - 1) \approx 2.699
$$