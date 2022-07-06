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

# RNN architecture(记忆单元分类，记忆单元存储过去的信息)
* 主要存在三种类型的RNN
    * Vanilla RNN
    > 简单地用前一个状态的状态信息和当前状态的输入来声称当前状态的状态信息
    >
    > 存在梯度消失的问题
    * LSTM (Hochreiter, S., and J. Schmidhuber, 1997 Long short-term memory. Neural computation 9: 1735–1780.)
    * GRU (Cho, K., B. van Merriënboer, C. Gulcehre, D. Bahdanau, F. Bougares et al., 2014 Learning Phrase Representations using RNN Encoder–Decoder for Statistical Machine Translation. Proceedings of the 2014 Conference on Empirical Methods in Natural Language Processing (EMNLP) 1724–1734. 10.3115/v1/D14-1179 https://www.aclweb.org/anthology/D14-1179)
    > LSTM和GRU解决了Vanilla RNN梯度消失的问题，总的来说，LSTM和GRU通过加法而不是乘法来计算前层中的权重/偏差更新，这样的话架构就能避免梯度消失的问题。

# RNN模型分类
* 三种类别
    * 单向循环
    * 双向循环
    > ![image.png](https://s2.loli.net/2022/07/06/VvcyJSBnoDzw1Gs.png)
    * 多层单向或双向叠加(Deep RNN)
# RNN优点
* RNN每个时刻的权重都是相同的，这样才能够处理变长序列
* 模型大小与序列长度无关
* 计算量与序列长度成线性关系，而不是平方关系
* 相比于DNN，考虑了历史信息
# pytorch RNN
* 这个RNN可以实现一个简单的Elman RNN
* RNN的公式
> ![image.png](https://s2.loli.net/2022/07/04/S68WRq9Eeldw5xu.png)
# feedforward and backpropagation
* feedforward是neural network的类型，而backpropagation是优化算法。
* [具体网址](https://stackoverflow.com/questions/28403782/what-is-the-difference-between-back-propagation-and-feed-forward-neural-network)
# RNN存在的问题
* Vanishing Gradient Problem
> RNN中反向传播与feedforward神经网络反向传播的概念上有些区别:
>   * 在feedforward神经网络中，我们的前向传播是一个一个神经元进行传播的，而在RNN中，前向传播是一个一个时间点进行传播的
>   * 可以计算error function at each time point
>   > basically, during the training, your cost  function compares your outcomes (red circles on the image below) to your desired output
* Exploding Gradient Problem
* Long Term Dependency Issue
> 