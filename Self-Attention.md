# Self-Attention

- 输入输出向量等长时由给定的$a$计算$b$
  - 计算输入向量元素之间的关联性$\alpha$
  - $QueryKey-Value，QKV$
    - $q^i = a^i * W^q$
    - $k^i = a^i * W^k$
    - $\alpha_{ij}=q^i \cdot k^j$（表示i和j向量之间的关联性）
    - 再对$\alpha$进行激活，如使用softmax，$\alpha'_{1,i}=exp(\alpha_{1, i})/\sum\limits_jexp(\alpha_{1,j})$
  - $v^i=a^i * W^v$
  - $b^1=\sum\limits_i \alpha'_{1, i}v^i$，$\alpha'_{1, i}$越大越接近$v^i$
  - ![image-20240715130335315](C:\Users\Fighoh\Pictures\image-20240715130335315.png)
  - 位置编码，给输入加上位置信息，每一个位置有一个不同的$e^i$，每一个位置的输入从$a^i$变成$a^i+e^i$

- **多头自注意力机制**就是对于每一个$a^i$有多个$q^i, k^i, v^i$，代表多种不同的相关性，也会产生多个$b^i$，最后在用矩阵做一次变换得到单个$b^i$
- **截断自注意力机制**是用于处理序列过长时，如语音序列，只需看小范围就能够判断，从而缩短输入序列
