> RNN 学习笔记
# 循环神经网络
> The Recurrent Neural Network will standardize the different activation functions and weights and biases so that each hidden layer has the same parameters. Then, instead of creating multiple hidden layers, it will create one and loop over it as many times as required. 
> 
> 所以叫循环神经网络
# RNN类型
> 这里看一下这个网址
>
> [链接](https://stanford.edu/~shervine/teaching/cs-230/cheatsheet-recurrent-neural-networks)
* one to one
> one to one的RNN相当于普通的神经网络，即可以认为a0为0，g2为线性函数且权重为1，偏移为0
* one to many
* many to one
* many to many

# 存在问题
* 存在梯度消失的问题
* 梯度爆炸问题
> 这些问题的解决办法：LSTM