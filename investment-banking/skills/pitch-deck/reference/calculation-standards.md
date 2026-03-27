# 计算校验参考

本文件提供公式和指引，用于在填充模板前校验源数据中已经预先计算好的数值。源数据通常应已包含计算结果，这里的公式用于验证准确性。

## 目录

- [关键校验公式](#关键校验公式)
- [Consensus 方法](#consensus-方法)
- [舍入指引](#舍入指引)
- [校验清单](#校验清单)
- [需要调查的红旗信号](#需要调查的红旗信号)

---

## 关键校验公式

### CAGR Projection

**Formula:**
```
Future Value = Present Value × (1 + CAGR)^n
```

**Variables:**
- Present Value: 当前 / 基准年的市场规模
- CAGR: 复合年增长率，按小数表示，例如 16.4% = 0.164
- n: 基准年与目标年之间的年数

**Verification example:**
```
Source claims: $22.1bn (2024) at 16.4% CAGR = $55.0bn (2030)

Verify: 22.1 × (1.164)^6 = 22.1 × 2.488 = 55.0 ✓
```

**Calculating n (years):** 计算基准年与目标年之间的年数。例如 2024→2030 = 6 年，2025→2030 = 5 年。

### Valuation Multiples

**EV/Revenue:**
```
EV/Revenue Multiple = Enterprise Value ÷ Revenue
Implied EV = Revenue × Multiple
```

**EV/EBITDA:**
```
EV/EBITDA Multiple = Enterprise Value ÷ EBITDA
Implied EV = EBITDA × Multiple
```

**Verification example:**
```
Source claims: $436m deal at 9.7x revenue multiple on $45m revenue

Verify: 436 ÷ 45 = 9.69 ≈ 9.7x ✓
```

### Market Share

**Formula:**
```
Market Share = (Segment Size ÷ Total Market Size) × 100
```

**Verification example:**
```
Source claims: Online segment ($18bn) is 28% of total market ($65bn)

Verify: 18 ÷ 65 = 0.277 = 27.7% ≈ 28% ✓
```

### Growth Rate

**Year-over-Year:**
```
YoY Growth = (Current Year - Prior Year) ÷ Prior Year × 100
```

**CAGR from endpoints:**
```
CAGR = (End Value ÷ Start Value)^(1/n) - 1
```

---

## Consensus 方法

当源数据包含多个估计值时，要验证 consensus 计算逻辑：

### Size Consensus (Range)

**Method:** 对所有来源取完整的最小值到最大值区间

**Example:**
```
Sources: $14.9bn, $18.3bn, $21.1bn, $21.2bn, $22.1bn
Consensus: $15-22bn (rounded to nearest $1bn)
```

### CAGR Consensus (Central Cluster)

**Method:** 剔除最高和最低值，取中间聚类区间

**Example:**
```
Sources: 10.6%, 16.4%, 17.2%, 19.0%, 22.7%
Exclude outliers: 10.6% (low), 22.7% (high)
Central cluster: 16.4%, 17.2%, 19.0%
Consensus: 16-19% or 16-17% (conservative)
```

### Projection Consensus

**Method:** 对市场规模区间中点应用 consensus CAGR

**Example:**
```
Size range: $15-22bn → Midpoint: $18.5bn
CAGR consensus: 16-17%
At 16%: 18.5 × (1.16)^6 = $45.1bn
At 17%: 18.5 × (1.17)^6 = $47.5bn
Consensus projection: $45-48bn
```

---

## 舍入指引

以下是**常见惯例**，应根据数值量级和模板风格调整：

| Value Type | Typical Rounding | Example |
|------------|------------------|---------|
| Large market sizes ($10bn+) | 取整到最近 $1bn | 18.47 → $18bn |
| Smaller market sizes (<$10bn) | 取整到最近 $0.5bn 或 $0.1bn | 2.3 → $2.5bn |
| Size ranges | 匹配源数据精度 | 14.9-22.1 → $15-22bn |
| CAGR | 整数 % 或 0.5% | 16.4% → 16% 或 16.5% |
| Market share | 取整到最近 5% 或与源数据一致 | 27.7% → 25% 或 30% |
| Revenue ($m) | 保留 1 位小数 | 18.47 → $18.5m |
| Multiples | 保留 1 位小数 | 9.688 → 9.7x |

**Rounding principles:**
- 舍入不能实质改变数值含义，数值越小，越应保留更细精度
- 一致性比极致精度更重要，相似数据应采用同样的舍入方式
- 做区间时，低值向下取整，高值向上取整
- 对均值、中位数等摘要统计，精度应与输入数据保持一致

---

## 校验清单

使用源数据中的任何计算值前，请先检查：

### Formula Verification
- [ ] Projection 使用了正确的 CAGR 公式：`PV × (1 + r)^n`
- [ ] Multiple 按 `EV ÷ Metric` 计算，没有反过来
- [ ] 增长率分母使用了正确的基准年
- [ ] 适用时，各项份额加总约等于 100%

### Input Verification
- [ ] 基准年数据与源文件一致
- [ ] CAGR / 增长率与源文件声明的方法一致
- [ ] 时间跨度 `n` 计算正确
- [ ] 货币和单位一致，$bn 与 $m 没有混淆

### Output Verification
- [ ] 计算结果与源文件给出的结果一致
- [ ] 如果不一致，已调查方法差异
- [ ] 舍入方式前后一致
- [ ] 结果在量级上合理，没有数量级错误

### Consensus Verification
- [ ] 区间计算已纳入所有来源
- [ ] 剔除 outlier 的方法已记录
- [ ] 中点计算使用了正确的平均方法
- [ ] 区间上下限确实对应最小 / 最大值，或是已说明的子集

---

## 需要调查的红旗信号

**Projection mismatches:**
- 你的 projection 与源文件差异超过 5%
- 常见原因：基准年不同、CAGR 不同、舍入不同

**Multiple mismatches:**
- 你算出的 multiple 与源文件不一致
- 常见原因：口径不同，LTM vs. NTM，Revenue vs. Net Revenue

**Consensus mismatches:**
- 你的 consensus 与源文件的 consensus 不同
- 常见原因：源文件排除了部分数据点，或 outlier 处理方式不同

**When in doubt:** 在脚注中记录差异，并展示你的计算方法。
