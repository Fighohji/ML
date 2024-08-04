## 强化学习（Reinforcement Learning）

- 是一种学习方式，强化学习训练时，需要环境给予反馈，以及对应具体的反馈值。主要是指导训练对象每一步如何决策，采用什么样的行动可以完成特定的目的或者使收益最大化。
- 组成
  - **Agent**
  - **Environment**
  - **State**
  - **Action**
  - **Reward**
- 训练过程是基于**马尔可夫决策过程（Markov Decision Process）**，核心思想是下一步的State只和当前的状态State以及当前状态将要采取的Action有关，只回溯一步

- 算法

  - **Value Based**
    - 基于每个State下可以采取的所有Action，这些Action对应的Value，来选择当前State如何行动

    - value不是reward，通常用贝尔曼方程计算

    - **Q-Learning、SARSA**

    - 一般要求**Action空间是离散的**，如游戏时的指令

  - **Policy Based**
    - 基于每个State可以采取的Action策略，针对Action策略进行建模，学习出具体State下可以采取的Action对应的概率，然后根据概率来选择Action。
    - **Policy Gradients**
  - **Actor-Critic**
    - 将Value-Based和Policy-Based结合在一起
- **探索&利用**
  - 初期让agent更偏向于探索，遍历尽可能多的action可能性
  - 训练后期，降低探索比例，利用之前训练的结果选择action
  - 这样可以避免遍历可能性太少导致action选择陷入局部最优，比如选择的action带来的转移形成环
- **轨迹**
  - 是一个时间序列集合，通常包含以下元素，$τ=(s_0,a_0,r_0,s_1,a_1,r_1,…,s_T,a_T,r_T)$
    - 状态
    - 动作
    - 奖励
    - 下一状态
    - 是否结束