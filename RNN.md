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

# RNN模型分类[参考](https://www.bilibili.com/video/BV13i4y1R7jB/?spm_id_from=333.788&vd_source=6942082806aa0c4d4198eb27bcd0681a)
* 三种类别
    * 单向循环
    * 双向循环
    > ![image.png](https://s2.loli.net/2022/07/06/VvcyJSBnoDzw1Gs.png)
    * 多层单向或双向叠加(Deep RNN)
# RNN优点[参考](https://www.bilibili.com/video/BV13i4y1R7jB/?spm_id_from=333.788&vd_source=6942082806aa0c4d4198eb27bcd0681a)
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
>   > 
>   > ![image.png](https://s2.loli.net/2022/07/06/CedFpPmLXzRnuEs.png)
>   > ![image.png](https://s2.loli.net/2022/07/06/ZnJFh9ekXrDoMQ5.png)
>   > 
>   > [参考网站](https://www.superdatascience.com/blogs/recurrent-neural-networks-rnn-the-vanishing-gradient-problem)

* Exploding Gradient Problem
* Long Term Dependency Issue
    > Let us consider a sentence-
    > 
    > “I am a data science student and I love machine ______.”
    > 
    > We know the blank has to be filled with ‘learning’. But had there been many terms after “I am a data science student” like, “I 
    > 
    > am a data science student pursuing MS from University of…… and I love machine ______”.
    > 
    > This time, however, RNNS fails to work. Likely in this case we do not need unnecessary information like “pursuing MS from 
    >
    > University of……”. What LSTMs do is, leverage their forget gate to eliminate the unnecessary information, which helps them 
    >
    > handle long-term dependencies.

# 单向简单rnn和双向简单rnn的代码实现(代码在jupyter notebook)
```python
import torch
import torch.nn as nn

batch_size, T = 2, 3 # 批量大小，序列长度(比如时间序列的长度)
input_size, hidden_size = 2, 3 # 输入特征大小，隐含层特征大小
input = torch.randn(batch_size, T, input_size) # 随机初始化一个输入特征序列
h_prev = torch.zeros(batch_size, hidden_size) # 初始隐含状态

# step1 调用pytorch rnn api
rnn = nn.RNN(input_size, hidden_size, batch_first=True)
rnn_output, state_final= rnn(input, h_prev.unsqueeze(0))
print(rnn_output)
print(state_final)

# step2 手写一个rnn_forward函数，实现单向RNN的计算原理
def rnn_forward(input, weight_ih, weight_hh, bias_ih, bias_hh, h_prev):
    bs, T, input_size = input.shape
    h_size = weight_ih.shape[0]
    # 这里的公式是xt W_ih的转置
    # 这里公式的输出是t时刻的隐藏状态ht，这里ht的形状应该是(batch_size, hidden_size)
    # 所以如果按照公式xt W_ih的转置来说，想知道hidden_size的话，xt的形状为t时刻input的形状(batch_size, input_size)
    # 那么hidden_size的形状即为W_ih转置的shape[1]，即为W_ih的shape[0]
    # W_ih的shape为(hidden_size, input_size)
    h_out = torch.zeros(batch_size, T, h_size) # 初始化一个状态矩阵，即各个隐藏状态的输出
    
    for t in range(T):
        x = input[:, t, :] #获取当前时刻输入特征
        x_times_wt = torch.mm(x, weight_ih.transpose(0, 1)) # x_times_wt的shape为(batch_size, hidden_size)
        h_times_whht = torch.mm(h_prev, weight_hh.transpose(0, 1)) 
        # h_prev的shape为(batch_size, hidden_size), weight_hh的shape为(hidden_size, hidden_size), x_times_whht的shape为(batch_size, hidden_size)
        h_prev = torch.tanh(x_times_wt + bias_ih + h_times_whht + bias_hh)
        # 要进行递归运算
        
        h_out[:, t, :] = h_prev
        
    return h_out, h_prev.unsqueeze(0)

# 验证rnn_forward的正确性
# 从torch的rnn中找出我们验证所需的参数
for name, parameter in rnn.named_parameters():
    print(name)
    print(parameter)
# 参数中l0的意思是第0层，即第1层

custom_rnn_output, custom_state_final = rnn_forward(input, rnn.weight_ih_l0, rnn.weight_hh_l0, rnn.bias_ih_l0, rnn.bias_hh_l0, h_prev)
print(custom_rnn_output)
print(custom_state_final)

# step3 手写一个bidirectional_rnn_forward函数，实现双向RNN的计算原理
def bidirectional_rnn_forward(input, weight_ih, weight_hh, bias_ih, bias_hh, h_prev, \
                             weight_ih_reverse, weight_hh_reverse, bias_ih_reverse, bias_hh_reverse, h_prev_reverse):
    batch_size, T, input_size = input.shape
    h_size = weight_ih.shape[0]
    h_out = torch.zeros(batch_size, T, h_size*2) # 初始化一个状态矩阵，注意双向是两倍的特征大小，两倍的hidden_size
    
    forward_output = rnn_forward(input, weight_ih, weight_hh, bias_ih, bias_hh, h_prev)[0]
    backward_output = rnn_forward(torch.flip(input, [1]), weight_ih_reverse, weight_hh_reverse, bias_ih_reverse, bias_hh_reverse, h_prev_reverse)[0]
    # 这里input需要进行翻转，就是时间靠后的在前面，所以需要对input的t维度即第二个维度进行翻转
    
    h_out[:, :, :h_size] = forward_output
    h_out[:, :, h_size:] = backward_output
    # forward_output和backward_output都是经过rnn_forward函数拼接过的
    
    return h_out, h_out[:, -1, :].reshape(batch_size, 2, h_size).transpose(0, 1)

# 验证bidirectional_rnn_forward的正确性
bi_rnn = nn.RNN(input_size, hidden_size, batch_first=True, bidirectional=True)
h_prev = torch.zeros(2, batch_size, hidden_size)
bi_rnn_output, bi_state_final = bi_rnn(input, h_prev)
for name, parameter in bi_rnn.named_parameters():
    print(name)
    print(parameter)
    
print(bi_rnn_output, bi_state_final)

custom_bi_rnn_output, custom_bi_rnn_state_final = bidirectional_rnn_forward(input, bi_rnn.weight_ih_l0, bi_rnn.weight_hh_l0,\
                                                                            bi_rnn.bias_ih_l0, bi_rnn.bias_hh_l0, h_prev[0], \
                         bi_rnn.weight_ih_l0_reverse, bi_rnn.weight_hh_l0_reverse, bi_rnn.bias_ih_l0_reverse, bi_rnn.bias_hh_l0_reverse,\
                          h_prev[1])
print(custom_bi_rnn_output, custom_bi_rnn_state_final)
```
* 现在pytorch中RNN的公式：
    > ![image.png](https://s2.loli.net/2022/07/08/FyfI17oUscwPGid.png)

# Long-short-term-memory(LSTM)
* [参考](https://www.pluralsight.com/guides/introduction-to-lstm-units-in-rnn)LSTM primarily solves the vanishing gradient problem in backpropagation. LSTMs use a gating mechanism that controls the memoizing process. Information in LSTMs can be stored, written, or read via gates that open and close. These gates store the memory in the analog format, implementing element-wise multiplication by sigmoid ranges between 0-1. Analog, being differentiable in nature, is suitable for backpropagation.
    > analog: 模拟信号
* sigmoid function in LSTM[参考](https://www.pluralsight.com/guides/introduction-to-lstm-units-in-rnn)
    > sigmoid function maintains the values between 0 and 1. It helps the network to update or forget the data. If the multiplication results in 0, the information is considered forgotten. Similarly, the information stays if the value is 1.
    >
    > This will help the network learn which data can be forgotten and which data is important to keep.

# Gates in LSTM cells
* The term cell[参考](https://www.analyticsvidhya.com/blog/2022/01/the-complete-lstm-tutorial-with-implementation/)
    > every unit of the LSTM network is known as a `cell`. each cell is composed of 3 inputs:
    >   * x(t): token(output) at timestamp t
    >   * h(t-1): previous hidden state
    >   * c(t-1): previous cell state
    > and 2 outpus:
    >   * h(t): updated hidden state, used for predicting the output
    >   * c(t): current cell state
* The term gate[参考](https://www.analyticsvidhya.com/blog/2022/01/the-complete-lstm-tutorial-with-implementation/)
    > LSTM uses a special theory of controlling the memorizing process. Popularly referred to as gating mechanism in LSTM, what the gates in LSTM do is, store the memory components in analog format, and make it a probabilistic score by doing point-wise multiplication using sigmoid activation function, which stores it in the range of 0–1. Gates in LSTM regulate the flow of information in and out of the LSTM cells.
![image.png](https://s2.loli.net/2022/07/07/wLIQ93mb4E8ctz2.png)
## forget gate
![image.png](https://s2.loli.net/2022/07/07/O6mPFfLTreC9Mlv.png)
* The forget gate decides which information needs attention and which can be ignored. The information from the current input X(t) and hidden state h(t-1) are passed through the sigmoid function. Sigmoid generates values between 0 and 1. It concludes whether the part of the old output is necessary (by giving the output closer to 1). This value of f(t) will later be used by the cell for point-by-point multiplication.
    > 这里说 It concludes whether the part of the old output is necessary (by giving the output closer to 1). 从图片里面的公式来看，sigmoid函数的输入是h(t-1)和x(t)的拼接，然后输出sigmoid函数的值。我觉得这里的old output是c(t-1)。
## input gate
![image.png](https://s2.loli.net/2022/07/07/AHjry7bJa82Lq5B.png)
* The input gate performs the following operations to update the cell status.
  
  First, the current state X(t) and previously hidden state h(t-1) are passed into the second sigmoid function. The values are transformed between 0 (important) and 1 (not-important).
  
  Next, the same information of the hidden state and current state will be passed through the tanh function. To regulate the network, the tanh operator will create a vector (C~(t) ) with all the possible values between -1 and 1. The output values generated form the activation functions are ready for point-by-point multiplication.
## cell state
![image.png](https://s2.loli.net/2022/07/07/6eYZV8Efvt4Juaq.png)
* The network has enough information from the forget gate and input gate. The next step is to decide and store the information from the new state in the cell state. The previous cell state C(t-1) gets multiplied with forget vector f(t). If the outcome is 0, then values will get dropped in the cell state. Next, the network takes the output value of the input vector i(t) and performs point-by-point addition, which updates the cell state giving the network a new cell state C(t).
## output gate
![image.png](https://s2.loli.net/2022/07/07/vr5CWIF4RdO1KxU.png)
* **The output gate determines the value of the next hidden state.** This state contains information on previous inputs.

  First, the values of the current state and previous hidden state are passed into the third sigmoid function. Then the new cell state generated from the cell state is passed through the tanh function. Both these outputs are multiplied point-by-point. Based upon the final value, the network decides which information the hidden state should carry. This hidden state is used for prediction.

Finally, the new cell state and new hidden state are carried over to the next time step.

To conclude, the forget gate determines which relevant information from the prior steps is needed. The input gate decides what relevant information can be added from the current step, and the output gates finalize the next hidden state.
# LSTM code implementation
* pytorch中lstm的公式如下
> ![image.png](https://s2.loli.net/2022/07/07/DAX6RJTfjLkHMtd.png)
> > 其中分别对应着不同gate的输出
> > 
> > x(t)表示当前timestamp的input
> >
> > h(t-1)表示前一个timestamp的hidden state
> >
> > i(t)表示**input gate中sigmoid函数**的输出
> > 
> > f(t)表示**forget gate**的输出
> > 
> > g(t)表示**input gate中tanh函数**的输出
> > 
> > o(t)表示**output gate中sigmoid函数**的输出
> > 
> > c(t)表示**cell state**的输出
> >
> > h(t)表示**output gate**的输出
> 
> h(t)就是LSTM的输出
>
> 下标是t-1的就是我们使用LSTM时需要设置的初始状态
> , RNN中我们需要设置h(0)，LSTM中我们还需要设置c(0)
# famous LSTM tutorial
* [连接](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
## lstmp
* pytorch的lstm的初始化参数中有一个参数是`proj_size`
    > 如果这个参数的值大于零，那么lstm就变成了lstmp，因为lstm的计算量太大了，所以lstmp对减少了计算量，它对h(t)的计算进行了压缩
    >
    > 如果设置了`proj_size`，那么hidden state的size就变成了`proj_size`的数值