# Olist 巴西电商经营分析报告

> 基于 Olist Brazilian E-Commerce Public Dataset 的端到端数据分析
> 覆盖 GMV 趋势、用户分层、物流履约、RFM 模型等十大主题

---

## 📌 项目概览

| 项目 | 说明 |
|---|---|
| **数据集** | [Olist Brazilian E-Commerce Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)（Kaggle） |
| **数据周期** | 2017-01 ～ 2018-08 |
| **订单规模** | ~10 万笔有效订单，~9.8 万独立买家 |
| **总 GMV** | ~1600 万 BRL（巴西雷亚尔） |
| **分析工具** | Python 3 · DuckDB（内存数据库） · SQL · Matplotlib |
| **[飞书版电商用户行为分析报告](https://my.feishu.cn/wiki/TBq0wpg7Aiqpx2kK36YcbRvSnLd)**|
| **作者** | Cristina Yan |

---

## 📊 分析结构（10 个章节）

| 章节 | 分析主题 | 核心问题 |
|:---:|---|---|
| 一 | 平台核心 KPI 概览 | 业务规模与健康度如何？ |
| 二 | 月度 GMV 与订单趋势 | 增长拐点在哪里？ |
| 三 | 订单状态漏斗 | 各状态分布与流转情况？ |
| 四 | 商品品类销售分析 | 哪些品类贡献最多？ |
| 五 | 地理分布分析 | GMV 地域集中度如何？ |
| 六 | 物流履约深度分析 | 配送时效与运费合理性？ |
| 七 | 评价与满意度分析 | 配送对评分影响几何？ |
| 八 | 留存群组分析 | 新客复购率为何偏低？ |
| 九 | RFM 用户分层 | 如何识别高价值客户？ |
| 十 | 策略建议与结论 | 优化方向与落地优先级？ |

---

## 🗂️ 文件结构

```
.
├── olist_analysis_report.ipynb    # 完整分析报告（Jupyter Notebook，含代码+图表）
├── 01_kpi_overview.png            # 第一章：核心 KPI 图表
├── 02_monthly_trend.png           # 第二章：月度 GMV 趋势
├── 03_order_status.png            # 第三章：订单状态漏斗
├── 04_category_analysis.png       # 第四章：品类销售分析
├── 05_geo_distribution.png        # 第五章：地理分布
├── 06_delivery_analysis.png       # 第六章：物流履约分析
├── 07_review_analysis.png         # 第七章：评价与满意度
├── 08_cohort_retention.png        # 第八章：留存群组分析
└── README.md                      # 本文件
```

---

## 🚀 如何运行

### 1. 下载数据集

从 Kaggle 下载原始 CSV 文件，放到本地任意目录，推荐路径结构：

```
olist_data/
├── olist_orders_dataset.csv
├── olist_order_items_dataset.csv
├── olist_order_payments_dataset.csv
├── olist_order_reviews_dataset.csv
├── olist_products_dataset.csv
├── olist_customers_dataset.csv
├── olist_sellers_dataset.csv
└── product_category_name_translation.csv
```

> Kaggle 页面：https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

### 2. 修改数据路径

在 `olist_analysis_report.ipynb` 的第一个代码格中，修改 `DATA_PATH` 变量：

```python
DATA_PATH = '/你的路径/olist_data'
```

### 3. 安装依赖

```bash
pip install pandas numpy duckdb matplotlib
```

推荐使用 conda 或 venv 创建独立环境。

### 4. 运行

```bash
jupyter notebook olist_analysis_report.ipynb
```

按顺序执行所有单元格，或使用 `Kernel → Restart & Run All`。

---

## 🔍 核心发现摘要

### 规模与质量
- **GMV**：~1600 万 BRL，AOV ~161 BRL，数据周期 20 个月
- **履约**：92% 准时送达率，平均评分 4.1/5，好评率 91%

### 三大瓶颈
1. **复购率极低**：新客首月复购率仅 3-5%，是行业均值的 1/3，是最关键的 GMV 增长杠杆
2. **物流区域失衡**：SP 省以外运费高、时效长，RR/AM 等偏远省份履约率不足 89%
3. **高价值用户集中**：18% 的重要价值用户贡献 50%+ GMV，单一依赖风险大

### 最大机会点
- 首月复购率从 5% 提升至 10%，预估年新增 GMV **150-250 万 BRL**
- 长分期用户 LTV 是全站均值 **3.3 倍**，是高客单价品类天然优势群体
- 礼品与美妆品类抗周期韧性最强，适合作为留存锚点品类

### RFM 用户分层结论（仅用 R×F，M 仅作描述统计）
- **重要价值用户**：忠诚核心，GMV 占比最高，是平台利润主要来源
- **重要发展用户**：新客，近期活跃，极具转化潜力，是复购提升的主要目标群体
- **重要挽留用户**：曾多次购买但已沉默，物流问题是核心流失驱动因素
- **一般保持用户**：低频低价或已流失，占用户主体但贡献有限

---

## 📋 分析方法说明

- **GMV 口径**：使用 `payment_value`（实际支付金额），而非商品标价
- **有效订单**：排除 `canceled` 状态
- **配送时长**：`order_delivered_customer_date - order_purchase_timestamp`
- **RFM 分层**：R/F 各 1-5 分（分位法），M 仅作描述性统计，不参与分层判定
- **留存群组**：按首购月份分组，追踪各群组后续月份的留存率

---

## 📝 License

数据集来源：[Olist / Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)，遵循 Olist 开放数据协议。
