---
name: vehicle-steering-system
description: |
  当用户处理汽车「转向系统」问题时调用：由转向盘转角算车轮转角（设计比 vs 实测比，实测≈设计 2 倍）、
  算阿克曼内外轮转角并判梯形能否逼近、判阿克曼/平行转向的低速自定心力矩行为、判转向几何误差方向
  （纵向偏移→前束变化、垂向偏移→侧倾转向）、由 ε 算侧倾转向的不足转向贡献、算内倾项垂直力力矩 $M_V$、
  算侧向力经后倾的力矩与回正力矩沿转向轴的分量、算牵引力经主销偏距的力矩并区分驱动/制动/内侧制动的力臂、
  算柔顺性不足转向增量 $K_{strg}=W_f(r\nu+p)/K_{ss}$ 并换算转向盘/车轮两个口径、判制动时轮胎后倾效应的翻向
  与制动力不平衡的 2–3 倍放大、分解前驱五机制并求净效果、算四轮转向半径与判低速反向/高速同向。
  
  输出一律是**角度 / 力矩 / deg·g⁻¹ / 半径**并附口径声明：单位口径（全章英制：lb、in、in·lb、deg、rad；
  $\nu$ 与 $\lambda$ 公式内用 rad）、传动比口径（设计 / 实测）、不足转向梯度口径（转向盘 / 车轮 + 传动比来源 +
  工况）、$W_f$ 的「每 g 前轮载荷」读法（式 8-8 的量纲必需，原文未明说）、$K_{ss}$ 的取值（式 8-8 对其极敏感：
  600→4.76、900→3.17 deg/g）、$\xi_{4WS}$ 的符号约定（叠加口径反相位为正 / SAE 口径反相为负，两者不得混）。
  强制声明五个全局前提：①术语上 $M_V$（几何自定心力矩）≠ $M_z$（轮胎回正力矩）；②式(8-4) 第二项 $\sin\delta$/$\cos\delta$
  冲突未决 → 后倾项定量不可用；③式(8-17) 残缺 → 轨迹偏移严禁补全，只给 $\xi=0$ 与 $\xi=1$ 两个边界；
  ④图 8.18/8.19/8.20/8.24/8.25 无数据表 → 零读数；⑤小角度近似原文从未给角度上限。
  
  不适用于：转向系统摩擦/间隙/滞回与转向手感的主观评价（本章只有「厂商评估」一句，模型定位为低频集中刚度）、
  EPS / 线控转向 / 主动前轮转向的失效模式（1992 年文本）、轮胎松弛长度与瞬态侧偏（第 9 章）、
  轨迹偏移（内轮差）的定量、「低/高制动系数」的分界值与「制动时降低百分之几」、理想运动中心点的作图步骤、
  4WS 对侧倾/侧翻裕度与极限转向储备的影响（本章无原文）、$\varepsilon$/$d\phi/da_y$/$K_{ss}$/$p$/$F_y$/$M_z$
  的典型值与测量方法、任何法规条款（本章无）。
  
  Triggers: 转向传动比/steering ratio/方向盘转多少/阿克曼/Ackermann/内外轮转角/梯形布置/平行转向/自定心力矩/
  self-centering torque/主销内倾/kingpin inclination/磨胎半径/scrub radius/偏距/后倾角/caster/回正力矩/
  aligning torque/拖矩/pneumatic trail/前束变化/bump steer/侧倾转向/roll steer/理想中心点/instant center/
  柔顺性/compliance/转向刚度/Kss/不足转向梯度/understeer gradient/deg/g/150 deg/g/4 deg/g/制动跑偏/brake steer/
  split-mu/对开路面/负偏距/torque steer/力矩转向/前驱/FWD/五机制/差速器摩擦/四轮转向/4WS/rear steer/
  counter-phase/in-phase/ξ/转弯半径/后轮 5°。
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch8-steering-system
  cangjie.capability-count: 11
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 8 章 转向系统 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 转向系统摩擦、间隙、滞回与转向手感的主观评价方法（本章只有「由车辆制造商评估」一句；§8.6 明确为低频集中刚度模型）
- EPS / 线控转向 / 主动前轮转向 / 扭矩矢量的失效模式与控制策略（1992 年文本，无此内容）
- 转向系统部件的疲劳、强度、NVH、齿轮齿条参数设计
- 轮胎松弛长度、瞬态侧偏、高频方向响应（第 9 章；本章全部准静态）
- 四轮转向轨迹偏移（内轮差）的定量（式 8-17 残缺，严禁补全）
- 「低/高制动系数」的分界值与「制动时稳定效果降低百分之几」（只存在于图 8.20，无文字数值）
- 理想运动中心点的作图步骤（变形圆/哈特曼/鲍勃利尔只有名称与文献号）
- 4WS 对侧倾/侧翻裕度、极限转向储备的影响（本章无原文，须第 9 章另行提取）
- $\varepsilon$、$d\phi/da_y$、$K_{ss}$、$p$、$F_y$、$M_z$ 的典型值、测量方法与车型分布（原书全无）
- 任何法规条款与合规判定（本章不含 FMVSS/ECE/GB）

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 驾驶员转的是转向盘、车响应的是车轮转角，两者之间隔着传动比（实测恒大于设计，货车 37→76）、杆系几何、悬架位移、转向轴倾角、轮胎力矩与柔顺性；本章就是逐项算清「设计值被改了多少」。
2. 全章只有一根主链：传动比 → 阿克曼 → 悬架耦合（前束变化/侧倾转向）→ 转向轴力矩 → 柔顺性 → 特例（制动/前驱）→ 主动扩展（4WS）。跳步得到的是算术结果，不是诊断结论。
3. 口径先于数值：转向盘口径 vs 车轮口径（同一辆车 150/4/≈0）、设计传动比 vs 实测传动比、$K_{ss}$ vs $K_\phi$、$M_V$ vs $M_z$、$\xi_{4WS}$ vs 别章 $\xi$ —— 每一条都能静默出错且不报警。
4. 方向比大小重要：侧倾转向的符号、后倾项在制动时翻向、前驱五机制的净方向——符号错一次，后续所有数值都无意义。
5. 硬伤必须随结论走：凡依赖式(8-4) 第二项、式(8-17)、式(8-9)~(8-12) 力臂或无数据表的图的定量结论，一律不得作为正确结论发布。
6. 「不可避免」是本章的基调：几何误差不可避免、柔顺性必然存在、力矩转向可减轻不可消除——所以交付物只能承诺方向与量级，不能承诺消除。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 由转向盘转角算车轮转角；泊车打满几圈、最小转弯半径校核；手算结果与实车手感对不上；换胎/改装后转向变快变慢；判断报告里的传动比是设计值还是实测值 | references/capabilities/steering-ratio-and-wheel-angle.md | references/capabilities/ackermann-wheel-angles-and-low-speed-torque.md、references/capabilities/compliance-understeer-and-basis.md、references/capabilities/four-wheel-steering-radius-and-phase.md |
| 算内外轮转角与差角；阿克曼率能做到多少、球头放内侧还是外侧；满舵方向盘先沉后突然变轻；原地打方向回正力不够；用优化阿克曼治高速推头（应被拦住） | references/capabilities/ackermann-wheel-angles-and-low-speed-torque.md | references/capabilities/steering-ratio-and-wheel-angle.md、references/capabilities/kingpin-inclination-self-centering-moment.md、references/capabilities/roll-steer-gradient.md |
| 过坎/进弯跑偏、定位全绿仍吃胎；判断是前束变化还是侧倾转向；改球头高低能不能治推头；换件无效的跑偏是否运动学误差；理想中心点怎么求 | references/capabilities/steering-geometry-error-direction.md | references/capabilities/roll-steer-gradient.md、references/capabilities/caster-and-aligning-torque.md、references/capabilities/ackermann-wheel-angles-and-low-speed-torque.md |
| 由实测侧倾转向曲线算 K 贡献；侧倾转向与轮胎/柔顺性贡献谁大；改悬架硬点后不足转向变多少；纠正把 ε 直接当 deg/g 的报法；侧倾刚度变化对这一项的影响 | references/capabilities/roll-steer-gradient.md | references/capabilities/steering-geometry-error-direction.md、references/capabilities/compliance-understeer-and-basis.md |
| 原地打方向为什么越打越沉；回正力矩有多大（低速）；主销内倾角/偏距改大改小的影响；转向系统力矩账里内倾项占多少；区分自定心力矩与轮胎回正力矩 | references/capabilities/kingpin-inclination-self-centering-moment.md | references/capabilities/caster-and-aligning-torque.md、references/capabilities/ackermann-wheel-angles-and-low-speed-torque.md、references/capabilities/tractive-force-and-brake-lever.md |
| 正后倾角带来多少不足转向力矩；侧向力怎么折算成方向盘力矩；回正力矩沿转向轴损失多少；高速稳定性靠后倾角吗；力矩账里侧向力项与回正力矩项各占多少 | references/capabilities/caster-and-aligning-torque.md | references/capabilities/kingpin-inclination-self-centering-moment.md、references/capabilities/braking-caster-and-split-mu.md、references/capabilities/tractive-force-and-brake-lever.md |
| 对开路面刹车往一边跑；大油门方向盘被拽（torque steer）方向判读；负偏距能不能治制动跑偏；制动/驱动/内侧制动的力臂怎么取；转向力矩账里牵引力项是否应为零 | references/capabilities/tractive-force-and-brake-lever.md | references/capabilities/braking-caster-and-split-mu.md、references/capabilities/caster-and-aligning-torque.md、references/capabilities/fwd-five-mechanisms.md |
| 实测比理论大一个数量级怎么解释；150 deg/g 与 4 deg/g 哪个是真的；柔顺性对不足转向贡献多少；换硬衬套/改后倾角能减多少推头；报告里的 K 是转向盘口径还是车轮口径 | references/capabilities/compliance-understeer-and-basis.md | references/capabilities/steering-ratio-and-wheel-angle.md、references/capabilities/roll-steer-gradient.md、references/capabilities/caster-and-aligning-torque.md、references/capabilities/fwd-five-mechanisms.md |
| 急刹/ABS 介入时方向不稳；对开路面制动跑偏有多严重；加大后倾角能不能治制动跑偏；轮胎拖矩怎么换算成等效后倾角；负偏距值不值得（代价是什么） | references/capabilities/braking-caster-and-split-mu.md | references/capabilities/tractive-force-and-brake-lever.md、references/capabilities/caster-and-aligning-torque.md、references/capabilities/fwd-five-mechanisms.md |
| 前驱大油门推头还是甩尾；torque steer 归因与缓解；4–5 deg/g 怎么来的、能不能对账；差速器摩擦对前驱转向的影响；FWD 与 RWD 的转向差异归因 | references/capabilities/fwd-five-mechanisms.md | references/capabilities/tractive-force-and-brake-lever.md、references/capabilities/compliance-understeer-and-basis.md、references/capabilities/braking-caster-and-split-mu.md |
| 四轮转向半径能小多少；低速反向还是高速同向、怎么切；后轮转角 5° 限制的影响；4WS 高速收益是否被夸大；轨迹偏移/内轮差能不能算 | references/capabilities/four-wheel-steering-radius-and-phase.md | references/capabilities/ackermann-wheel-angles-and-low-speed-torque.md、references/capabilities/steering-ratio-and-wheel-angle.md |

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

- 缺传动比口径（设计值/实测值）时停止任何「转向盘↔车轮」换算；不得用设计比代替实测比，也不得在实测比上再叠 2 倍修正。
- 缺 $K_{ss}$ 时停止式(8-8) 计算：结果对 $K_{ss}$ 成反比（600→4.76、900→3.17、450→6.34 deg/g），猜值等于给错数。
- 缺 $\varepsilon$ 或 $d\phi/da_y$ 时停止侧倾转向的定量：原书无 $\varepsilon$ 的任何数值，$d\phi/da_y$ 不在本章。
- 需要式(8-4) 第二项（后倾项）或式(8-9)~(8-12) 力臂的定量时停止，只给定性；前者 $\sin\delta$/$\cos\delta$ 冲突，后者 $\lambda+\zeta$ 力臂与「$\zeta=0$ 时力臂 $=d$」不自洽。
- 需要四轮转向轨迹偏移数值时停止：式(8-17) 只剩 $L^2(1-\ ^2)$，只可给 $\xi=0$ 退化为式(6-4)、$\xi=1$ 为 0 两个边界，严禁补全。
- 要求「低/高制动系数的分界值」「制动时后倾角降低几度/百分之几」时停止：无文字数值，图 8.20 无数据表。
- 要求从图 8.7/8.18/8.19/8.20/8.24/8.25 读出任何数值时停止（无数据表，零读数）；只能引正文文字给出的数（37/76、150/4/≈0、4°–8°、2–3 倍、4–6、4–5）。
- 需要理想运动中心点的手算步骤时停止：原文只给工具名（变形圆/哈特曼/鲍勃利尔/CAD），只能交付「方向 + 该改哪里」。
- 要求把「4–5 deg/g」当精确值、或与其他来源的 deg/g 做减法对账时停止：那是取整汇总，逐项和 3.0–4.5。
- 要求 4WS 对侧翻裕度、极限操稳储备的结论时停止：本章无据，须第 9 章。
- 要求「精确到 0.1 deg/g 的净不足转向」或「精确放大倍数」时停止：五机制与 2–3 倍均为估计量级，精度只到 ±1 deg/g 级。
