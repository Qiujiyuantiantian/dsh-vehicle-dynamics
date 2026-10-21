---
name: vehicle-acceleration-performance
description: |
  当用户处理乘用车/商用车「加速性能」问题时调用：判断加速受功率限制还是附着限制（含交叉车速）、
  由扭矩表算功率或反算扭矩、用比功率粗估加速度上限、按三级精度选算法（粗估/单点/逐速度迭代）、
  由发动机扭矩经总速比与效率折算轮上驱动力、把有效转动惯量换成等效质量/等效重量/质量系数、
  做挡位-转速-车速换算、做整车纵向力平衡、画/复核驱动力-车速图与等功率包络、
  校验传动比等比级数、求最佳换挡点、判变矩器起步放大、算纵向载荷转移、
  算驱动扭矩引起的横向载荷转移、算开放式差速器的附着极限（单轮封顶）、
  算锁止差速器/独立悬架驱动轴的附着极限、算前驱附着极限、以及做前驱与后驱的同参数对比与差异归因。
  
  输出一律是**力/加速度/等效重量/载荷**并附口径声明：全章英制（lb、ft、in、psi、ft/s²、hp，
  g=32.2 ft/s²；半径用 in 时 g=386 in/s²）、$a_x$ 取正、功率取稳态 $P_{\max}$、
  $\eta_{tf}$ 采用例题部件级口径（1 挡 0.966×0.99=0.95634；正文 80–90% 与之差 6–16 点，未裁定）、
  附着支分母的 $N_{ft}$ 一律读作 $N_f\cdot t$（主减比 × 轮距，不是总传动比 $N_{tf}$）、
  质量系数只报实算值（1 挡 1.351），式(2-12) 的 1.89 与表值 1.50 只作对照且须标来源。
  
  强制声明四个全局前提：①准静态（$F_x$、$R_x$、$D_A$ 都随车速变，单点结果不代表整段）；
  ②$\mu$ 取单值、与载荷/滑移率无关（与第 3 章的载荷敏感性冲突，本章内部矛盾）；
  ③开放式差速器按理想等分扭矩建模，锁止只有两态、无锁止率连续值；
  ④1 挡"88 ft/s（60 mph）"是 OCR 错误（复算 38.7 ft/s / 26.4 mph），凡依赖它的结论一律作废。
  
  不适用于：0–60 mph 的工程级预测（误差可 >10%）、最高车速的数值（本章无滚阻/风阻表达式，缺口 G-2）、
  变矩器 TR–SR 曲线与锁止条件（缺口 G-3）、质量系数的经验式外推（缺口 G-1）、
  前驱/后驱的受控布局优劣（缺口 G-4，两例题不可相减）、图 2.1/2.2/2.4–2.9 的曲线读数（无数据表）、
  四驱的轴间扭矩分配、μ-split、锁止率连续值、轮胎滑移与瞬态换挡、
  以及"气门常开→泵气损失消失"这类第 3 章内容（本章零命中）。
  
  Triggers: 加速性能/加速能力/acceleration performance/功率限制/power limited/附着限制/traction limited/
  交叉车速/比功率/power-to-weight/0-60/加速时间/有效转动惯量/effective inertia/等效质量/effective mass/
  质量系数/mass factor/驱动力/tractive force/驱动力图/tractive effort curve/等功率线/power envelope/
  换挡点/shift point/等比级数/geometric ratio/液力变矩器/torque converter/失速/stall/
  载荷转移/weight transfer/横向载荷转移/lateral weight transfer/差速器锁止/locking differential/
  独立悬架/independent suspension/前驱/后驱/FWD/RWD/附着极限/traction limit/每轮驱动力/打滑/wheel spin
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch2-acceleration
  cangjie.capability-count: 20
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 2 章 加速性能 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 0–60 mph / 0–100 km/h 的工程级预测（准静态 + 稳态扭矩 + 无换挡耗时，误差可 >10%）
- 最高车速的数值交付（本章无滚阻、风阻表达式；图 2.4/2.6 无数据表，缺口 G-2）
- 液力变矩器的 TR–SR 曲线、锁止接合条件与失速转速（原文只在图上标"锁止"，缺口 G-3）
- 质量系数经验式（式 2-12）的适用范围与拟合来源（三值冲突未裁定，缺口 G-1）
- 前驱 vs 后驱的受控布局优劣结论（两例题参数全不同，缺口 G-4）
- 图 2.1/2.2/2.4/2.5/2.6/2.7/2.8/2.9 的曲线读数（无数据表，只可给读图判据）
- 四驱的轴间扭矩分配、左右 μ 不等（μ-split）、差速器锁止率的连续值、LSD 预紧力矩
- 轮胎滑移/瞬态换挡/离合器打滑、附件惯量、CVT 与电驱的连续变速
- 滚阻系数、风阻系数、μ(V)/μ(p)/μ(T) 的取值方法与解析式（全部推到"下一章"）
- 第 3 章内容误植：气门常开→泵气损失消失一类的发动机制动（本章 707 行零命中，属第 3 章）

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 加速有两个天花板：功率支 ∝1/V 随车速下降，附着支与车速无关；实际加速度是两者取小，交点就是分诊车速。
2. 传动比放大扭矩一次、放大惯量两次：低挡的收益与代价是同一件事，1 挡让 2500 lb 的车"变重"877 lb（+35%）。
3. 附着极限不是 μ×车重，而是 μ×驱动轮当时载荷；而载荷又被驱动力改变，所以 F 出现在自己的分母里，必须解自洽方程。
4. 附着支四分支（锁止/不锁止 × 前驱/后驱）不能混用：例 2.4-1 不锁止 1201 lb、锁止 1305 lb（差 104 lb）；前驱符号写错会高 25%。
5. 横向载荷转移是纯损失，纵向载荷转移对后驱是红利、对前驱是罚金；两者是独立通道，不会互相抵消。
6. 两态判据："锁止"与"该轴为独立悬架"是两条独立的充分条件，殊途同归到分母第三项消去；但锁止后 $W_y$ 仍然存在，消失的只是它造成的损失。
7. 全章英制且无换算表；$N_{ft}=N_f\cdot t$ 与 $N_{tf}=N_tN_f$、$b$ 与 $c$、in 配 386 与 ft 配 32.2——口径错不会自曝，只会给出"看起来像对的数"。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 判断当前加速受功率还是附着限制；加马力有用还是换抓地胎有用；交叉车速是多少；低速打滑是轮胎问题还是动力问题；0-60 落在哪条限制上 | references/capabilities/acceleration-limit-triage.md | references/capabilities/specific-power-acceleration-limit.md、references/capabilities/traction-limit-decision-tree.md、references/capabilities/acceleration-precision-ladder.md |
| 这个加速度大概能算到什么精度；只有功率和车重能不能估 0-60；手算够不够还是必须仿真；两份加速度结果差 1.4 倍哪个对；需要哪些输入才能算加速时间 | references/capabilities/acceleration-precision-ladder.md | references/capabilities/specific-power-acceleration-limit.md、references/capabilities/drivetrain-force-from-engine-torque.md、references/capabilities/longitudinal-force-balance.md |
| 扭矩换算成功率；5252 是什么；由最大功率反算扭矩；hp 换成 kW；最大功率点和最大扭矩点哪个先到 | references/capabilities/power-torque-rpm-conversion.md | references/capabilities/specific-power-acceleration-limit.md、references/capabilities/tractive-effort-map-and-envelope.md、references/capabilities/chapter-units-and-conventions.md |
| 比功率粗估加速能力；大概几个 g；匝道加速段要多长；长坡速度损失；功率重量比怎么用 | references/capabilities/specific-power-acceleration-limit.md | references/capabilities/acceleration-limit-triage.md、references/capabilities/longitudinal-force-balance.md、references/capabilities/acceleration-precision-ladder.md |
| 轮上驱动力怎么算；某一挡的驱动力是多少；低挡为什么推背强但加速度不如预期；改终传比后驱动力变多少；效率要不要乘进去 | references/capabilities/drivetrain-force-from-engine-torque.md | references/capabilities/effective-inertia-to-equivalent-weight.md、references/capabilities/longitudinal-force-balance.md、references/capabilities/tractive-effort-map-and-envelope.md |
| 有效转动惯量怎么算；等效质量/等效重量是多少；质量系数是几；为什么一挡最有劲；换大轮毂有效质量怎么变 | references/capabilities/effective-inertia-to-equivalent-weight.md | references/capabilities/drivetrain-force-from-engine-torque.md、references/capabilities/longitudinal-force-balance.md、references/capabilities/chapter-units-and-conventions.md |
| 这个转速对应多少车速；几挡多少码；一挡能跑到多快；齿比与车速的换算；88 ft/s 对不对 | references/capabilities/gear-speed-and-omega-scaling.md | references/capabilities/drivetrain-force-from-engine-torque.md、references/capabilities/tractive-effort-map-and-envelope.md、references/capabilities/acceleration-limit-triage.md |
| 加速度怎么从驱动力算；滚阻要不要减；上坡掉多少加速；拖挂车影响多大；加速阻力该放哪 | references/capabilities/longitudinal-force-balance.md | references/capabilities/drivetrain-force-from-engine-torque.md、references/capabilities/effective-inertia-to-equivalent-weight.md、references/capabilities/acceleration-precision-ladder.md |
| 驱动力图怎么画；这条驱动力曲线对不对；等功率线是什么；最高车速在哪里；后备驱动力有多少 | references/capabilities/tractive-effort-map-and-envelope.md | references/capabilities/gear-speed-and-omega-scaling.md、references/capabilities/shift-point-at-force-intersection.md、references/capabilities/drivetrain-force-from-engine-torque.md |
| 齿比配得匀不匀；级距/换挡落差是多少；等比级数怎么算；为什么二挡到三挡落差小；齿比怎么排 | references/capabilities/geometric-ratio-series.md | references/capabilities/shift-point-at-force-intersection.md、references/capabilities/tractive-effort-map-and-envelope.md |
| 多少转换挡最快；红线换挡对不对；最大扭矩点换挡行不行；换挡点怎么定；改齿比后换挡点怎么变 | references/capabilities/shift-point-at-force-intersection.md | references/capabilities/tractive-effort-map-and-envelope.md、references/capabilities/geometric-ratio-series.md、references/capabilities/power-torque-rpm-conversion.md |
| 变矩器放大几倍；自动挡起步为什么快；变矩器锁止是什么；起步扭矩能乘 2 吗；失速转速多少 | references/capabilities/torque-converter-start-boost.md | references/capabilities/drivetrain-force-from-engine-torque.md、references/capabilities/locked-or-independent-drive-axle.md |
| in·lb·s² 怎么换；386 还是 32.2；mph 换 ft/s；kW 换马力；单位对不上/量纲检查 | references/capabilities/chapter-units-and-conventions.md | references/capabilities/power-torque-rpm-conversion.md、references/capabilities/effective-inertia-to-equivalent-weight.md、references/capabilities/gear-speed-and-omega-scaling.md |
| 附着极限最大驱动力多少；几 g 起步；差速器锁不锁差多少；前驱/后驱附着极限怎么算；打滑时最大驱动力 | references/capabilities/traction-limit-decision-tree.md | references/capabilities/longitudinal-load-transfer.md、references/capabilities/lateral-load-transfer-from-drive-torque.md、references/capabilities/open-differential-traction-limit.md、references/capabilities/locked-or-independent-drive-axle.md |
| 加速时后轴压多少；前轴卸载多少；重心高度对轴荷的影响；上坡为什么前轮打滑；载荷转移怎么算 | references/capabilities/longitudinal-load-transfer.md | references/capabilities/traction-limit-decision-tree.md、references/capabilities/lateral-load-transfer-from-drive-torque.md、references/capabilities/open-differential-traction-limit.md |
| 横向载荷转移多少；左右轮载荷差多少；为什么后驱起步一侧打滑；侧倾刚度影响加速吗；第三项怎么算 | references/capabilities/lateral-load-transfer-from-drive-torque.md | references/capabilities/traction-limit-decision-tree.md、references/capabilities/longitudinal-load-transfer.md、references/capabilities/open-differential-traction-limit.md |
| 开放式差速器最大驱动力；单轮打滑另一轮还有多少；每轮多少力；不锁止怎么算；差速器把扭矩分给谁 | references/capabilities/open-differential-traction-limit.md | references/capabilities/traction-limit-decision-tree.md、references/capabilities/lateral-load-transfer-from-drive-torque.md、references/capabilities/locked-or-independent-drive-axle.md |
| 锁止差速器能提升多少；独立悬架为什么也有同样优势；锁止和独立悬架是一回事吗；横向载荷转移是不是消失了；第三项为什么能消去 | references/capabilities/locked-or-independent-drive-axle.md | references/capabilities/open-differential-traction-limit.md、references/capabilities/lateral-load-transfer-from-drive-torque.md、references/capabilities/traction-limit-decision-tree.md |
| 前驱能几 g；前驱附着极限怎么算；前驱为什么起步打滑；独立前悬算不算少一项；Wc/L 是什么意思 | references/capabilities/front-drive-traction-limit.md | references/capabilities/traction-limit-decision-tree.md、references/capabilities/fwd-vs-rwd-traction-comparison.md、references/capabilities/locked-or-independent-drive-axle.md |
| 前驱还是后驱加速好；哪个起步快；静态轴荷比重大是不是就强；同参数下前后驱差多少；两辆车数据能不能直接比 | references/capabilities/fwd-vs-rwd-traction-comparison.md | references/capabilities/front-drive-traction-limit.md、references/capabilities/traction-limit-decision-tree.md、references/capabilities/longitudinal-load-transfer.md |

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

- 用户给出 1 挡"88 ft/s（60 mph）"作输入时停止计算，先声明这是 OCR 错误（复算 38.7 ft/s / 26.4 mph；88 ft/s 需 10010 rpm 或 366 hp）。
- 缺驱动形式、差速器锁止状态或驱动轴型式（整体式/独立悬架）时停止附着支计算；不得默认"锁止"（高 8.7%）或"后驱符号"（高 25%）。
- 缺静态轴荷 $W_{fs}/W_{rs}$ 或 $h$、$L$ 时停止载荷转移与附着支；不得用"前后各半"代替。
- 缺 $N_f$ 与轮距 $t$ 时停止不锁止分支；不得用 $N_{tf}$ 代替 $N_{ft}=N_f t$（会把 1201 算成 1279）。
- 用户要求"0–60 mph 精确时间"或"最高车速"时停止，声明本章只有上限与交点判据，无法给工程级数值。
- 用户要求"踏板/变矩器锁止点""TR–SR 中间点""图 2.2/2.4/2.6 的曲线读数"时停止：无数据表，严禁编造。
- 用户要求"前驱一定比后驱强/弱"的结论时停止，只能给同参数对比与"静态份额不能单独外推"这条定性断言。
- 工况为瞬态（急加速打滑、换挡中断、热衰退、四驱扭矩矢量）时停止套用准静态公式，声明出界。
