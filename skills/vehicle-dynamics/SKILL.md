---
name: vehicle-dynamics
description: |
  当用户处理汽车「加速性能 / 制动性能 / 道路负载 / 乘适性 / 操纵稳定性 / 悬架几何 / 转向系统 / 侧翻安全 / 轮胎」问题时调用。**覆盖十章（全书）：**
  （第 1 章 基础）动态车轴载荷（静/加速/坡道三种工况）、由轴荷反求重心位置、轴荷之和的排障、附着力限制的爬坡能力（含拖挂）、
  SAE 坐标系与符号规则、建模自由度选择、自由体受力图；
  （第 2 章 加速）判断加速受功率限制还是附着限制、由发动机扭矩曲线算各挡驱动力、有效转动惯量与等效质量（质量系数）、
  驱动力图与最佳换挡点、液力变矩器的起步放大、传动比等比级数与万有特性匹配、
  附着力限制下的最大驱动力（区分差速器锁止/不锁止、前驱/后驱、整体轴/独立悬架）、驱动扭矩引起的横向载荷转移；
  （第 3 章 制动）制动距离与停车时间、制动能量与功率、减速时的动态载荷转移、前后轴最大制动力边界线、同时抱死点、效能三角形、制动力配比与压力比例阀、
  制动效率与制动系数、抱死顺序（前轮失转向 / 后轮失稳定）、FMVSS 105/121 符合性、ABS 为什么有用、踏板力增益；
  （第 4 章 道路负载）空气密度与标准大气、空气阻力与所需功率、顺风/逆风的不对称、阻力来源分解与改进定位、尾部倾角与分离、
  升力与侧向力、俯仰/横摆/侧倾力矩、横风敏感度（压力中心与中性转向点的距离）、滚动阻力的七个来源与四套经验式、
  滚阻的状态修正（温度/胎压/速度/磨损/侧偏/路面）、总道路负载与道路负载功率、油耗归因；
  （第 5 章 乘适性）振动频率窗与共振判定、路面不平度谱与轮辙拆分、四分之一车辆增益与谱相乘、
  乘适刚度与跳动频率、行程预算与阻尼上限、减振器阀片与迟滞、主动悬架的**成对**收益（−30%/−10%）、
  车轮 hop 与簧下质量、车上激振源阶次定位、轴距滤波零点、双模态与两个运动中心、Olley 准则与动态指数、人体判据的正确用法（不能当 KPI）；
  （第 6 章 稳态转向）不足转向梯度 K、特征车速/临界车速、质心侧滑角、静态裕度、低速阿克曼角与偏离轮迹、侧倾刚度与力矩分配、
  外倾推力与柔顺转向对 K 的贡献、驱动力对转向方向的影响、等半径法/等速法实测 K、改哪个零件能把过多转向调回不足转向；
  （第 7 章 悬架）整体式车轴 vs 独立悬架选型、叶片弹簧/四连杆/第迪安/拖曳臂/SLA/麦弗逊/多连杆/半拖曳臂/摆动轴结构对比、
  等效拖曳臂分析、抗后蹲/抗前仰/抗点头的 e/d 几何判据、俯仰角变化率、侧倾中心求法、举升(jacking)风险、主动与半主动悬架分级；
  （第 8 章 转向系统）转向传动比与车轮转角换算（设计 vs 实测）、阿克曼几何与低速自定心力矩、转向几何误差（前束变化/侧倾转向）的方向判定、
  主销内倾与后倾产生的回正力矩、转向柔顺性带来的不足转向增量与"转向盘口径 vs 车轮口径"换算、
  制动时后倾角的作用翻转与对开路面跑偏、前驱五机制（四不足一过多）、四轮转向的转弯半径与低速/高速相位。
  （第 9 章 侧翻）刚体准静态侧翻门槛 t/2h、超高与中性车速、悬挂车辆的实际门槛修正、先滑还是先翻的分诊、
  阶跃与正弦哪种更危险、瞬态门槛的阻尼修正、前后轴相位差与四轮转向、挂车抽鞭与侧倾耦合、绊倒侧翻的能量判据、事故统计的读法、FMVSS 门槛初筛。
  （第 10 章 轮胎）SAE 轮胎坐标系与符号校验（$F_z$ 取负、α vs β、$C_\alpha$ 有负号而 $C_\gamma$ 没有）、
  纵向滑移与 μ–s 曲线（斜率共、峰值分）、附着系数选值（干/湿/冰 + 滑动数）、载荷与气压敏感性、
  由侧偏系数×载荷反算 $C_\alpha$（量纲 1/deg）、侧偏力三区段、外倾刚度量级、**0.0175 lb/lb/deg 车辙判据（=sin1°）**、
  回正力矩三来源、复合滑动与摩擦圆、圆锥度 vs 帘布层转向的跑偏归因、台阶冲击、轮胎模态与反共振。
  输出一律为准静态、开环、英制口径（减速度 ft/s²、K 用 deg/g、几何量 in 或比值），并强制声明单位口径与模型适用域；
  不适用于瞬态响应（横摆阻尼、制动压力建立时间）、极限工况轮胎非线性与热衰退曲线、主观「操控好坏」评分、ESC/EBD/ABS 控制算法标定、
  具体零部件选型报价与法规认证（只做初筛）。
  Triggers: 车轴载荷/轴荷/载荷转移/重心位置/爬坡能力/坡度/SAE坐标系/法向力/垂直力/
  加速性能/加速能力/比功率/驱动力图/换挡点/传动比/质量系数/有效质量/转动惯量/液力变矩器/附着限制/差速器锁止/
  制动距离/刹车距离/制动力配比/抱死/制动效率/制动系数/比例阀/ABS/FMVSS/
  道路负载/空气阻力/风阻/阻力系数/Cd/空气密度/升力/横风/压力中心/中性转向点/滚动阻力/滚阻系数/油耗/燃油经济性/卡曼背/尾部倾角/
  乘适性/行驶平顺性/ride/振动/路面不平度/功率谱PSD/四分之一车辆/固有频率/阻尼比/乘适刚度/跳动bounce/车轮hop/簧下质量/悬架行程/减振器/阻尼阀/轴距滤波/Olley/动态指数/主动悬架/频率加权/ISO2631/
  不足转向/过多转向/推头/甩尾/understeer/oversteer/不足转向梯度/特征车速/临界车速/侧偏刚度/静态裕度/阿克曼/偏离轮迹/等半径法/等速法/
  悬架/整体式车轴/独立悬架/麦弗逊/多连杆/拖曳臂/摆动轴/抗后蹲/抗前仰/抗点头/俯仰角/侧倾中心/举升/jacking/主动悬架/
  转向系统/转向传动比/阿克曼/自定心力矩/前束变化/bump steer/侧倾转向/主销内倾/后倾角/磨胎半径/转向柔顺性/力矩转向/torque steer/前驱不足转向/四轮转向/4WS/
  侧翻/rollover/侧翻临界值/t/2h/SSF/超高/中性车速/阶跃转向/正弦转向/侧倾共振/相位差/挂车抽鞭/绊倒侧翻/倾斜平台/
  轮胎/tire/侧偏角/侧偏刚度/侧偏系数/CorneringStiffness/附着系数/mu/滑动率/滑移率/外倾推力/外倾刚度/回正力矩/轮胎拖距/摩擦圆/复合滑动/圆锥度/帘布层转向/侧拉/车辙/松弛长度/轮胎模态/胎压
---

# 《车辆动力学基础》— 全书能力入口

> **引用口径**：本书的卡片对原文只作带页号的短引用（单次 ≤25 汉字），其余一律转述；见包根目录 `NOTICE` 的 Quotation policy 节。

> 来源：Thomas D. Gillespie《车辆动力学基础》中译本（清华大学出版社 2006；英文原版 1992）
> 本入口承载 **10 章 / 164 张能力卡（全书）**：基础 8 ＋ 加速 20 ＋ 制动 19 ＋ 道路负载 14 ＋ 乘适性 13 ＋ 稳态转向 32 ＋ 悬架 18 ＋ 转向系统 11 ＋ 侧翻 14 ＋ 轮胎 15。
> **这是整本书。** 共 10 章、164 张能力卡、一个技能入口。

## 触发与不触发

**适用**：与制动、操纵稳定性、悬架结构与几何相关的定量计算、判据、选型与调校咨询。

**不适用**：
- 瞬态响应（横摆阻尼、入弯超调、制动压力建立时间、ABS 循环频率）与主观驾驶感受评分
- 极限工况轮胎非线性、附着极限、热衰退曲线
- ESC / EBD / ABS 的控制算法与标定
- 四轮转向、主动悬架控制策略实现（只到"类型与能力边界"）
- 具体零部件选型报价、法规认证（只做减速度量级初筛）
- **晕车与乘坐病**（0.1–0.5 Hz 前庭响应）、**减振器寿命/该不该换**、**摆振与方向盘抖动（shimmy / 40–120 Hz 横向振动）** —— 这三类本书未建模，请直接说"不在覆盖范围"，不要用乘适性或转向章节的指标外推
- **轮胎规格解析（225/45R17、换大一号）、花纹深度与磨耗、爆胎** —— 第 10 章只给规格标注的读法（p254 例还被 OCR 截断），不给选型与失效判据

**但仍应调用的情形**：用户拿准静态指标去解释主观手感、或用稳态公式去算瞬态现象时，**要加载本技能把指标域讲清楚并纠正前提**，而不是默不作声地跳过——区分"能算"与"不能算"本身就是本技能的用途。

## 全书五条主线

-1. **基础**：轴荷（静/加速/坡道）→ 每轴可用附着力 → 加速/爬坡/拖挂能力的共同分母
0. **纵向 · 加速**：发动机扭矩 → 传动系（惯量按速比²放大）→ 驱动力 → 与阻力线交点（最高车速）/ 相邻挡交点（换挡点）；并行一支是附着上限
1. **纵向 · 制动**：减速度 → 动态载荷转移 → 前后轴最大制动力 → 谁先抱死 → 配比怎么改
1b. **纵向 · 阻力账**：空气密度 → 风阻（∝V²）→ 滚阻（∝W）→ 坡阻 → **总道路负载** → 功率（∝V³）→ 油耗
2. **纵向 · 姿态**：驱动/制动力 → 车身俯仰 → 悬架几何（e/d）→ 抗后蹲 / 抗前仰 / 抗点头
2b. **垂向 · 乘适**：路面谱 → 四分之一车辆传递 → 跳动/hop 频率 → 行程与阻尼 → **人的感受（无公认换算尺）**
3. **侧向**：侧倾中心 → 侧向载荷转移 → 前后轴侧偏角 → 不足转向梯度 K → 特征/临界车速
3b. **转向系统的现实修正**：驾驶员输入 → 传动比 → 杆系/悬架几何 → 主销倾角力矩 → **柔顺性** → 实际车轮转角
4. **侧向 · 极限**：t/2h 标尺 → 与摩擦极限对比 → 先滑还是先翻 → 瞬态/共振/绊倒/挂车把门槛压低

**交汇点**：
- 轴荷（线 -1）是所有附着力分析的分母：加速、制动、爬坡、侧翻都从它出发
- 制动时的载荷转移与**悬架几何**共同决定 pitch 与 ride height（线 1 ↔ 线 2）
- 侧倾中心高度决定侧向载荷转移，而载荷转移是 K 的分项之一（线 3 ↔ 线 2）
- **侧翻门槛与稳态转向共用同一批几何量（t、h、h_r、R_φ）**（线 4 ↔ 线 3）
- 所以跨章问题要**按顺序读**，不要只算一章就下结论。

## 第 0 步：先分章

| 用户在问什么 | 去哪一章 |
|---|---|
| 车轴载荷多少、重心在哪、上坡为啥两轴载荷之和变小、拖挂能爬多陡 | **第 1 章** |
| 加速多快、受功率还是附着限制、换挡点、比功率、有效质量、差速器锁止 | **第 2 章** |
| 刹车距离/时间、能量功率、抱死、制动力配比、制动效率、比例阀、ABS、法规 | **第 3 章** |
| 风阻多少、Cd 怎么定、滚阻系数取多少、总道路负载和功率、油耗、横风稳定性 | **第 4 章** |
| 车太颠/太晃、悬架软硬怎么定、减振器怎么调、主动悬架能改善多少、路面谱怎么用、Olley 准则 | **第 5 章** |
| 这车推头还是甩尾、算 K、特征/临界车速、侧滑角、静态裕度、阿克曼、怎么改才不甩尾 | **第 6 章** |
| 选哪种悬架、抗后蹲/抗前仰/抗点头取多少、俯仰角、侧倾中心、举升、主动悬架 | **第 7 章** |
| 转向盘转角对应多少车轮转角、阿克曼、跳动转向、侧倾转向、方向盘拉扯(力矩转向)、前驱车加油门更推头、四轮转向 | **第 8 章** |
| 这车会不会翻、侧翻门槛多少、阶跃还是正弦更危险、挂车怎么翻的、绊倒侧翻 | **第 9 章** |
| 侧偏刚度取多少、附着系数选多少、轮胎符号怎么定、外倾推力/回正力矩、跑偏归因、车辙、胎压与载荷的影响 | **第 10 章** |

---

## 第 1 章 基础 — 意图索引（8 张卡）

| 用户意图 | 加载 |
|---|---|
| **算静态轴荷；由两轴载荷反求重心位置 b、c** | `references/ch01-introduction/capabilities/static-axle-load-and-cg-location.md` |
| **算加速/减速/坡道/拖挂的轴荷（完整一般式）** | `references/ch01-introduction/capabilities/dynamic-axle-load-general-form.md` |
| 只算加速时的载荷转移量 ΔW | `references/ch01-introduction/capabilities/acceleration-load-transfer.md` |
| 坡道上的轴荷；坡度 % 与 ° 的换算 | `references/ch01-introduction/capabilities/grade-axle-load-and-grade-angle.md` |
| **两轴载荷之和小于总重，是不是算错了** | `references/ch01-introduction/capabilities/axle-load-sum-diagnostic.md` |
| 拖挂时能爬多陡（FWD/RWD/4WD） | `references/ch01-introduction/capabilities/towing-gradeability-analysis.md` |
| 该用单质量还是两质量模型；怎么画自由体图 | `references/ch01-introduction/capabilities/model-setup-fbd-and-assumptions.md` |
| **符号搞不清（法向力/垂直力、力矩正方向）** | `references/ch01-introduction/capabilities/sign-convention-and-moment-direction-check.md` |

> 本章完整 8 张卡的索引见 `references/ch01-introduction/capability-index.md`。

## 第 2 章 加速 — 意图索引（20 张卡）

| 用户意图 | 加载 |
|---|---|
| **先判断加速受功率限制还是附着限制** | `references/ch02-acceleration/capabilities/acceleration-limit-triage.md` |
| 精度该选哪一档（粗估/单点/逐速度） | `references/ch02-acceleration/capabilities/acceleration-precision-ladder.md` |
| 功率-扭矩-转速换算（hp=T·rpm/5252） | `references/ch02-acceleration/capabilities/power-torque-rpm-conversion.md` |
| 用比功率粗估加速度上限 | `references/ch02-acceleration/capabilities/specific-power-acceleration-limit.md` |
| 由发动机扭矩算各挡驱动力 | `references/ch02-acceleration/capabilities/drivetrain-force-from-engine-torque.md` |
| **有效转动惯量 → 等效质量 → 质量系数** | `references/ch02-acceleration/capabilities/effective-inertia-to-equivalent-weight.md` |
| 转速与角速度按速比缩放 | `references/ch02-acceleration/capabilities/gear-speed-and-omega-scaling.md` |
| 整车纵向力平衡 | `references/ch02-acceleration/capabilities/longitudinal-force-balance.md` |
| 读驱动力图：最高车速、等功率线包络 | `references/ch02-acceleration/capabilities/tractive-effort-map-and-envelope.md` |
| 传动比等比级数 / 用万有特性选传动比 | `references/ch02-acceleration/capabilities/geometric-ratio-series.md` |
| **最佳换挡点在相邻挡交点** | `references/ch02-acceleration/capabilities/shift-point-at-force-intersection.md` |
| 液力变矩器为什么改善起步 | `references/ch02-acceleration/capabilities/torque-converter-start-boost.md` |
| 本章单位与常数（550/386/32.2/in·lb·s²） | `references/ch02-acceleration/capabilities/chapter-units-and-conventions.md` |
| **附着限制四分支（锁止×前驱×整体/独立）** | `references/ch02-acceleration/capabilities/traction-limit-decision-tree.md` |
| 加速时的纵向载荷转移 | `references/ch02-acceleration/capabilities/longitudinal-load-transfer.md` |
| **驱动扭矩引起的横向载荷转移** | `references/ch02-acceleration/capabilities/lateral-load-transfer-from-drive-torque.md` |
| 差速器不锁止 → 被小载荷侧封顶 | `references/ch02-acceleration/capabilities/open-differential-traction-limit.md` |
| 锁止 / 独立驱动轴（**两个独立条件**） | `references/ch02-acceleration/capabilities/locked-or-independent-drive-axle.md` |
| 前驱车附着限制 | `references/ch02-acceleration/capabilities/front-drive-traction-limit.md` |
| 前驱 vs 后驱对比 | `references/ch02-acceleration/capabilities/fwd-vs-rwd-traction-comparison.md` |

## 第 3 章 制动 — 意图索引（19 张卡）

| 用户意图 | 加载 |
|---|---|
| 算制动距离与停车时间（含/不含风阻） | `references/ch03-braking/capabilities/braking-distance-and-time.md` |
| 算制动吸收的能量与功率（峰值/平均） | `references/ch03-braking/capabilities/brake-energy-and-power.md` |
| 由踏板/管路压力算制动力，鼓式 vs 盘式 | `references/ch03-braking/capabilities/pressure-to-brake-force.md`、`references/ch03-braking/capabilities/drum-brake-factor.md` |
| 减速时前后轴各承受多少载荷 | `references/ch03-braking/capabilities/dynamic-load-transfer.md` |
| 画前后轴最大制动力边界线 | `references/ch03-braking/capabilities/lockup-boundary-lines.md` |
| 求前后轴同时抱死的交点 | `references/ch03-braking/capabilities/simultaneous-lockup-point.md` |
| 效能三角形怎么画、多工况叠加怎么看 | `references/ch03-braking/capabilities/effectiveness-triangle.md` |
| 配比线的斜率（用制动增益定） | `references/ch03-braking/capabilities/proportion-line-slope.md` |
| 压力比例阀 500/0.3 是什么意思 | `references/ch03-braking/capabilities/proportioning-valve.md` |
| 算制动效率（七步表法） | `references/ch03-braking/capabilities/brake-efficiency-table.md` |
| **判断哪个轮先抱死、后果是什么** | `references/ch03-braking/capabilities/lockup-order-and-consequence.md` |
| 固定配比无解时怎么办（决策树） | `references/ch03-braking/capabilities/no-solution-decision-tree.md` |
| 配比设计的完整流程 | `references/ch03-braking/capabilities/proportion-design-workflow.md` |
| FMVSS 105/121 减速度符合性初筛 | `references/ch03-braking/capabilities/fmvss-compliance-screen.md` |
| 解释 ABS 为什么有用（μ 峰值不稳定） | `references/ch03-braking/capabilities/mu-peak-instability.md` |
| 载荷增加对 μ 的影响 | `references/ch03-braking/capabilities/load-sensitivity.md` |
| 滚动/空气/传动/坡度阻力要不要计入 | `references/ch03-braking/capabilities/resistance-terms.md` |
| 转动惯量对有效质量的影响 | `references/ch03-braking/capabilities/rotational-inertia-effective-mass.md` |

> 本章完整 19 张卡的索引见 `references/ch03-braking/capability-index.md`。

## 第 4 章 道路负载 — 意图索引（14 张卡）

| 用户意图 | 加载 |
|---|---|
| **由温度气压算空气密度** | `references/ch04-road-loads/capabilities/air-density-and-standard-atmosphere.md` |
| **算风阻与所需马力** | `references/ch04-road-loads/capabilities/aero-drag-and-power.md` |
| **顺风/逆风为什么不对称** | `references/ch04-road-loads/capabilities/wind-relative-velocity-and-asymmetry.md` |
| 阻力都花在哪、该改哪里（0.42 的分解） | `references/ch04-road-loads/capabilities/drag-source-breakdown-and-modifications.md` |
| 尾部倾角与分离（≤15° 规则、卡曼背） | `references/ch04-road-loads/capabilities/tail-shape-and-separation-limit.md` |
| 俯仰/横摆/侧倾力矩；压力中心在哪 | `references/ch04-road-loads/capabilities/aero-moments-and-pressure-center.md` |
| 升力与侧向力（用前端面积，不是侧面） | `references/ch04-road-loads/capabilities/lateral-force-and-lift.md` |
| **横风为什么飘；降阻与横风稳定的取舍** | `references/ch04-road-loads/capabilities/crosswind-sensitivity-and-tradeoff.md` |
| 滚阻的基础口径（$f_rW$、静态重量够用） | `references/ch04-road-loads/capabilities/rolling-resistance-baseline.md` |
| **滚阻系数该套哪个式子**（常数/线性/V^2.5/货车双式） | `references/ch04-road-loads/capabilities/rolling-resistance-coefficient-models.md` |
| 温度/胎压/速度/磨损/侧偏怎么改滚阻 | `references/ch04-road-loads/capabilities/rolling-resistance-state-corrections.md` |
| 铺装 vs 越野 vs 湿路的滚阻 | `references/ch04-road-loads/capabilities/road-surface-and-offroad-friction.md` |
| **总道路负载与功率**（力 V²、功率 V³） | `references/ch04-road-loads/capabilities/road-load-and-power.md` |
| 油耗归因（为什么不能由 ΔCd 直接推 Δmpg） | `references/ch04-road-loads/capabilities/fuel-economy-chain-and-attribution.md` |

> 本章完整 14 张卡的索引见 `references/ch04-road-loads/capability-index.md`。

## 第 5 章 乘适性 — 意图索引（13 张卡）

| 用户意图 | 加载 |
|---|---|
| **车太颠/太晃，先按频率归段**（三段链总流程） | `references/ch05-ride/capabilities/ride-triage-and-resonance-windows.md` |
| 路面不平度谱怎么用；轮辙和/差怎么拆 | `references/ch05-ride/capabilities/road-input-spectrum-and-track-split.md` |
| 四分之一车辆增益；由输入谱算响应谱 | `references/ch05-ride/capabilities/quarter-car-gain-and-spectrum-product.md` |
| **乘适刚度 → 跳动频率 → 静挠度尺** | `references/ch05-ride/capabilities/ride-rate-and-bounce-frequency.md` |
| 悬架行程够不够；阻尼上限 | `references/ch05-ride/capabilities/travel-budget-and-damping-limits.md` |
| 减振器怎么调（阀片/迟滞/压缩回弹比） | `references/ch05-ride/capabilities/damper-valving-and-hysteresis.md` |
| **主动悬架能改善多少（−30% 与 −10% 必须成对）** | `references/ch05-ride/capabilities/active-vs-passive-paired-gain.md` |
| 车轮 hop 与簧下质量 | `references/ch05-ride/capabilities/wheel-hop-and-unsprung-mass.md` |
| 车上振动源是谁（阶次定位） | `references/ch05-ride/capabilities/onboard-excitation-orders.md` |
| **为什么高速颠、低速晃**（轴距滤波零点） | `references/ch05-ride/capabilities/wheelbase-filter-zeros.md` |
| 双模态与两个运动中心（跳动/俯仰谁主导） | `references/ch05-ride/capabilities/pitch-bounce-bimodal-and-centers.md` |
| **Olley 准则怎么用**（经验法则，不是定律） | `references/ch05-ride/capabilities/olley-criteria-and-dynamic-index.md` |
| 人体判据怎么用；为什么不能当 KPI | `references/ch05-ride/capabilities/human-limit-and-spectrum-presentation.md` |

> 本章完整 13 张卡的索引见 `references/ch05-ride/capability-index.md`。

## 第 6 章 稳态转向 — 意图索引（32 张卡）

| 用户意图 | 加载 |
|---|---|
| 判断推头/甩尾；算 K | `references/ch06-steady-state-steering/capabilities/steer-character-k.md`、`references/ch06-steady-state-steering/capabilities/sae-k-definition.md`（SAE 的转向盘口径） |
| 侧偏刚度要不要乘 2、每轴两轮还是单胎 | `references/ch06-steady-state-steering/capabilities/understeer-gradient-definition.md` |
| 特征车速；"247 mph 是不是很稳" | `references/ch06-steady-state-steering/capabilities/characteristic-speed.md` |
| 临界车速；甩尾是不是车的问题 | `references/ch06-steady-state-steering/capabilities/critical-speed.md` |
| 质心侧滑角 β；β 什么时候为零 | `references/ch06-steady-state-steering/capabilities/cg-sideslip-angle.md`、`references/ch06-steady-state-steering/capabilities/beta-zero-speed.md` |
| 静态裕度 e/L | `references/ch06-steady-state-steering/capabilities/static-margin.md` |
| 阿克曼角 / 内外轮转角差 / 偏离轮迹 | `references/ch06-steady-state-steering/capabilities/low-speed-geometry.md`、`references/ch06-steady-state-steering/capabilities/ackerman-angle.md`、`references/ch06-steady-state-steering/capabilities/off-tracking.md` |
| 侧倾刚度、侧倾率、轮荷差、力矩怎么分到前后轴 | `references/ch06-steady-state-steering/capabilities/roll-chain-kphi-phi-dfz.md`、`references/ch06-steady-state-steering/capabilities/roll-rate.md`、`references/ch06-steady-state-steering/capabilities/load-transfer-two-mechanisms.md`、`references/ch06-steady-state-steering/capabilities/roll-stiffness-formula.md`、`references/ch06-steady-state-steering/capabilities/roll-moment-front-bias.md`、`references/ch06-steady-state-steering/capabilities/load-transfer-only-distributed.md` |
| 外倾对 K 的贡献；地面外倾角怎么合成 | `references/ch06-steady-state-steering/capabilities/camber-thrust-k.md`、`references/ch06-steady-state-steering/capabilities/camber-magnitude-screen.md`、`references/ch06-steady-state-steering/capabilities/camber-angle-composition.md` |
| 换衬套后转向往哪边变；回正力矩算不算 | `references/ch06-steady-state-steering/capabilities/compliance-steer-k.md`、`references/ch06-steady-state-steering/capabilities/aligning-torque-k.md` |
| 加油门时车头往哪偏 | `references/ch06-steady-state-steering/capabilities/drive-force-steering.md` |
| 定圆/等速试验测 K | `references/ch06-steady-state-steering/capabilities/constant-radius-test.md`、`references/ch06-steady-state-steering/capabilities/constant-speed-test.md`、`references/ch06-steady-state-steering/capabilities/test-method-choice.md` |
| **把过多转向调回不足转向** | `references/ch06-steady-state-steering/capabilities/understeer-tuning.md`、`references/ch06-steady-state-steering/capabilities/axle-rule-direction.md`、`references/ch06-steady-state-steering/capabilities/design-lever-inventory.md` |
| 单位换算、出现负侧倾率、数量级不对 | `references/ch06-steady-state-steering/capabilities/units-constants-checklist.md` |
| 不用公式判推头（侧风扰动测试） | `references/ch06-steady-state-steering/capabilities/olley-criterion.md` |
| 模型适用域 | `references/ch06-steady-state-steering/capabilities/two-wheel-preconditions.md` |

> 本章完整 32 张卡的索引见 `references/ch06-steady-state-steering/capability-index.md`（或 `references/ch01-introduction/_chapter-routing.md`）。

## 第 7 章 悬架 — 意图索引（18 张卡）

| 用户意图 | 加载 |
|---|---|
| 选哪种悬架；两族怎么选 | `references/ch07-suspension/capabilities/structure-family-selection.md` |
| **100% 抗后蹲的 e/d** | `references/ch07-suspension/capabilities/anti-squat-100.md` |
| 抗后蹲做到百分之多少 | `references/ch07-suspension/capabilities/anti-squat-percent.md` |
| **完全抗前仰的 e/d**（车身水平） | `references/ch07-suspension/capabilities/anti-pitch-up-precision.md` |
| 前驱车抗提升 | `references/ch07-suspension/capabilities/front-drive-anti-lift.md` |
| 俯仰角变化率 θ_p/a_x | `references/ch07-suspension/capabilities/pitch-rate-theta-p.md`、`references/ch07-suspension/capabilities/example1-anchors.md` |
| 初始尺寸速算 | `references/ch07-suspension/capabilities/five-e-quick-rule.md` |
| 等效拖曳臂 / 虚拟作用点 | `references/ch07-suspension/capabilities/equivalent-trailing-arm-ed.md`、`references/ch07-suspension/capabilities/virtual-point-method.md` |
| 整体式车轴的侧倾中心 | `references/ch07-suspension/capabilities/roll-center-solid-axle.md` |
| 独立悬架的侧倾中心 | `references/ch07-suspension/capabilities/roll-center-independent.md` |
| **举升（jacking）风险** | `references/ch07-suspension/capabilities/jacking-risk.md` |
| 满额补偿该不该做（8 条否决） | `references/ch07-suspension/capabilities/full-compensation-veto.md` |
| 选主动悬架等级 | `references/ch07-suspension/capabilities/active-suspension-ladder.md`、`references/ch07-suspension/capabilities/active-mode-signals.md` |
| 平行杆退化 | `references/ch07-suspension/capabilities/parallel-arm-infinite-point.md` |
| 例题回归锚点 | `references/ch07-suspension/capabilities/example1-anchors.md`、`references/ch07-suspension/capabilities/example2-anti-lift-anchors.md` |

> 本章完整 18 张卡的索引见 `references/ch07-suspension/capability-index.md`。

## 第 8 章 转向系统 — 意图索引（11 张卡）

| 用户意图 | 加载 |
|---|---|
| **转向盘转角对应多少车轮转角**（设计 vs 实测差一倍） | `references/ch08-steering-system/capabilities/steering-ratio-and-wheel-angle.md` |
| 阿克曼内外轮转角；平行转向的手感差异 | `references/ch08-steering-system/capabilities/ackermann-wheel-angles-and-low-speed-torque.md` |
| **车轮一跳就自己转向**（前束变化/侧倾转向的方向判定） | `references/ch08-steering-system/capabilities/steering-geometry-error-direction.md` |
| 由侧倾转向系数算对不足转向的贡献 | `references/ch08-steering-system/capabilities/roll-steer-gradient.md` |
| 主销内倾产生的自定心力矩 | `references/ch08-steering-system/capabilities/kingpin-inclination-self-centering-moment.md` |
| 后倾角与回正力矩 | `references/ch08-steering-system/capabilities/caster-and-aligning-torque.md` |
| **为什么实测不足转向比理论大一个数量级**（柔顺性 + 两口径换算） | `references/ch08-steering-system/capabilities/compliance-understeer-and-basis.md` |
| 刹车时的后倾角还灵不灵；对开路面跑偏 | `references/ch08-steering-system/capabilities/braking-caster-and-split-mu.md` |
| **前驱车加油门为什么更推头**（五机制分解） | `references/ch08-steering-system/capabilities/fwd-five-mechanisms.md` |
| 驱动力/制动力作用在转向轴上的力臂 | `references/ch08-steering-system/capabilities/tractive-force-and-brake-lever.md` |
| 四轮转向的转弯半径；低速反向 vs 高速同向 | `references/ch08-steering-system/capabilities/four-wheel-steering-radius-and-phase.md` |

> 本章完整 11 张卡的索引见 `references/ch08-steering-system/capability-index.md`。

## 第 9 章 侧翻 — 意图索引（14 张卡）

| 用户意图 | 加载 |
|---|---|
| **这车侧翻门槛多少（t/2h）**；典型车型对比 | `references/ch09-rollover/capabilities/rigid-rollover-threshold.md` |
| 有超高的弯道；中性车速 | `references/ch09-rollover/capabilities/superelevation-and-neutral-speed.md` |
| 什么时候算"开始翻"、还能不能救回来 | `references/ch09-rollover/capabilities/rollover-onset-staging.md` |
| **会先滑还是先翻**（门槛 vs 摩擦极限） | `references/ch09-rollover/capabilities/slide-vs-trip-diagnosis.md` |
| **悬挂车辆的实际门槛**（侧倾率 + 侧倾中心修正） | `references/ch09-rollover/capabilities/suspension-threshold-correction.md` |
| 精确建模与倾斜平台试验 | `references/ch09-rollover/capabilities/precise-model-and-tilt-test.md` |
| **阶跃还是正弦更危险**（按共振频率分车型） | `references/ch09-rollover/capabilities/step-vs-sine-selection.md` |
| 瞬态门槛的阻尼修正 | `references/ch09-rollover/capabilities/transient-threshold-damping.md` |
| 前后轴相位差；四轮转向的代价 | `references/ch09-rollover/capabilities/phase-lag-and-four-wheel-steer.md` |
| 挂车抽鞭；侧倾耦合怎么做 | `references/ch09-rollover/capabilities/trailer-whip-and-roll-coupling.md` |
| **绊倒侧翻**（撞路缘翻不翻） | `references/ch09-rollover/capabilities/tripped-rollover-energy.md` |
| 读侧翻事故统计；门槛能当指标吗 | `references/ch09-rollover/capabilities/accident-statistics-reading.md` |
| FMVSS 门槛初筛 | `references/ch09-rollover/capabilities/fmvss-1-2-screening.md` |
| 该用哪一层模型（准静态 → 瞬态 → 多体） | `references/ch09-rollover/capabilities/model-tier-router.md` |

> 本章完整 14 张卡的索引见 `references/ch09-rollover/capability-index.md`。

## 第 10 章 轮胎 — 意图索引（15 张卡）

| 用户意图 | 加载 |
|---|---|
| **轮胎符号怎么定**（$F_z$ 取负、α vs β、$C_\alpha$ 有负号而 $C_\gamma$ 没有） | `references/ch10-tires/capabilities/tire-sign-and-unit-gate.md` |
| 七个系数由什么决定（结构 vs 胶料） | `references/ch10-tires/capabilities/tire-structure-coefficient-map.md` |
| **附着系数选多少**（干/湿/冰 + 滑动数） | `references/ch10-tires/capabilities/mu-surface-selection.md` |
| 纵向滑移与 μ–s 曲线（斜率共、峰值分） | `references/ch10-tires/capabilities/longitudinal-slip-and-mu-s-curve.md` |
| **载荷 +10% 与胎压的影响** | `references/ch10-tires/capabilities/mu-load-and-pressure-sensitivity.md` |
| 侧偏力怎么随侧偏角变（三区段） | `references/ch10-tires/capabilities/lateral-force-three-regimes.md` |
| **侧偏刚度取多少**（由侧偏系数 × 载荷反算） | `references/ch10-tires/capabilities/cornering-stiffness-from-coefficient.md` |
| **前后轴侧偏刚度怎么配才是不足转向**（须按载荷正则化） | `references/ch10-tires/capabilities/understeer-balance-by-normalized-stiffness.md` |
| 外倾推力有多大 | `references/ch10-tires/capabilities/camber-stiffness-magnitude.md` |
| **会不会爬不出车辙**（0.0175 = sin1°） | `references/ch10-tires/capabilities/rut-criterion-0175.md` |
| 回正力矩三个来源 | `references/ch10-tires/capabilities/aligning-moment-three-sources.md` |
| 复合滑动与摩擦圆 | `references/ch10-tires/capabilities/combined-slip-and-friction-circle.md` |
| **跑偏是轮胎还是定位问题**（圆锥度 vs 帘布层转向） | `references/ch10-tires/capabilities/conicity-and-ply-steer.md` |
| 过台阶/坑的冲击载荷 | `references/ch10-tires/capabilities/step-impact-and-longitudinal-forces.md` |
| 轮胎模态与反共振（噪声/传递率） | `references/ch10-tires/capabilities/tire-modes-and-anti-resonance.md` |

> 本章完整 15 张卡的索引见 `references/ch10-tires/capability-index.md`。

## 加载规则

**两级索引**：上面十张表是**高频入口精选**（每个意图一行，列出该意图最该读的 1–3 张卡），不是全部 164 张卡的穷举。
若表里查不到你要的意图，按顺序查两级：① 本章 `references/ch01-introduction/capability-index.md`（完整意图与关键词索引）→ ② 本章 `references/ch01-introduction/_chapter-routing.md`（该章编译时生成的全量路由表）。
**各章的 `references/ch01-introduction/capability-index.md` 与 `references/ch01-introduction/_chapter-routing.md` 各自 100% 覆盖本章全部卡**，所以不存在"找不到"的卡，只有"顶层表没列"的卡。

- 每次任务先读本文件，再按上表加载 **1** 张能力卡；跨章问题最多 2 张（各章一张）。
- 概览类问题不加载能力卡，用「四条主线」与 `references/*/overview.md` 回答。
- 四章都查不到的意图 → 明确告知超出已蒸馏章节范围，不要硬套。

## 口径与红线（必须随答案一起给出）

1. **英制**：lb / in / ft / ft·s² / mph / deg-g。第 6 章的 `r` 有两义（式 6-21 是 deg/s、式 6-71 是 rad/s）。
2. **C_α 是整轴两轮之和**（第 6 章）；轮胎表给的是单胎，必须 ×2。漏乘 → K 减半、V_char 虚高 √2 倍。
3. **制动效率 η_b 有两个分母口径**（第 3 章）：`D/μ_p`（路面峰值）与 `D/max(μ_f,μ_r)`（所需摩擦），同一工作点可差十几到二十几个百分点。**每次计算必须声明用哪个**。
4. **K 是开环稳态指标**，不是"操控好坏"评分。
5. **第 7 章没有"侧倾中心该取多高"的经验值**——只讲怎么求。任何目标值都属编造。
6. **原书存在多处硬伤**，卡片已就地标注（`⚠️` / "需纸书复核"）。遇到标注项**照标注说，不许替原文裁决**。

### 已知硬伤速查

| 章 | 位置 | 问题 |
|---|---|---|
| 4 | 例题 4.5-1 | **油耗链不闭合**：215 hp × 0.35 = 75.3 lb/h，书印 82.6 lb/h（反推需 236 bhp，来源未交代）；13 gal/h ↔ 5.25 mpg 自洽但隐含柴油密度 6.35 lb/gal（偏低）→ **不许把 5.25 mpg 当 215 hp 的严格推论** |
| 4 | 4.3 正文 vs 图题 | 正文写"典型大型车辆"，图 4.35/4.36 图题写"典型轿车"（3650 lb 是轿车量级）→ **以轿车为准** |
| 4 | 例题 4.5-2 | 解答说"用式(4-4) 算相对速度"，应为 **(4-5)**；题干 OCR 丢失，参数是反推的 |
| 4 | 式(4-11) | 分母 OCR 损坏（只剩 $d_{ns}+\xi_d$，$C_f/C_r$ 丢失）→ **横风敏感度只能定性，不可公式化** |
| 4 | 式(4-13) | 称"随载荷线性增加"，但 $f_r\propto W$ 使 $R_x\propto W^2$ → 口径冲突 |
| 4 | 图 4.12/4.34/4.37 | 读数缺失；图 4.37"车重=136 kg"是 OCR 讹误 → **禁引其百分数**；**图 4.8 OCR 错行** → 禁编车型↔系数配对 |
| 4 | 单位 | 式(4-2) 的 $\rho$ 是 **lb·s²/ft⁴**（质量密度）；用 lb/ft³ 会高 **32.2 倍**。$f_r$ 无量纲（OCR 曾标 "lb"）|
| 4 | 前端面积 | 式(4-6)~(4-10) 全用**前端面积**，不用侧面面积（作者唯一亲自预警处）；错得"像合理值"，不报错 |
| 4 | 概念 | **伯努利不能解释阻力**（无粘时前后压力平衡 → 阻力为 0）；**"湍流边界层更耐逆压梯度"本章没有** → 章外补充 |
| 4 | 三仓 | 仓A 72500 lb 货车（ρ=0.00207、$f_r$=0.00685）/ 仓B 3650 lb 轿车（$f_r$=0.02、A=23.3、$C_D$=0.34）/ 仓C 未知车（A=21、$C_D$=0.42）。**ρ 不能跨仓**；仓C 的 $C_D$=0.42 与分解表 0.42 **纯属数值巧合，严禁互引** |
| 4 | 湿度 | 正文说密度随湿度变，但式(4-3a/b) 只有 P、T（量级约 1%）|
| 5 | 式(5-11) | **整条缺失**（5.2.4 引用它定义阻尼比）→ ζ 只能由式(5-19c) 重构，须标"非原文" |
| 5 | 式(5-15)(5-16) | **OCR 损坏不可用** → 力通道 $F_w/F_b$ 不可复现；图 5.16 后两条曲线定量读数一并降级 |
| 5 | 例 5.2.11-1 | 原文印 "7.19 rad/s" 与同页 $\omega^2$=50.41 不自洽（7.19²=51.7）→ **应为 7.10 rad/s = 1.130 Hz** |
| 5 | 例 5.2.11-2 表 | 表头 OCR 错序，已复原为 11 列；行 567 的 $k^2$=**3011.8**（非 3001.8）；行 675 的 $Z/\theta_2$=**−36.9**（补回负号）；$Z/\theta$ 是病态量，只给区间（例 1 为 −230~−260 in，±6%），行 725 的 957.3 只能读"10³ in 量级" |
| 5 | 轴距滤波 | **不是"$V/2L$ 的整数倍"**：跳动零点 = $V/2L$ 的**奇次倍**（4/12/20），俯仰 = **偶次倍**（8/16/24）|
| 5 | Olley 准则 | ①方向是"**前乘适刚度低 30%**"（前软后硬）；②"低 30%"与"后移 6.5%L"**不等价**（前者⇔后移 8.8%，后者⇔前低 23%）；③四条来自 1930s **单车**主观实验、无统计样本、互不独立 → **称为"经验法则"，不是定律** |
| 5 | 人体判据 | 图 5.36/5.38 是作者**抄录**曲线（自述"不可跨曲线比较"），图 5.37 是 NASA；**全章无任何 m/s² 或 g 的数值限值**；ISO 只有"第二版"、**标准号 OCR 缺失** → **禁写 ISO 2631-1:1997、禁引 VDV** |
| 5 | 阻尼口径 | **"200% 阻尼" = ζ=2.0**（100% 才是临界）；主动悬架的 ζ=5%/20% 是**非悬挂**阻尼比，与乘适 ζ 不同源 |
| 5 | 刚度 | **$RR$ ≠ $K_s$**（$RR$ 是 $K_s$ 与 $K_t$ 串联）；**同一对弹簧在跳动模态串联、在 hop 模态并联**；式(5-19d) 只写 "K/m" 未指明 K |
| 5 | $G_0$ 标度 | **不自洽**：按式(5-1) 算得 11.8 in²/(cyc/ft)，图 5.2 纵轴上限 0.1，**差两个数量级** → **绝对数值禁出**，只给形状/拐点/波数窗/"两档差 10 倍" |
| 5 | 范围 | **"0–25 Hz"不是原文判据**（25 Hz 只是三张隔振图横轴右端，图 5.17 画到 100 Hz）；本章**没有** $V^{-1.25}$ 谱形式 |
| 5 | 图 | **41 张图全为 PNG 占位符** → 零读数；5.3「人的感受」不可做成可算能力 |
| 2 | 例题 2.2 | "1 挡 88 ft/s（60 mph）"**是 OCR 错误**：按 ω=36.87 rad/s、r=12.59 in 应为 **38.7 ft/s（26.4 mph）**；88 ft/s 需 366 hp ≫ 该机 181 hp |
| 2 | 式(2-18a)(2-23)(2-25) | 分母的 `N_ft` 是 **`N_f × t`**（主减比 × 轮距），**不是** `N_tf`；用错 1201→1279 |
| 2 | p48 表 + p52 注 | 质量系数三值互斥：式(2-12) 1.89 / 表 1.50 / 例题实算 **1.35**；从动轮 27 lb 疑漏乘 2（应 53.6）；"5 挡 9.7" 只是首项（完整 41.6） |
| 2 | 传动效率 | 正文 80–90% vs 例题 0.966×0.99≈**96%**，差 6–16 个点 |
| 2 | 例题 2.4 | `1+0.0122` 应为 `1+0.1122`；式(2-24) 分子 `W D` 应为 `Wb`；式(2-25) 第三项 `N_t` 应为 `N_{ft}`；"每轮 548 lb" 应为 **600.5** |
| 2 | 图 2.1/2.2/2.4–2.9 | **无数据表** → 只给读图判据，不许编造曲线读数 |
| 2 | 概念 | **独立悬架 ≠ 差速器锁止**（两个独立充分条件）；且锁止后 $W_y$ 仍存在，消失的只是它造成的损失 |
| 3 | 例题 3.12 表 | 500 psi 行 μ_f 印 0.6617，按 F/W 应为 **0.617**（否则与同行 η_b=98% 矛盾）|
| 3 | 注(1) | 称"效率随减速度增加而降低"，但表格实际非单调（97→99→94→100→98→98→98）→ **照表不照注** |
| 3 | 例题 3.5 | 平均功率式内代入 4.996 s（应 4.966）；初始风阻印 74.4 lb（应 72.4）|
| 3 | 符号 | `F_b` 双义；式(3-31) 的 `G·T_a/r` 应为 `G·P_a/r`；式(3-7) 分母 `F_x1` 应为 `F_xt`；式(3-22) 的 `W_r0`= `W_rs` |
| 3 | 滑动数 | 文中把 "SN 81" 当 μ_p=0.81；ASTM E274 是 SN=100μ |
| 3 | C_D | 带量纲（lb·s²/ft²），式(3-10) 只在该口径下成立 |
| 3 | 图 3.16 / 3.17 | 抱死频次对应关系、踏板力阴影区边界**在 OCR 中丢失**，只能定性，不许编造阈值 |
| 6 | 例题 1 | 后轴载荷印 1932 lb（应 1552）；刚度 232/195 串行；K 印 0.11（复算 0.1175）|
| 6 | p179 vs p188 | 后轴导向臂"支点低于轮心"一处说过多、一处说不足，**方向自相矛盾** |
| 6 | 式(6-20)(6-22)(6-24) | 印刷残缺/缺号，增益类数值只能靠例题反推 |
| 6 | 式(6-67) 后 | `F_xr` 疑为 `F_xf` 笔误 |
| 7 | 式(7-16) | `2h/L` 近似比精确值（0.301）偏大 25.5%，只在 K 比 ±10% 内可速算 |
| 7 | 式(7-19)(7-23)(7-28) | 符号/下标待核 |
| 7 | 式(7-26) vs (7-12) | 载荷转移项符号相反 → 四驱分支不可用 |
| 7 | p206 vs p210 | "侧倾中心高→转向"方向相反，引用必须带"哪根轴、哪种结构" |
| 7 | ξ | 7.3.6 是驱动力占比，7.4 是制动力占比 |
| 8 | 式(8-4) | 第二项写 `sinδ`，正文与图注写 `d sinν cosδ` → **后倾项不可用**，只可定性 |
| 8 | 式(8-17) | OCR 只剩 `L²(1-²)`，分母丢失 → **严禁补全**；只可给两个边界（ξ=0 退化、ξ=1 为零）|
| 8 | 式(8-9) | 力臂 `d+r·sin(λ+ζ)` 与"半轴水平时力臂=d"在 λ≠0 时不自洽 → 前驱机制②只引文献估值 ≈1 deg/g |
| 8 | 术语 | **自定心力矩 ≠ 回正力矩 M_z**（前者几何项不进 K，后者轮胎项进式 8-8 且制动会变号）；**K_ss ≠ K_φ**（同单位，代错不报错）；**理想中心点 ≠ 抗点头/抗后蹲的虚拟中心**（沿用第 7 章作图法会让侧倾转向符号整体判反）|
| 8 | 传动比 | 实测 ≈ 设计 ×2 且总偏大（货车 37→76）；三口径必须同报：转向盘 150 / 车轮 4 / 单测车轮 ≈0 |
| 8 | 前驱五机制 | 书报 4–5 deg/g 是**取整**，逐项和实为 3.0–4.5；"AWD" 是笔误应为 FWD |
| 8 | 图 8.18/8.19/8.20/8.24/8.25 | 无数据表 → 零读数 |
| 8 | 式(8-8) | 明说"忽略垂直力"与式(8-4) 保留 M_V 不一致；量纲要求 W_f 是"每 g 的前轮载荷"（未明说）；对 K_ss 极敏感（600→4.76、900→3.17 deg/g）|
| 8 | 符号 | **ξ 全书四章四义**（第 1/2/7/8 章，第 3 章无 ξ）；本章是 ξ_4WS 且**可负**。`p` 是轮胎拖矩不是压力；`λ` 被 OCR 打成汉字「入」|
| 8 | 小角度 | 原文明说但**从未给角度上限** |
| 9 | p241 | **原文自相矛盾**："要达到最高的侧翻临界值需要使侧倾率尽可能的**高**（使用高侧倾刚度的悬架）"——按式(9-6) 应为**低**（低侧倾刚度）。照抄这句会把悬架越改越软 |
| 9 | 式(9-5) | 式中的 φ 实际是**车身侧倾角 Φ**，不是超高角 |
| 9 | φ | **一符两义**：一处是路面超高角，一处是侧倾角 |
| 9 | 概念 | **"侧翻临界值"有三义**（以 g 计 / 以能量计 / 无量纲 t/2h），必须说明用的是哪一种；**"保守"= 算出的值偏高（偏乐观）**，与中文工程用法相反 |
| 9 | FMVSS | **"FMVSS 1.2"没有标准编号**（绝不是 216）→ 任何下游补 216 即整条失效 |
| 9 | 车速 | **中性车速 ≠ 最安全车速** |
| 9 | 量纲 | **23.075 是 ft/s 不是 g**；$R_\phi$ 单位是 **rad/g** |
| 9 | 图 9.2/9.4/9.7–9.15 | **零读数**；图 9.15 上下不可辨 |
| 9 | 表 9.1 | 端点复算越界（0.833 > 0.8）|
| 9 | p247/p249 | 方向相反，两条均不采信 |
| 9 | p243 | 轿车/SUV 阶跃降幅 OCR 断裂 → **不许编造**，只能把"未说明"作为合法输出 |
| 10 | 术语 | **"侧偏系数无量纲"是错的**：量纲 **1/deg**（lb/deg ÷ lb）；换 per-rad ×57.3 → 0.12→**6.88**、0.15→**8.60**、0.25–0.30→**14.3–17.2 rad⁻¹**。**"驻波"在本章不存在**（检索 0 次）|
| 10 | 外倾角 | **正文内部冲突**：p255 定义(12)"上端朝车辆**外侧**"（整车基准）vs p266"上端向**右**为正"（轮胎基准）→ 左右轮符号问题在正文内部就存在 |
| 10 | 符号 | **$C_\gamma$ 没有负号而 $C_\alpha$ 有**（正 α 出 $-F_y$、正 γ 出 $+F_y$）→ 照抄会让车辙判据判反；$F_z$ 取负、垂直载荷 = $-F_z$（p262 原文把 F 同时用作 $F_z$ 与 $W$）|
| 10 | p268 车辙 | **口径滑移**："外倾**系数** > 0.0175" vs "外倾**刚度** < 0.0175"，单位都写 lb/lb/deg → 拿 $C_\gamma$=30–100 比 0.0175 会永远判"爬出"；0.0175 原书印作 "0.01751"（sin1°=0.017452）|
| 10 | 载荷敏感 | **两数字不相容**：p258"每 +10% μ −0.01"（近额定**局部斜率**）vs p265"50%→125% 降 >20%"（**全域割线**）→ 不得线性衔接、不得插值成曲线 |
| 10 | 湿路 | **"25%–50%"是 $\mu_p$（峰值摩擦力占载荷比），不是峰值滑动率**；湿路 $s_p$ 全章未给（易被系统性误读）|
| 10 | 侧偏刚度 | **$C_\alpha$ 绝对值（lb/deg）本章未给**（图 10.15 只有轴到 200）→ 只能反算并声明"反算值≠原始数据"；**拟合前须扣残差**（附录 A 7.3.3.10"侧偏角力"）|
| 10 | 附录 A | 7.3.3.14 定心力 **sin 印成 cos**；7.3.3.6 滚阻**乘除颠倒**（应除 $R_l$，$\nu$ 应为 $\gamma$）；**7.6 是 $\mu_p/\mu_s$ 官方对应表**（$\mu_p$ 有侧向/驱动/制动**三条通道**，不可混用）|
| 10 | 正文 vs 附录 A | 三处定义冲突：滑动率分母（10-1 用 $V$ / 7.2.8 用 $r\omega$）→ **以 (10-1) 为准**；传递率（p278 带量纲 1/s² vs 附录 A 2.8 力/力）→ **以 p278 为准**；外倾角 vs 倾斜角 |
| 10 | 其他 | 圆锥度"差值"**严格需 /2**（否则与帘布层转向的"平均值"混）；p263"0.12 ≈ 10% 载荷"与 12% 取整不自洽 → 统一 $k\times100\%$；**复合滑动无解析式**、$\mu(F_z)$ 的 a/b 系数全书缺值 |
