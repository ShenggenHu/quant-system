# 量化交易系统完整手册

## 目录
1. [核心策略体系](#核心策略体系)  
2. [Python实现方案](#python实现方案)  
3. [阿里云部署指南](#阿里云部署指南)  
4. [维护更新方案](#维护更新方案)  
5. [收益计算模型](#收益计算模型)  
6. [风险提示](#风险提示)

---

## 核心策略体系
### 集合竞价策略
```python
# 竞价信号检测函数
def check_auction_signal(df):
    # 计算最后5分钟价格变化
    last_5min = df['price'][-5:].pct_change().sum()
    # 量比指标
    vol_ratio = df['volume'][-1] / df['volume'].mean()
    return last_5min > 0.03 and vol_ratio > 2
