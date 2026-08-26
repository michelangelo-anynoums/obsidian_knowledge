# 10.2 Entropy

## Entropy

**Entropy** is a measure of **randomness or uncertainty** in a system.

It tells us how **unpredictable** the result is.

- **Low entropy** → less randomness → more predictable.
- **High entropy** → more randomness → less predictable.

### Simple example

A coin that always gives **heads** has very low entropy because the result is easy to predict.

A fair coin can give **heads or tails** with equal probability, so it has **higher entropy**.

## Entropy equation

For possible outcomes with probabilities $p_1, p_2, \ldots, p_n$:

$$H=−∑ipilog⁡2(pi)H = -\sum_i p_i \log_2(p_i)$$

where $H$ is the **entropy in bits**.

For a fair coin:

$$H=−(12log⁡212+12log⁡212)H = -\left(\frac12\log_2\frac12+\frac12\log_2\frac12\right)$$

$$H=1bitH = 1\text{bit}$$

So, a fair coin has **1 bit of entropy**.

### Remember

- **Entropy measures randomness and uncertainty.**
- **Higher entropy → higher unpredictability.**
- **Lower entropy → greater predictability.**
- Entropy is usually measured in **bits** when using $\log_2$.