## 合约交互架构

与 BSC 上的 `KaleidoStaking` 合约交互：

1. **主动读取**：`useReadContract` / `useReadContracts` 批量查询用户数据、订单信息、系统参数
2. **批量聚合**：`useSystemAggregation` 从最新 N 笔订单中提取唯一用户、计算等级分布、持仓/KLD TOP 排行
3. **组织结构树**：采样用户 `referrer` 字段构建反向关系 Map，未采样节点展开时通过 `publicClient.readContract(getDirectReferrals)` 实时拉取
4. **写入操作**：通过 `useWriteContract` 实现代币转账、订单结算等功能

### 链上数据流

```
BSC Node ← (RPC) → wagmi Client → React Query Cache → React 组件
                           ↘ Contract ABI (config.js)
```

## 合约地址

- **KaleidoStaking**: `0x10506414EfAe908A50e2B48637B169Af1309549e`
- **KLD Token**: `0x10506414EfAe908A50e2B48637B169Af1309549e`（同一合约）
- **USDT**: `0x55d398326f99059fF775485246999027B3197955`
- **KLD/USDT 池**: `0x2F6BAb5928c5899C670d2849870181301B2B70eB`
- **Owner**: `0x5B5B64D7747755DAAA03287431B5F27631A92DA0`
