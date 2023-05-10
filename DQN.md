---
title: "Deep Reinforcement Learning paper notes"
permalink: /
layout: default
theme: minima
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

## 论文内容记录
The environment(or emulator) is The Arcade Learning Environment.

进行实际仿真的时候应当采用模拟、训练相互独立的形式进行，这样的目的是提高训练的效率，减少渲染环境所消耗的电脑算力。游戏的分数是根据规定的*奖励函数*来进行计算的.
在进行实际的演算的过程中，通过设定最大的时间步长，即设定最多的运行步数(step次数)，超过后将会进入下一次迭代，并在迭代开始时进行reset().

论文中采用的是像素级别的强化学习进行的训练，通过记录整个屏幕的图像来进行训练，通过观察其中的动作数值以及状态数值的序列来进行的相关的游戏策略的设计。所有的游戏策略是一个有限的时间步长就可以实现的过程，通过MDP将每个序列作为一个确定的状态来进行马尔可夫决策过程规划的解决方法，来进行奖励的计算。每个智能体的目标均为利用模拟器来获取未来能够获取最大奖励函数的动作。我们通过定义可以选择的动作价值函数Q,通过动作价值函数来确定要采用的策略$\pi$,即采取的连续动作序列。

在动作价值函数的设置过程中，遵循的方程为贝尔曼最优方程。在迭代次数$i->\infin$的过程中，会出现Q=Q\*结果，即最终会收敛到最优动作价值函数Q*。由于每一个序列都是相互独立的，而并非是什么不断延续下去的结果，因此我们只能通过函数拟合的方法，来构造函数$Q(s,a,\theta)\approx Q(s,a)$。

Q网络的目的是最小化序列的损失函数，即最小化损失函数的数值，类似于大多数神经网络最小化loss数值的形式，采用随机梯度下降等方式来进行正向反向传播，最终实现参数的更改，使得原本的参数数值不断接近最优的参数值，进而更好的拟合原本需要的动作价值函数Q。

### DQN算法的性质

$model\ free$

采样的方法来进行仿真器的设计，明确的构建了强化学习的估计环境。

$off-policy$

离线策略，采用贪心算法获取动作，同时允许一定的状态空间的探索，具体采用的是$\epsilon-greedy$算法来进行这种目的的实现。

## Formula Record

奖励函数：
$R_t=\sum_{t'=t}^T\gamma^{t'-t}r_{t'}$

动作价值函数：
$Q*(s,a)=max_{\pi}E[R_t|s_t=s,a_t=a,\pi]$

贝尔曼最优方程：
$Q*(s,a)=E_{s'-\epsilon}[r+\gamma max_{a'}Q*(s',a')|s,a]$

损失函数：
$L_i(\theta_i)=E_{s.a-\rho(·)}(y_i-Q(s,a;\theta_i))^2$

