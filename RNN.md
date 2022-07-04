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

# 其他
* Elman RNN and Jordan RNN is simple recurrent network
> [参考链接](https://en.wikipedia.org/wiki/Recurrent_neural_network)

# RNN architecture
* 主要存在三种类型的RNN
    * Vanilla RNN
    > 简单地用前一个状态的状态信息和当前状态的输入来声称当前状态的状态信息
    >
    > 存在梯度消失的问题
    * LSTM (Hochreiter, S., and J. Schmidhuber, 1997 Long short-term memory. Neural computation 9: 1735–1780.)
    * GRU (Cho, K., B. van Merriënboer, C. Gulcehre, D. Bahdanau, F. Bougares et al., 2014 Learning Phrase Representations using RNN Encoder–Decoder for Statistical Machine Translation. Proceedings of the 2014 Conference on Empirical Methods in Natural Language Processing (EMNLP) 1724–1734. 10.3115/v1/D14-1179 https://www.aclweb.org/anthology/D14-1179)
    > LSTM和GRU解决了Vanilla RNN梯度消失的问题，总的来说，LSTM和GRU通过加法而不是乘法来计算前层中的权重/偏差更新，这样的话架构就能避免梯度消失的问题。
    