---
name: vehicle-steady-state-steering
description: |
  当用户处理乘用车/商用车「稳态转向特性」问题时调用：判断一辆车是不足转向还是过多转向、由轴荷与轮胎侧偏刚度算不足转向梯度 K、
  算特征车速/临界车速/质心侧滑角/静态裕度、低速阿克曼角与偏离轮迹、悬架侧倾刚度与侧倾力矩分配、外倾推力与侧向力柔顺转向对 K 的贡献、
  驱动力（前驱/后驱/四驱）对转向方向的影响、用等半径法/等速法实测 K、以及「改哪个零件能把过多转向调回不足转向」。
  输出一律是开环、稳态、英制口径（K 用 deg/g），并强制声明单位口径与模型适用域；不适用于瞬态操控（横摆阻尼/响应时间）、极限工况轮胎非线性、
  主观「操控好坏」评分、ESC 标定、四轮转向与主动悬架控制策略。
  但仍应调用的情形：用户拿 K 去解释主观手感（"跟手/发木"）、或用稳态公式去算瞬态现象（入弯瞬间的甩动）时，**要加载本技能把指标域讲清楚并纠正前提**，
  而不是默不作声地跳过——区分"能算"与"不能算"本身就是本技能的用途。
  Triggers: 不足转向/过多转向/推头/甩尾/understeer/oversteer/understeer gradient/cornering stiffness/特征车速/临界车速/侧倾刚度/侧倾率/外倾/阿克曼/偏离轮迹/等半径法/等速法/稳态回转
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch6-steady-state-steering
  cangjie.capability-count: 32
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 6 章 稳态转向 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 瞬态操控评价（横摆阻尼、响应时间、入弯超调）与主观驾驶感受
- 极限工况轮胎非线性、附着极限、ESC/ESP 标定与介入逻辑
- 四轮转向、主动悬架、扭矩矢量等实时改变分项的系统
- 具体零部件选型/供应商报价/法规认证
- 需要厂商轮胎特性表（a、b 系数）才能完成的 K_lt 与 K_rollsteer 数值计算

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. K = W_fs/C_αf − W_rs/C_αr（deg/g，C_α 为整轴两轮之和）是本章唯一主变量：K>0 不足、=0 中性、<0 过多；判错符号则后续全部方向相反。
2. 任何设计因素都只通过「改变某一轴的等效侧偏角」起作用：前轴侧偏角变大→不足，后轴侧偏角变大→过多（方向层的公共内核）。
3. K 可分项相加（轮胎/载荷转移/外倾/侧倾转向/柔顺转向/回正力矩/驱动力），但本章只对轮胎项、外倾项、柔顺项、回正力矩项给出可算数值；载荷转移项与侧倾转向项的数值层不闭合。
4. 低速转向是纯几何（阿克曼角、偏离轮迹），不需要轮胎数据；高速转向的额外转角需求来自侧偏角，两者不可混用指标域。
5. 稳态、线性（α≤5°）、R≫L、刚性车身是全部公式的入场券；瞬态与极限工况一律出界。
6. 全章英制且无 SI 换算表；单位与口径（单胎/整轴、车轮/转向盘、deg/rad、r 的双单位）错不会自曝，必须先过清单再计算。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 判断一辆车是推头还是甩尾；由轴荷与轮胎侧偏刚度算不足转向梯度 K；校核算出的 K 是否差了两倍（口径错） | references/capabilities/steer-character-k.md | references/capabilities/understeer-gradient-definition.md、references/capabilities/understeer-tuning.md、references/capabilities/characteristic-speed.md |
| 某个改装动作会让车更推头还是更甩尾；手头没有系数但需要一个可靠的方向结论；六项分项符号互相矛盾需要一个仲裁判据 | references/capabilities/axle-rule-direction.md | references/capabilities/understeer-tuning.md、references/capabilities/load-transfer-only-distributed.md、references/capabilities/compliance-steer-k.md |
| 由弹簧刚度与间距算侧倾刚度、侧倾率与轮荷差；前后轴各分到多少侧倾力矩；加了稳定杆侧倾率能降多少 | references/capabilities/roll-chain-kphi-phi-dfz.md | references/capabilities/roll-stiffness-formula.md、references/capabilities/roll-rate.md、references/capabilities/load-transfer-two-mechanisms.md |
| 外倾对不足转向梯度贡献多少 deg/g；外倾梯度与侧倾率怎么接进 K；整体轴要不要算外倾项 | references/capabilities/camber-thrust-k.md | references/capabilities/camber-magnitude-screen.md、references/capabilities/camber-angle-composition.md、references/capabilities/roll-rate.md |
| 换衬套后转向特性会往哪边变；柔顺转向 K_lfcs 贡献多少；横摆中心位置怎么判不足还是过多 | references/capabilities/compliance-steer-k.md | references/capabilities/axle-rule-direction.md、references/capabilities/aligning-torque-k.md |
| 前驱/后驱/四驱加油门时车头往哪偏；扭矩分配怎么影响转向特性；用三项式解释前驱出弯表现 | references/capabilities/drive-force-steering.md | references/capabilities/steer-character-k.md、references/capabilities/understeer-tuning.md |
| 设计并执行一次定圆稳态回转试验；从 δ–a_y 数据读不足转向梯度；判断曲线在大侧向加速度处是否变号 | references/capabilities/constant-radius-test.md | references/capabilities/test-method-choice.md、references/capabilities/sae-k-definition.md、references/capabilities/units-constants-checklist.md |
| 用等速法测不足转向梯度；固定车速打方向的数据怎么算 K；与阿克曼梯度线怎么比 | references/capabilities/constant-speed-test.md | references/capabilities/constant-radius-test.md、references/capabilities/units-constants-checklist.md |
| 把过多转向的车调成不足转向；这套改装方案的方向对不对；除了改弹簧还能动什么 | references/capabilities/understeer-tuning.md | references/capabilities/design-lever-inventory.md、references/capabilities/axle-rule-direction.md、references/capabilities/load-transfer-only-distributed.md |
| 算某半径下的阿克曼角与内外轮转角差；算货车/客车的偏离轮迹（内轮差）；判断停车场刮胎是不是几何问题 | references/capabilities/low-speed-geometry.md | references/capabilities/ackerman-angle.md、references/capabilities/off-tracking.md |
| 侧偏刚度要不要乘 2、每轴两轮还是单胎；算出的 K 是别人的两倍，怀疑口径；只有单胎侧偏刚度，要接进整车公式 | references/capabilities/understeer-gradient-definition.md | references/capabilities/steer-character-k.md、references/capabilities/units-constants-checklist.md |
| 算特征车速；这车多少速度转向最敏感；为什么特征车速很高反而不安全 | references/capabilities/characteristic-speed.md | references/capabilities/critical-speed.md、references/capabilities/static-margin.md |
| 算临界车速并说明含义；过多转向的车开到多快会失控；甩尾是不是车的问题而不是技术问题 | references/capabilities/critical-speed.md | references/capabilities/characteristic-speed.md、references/capabilities/olley-criterion.md |
| 算质心侧滑角 β；判断某工况下车尾会不会外甩；与实车测得的 β 对比 | references/capabilities/cg-sideslip-angle.md | references/capabilities/beta-zero-speed.md、references/capabilities/two-wheel-preconditions.md |
| 什么速度下侧滑角为零；车尾什么时候开始外甩；β=0 车速与转弯半径有关系吗 | references/capabilities/beta-zero-speed.md | references/capabilities/cg-sideslip-angle.md |
| 算静态裕度 e/L；中性转向点在哪里；静态裕度 0.8% 是不是不安全 | references/capabilities/static-margin.md | references/capabilities/steer-character-k.md、references/capabilities/characteristic-speed.md |
| 算某半径下的内外轮转角；阿克曼误差有多大；平行转向有什么问题 | references/capabilities/ackerman-angle.md | references/capabilities/low-speed-geometry.md、references/capabilities/off-tracking.md |
| 算偏离轮迹/内轮差；大车转弯扫过多宽；一次近似能用吗 | references/capabilities/off-tracking.md | references/capabilities/low-speed-geometry.md、references/capabilities/ackerman-angle.md |
| 这个公式/工况适不适用；为什么我的仿真与公式差很多；报告里要写模型适用域与局限 | references/capabilities/two-wheel-preconditions.md | references/capabilities/units-constants-checklist.md、references/capabilities/steer-character-k.md |
| 由弹簧刚度与间距算侧倾刚度；稳定杆刚度怎么叠加；in·lb/rad 与 in·lb/deg 怎么换 | references/capabilities/roll-stiffness-formula.md | references/capabilities/roll-chain-kphi-phi-dfz.md、references/capabilities/roll-rate.md |
| 加稳定杆能减少多少载荷转移；轮荷差怎么拆成两部分；为什么调了悬架轮胎还是偏磨 | references/capabilities/load-transfer-two-mechanisms.md | references/capabilities/load-transfer-only-distributed.md、references/capabilities/roll-chain-kphi-phi-dfz.md |
| 每 g 侧倾几度；侧倾率算出负的怎么办；10.5 deg/g 正常吗 | references/capabilities/roll-rate.md | references/capabilities/roll-stiffness-formula.md、references/capabilities/camber-thrust-k.md |
| 防倾杆装前轴还是后轴；只加后稳定杆行不行；为什么原厂前防倾杆更粗 | references/capabilities/roll-moment-front-bias.md | references/capabilities/roll-chain-kphi-phi-dfz.md、references/capabilities/understeer-tuning.md |
| 地面外倾角怎么算；外倾等效多少侧偏角；两个外倾角要不要相加 | references/capabilities/camber-angle-composition.md | references/capabilities/camber-thrust-k.md、references/capabilities/camber-magnitude-screen.md |
| 这辆车要不要算外倾项；外倾对 K 影响大不大；改外倾能治推头吗 | references/capabilities/camber-magnitude-screen.md | references/capabilities/camber-thrust-k.md、references/capabilities/camber-angle-composition.md |
| 回正力矩对 K 有多大影响；能不能靠主销后倾把车调向过多；K_at 恒正是好事吗 | references/capabilities/aligning-torque-k.md | references/capabilities/compliance-steer-k.md、references/capabilities/understeer-tuning.md |
| 我的 K 和厂家差 10% 正常吗；hand-wheel 还是 road-wheel；转向盘转角除以传动比对不对 | references/capabilities/sae-k-definition.md | references/capabilities/constant-radius-test.md、references/capabilities/units-constants-checklist.md |
| 用哪种方法测 K；等半径还是等速；只有油门和方向盘可控能测吗 | references/capabilities/test-method-choice.md | references/capabilities/constant-radius-test.md、references/capabilities/constant-speed-test.md |
| 这些公式用英制还是 SI、怎么换算；为什么算出负的侧倾率/异常半径；结果数量级不对，先查什么 | references/capabilities/units-constants-checklist.md | references/capabilities/two-wheel-preconditions.md、references/capabilities/understeer-gradient-definition.md |
| 不用公式怎么判推头还是甩尾；侧风/路面凸起后车头往哪偏说明什么；为什么甩尾会越来越严重 | references/capabilities/olley-criterion.md | references/capabilities/steer-character-k.md、references/capabilities/critical-speed.md |
| 这车推头，除了改弹簧还能动什么；改装方案有没有漏掉某条通道；调校从哪儿入手 | references/capabilities/design-lever-inventory.md | references/capabilities/understeer-tuning.md、references/capabilities/axle-rule-direction.md |
| 能不能消除横向载荷转移；调前后侧倾刚度比会让车往哪边变；为什么加硬弹簧没用 | references/capabilities/load-transfer-only-distributed.md | references/capabilities/load-transfer-two-mechanisms.md、references/capabilities/roll-moment-front-bias.md |

**非能力类查询**：
- 书名/作者/章节/整书概览 → references/overview.md
- 术语解释 → references/glossary.md
- 决策规则速查（不需要原文依据时） → references/cheatsheet.md
- 完整意图与关键词索引（本表未覆盖的意图先查这里） → references/capability-index.md

## 加载规则

- 每次任务先读本文件，再按路由表加载 **1** 张能力卡；任务明确跨域时最多加载 2 张。
- 概览/书名类问题不加载能力卡，用「核心原则」与 overview.md 回答。
- 路由表与 capability-index.md 都无法命中的意图，明确告知超出本书范围，不要硬套。

## 边界与判停

- 缺少 C_α、轴荷、轴距中的任一项且用户无法补充时，停止计算，只给方法与所需数据清单。
- 工况为瞬态、极限（α>5°）、多轴/铰接或四轮转向时，停止套用本章公式，声明出界。
- 涉及后轴导向臂角度对不足/过多转向的方向判断时，停止给方向，标注「原文自相矛盾（p179 正文 vs p188 例题），需实车/台架标定」。
- 用户要求「算出整车 K 总和」时，停止并说明 6.5 表的转向系统行无公式、b/A/p/ε 无来源值，数值层缺一块。
