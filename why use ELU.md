# ReLU
* solve the gradient vanishing problem
* has the dead ReLU problem
* do not avoid exploding gradient problem

# ELU
* avoid dead ReLU problem
* produce negative outputs, the mean of ELU is closer to zero, accelerating the train of the network
* do not avoid exploding gradient problem

# LeakyReLU
* like ELU avoid dead ReLU problem
* compute faster
* become linear function, the ELU is easier to fit a nonlinear function, ELU is partly linear and nonlinear

# GeLU


# compare to ReLU
* the mean of ELU closer to zero
> 参考那个efficient propagation文献，更接近零，网络收敛速度更快
* avoid the dead ReLU problem
# compare to LeakyReLU
* LeakyReLU is linear, ELU is partly nonlinear
> 更好地拟合非线性函数
# compare to GeLU
* faster to compute