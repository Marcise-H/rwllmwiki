# 05｜Python 隨機漫步模擬

## 模擬概念
每一期抽取一個隨機步長，再將步長累加到前一期位置，即可形成一條隨機漫步路徑。

```python
import numpy as np
import matplotlib.pyplot as plt

rng = np.random.default_rng(42)
n = 200
steps = rng.choice([-1, 1], size=n)
walk = np.r_[0, np.cumsum(steps)]

plt.figure(figsize=(9, 4))
plt.plot(walk)
plt.axhline(0, linestyle="--", alpha=0.5)
plt.xlabel("Time")
plt.ylabel("Position")
plt.title("A Simple Random Walk")
plt.show()
```

## 觀察問題
1. 每次重新抽樣，路徑是否相同？
2. 路徑是否可能連續向上或向下？
3. 為什麼路徑看起來有趨勢，不代表下一步可被確定預測？

## 來源與界線
此程式是教學示範，使用對稱的 ±1 步長；它不是對任何特定股票的估計模型。隨機數產生器的實際使用方式可參考 NumPy 文件（請另增 NumPy 官方文件作為來源，若課程要求來源至少五篇，建議將它列為 S6）。
