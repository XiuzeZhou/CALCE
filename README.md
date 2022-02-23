# 马里兰大学锂电池数据集 CALCE，基于 Python 的锂电池寿命预测（Remaining Useful Life，RUL）& （End Of Life，EOL）

**主要库版本：** 

- pytorch 1.6.0

- pandas 0.24.2

**相关论文：** 

- D. Chen, W. Hong, and X. Zhou, "Transformer Network for Remaining Useful Life Prediction of Lithium-Ion Batteries", IEEE Access, 2022.

欢迎引用！

**版本更新** 

- 2022年2月，解决错误“Tensor for argument #2 ‘mat1’ is on CPU, but expected it to be on GPU (while checking arguments for addmm)”

- 2021年12月 添加数据读取模块

    如果原始数据集无法成功读取，可以直接选择加载我已经提取出来的数据：NASA.npy

    Battery = np.load('NASA.npy', allow_pickle=True)

    Battery = Battery.item()

**Homepage:** http://zhouxiuze.com

**个人博客：** http://snailwish.com/

**更多内容**

1. 马里兰大学锂电池数据集 CALCE，基于 Python 的锂电池寿命预测: https://snailwish.com/437/

2. NASA 锂电池数据集，基于 Python 的锂电池寿命预测: https://snailwish.com/395/

3. NASA 锂电池数据集，基于 python 的 MLP 锂电池寿命预测: https://snailwish.com/427/

4. NASA 和 CALCE 锂电池数据集，基于 Pytorch 的 RNN、LSTM、GRU 寿命预测: https://snailwish.com/497/

