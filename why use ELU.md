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
## 伯努利分布
* 伯努利分布是一个离散概率分布(Discrete probability distribution)
* 介绍离散概率分布中两个重要的函数：
    * 概率质量函数(probability mass function, PMF)
        > 是离散随机变量在特定取值上的概率P(x)，其总和为1。
        >
        > 与概率密度函数f(x)不同，概率质量函数是对离散随机变量定义的，本身就代表该值的概率，而概率密度函数在某一区间的积分才是概率。
    * 累计分布函数(cumulative distribution function, CDF)
        > 定义为F(x)=P(X≤x)，是单调递增的，且满足F(负无穷)=0和F(正无穷)=1。
        >
        > 对应于离散分布，他是所有小于等于x的值出现的概率之和。
* 伯努利分布又称为两点分布或者0-1分布，我们记成功的概率为p，则失败的概率q=1-p，则
    * 其概率质量函数(probability mass function, PMF)为
        > ![image.png](https://s2.loli.net/2022/06/10/soP8rweh5WYvucq.png)
# compare to ReLU
* the mean of ELU closer to zero
> 参考那个efficient propagation文献，更接近零，网络收敛速度更快
* avoid the dead ReLU problem
# compare to LeakyReLU
* LeakyReLU is linear, ELU is partly nonlinear
> 更好地拟合非线性函数
# compare to GeLU
* faster to compute