---
name: vehicle-road-loads
description: |
  当用户处理乘用车/商用车「道路负载（road load）」问题时调用：由温度气压算空气密度（英制/公制两式，
  英制必须先除以 g）、算空气阻力与风阻功率、算顺风/逆风与相对速度（含「逆风代价 > 顺风收益」）、
  算横向力/升力/俯仰-横摆-侧倾力矩与压力中心、用阻力来源分解表（0.42 账本）定位「该改哪里」、
  判尾部倾角与卡曼-背的分离阈值、判横风敏感度（CP 与 NSP 的距离，只定性）、
  算滚动阻力（常数/线性/幂式/货车双式四选一）、查典型 f_r 表、判 f_r 的状态修正（温度/胎压/材料/侧偏）、
  算总道路负载与道路负载功率（力 ∝V²、功率 ∝V³）、以及把道路负载接到油耗（只按循环归因）。
  
  输出一律是**力/力矩/功率/系数**并附口径声明：全章英制（lb、ft、ft²、mph、hp、inHg、°F，
  g=32.2 ft/s²）；$\rho$ 必须是质量密度 lb·s²/ft⁴（标准 0.076 lb/ft³ = 0.00236 lb·s²/ft⁴，
  漏除 g 会高 32.2 倍）；$A$ 必须是**前端投影面积**（式 4-2、4-6~4-10 全用，不是侧面面积）；
  $V$ 在阻力式里用 ft/s、在 $f_r$ 经验式里用 mph（**1 mph = 1.466 ft/s**，即 ft/s = mph ÷ 0.682）；力矩必须乘轴距 $L$；
  坡度用 $\sin\theta$（% 坡度=100·tanθ）；道路负载**不含加速阻力**（惯性项属第 2 章）。
  
  强制声明四个全局前提：①三项阻力线性叠加只在**直线准稳态**成立（侧偏使 $f_r$ 翻倍、升力改
  $W_{eff}$、横风改 $C_D$）；②单值 $C_D$ 只在**零偏角**下成立（轿车典型偏角 +5%~10%）；
  $f_r$ 是状态量而非常数（需 20 mile/20 min 预热）；③**三仓隔离**——仓 A 72500 lb 货车
  （$\rho$=0.00207、$C_D$=0.65、$f_r$=0.00685 货车式）、仓 B 3650 lb 轿车（$f_r$=0.02 设定值、
  $A$=23.3、$C_D$=0.34、标准 $\rho$）、仓 C 未知车（55 mph、$A$=21、$C_D$=0.42、标准 $\rho$），
  $\rho$ 不跨仓、仓 C 的 0.42 与分解表的 0.42 纯属数值巧合严禁互引、仓 B 的 0.02 与「牵引车 0.02」
  同值不同义；④油耗只能按循环归因，$\Delta C_D$ 不可线性外推成 $\Delta$mpg。
  
  不适用于：$C_D$ 的估算法与六力系数的求法（本章明确要风洞/滑行/试验，无估算式）、横风敏感度的
  任何数值（式(4-11) 分母 OCR 损坏，只能给方向）、油耗的定量百分比与图 4.37 的逐柱数值（OCR 混排 +
  "车重=136 kg"讹误）、例题 1 的油耗链（215 hp×0.35=75.3 lb/h vs 书印 82.6 lb/h，不闭合）、
  式(4-15) 的 $f_o$/$f_s$（需图 4.34，读数缺失）、式(4-13) 的载荷律（与 $R_x\propto W^2$ 冲突）、
  图 4.8 的车型↔$C_L$/$C_D$ 配对（OCR 错行）、图 4.12 的 ΔC_D（读数缺失）、
  湿度对密度的修正（式(4-3a)(4-3b) 不含湿度）、加速阻力与第 2 章加速性能、
  侧倾转向/轮胎侧偏刚度的定量（第 6 章）、温升与传动系效率、ECE/GB 法规。
  
  Triggers: 道路负载/road load/风阻/空气阻力/aerodynamic drag/drag force/空气密度/air density/
  迎风面积/frontal area/风阻系数/C_D/C_DA/风阻功率/drag horsepower/顺风/逆风/headwind/tailwind/
  相对风/relative wind/侧向力/side force/升力/lift/俯仰力矩/pitch moment/横摆力矩/yaw moment/
  侧倾力矩/rolling moment/压力中心/center of pressure/CP/NSP/横风敏感度/crosswind sensitivity/
  横摆率响应/yaw rate response/滚动阻力/rolling resistance/滚阻系数/f_r/滚阻系数表/路面系数/C_h/
  沙地/sand/越野/off-road/胎压/tire pressure/吃胎/磨耗/总道路负载/道路负载功率/road load power/
  坡阻/爬坡阻力/grade/风阻滚阻交叉点/降阻/降风阻/spoiler/扰流器/卡曼背/Kamm-back/尾部倾角/
  油耗/mpg/fuel economy/EPA 循环/BSFC
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch4-road-loads
  cangjie.capability-count: 14
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 4 章 道路负载 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- $C_D$、$C_S$、$C_L$、$C_{PM}$、$C_{YM}$、$C_{RM}$、$f_o$、$f_s$ 的求法（本章明确要风洞/滑行/试验，无估算法）
- 横风敏感度 $r/\alpha$ 的任何数值（式(4-11) 分母 OCR 损坏，只能给方向与杠杆）
- 油耗的定量百分比、图 4.37 的逐柱百分数（OCR 混排 + "车重=136 kg"讹误）、循环级积分
- 例题 1 的油耗链数值（215 hp×0.35=75.3 lb/h vs 书印 82.6 lb/h，不闭合，登记为 NR-03）
- 式(4-15) 的 $f_o$、$f_s$ 数值（需图 4.34，读数缺失）；图 4.12 的 ΔC_D（读数缺失）；图 4.8 的车型↔系数配对（OCR 错行）
- 湿度对空气密度的修正（式(4-3a)(4-3b) 只含 P、T）
- 式(4-13) 的载荷律（"随载荷线性"与 $R_x\propto W^2$ 冲突，标 conflict 不采用）
- 加速阻力与第 2 章加速性能；制动/驱动工况下的滚阻矢量合成（第 5/6 章）
- 侧倾转向、轮胎侧偏刚度、悬架运动学的定量（第 6/7 章）；ABS/ESC/主动气动的策略
- 温升、传动系效率、发动机万有特性、附件功率；ECE/GB 法规合规

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 全章一根主链：密度/动压 → 风阻与六力 → 阻力账 → 滚阻及其五个状态修正 → 总道路负载 → 功率 → 油耗。任何一环的口径错都不会自曝，只会给出「看起来像对的数」。
2. 力对速度是二次，功率是三次——所以「多开 5 mph」的代价必须按 V³ 算；但总道路负载功率的实际倍数低于风阻分量的三次，两个百分比不可互换。
3. 三个参考量各有一个静默陷阱：$\rho$ 忘除 g（×32.2）、$A$ 用侧面面积（×3 起）、$V$ 用 mph（÷1.47）。三者都落在"像合理值"的区间里，只能靠口径检查抓。
4. 阻力账里后部 0.14 是最大单项（33%），轮坑 0.09 排第二（21%）——按投影面积分摊会严重低估车轮；降阻必须与横风/升力代价成对记账。
5. $f_r$ 不是常数而是状态量：温度（20 mile 预热）、胎压（最优取决于路面）、速度（低速线性、高速 ∝V^2.5）、材料（磨胎 −20%/叠层 +25%）、侧偏（几度翻倍）五项全部只能给方向与量级。
6. 阻力系数与经验式必须与标定域配套：同一车速下轿车线性式与货车双式差 2.4 倍；$C_h$ 是乘子不是加项；常数 $f_r$ 在适用区间内是作者推荐的正解。
7. 横风敏感度由「CP 与 NSP 的距离」与速度共同决定，不是侧向力的大小；式(4-11) 分母残缺，因此本章只能定性。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 由温度气压算空气密度；高原/高温下风阻小多少；密度要不要除以 32.2；英制与公制的密度式怎么对齐 | references/capabilities/air-density-and-standard-atmosphere.md | references/capabilities/aero-drag-and-power.md、references/capabilities/road-load-and-power.md |
| 算空气阻力与所需马力；C_D 0.3、面积 2.2 平米，风阻多少；为什么风阻算出来大得离谱；侧面面积能不能算风阻；风洞 C_D 和路上差多少 | references/capabilities/aero-drag-and-power.md | references/capabilities/air-density-and-standard-atmosphere.md、references/capabilities/wind-relative-velocity-and-asymmetry.md、references/capabilities/road-load-and-power.md、references/capabilities/drag-source-breakdown-and-modifications.md |
| 逆风风阻多少；顺风能省多少；顺逆风是不是能互相抵消；平均风速算平均阻力对不对；25 mph 逆风车跑 55 mph | references/capabilities/wind-relative-velocity-and-asymmetry.md | references/capabilities/aero-drag-and-power.md、references/capabilities/crosswind-sensitivity-and-tradeoff.md、references/capabilities/road-load-and-power.md、references/capabilities/fuel-economy-chain-and-attribution.md |
| 侧向力多大；横风把车推多狠；升力多少磅、发飘是不是升力；侧向力系数斜率怎么取；侧风 20 度时侧向力与风阻谁大 | references/capabilities/lateral-force-and-lift.md | references/capabilities/aero-moments-and-pressure-center.md、references/capabilities/aero-drag-and-power.md、references/capabilities/crosswind-sensitivity-and-tradeoff.md |
| 横摆力矩/俯仰力矩/侧倾力矩多少；压力中心在哪；力矩要不要乘轴距；气动抬头会不会改变不足转向；这个力矩作用在哪个点 | references/capabilities/aero-moments-and-pressure-center.md | references/capabilities/lateral-force-and-lift.md、references/capabilities/crosswind-sensitivity-and-tradeoff.md |
| 想降风阻先改哪里；0.42 的分解怎么读；后部是不是最大、轮坑占多少；加尾翼/扰流板能不能降风阻；细节优化累计 21% 值多少 | references/capabilities/drag-source-breakdown-and-modifications.md | references/capabilities/tail-shape-and-separation-limit.md、references/capabilities/aero-drag-and-power.md、references/capabilities/crosswind-sensitivity-and-tradeoff.md |
| 后窗倾角多少合适；尾部越斜越省油吗；卡曼背是什么、什么时候用；倾角 20 度会不会分离；15 度是不是硬阈值 | references/capabilities/tail-shape-and-separation-limit.md | references/capabilities/drag-source-breakdown-and-modifications.md、references/capabilities/crosswind-sensitivity-and-tradeoff.md |
| 这车横风稳不稳；侧风为什么总要修方向；降阻会不会让横风变差；压力中心该往前还是往后；横摆率响应能不能当指标 | references/capabilities/crosswind-sensitivity-and-tradeoff.md | references/capabilities/aero-moments-and-pressure-center.md、references/capabilities/lateral-force-and-lift.md、references/capabilities/drag-source-breakdown-and-modifications.md |
| 这车滚阻多少磅；滚阻要不要用动态轴荷；弯道滚阻怎么算；滚阻和摩擦有什么区别；滚阻系数是不是力 | references/capabilities/rolling-resistance-baseline.md | references/capabilities/rolling-resistance-coefficient-models.md、references/capabilities/rolling-resistance-state-corrections.md、references/capabilities/road-load-and-power.md |
| f_r 该用哪个公式；滚阻系数取多少；热沥青比混凝土高多少；子午线比斜交低多少；C_h 是乘还是加 | references/capabilities/rolling-resistance-coefficient-models.md | references/capabilities/rolling-resistance-baseline.md、references/capabilities/rolling-resistance-state-corrections.md、references/capabilities/road-surface-and-offroad-friction.md |
| 实测 f_r 为什么比手册高/低；短途工况该取哪个 f_r；沙地要不要放气、硬路打多少；弯道多的路线为什么油耗算不准；低滚阻胎值不值得、磨胎是不是省油 | references/capabilities/rolling-resistance-state-corrections.md | references/capabilities/rolling-resistance-baseline.md、references/capabilities/rolling-resistance-coefficient-models.md、references/capabilities/road-surface-and-offroad-friction.md |
| 沙地滚阻系数多少；越野油耗为什么这么高；典型滚阻表怎么查；重卡滚阻比轿车高吗；热沥青/磨损路面高多少 | references/capabilities/road-surface-and-offroad-friction.md | references/capabilities/rolling-resistance-coefficient-models.md、references/capabilities/rolling-resistance-state-corrections.md、references/capabilities/road-load-and-power.md |
| 80 mph 巡航要多少马力；道路负载是多少磅；多开 10 mph 多费多少功率；风阻和滚阻从多少速度开始交叉；上坡 5% 多耗多少 | references/capabilities/road-load-and-power.md | references/capabilities/aero-drag-and-power.md、references/capabilities/rolling-resistance-baseline.md、references/capabilities/fuel-economy-chain-and-attribution.md、references/capabilities/air-density-and-standard-atmosphere.md |
| 降风阻能省多少油；C_D 降 0.02 值不值；城市和高速哪个更省；为什么降阻百分比不等于省油百分比；mpg 怎么从道路负载算 | references/capabilities/fuel-economy-chain-and-attribution.md | references/capabilities/road-load-and-power.md、references/capabilities/aero-drag-and-power.md、references/capabilities/rolling-resistance-baseline.md |

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

- 缺 $C_D$（或 $C_S$/$C_L$ 等系数）时停止任何气动力/力矩计算——本章不给估算法，猜一个等于编造。
- 缺 $A$ 或用户给的 $A$ 明显是侧面/表面积（轿车 >30 ft²）时停止：先确认是前端投影面积。
- 用户要求把 $\rho$ 用 lb/ft³ 代入式(4-2)、或要求「湿度修正」时停止：前者差 32.2 倍，后者本章无该项。
- 用户要求横风敏感度的数值/排名/验收阈值时停止：式(4-11) 分母残缺，只能给方向与杠杆。
- 用户要求「降 x% $C_D$ 省 y% 油」或任何单一换算系数时停止：只能按循环给方向。
- 用户要求引用图 4.12/4.34/4.37 或图 4.8 的读数时停止：读数缺失/错行，只能给定性。
- 工况为转弯、制动、驱动、强侧风或瞬态阵风时，停止套用「三项线性叠加 + 直线 $f_r$」，声明出界。
- 缺 $f_r$ 的层级与出处时停止：四套式子差 2.4 倍，选式即是选数。
- 用户要求把某一仓的 $\rho$/$C_D$/$f_r$ 用到另一仓时停止：三仓隔离是硬性口径。
