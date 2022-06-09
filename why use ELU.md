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
