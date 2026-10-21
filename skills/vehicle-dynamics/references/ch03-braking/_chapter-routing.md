---
name: vehicle-braking-performance
description: |
  当用户处理乘用车/商用车「制动性能」问题时调用：算制动距离与停车时间（含风阻闭式解）、
  算制动能量与峰值/平均功率、算减速时的前后轴动态载荷转移、算各轴最大制动力边界线与同时抱死点、
  画/读效能三角形与多工况交集、算配比线斜率与压力比例阀分段压力、逐压力点算制动系数与制动效率、
  判断哪个轴先抱死及其后果、固定配比无解时选机构（压力比例阀/载荷敏感阀/惯性阀/ABS）、
  判 FMVSS 105/121 减速度符合性、以及把非制动器阻力（滚阻 0.01 g、坡度 %→g）折成 g 并入 ΣF_x。
  
  输出一律是**力/减速度/距离/效率**并附口径声明：单位口径（全章英制：lb、ft、in、psi、ft/s²、hp，
  g=32.2 ft/s²）、$D_x$ 取正、有效减速段（不含反应时间与压力建立时间）、
  $\eta_b$ 的分母口径（式 3-33 的 $\mu_p$ 口径 vs 例题 3.12 的 $\max(\mu_f,\mu_r)$ 口径）。
  强制声明四个全局前提：①线性化（$\mu_p$ 与载荷无关——与 3.4.3 的 +10%→−0.01 冲突，本章内部矛盾）；
  ②$\eta_b$ 分母口径；③SN 口径（ASTM E274，SN=100μ，标准试验胎）；④$C_D$ 带量纲（lb·s²/ft²）。
  
  不适用于：温升与热容量计算（本章无传热模型）、瞬态与 ABS 循环的定量判读（阈值/升压率/频率原文全无）、
  抱死频次的定量估计（图 3.16 刻度对应丢失，只能定性）、踏板力增益的合格判定（图 3.17 阴影区无边界数值，
  严禁补造）、ECE R13 / GB 21670 合规、$D_{dt}$ 传动系阻力的定量、27 系数力矩模型的外推、
  EBD/ESC 的分配策略。
  
  Triggers: 制动距离/刹车距离/braking distance/停车时间/stopping time/制动能量/制动功率/brake energy/
  brake power/载荷转移/weight transfer/轴荷/最大制动力/抱死边界/lockup boundary/同时抱死/理想配比/
  效能三角形/配比图/proportioning/理想斜率/压力比例阀/500/0.3/感载阀/惯性阀/制动系数/braking coefficient/
  制动效率/ηb/brake efficiency/先抱死哪个轮/后轮抱死/前轮抱死/甩尾/横摆发散/ABS/FMVSS 105/FMVSS 121/
  滑动数/SN 81/滚动阻力/坡度/坡道制动/踏板力增益/制动配比设计流程
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch3-braking
  cangjie.capability-count: 19
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 3 章 制动性能 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 温升、热容量、制动器传热模型与热衰退曲线（本章只说「必要时加入」，无数值）
- ABS 循环的阈值、升压率、循环频率与滑移率的动态轨迹（原文全无；图 3.10/3.11 只有示意）
- 抱死频次的定量估计（图 3.16 的标签↔横轴对应丢失；只能定性）
- 踏板力增益的合格判定与「最佳区间」数值（图 3.17 阴影区无上下边界数值）
- ECE R13 / R13-H / GB 21670 与任何非美标合规
- 传动系阻力 $D_{dt}$ 的取值、$f_r$ 的路面/胎压/速度依赖表、$C_D$ 的取值方法、$\mu(V)/\mu(p)/\mu(T)$ 的解析式
- 27 系数制动力矩模型及其在 >650 °F 的外推
- EBD/ESC 的分配策略、线控制动、再生制动分流

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 制动的瓶颈不在制动器，而在「哪个轮先抱死」；整章的重心是把前后制动力按载荷转移配平，让抱死顺序可控。
2. 全章只有一根主链：载荷转移 → 各轴最大制动力 → 边界线交点（理想点）→ 效能三角形 → 机构选型 → 配比线斜率 → 抱死顺序 → 制动效率 → 人机。跳步得到的只是算术结果，不是设计结论。
3. 制动距离对初速是二次的、对减速度是一次倒数：降速永远比增力更有效；风阻在 60 mph 只值 1.7%，别把 1.7% 的项做成高保真。
4. 固定配比只有 1 个自由度，「无解」是几何过约束而非调参失败；出路只有增加自由度（折一次阀/感载阀/惯性阀/ABS）。
5. 抱死后果不对称：前轮抱死是能力归零（失转向但方向稳定），后轮抱死是方向发散（短轴距轿车不可救）——所以设计共识是取偏大前制动力，但那是两害相权，不是「安全」。
6. 制动效率是唯一的横向配平指标，但它没有验收阈值，且有两个互不等价的分母口径；跨口径比较无效，拿它立法/排名已由作者本人否证。
7. 全章英制且无换算表；$D_x$ 取正、$W_d$ 与 $W_{fs}$ 不可混、$F_b$ 在 3.1.2 与 3.3/3.7 两义、$C_D$ 带量纲——口径错不会自曝，只会给出「看起来像对的数」。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 算某初速下的制动距离与停车时间；速度加倍制动距离是不是加倍；高速制动要不要算风阻、算了差多少；由实测制动距离反算平均减速度 | references/capabilities/braking-distance-and-time.md | references/capabilities/brake-energy-and-power.md、references/capabilities/resistance-terms.md、references/capabilities/fmvss-compliance-screen.md |
| 算这辆车的制动效率、给逐压力点的效率表；为什么效率只有 88%、哪一轴拖后腿；表里的 μf=0.14 是不是说前轮在冰上；两种 ηb 分母口径有什么区别、能不能横比 | references/capabilities/brake-efficiency-table.md | references/capabilities/pressure-to-brake-force.md、references/capabilities/dynamic-load-transfer.md、references/capabilities/lockup-order-and-consequence.md、references/capabilities/proportion-line-slope.md |
| 我这套配比是前轮先抱还是后轮先抱；后轮抱死会甩尾吗、能不能忍；前轮抱死还能转向吗；湿路/满载下抱死顺序会不会翻转 | references/capabilities/lockup-order-and-consequence.md | references/capabilities/lockup-boundary-lines.md、references/capabilities/mu-peak-instability.md、references/capabilities/brake-efficiency-table.md、references/capabilities/proportion-design-workflow.md |
| 最大制动力线怎么画、抱死边界在哪；为什么不能直接用 μp 乘静态轴荷；换路面/换载荷边界怎么变；校验别人给的边界线方程 | references/capabilities/lockup-boundary-lines.md | references/capabilities/dynamic-load-transfer.md、references/capabilities/simultaneous-lockup-point.md、references/capabilities/effectiveness-triangle.md、references/capabilities/load-sensitivity.md |
| 制动配比设计要从哪一步开始、按什么顺序做；我算完了吗、还差哪些环节；评审要覆盖哪些项；这个问题该回到哪一步改 | references/capabilities/proportion-design-workflow.md | references/capabilities/dynamic-load-transfer.md、references/capabilities/lockup-boundary-lines.md、references/capabilities/effectiveness-triangle.md、references/capabilities/brake-efficiency-table.md |
| 减速时前轴增加多少载荷、后轴还剩多少；空载为什么更容易抱死；重心高度对制动的影响；后轮会不会离地 | references/capabilities/dynamic-load-transfer.md | references/capabilities/lockup-boundary-lines.md、references/capabilities/load-sensitivity.md、references/capabilities/brake-efficiency-table.md |
| 理想的前后制动力分配是多少、同时抱死点在哪；我的配比偏前还是偏后（用理想 k 比）；为什么固定配比不可能对所有路面理想；哪个压力点已经接近两轴同时到极限 | references/capabilities/simultaneous-lockup-point.md | references/capabilities/lockup-boundary-lines.md、references/capabilities/proportion-line-slope.md、references/capabilities/effectiveness-triangle.md |
| 这套固定配比能不能覆盖我的所有工况；效能三角形怎么画、多工况交集怎么求；怎么调都过不了是不是本来就无解；某路面能不能做到 0.75 g | references/capabilities/effectiveness-triangle.md | references/capabilities/lockup-boundary-lines.md、references/capabilities/no-solution-decision-tree.md、references/capabilities/proportion-line-slope.md |
| 我的配比线斜率是多少、怎么算；换了卡钳/盘径后配比会怎么变；装了比例阀后折线怎么画；0.3 是不是后轴制动力占 30% | references/capabilities/proportion-line-slope.md | references/capabilities/proportioning-valve.md、references/capabilities/simultaneous-lockup-point.md、references/capabilities/pressure-to-brake-force.md |
| 500/0.3 是什么意思、后轮压力多少；由实测后轮压力反推主缸压力；有阀/无阀在高压力段差多少；感载阀/惯性阀和这个阀有什么区别 | references/capabilities/proportioning-valve.md | references/capabilities/proportion-line-slope.md、references/capabilities/no-solution-decision-tree.md |
| 配比怎么调都过不了该怎么办；该装压力比例阀、感载阀还是惯性阀；货车空/满载差异大，为什么乘用车经验不能用；某工况达不到目标减速度算不算不能交付 | references/capabilities/no-solution-decision-tree.md | references/capabilities/effectiveness-triangle.md、references/capabilities/proportioning-valve.md、references/capabilities/lockup-order-and-consequence.md |
| 350 psi 能出多少制动力；制动增益 in·lb/psi 怎么换算成 lb；算出来差一倍是不是漏了什么；换制动盘后增益怎么变 | references/capabilities/pressure-to-brake-force.md | references/capabilities/proportion-line-slope.md、references/capabilities/brake-efficiency-table.md、references/capabilities/rotational-inertia-effective-mass.md |
| 为什么需要 ABS、为什么不能一直踩死；峰值附着能不能一直用满；为什么压力再大反而刹不住；某压力设定会不会穿过峰值 | references/capabilities/mu-peak-instability.md | references/capabilities/lockup-order-and-consequence.md、references/capabilities/load-sensitivity.md、references/capabilities/drum-brake-factor.md |
| 重载是不是制动力按比例增加；线性假设 μp·W 有多准、代价多少；空载/满载两套配比差异为什么这么大；低摩擦路面上这条修正是不是更重要 | references/capabilities/load-sensitivity.md | references/capabilities/lockup-boundary-lines.md、references/capabilities/dynamic-load-transfer.md、references/capabilities/resistance-terms.md |
| 制动过程吸收多少能量、峰值/平均功率多少；制动器热容量够不够、要多重；长下坡连续制动会不会烧；能量和减速度有没有关系 | references/capabilities/brake-energy-and-power.md | references/capabilities/braking-distance-and-time.md、references/capabilities/rotational-inertia-effective-mass.md、references/capabilities/resistance-terms.md |
| 这车符不符合 FMVSS 105；实测制动距离按法规算达标吗；法规要求的 19 ft/s² 是几个 g；过了法规为什么雨天还是容易甩尾 | references/capabilities/fmvss-compliance-screen.md | references/capabilities/braking-distance-and-time.md、references/capabilities/lockup-order-and-consequence.md、references/capabilities/no-solution-decision-tree.md |
| 滚阻要不要算、0.01 g 是多少 ft/s²；坡度 4% 相当于多少 g、下坡要按几个 g 算；滚阻随载荷转移变化吗；轻制动时滚阻为什么重要 | references/capabilities/resistance-terms.md | references/capabilities/braking-distance-and-time.md、references/capabilities/brake-energy-and-power.md、references/capabilities/load-sensitivity.md |
| 制动因数怎么算、领蹄从蹄有什么区别；鼓刹为什么省力、会不会自锁；换高摩擦衬片前要不要校核自锁；鼓刹热了为什么会尖叫/跑偏 | references/capabilities/drum-brake-factor.md | references/capabilities/pressure-to-brake-force.md、references/capabilities/mu-peak-instability.md |
| 算制动力要不要考虑车轮/传动系惯量；驱动轮制动器要不要留余量；为什么实测制动力比 T_b/r 小几个百分点；为什么式(3-19) 能干写成 F=T/r | references/capabilities/rotational-inertia-effective-mass.md | references/capabilities/pressure-to-brake-force.md、references/capabilities/brake-energy-and-power.md |

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

- 缺 $\mu_p$ 的具体值或口径（路面/SN/试验胎）时停止画边界线与三角形——$\mu_p$ 决定斜率，猜一个等于画错图。
- 缺静态轴荷 $W_{fs}/W_{rs}$ 时停止进载荷转移与配比计算；不得用 $b/L$、$c/L$ 代替（原文取向未统一）。
- 用户要求「$\eta_b$ 合格线」或「$\eta_b$ 最低多少算过」时停止：原书无验收阈值。
- 用户要求「踏板力增益落在最佳带没有」的通过/不通过判定时停止：图 3.17 阴影区无边界数值，只能给增益计算与定性参照。
- 用户要求「某效率对应每年抱死几次」时停止：图 3.16 不可定量复现，只能给「效率↓→频次↑」与「高发于 $\mu$ 0.4–0.6 湿路」这两条定性结论。
- 用户要求 ECE / GB 合规结论时停止，声明本章只覆盖 FMVSS 105/121。
- 工况为瞬态/极限（压力建立过程、ABS 循环、热衰退中的连续制动）时停止套用准静态公式，声明出界。
- 出现「后轮先抱死」时不得以任何措辞收尾为「可接受」，必须先给方向不稳定性结论并要求整改。
