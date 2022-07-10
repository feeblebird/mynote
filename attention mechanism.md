# introduce [参考](https://machinelearningmastery.com/the-attention-mechanism-from-scratch/)
* 提出attention mechanism的文章[链接](https://arxiv.org/abs/1409.0473)
* The attention mechanism was introduced to improve the performance of the encoder-decoder model for machine translation. The idea behind the attention mechanism was to permit the decoder to utilize the most relevant parts of the input sequence in a flexible manner, by a weighted combination of all of the encoded input vectors, with the most relevant vectors being attributed the highest weights. 
* The attention mechanism was introduced by Bahdanau et al. (2014), to address the bottleneck problem that arises with the use of a fixed-length encoding vector, where the decoder would have limited access to the information provided by the input. This is thought to become especially problematic for long and/or complex sequences, where the dimensionality of their representation would be forced to be the same as for shorter or simpler sequences.
# 李沐视频 [参考](bilibili.com/video/BV1264y1i7R1?spm_id_from=333.337.search-card.all.click&vd_source=6942082806aa0c4d4198eb27bcd0681a)
* 人类根据随意线索和不随意线索选择注意点
    * 不随意线索：可以说是客观的线索，就是说不是我们刻意的
    * 随意线索：是主观的线索，使我们刻意的
* 卷积、全连接、池化层都只考虑不随意线索
    * 注意力机制则考虑随意线索
        * 随意线索被称之为查询(query)
        * 每个输入是一个值(value)和不随意线索(key)的对(pair)
        * 通过注意力池化层会根据query来有偏向地选择某些输入
* 非参注意力池化层
![image.png](https://s2.loli.net/2022/07/10/z8a3Q2Mm1hGypcr.png)
    * 这里就是key-value对
    * 平均池化是最简单的方案：f(x) = 将所有y值平均
        > f(x)的x就是我们的query，这里是不管query是啥，直接将所有value做均值返回
    * 更好的方法是：
        > 给定了query，我们去衡量query和每个候选x_i的距离，K为kernel函数，每个K(x-x_i)除以分母之后，可以理解为变成一个概率，可以说是相对的重要性。在通过这个权重对y_i求和，
        >
        > 非参的意思是不需要学任何东西，只需要数据就可以，来一个新值，只看与它相似的数据的value就行，其他的不管。
    * 选择高斯kernel
        > ![image.png](https://s2.loli.net/2022/07/10/qvE6W9zjJOIMLHS.png)
    > 非参注意力池化层与现代的池化层是很相近的
    