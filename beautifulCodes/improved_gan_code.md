# improved gan codes tutorials

## cross-entropy

```
# First define 'log_sum_exp' function
# sum_k(logit_k): logit_k isn't squashed

def log_sum_exp_1(x, axis=1):
    return T.log(T.sum(T.exp(x), axis))


def log_sum_exp(x, axis=1):
    m = T.max(x, axis)
    return m+T.log(T.sum(T.exp(x-m.dimshuffle(0, 'x')), axis=axis))
    
    
# find logit of x corresponding to its label
# here, labels are vectors. labels[i] corresponds to x_i's label. i.e. 0-k 
# cross-entropy = -{ log(exp(logit)) - log(sum_j[exp(logit_j]) } = - {logit - ...}

corresponding_logit = logit[T.arange(batch), labels]  # shape(batch, 1)
cross_entropy = -(T.mean(corresponding_logit) - T.mean(log_sum_exp(logit)))

```

softplus = ln(1+exp(x))

softmax = exp(x_j)/sum_k(x_k)

The unsupervised loss computation can be referred to [improved gan test](https://github.com/SpinachR/dl_udacity_ex/blob/master/improved_gan_test.py)
There should be (K+1) classes. Here it uses a trick that fix the fake class to be 0. Because for a vector, we subtract 
every component with the same number, its softmax value won't be changed.

```buildoutcfg
''' Here, 1 indicates exp(0) for the fake class
    log_sum_exp = sum_j(exp(logit_j))
    loss_unl = - { log([log_sum_exp]/[1+log_sum_exp]) + log([1]/[1+log_sum_exp])}
'''
```


time: 7/31/2017
