

```python
data = [
3.23, -2.5, 1.88, -0.68, 4.43, 0.17,
1.03, -0.07, -0.01, 0.76, 1.76, 3.18,
0.33, -0.31, 0.3, -0.61, 1.52, 5.43,
1.54, 2.28, 0.42, 2.33, -1.03, 4.0,
0.39
]

n = len(data)
%pylab inline
```

    Populating the interactive namespace from numpy and matplotlib



```python
mu = mean(data)
s = std(data)
tau = 1.645*s + mu
print "Mu: %f\nSigma: %f\nTau: %f" % (mu, s, tau)
```

    Mu: 1.190800
    Sigma: 1.817554
    Tau: 4.180677


$$ \tau = g(\theta) = \Phi^{-1}(0.95) \sigma + \mu \approx 1.645\sigma + \mu$$

$$ \hat{se} = \sqrt{\left( \nabla_{\theta}g \right)^T I_n^{-1} \left( \nabla_{\theta}g \right) } $$

Where

$$ \nabla_{\theta}g = \begin{pmatrix} 1 \\ 1.645 \end{pmatrix} $$


```python
se_hat = s*sqrt(1 + 0.5*1.645**2)/sqrt(n)
print "Analytic estimate of se: %f" % se_hat
```

    Analytic estimate of se: 0.557609



```python
B = 10000

def compute_tau(d):
    return 1.645*std(d) + mean(d)

bootstrap_samples = [compute_tau(normal(mu, s, size=n)) for i in range(B)]
se_boot = std(bootstrap_samples)
print "Bootstrap estimate of se: %f" % se_boot
```

    Bootstrap estimate of se: 0.555862



```python
print "95% Confidence Intervals:"
print "Analytic\t(%.3f, %.3f)" % (mu-2*se_hat, mu+2*se_hat)
print "Bootstrap\t(%.3f, %.3f)" % (mu-2*se_boot, mu+2*se_boot)
```

    95% Confidence Intervals:
    Analytic	(0.076, 2.306)
    Bootstrap	(0.079, 2.303)



```python

```
