---
title: Business Scenarios Overview
author: "Misty"
tags: ["Note","Job"]
categories: ["Data Analysis"]
date: 2021-04-25
---

## 热门行业+业务场景

* 零售行业
    * 会员打标
        * 用户标签、MECE原则
    * A/B测试
        * AB实验、核心业务指标的制定
    * 流失预警
        * RFM模型、防流失模型、GB/NBG模型
    * 偏好分析
        * 用户画像、标签任务自动化
    * 聚类分析
        * 聚类算法、无监督学习、Scaling
    * 数据推演
        * 数据推演、case when函数
* 跨境电商行业
    * 选品分析
        * 主观赋权法、CRITIC客观赋权法
    * 报表制作
        * 漏斗模型、人货场模型、指标搭建
    * 盈亏分析
        * 费米分解法、蒙特卡洛模型
    * 策略复盘
        * 贝叶斯公式、Possion分布、参数估计
    * 竞品分析
        * RFM模型、DBSCAN聚类分析
    * 广告策略
        * 细分分析、AARRR、敏感性分析
* 电商行业
    * 薪资预测
        * 线性回归模型
    * 用户行为
        * AARRR模型、漏斗分析
    * 用户价值
        * RFM模型、用户分析
    * 用户画像
        * 标签体系建立、用户生命周期开发
    * 销售预测
        * ARIMA模型、智能补货流程搭建
    * 协同过滤
        * 用户相似度、智能推荐

## 数据分析流程

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429002938.png)


## 用户流失模型

应用数据挖掘技术可以根据过去拥有的客户流失数据建立客户属性、服务属性和客户消费数据与客户流失可能性关联的数学模型，找出客户属性、服务属性和客户消费数据与流失的关系，给出明确的数学公式或规则，从而计算出客户流失的可能性。


### 业务沟通

* 怎样才算流失？
* 流失的原因有哪些？
* 流失前有什么表现？
* 流失客户中有哪些值得挽回？
* 目前对流失客户采取的策略和手段有哪些？谁执行？效果如何？

### 预测流失

* 确定客户流失模型的目标
* 获取用于建模的数据
* 对数据进行清洗，转换成建模数据集
* 建立模型
* 模型评估
    * 命中率=实际流失人数/每个箱的人数
        * 即实际流失率，表示对选取一定数量的客户假设不进行任何挽留时实际流失人数占总数的比例，体现了模型判断的正确性；
    * 提升率=实际流失率/总体平均流失率
        * 即使用模型捕获的流失人数与不使用模型捕获的流失人数的比例，体现了对所选取的客户使用模型进行挽留与不使用模型进行挽留的提升效果；
    * 覆盖率=实际流失人数/总体实际流失人数
        * 表示在进行挽留时，能“召回”的流失客户占全部流失的比例。
* 模型预测结果用于支持决策

## RFM模型

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429004007.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429004028.png)

## 用户画像

### 用户画像基础
#### 用户生命周期

* 获取、激活、留存、变现、推荐
* 认知、接触、使用、首单、复购、习惯、分享和流失
* 用户关键路径、用户旅程、用户决策过程

#### 用户画像的定义

* 刻画用户需求的模型
* 用户画像是一种公共语言，串联互联网商业

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429004908.png)

#### 用户画像的模型

* 目标：刻画用户需求
* 要素：人、物、环境
* 关系：人与人（社交）、人与物（电商）、人与环境、人与物与环境（o2o）
    * 人：自然属性、社会属性
    * 物：文本、图片、音频、视频、商品
    * 环境：时间、地点、场景

#### 用户画像的意义

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429005159.png)

### 用户画像的原理

#### 用户画像的方法

* 用户标签化
    * 标签的定义：用户属性、兴趣、行为等特征的抽象与描述
    * 标签的关系：层次关系、序列关系、集合关系、独立关系
    * 标签的分类：人工标签、机器标签、属性标签、兴趣标签、行为标签、分层标签、分群标签、个性化标签
* 分层-》分群-》个性化

#### 分层标签

* 业务分层
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429005639.png)

* 流量漏斗（AARRR）
![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429005518.png)

#### 分群标签

* RFM用户分群模型

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429005606.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429005741.png)

* 用户属性分群

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429005838.png)

#### 个性化标签

* 全面、完整、细致地标签化用户个性化特征。
* 通常把用户的个性化标签近似称为用户画像。
* 个性化标签生成主要三种方式：人工打标签、机器打标签、混合打标签（人工+机器）。
    * 人工打标签：自然属性、社会属性、关系属性
    * 机器打标签
    * ![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429010023.png)
    * 混合打标签
    * ![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429010159.png)


#### 用户画像的原则

* 有效性
* 真实性
* 独立性
* 全面性
* 统一性（用户标签与物品标签要统一，双向匹配）

#### 用户画像的检验

* 业务评估标准
    * 抽样检验、业务反馈、AB测试（点击率、时长）
* 离线评估指标
    * Top N的预估画像真是点击数/N
* 线上评估指标
    * 画像有点数=用户点击画像个数
    * 画像有点率=用户点击的画像个数/用户曝光的画像个数

### 应用

#### 例子

* 共同：自然属性、社会属性
* 不同：百度突出垂直领域、微博突出用户关系、今日头条突出用户喜好

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429010503.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429010512.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429010528.png)

#### 推荐系统

* 召回阶段：用户画像用于物品过滤
* 排序阶段：用户画像用于物品排序


## 人货场模型

* 传统零售的人货场——管理

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429011109.png)

* 传统零售客单价下降的人货场——剖析

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429011134.png)

* 电商的人货场
    * 电商的人货场分析模型与传统零售相似，在“场”的角度略有差异，电商的场指的是APP、小程序、官网等线上渠道，不是指线下实体店、卖场。用户端看到的商品划分都是通过品类划分，点击后具体到一个SKU。另一点不同的是加入了物流维度，需要快递公司将商品从货仓运输到用户数手中。

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429011259.png)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429011326.png)



## 电商模式决定关注指标

[数据指标](https://zhuanlan.zhihu.com/p/186295427)

![](https://raw.githubusercontent.com/M1styDay/image_hosting/master/hugo_images/20210429011459.png)


## 漏斗分析

* 四要素
    * 时间、节点、研究对象、指标
* 三特点
    * “四分”反映结构：所谓“四分”是指流程分步骤，时间分先后，结果分层级，用户有分流。漏斗分析中的节点将流程分解为多个步骤，各个步骤有先后顺序和时间间隔，经过中间步骤的筛选得到的结果形成自然的分层，每次中间步骤的过滤是对用户的分流。
    * 指标描述漏斗：漏斗的形成过程会自然的生产出数据，指标是从数据的角度对漏斗模型的描摹，用指标可以全面解读漏斗模型。这些指标可分为用户类指标、时长类指标和比率类指标等。
    * 过程影响结果：漏斗的作用过程是环环相扣的，前面的步骤会影响后续的步骤，上个步骤的结果会影响下个步骤的表现，过程的不断累积会影响到最终的结果。
* 三步骤
    * 第一步：梳理关键节点，绘制流程与路径。根据业务场景的设定规则或节点的定义，绘制事件的流程；比如：电商购物、APP获客等场景下都有一些通用的流程与路径描述模板，借助这些模板可以快速定义关键节点、绘制出漏斗的大致轮廓。
    * 第二步：收集对各环节的痕迹数据，进行数据分析。针对整个漏斗形成过程首先要进行指标的定义和数据的收集。指标的定义不外乎从行为、时间、比率等角度入手，指标对应数据的获取可以通过爬虫、埋点等方式。收集到相应数据后就可以开始进行数据分析了。基于数据分析，用EXCEL等工具绘制出漏斗图，标上相应的指标数据。
    * 第三步：确定需要优化的节点。通过在关键指标上与同类用户的平均水平、行业平均水平等进行比较，分析差距、找到自身的薄弱环节；通过与自身历史同期水平进行比较，确定某一流程中需要优化的节点，采取措施进行针对性整改。
* 六场景
    * 漏斗分析法在电商购物、APP获客与增长、用户消费决策分析等领域有着广泛的应用，漏斗分析模型常用于6个方面的应用场景：电商购物漏斗分析模型、AARRR模型、AIDMA模型、AISAS模型、营销广告投放漏斗模型、招聘漏斗模型。

