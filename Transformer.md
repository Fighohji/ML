## Transformer

### 结构

- 输入
- 编码器
  - 分成多个块
  - 每个块输入一排向量做自注意力，输出向量在全连接网络计算输出一排向量作为块的输出
  - 引入了残差连接（residual connection），就是每次输出的结果加上输入向量，并做**层归一化*
  - 层归一化：在每一个样本的特征维度上进行归一化
  - 批量归一化：在每一批数据的每个维度上进行归一化
  - <img src="C:\Users\Fighoh\Pictures\image-20240716210148749.png" alt="image-20240716210148749" style="zoom:50%;" />
- 解码器
  - 自回归（autoregressive）解码器
    - 先输入\<BOS\> ，输出w1，再把w1当做输入，再输出w2，直到输出\<EOS\>为止
    - 使用掩蔽自注意力（masked self-attention），通过一个掩码（mask）来阻止每个位置选择其后面的输入信息，保证产生当前输出时只考虑到目前为止的输入信息
  - 非自回归（non-autoregressive）解码器
    - 一次生产整个句子，输出长度未知
    - 确定长度可以使用分类器（用编码器的输入）或者限定最大长度
    - 优点
      - 平行化
      - 能够控制输出的长度
- 编码器-解码器注意力
  - <img src="C:\Users\Fighoh\Pictures\image-20240717203944195.png" alt="image-20240717203944195" style="zoom:50%;" />

- 输出

### 训练

- 教师强制（teacher forcing）：输入的时候给定正确答案
- 复制机制：从输入中复制一些东西
- 引导注意力：给注意力的顺序一个固定的顺序，如语音识别从左到右
- 束搜索：往往用于答案比较固定的时候，答案比较比较创造力时会表现比较差
- 加入噪声：有点像图像处理时的数据增强，但不一样，这里是加入一些错误的输入，比如语音识别时在测试集加入一些有点小错误的答案



### Conformer

- 多头注意力模块

  - transformer中的位置编码
  - 残差单元
  - <img src="C:\Users\Fighoh\Pictures\image-20240721171347003.png" alt="image-20240721171347003" style="zoom: 50%;" />

- 卷积模块

  - a pointwise convolution and a gated linear unit (GLU)
  - 1-D depthwise convolution layer
  -  Batchnorm

- 前向传播模块

  - Swish activation
  - <img src="C:\Users\Fighoh\Pictures\image-20240721172613907.png" alt="image-20240721172613907" style="zoom: 50%;" />

- conformer块

- ```python
  self.conformer_block = ConformerBlock(
      dim=d_model, ## 输入和输出的特征维度。这通常是嵌入向量的维度。
      dim_head=256, ## 每个注意力头的特征维度。多头自注意力机制中，每个头将处理特征维度为 dim_head 的输入。
      heads=1, ## 注意力头的数量
      ff_mult=4, ## 前馈神经网络的扩展倍数
      conv_expansion_factor=18, ## 卷积模块中扩展因子,就是通道扩展
      conv_kernel_size=41, ## 卷积层的核大小
      attn_dropout=dropout, ## 自注意力模块中的 dropout 比例
      ff_dropout=dropout, ## 前馈神经网络中的 dropout 比例
      conv_dropout=dropout ## 卷积模块中的 dropout 比例
  )
  ```

