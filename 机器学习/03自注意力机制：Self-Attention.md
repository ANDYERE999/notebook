前提条件：输入n个向量（可以来自于hidden layer），输出n个向量
![[Pasted image 20251004183257.png]]
$$\alpha_{1,1}=\alpha^1\times q^1\times k^1(矩阵乘法)$$
$$\alpha'_{1,1}=Softmax(\alpha'_{1,1},\alpha'_{1,i})其中i\in\{1,2,3,4\}$$
$$b^1=\Sigma\alpha'_{1,i}v^1$$
$$b^1是最终的输出$$
$$Self-attention需要找出W^q、W^k、W^v三个最佳的矩阵$$![[Pasted image 20251004182938.png]]
$$e^i是位置编码$$
常用的位置编码：
![[Pasted image 20251004184529.png]]

# 多头自注意力机制：
$$W^q、W^k、W^v各n个(n\ge 2)$$
# Self-Attention、CNN、RNN
- CNN是一种特殊的Self-Attention
- RNN逐渐被Self-Attention取代，因为其不能并行计算，不能跨越巨大的文本长度
# 演变
![[Pasted image 20251004185820.png]]
# Glossary
Softmax:
$$Softmax(v_i)=\frac{e^{v_i}}{\Sigma_{j=1}^K{e^{v_i}}}其中v_i是向量V中的其中一个值$$
对于上述提到的Softmax,换成ReLU有时候效果更好
Softmax可以进行normalize，并且让大值更大、小值更小
# Reference
更高效的Transformer:**Efficient Transformers: A survey" https://arxiv.org/abs/2009.06732

