---
name: vehicle-rollover
description: |
  当用户处理汽车「侧翻」问题时调用：算刚体准静态侧翻门槛 $t/2h$（含 $2h/t$ 方向、表 9.1 七类车型区间）、
  算弯道超高与中性车速（$a_y/g=t/2h+\phi$、$v=\sqrt{gR\phi}$）、判定侧翻的三档状态（未离地 / 已离地可救 / 重心越线）、
  分诊「先翻还是先滑」（门槛 vs 轮胎峰值 $\mu\approx0.8$）、算悬挂车辆的实际门槛（式 9-6 的 $R_\phi$ 与 $h_r/h$，
  含悬挂约 −5% 与轮胎约 −5% 两笔独立折扣）、判断手算够不够并读图 9.4 折线（第一轴离地 / 第二轴离地）、
  判倾斜平台试验在 45° 附近失效、按侧倾共振频率判别阶跃与正弦哪种输入更危险、算阶跃工况的瞬态门槛降幅（阻尼修正）、
  算前后轴相位差（1 Hz 时 0.2 s≈70°、$a_y$ 由 0.8 g 降到 0.5 g）与四轮转向的"灵敏度换裕度"、
  识别挂车"抽鞭"（反相 180° + 放大）与侧倾耦合解法、用能量判据判绊倒侧翻（22 / 23.075 / 25 / 27 ft/s 锚点）、
  读事故统计并划出 $t/2h$ 的使用边界（相关但不决定，同门槛可差 3 倍）、以及做 FMVSS 1.2（无量纲 $t/2h$）的准入初判。
  
  输出一律附口径声明：①门槛以 **$g$** 计（无量纲 $t/2h$ 与"以 $g$ 计的加速度"数值相同，但必须声明是刚体**上限**）；
  ②$R_\phi$ 一律 **rad/g**（第 6 章习惯 deg/g，1 rad/g = 57.3 deg/g，6 deg/g = 0.105 rad/g）；
  ③$\phi$ 是**路面超高角**、$\Phi$ 是**车身侧倾角**，式(9-5) 里的希腊字母实为 $\Phi$；
  ④「侧翻临界值」一词三义——加速度（g）/ 能量（图 9.12）/ 无量纲 $t/2h$（图 9.13/9.14 横轴），
  而 23.075 是**初始侧向速度 ft/s**；
  ⑤全章英制（in、lb、ft/s、slug），$g=32.2$ ft/s²。
  
  强制四个全局前提：①刚体门槛是**上限**，真车门槛更低（悬挂约 −5%、轮胎约 −5%、阶跃可达 −50%）；
  ②「保守」在本章指**算高了**（对安全偏乐观），与中文工程语境相反；
  ③p241「侧倾率尽可能的高」与式(9-6) 方向相反，一律改写为「侧倾率尽可能**低**（用高侧倾刚度）」并标 ⚠️；
  ④FMVSS 1.2 **没有标准编号**，严禁补成 "FMVSS 216"（216 是车顶强度）。
  
  不适用于：温升与热容量、ABS/ESC 的阈值与循环、9.3.3 的 $\Delta h_{crit}$ 几何式与 $I/\omega$ 换算（原文未给，
  只能解读 E(t) 曲线）、图 9.2/9.4/9.7–9.15 的任何读数（只有曲线无数据表，零读数）、
  重型货车统计的"按总重反推门槛"算法（p38 缺值，未进本 Bundle）、ECE R13 / GB 21670 等非美标合规、
  1992 年之后的 ESC / 主动防倾杆 / 主动悬架措施层、$\mu$ 的路面-轮胎对应表、$f_n$ 的 $h/t$ 换算式。
  
  Triggers: 侧翻/侧翻临界值/抗侧翻/rollover/rollover threshold/t/2h/2h/t/SSF/轮距重心高度/门槛/
  超高/横向坡度/中性车速/superelevation/neutral speed/先翻还是先滑/spinout/急剧回转/悬挂修正/侧倾率/roll rate/
  侧倾中心/roll center/rad/g/deg/g/倾斜平台/tilt-table/缆绳拖曳/折线/第一轴离地/阶跃/正弦/共振/阻尼比/
  超调/overshoot/相位差/phase lag/四轮转向/4WS/抽鞭/cracking the whip/全挂车/侧倾耦合/roll coupling/
  绊倒/tripped rollover/路缘/能量判据/侧翻率/事故统计/暴露因素/Capri/Vega/FMVSS 1.2/1.2/离地/LTR/
  两秒内/arctan(t/2h)/模型层级/准静态什么时候失效
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch9-rollover
  cangjie.capability-count: 14
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 9 章 车辆侧翻 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 温升、热容量、制动/轮胎热衰退（本章无传热模型）
- ABS / ESC / EBD / 主动防倾杆 / 主动悬架 / 线控转向的控制策略与阈值（1992 年视角）
- 9.3.3 绊倒模型的内部实现：$\Delta h_{crit}$ 几何式、"旋转点"取法、$I/\omega$ 与初始侧向速度的换算（原文全无，只能解读 E(t) 曲线）
- 图 9.2 / 9.4 / 9.7 / 9.8 / 9.9 / 9.10 / 9.12 / 9.13 / 9.14 / 9.15 的任何具体读数（只有曲线、无数据表）
- 重型货车"按整车总重反推门槛"的算法（p38 缺平均装载密度与典型特性取值，已入 needs_review，未进本 Bundle）
- ECE R13 / R13-H / GB 21670 及任何非美标侧翻合规
- $\mu$ 的路面/轮胎/胎压/温度对应表；侧倾共振频率 $f_n$ 由 $h/t$ 计算的换算式
- 1992 年后的措施层证据（ESC 降低致命侧翻约 1/3–1/2 等，不在本章）
- 乘员伤害、车顶强度（FMVSS 216）、约束系统、翻倒后的触地过程

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 全章只有一个几何标尺：$t/2h$。它能比较车辆、能做法规准入初判、能暴露"该先滑却先翻"的矛盾，但**不能**预测某辆车的实际门槛——真车门槛永远更低。
2. 本章的「保守」是反向词：作者括注"所得出的侧翻临界值大于实际值"⇒ 算高了、对安全偏乐观。任何只写「保守」不写「高估」的句子都是危险转述。
3. 门槛不是常数，是**输入形状的函数**：准静态（几何折减约 5%×2）→ 阶跃（超调，货车近 −50%）→ 正弦（共振，货车 <1 Hz）→ 绊倒（无门槛，换能量判据）。选错层级比算错数更致命。
4. 侧翻有三次"降格"：从"会不会翻"（门槛）到"何时翻完"（不稳定分支，两秒内）到"统计上翻不翻"（相关但不决定）。每一次降格都收窄一次适用范围。
5. 两条最容易做反的方向：侧倾刚度↑ ⇒ 侧倾率↓ ⇒ 门槛↑（不是"侧倾率高门槛高"）；四轮转向 ⇒ 响应更灵敏 ⇒ 侧翻可能性**增大**（不是更安全）。
6. 出路面是另一套物理：绊倒没有 $a_y$ 门槛，判据是"旋转动能 + 重心升高势能 > 抬到外侧轮上方所需势能"；此时该改的是轮距/重心高度与车身变形行程，加配重与加硬减震基本无效。
7. 合规章不是安全章：FMVSS 1.2 是准入线（无量纲 $t/2h$），作者本人反对"在搞清各因素关系之前用限值降事故率"。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 算水平路面的刚体侧翻门槛；这辆车多少 g 会翻；2h/t 与 t/2h 哪个大更好；查典型车型（轿车/SUV/货车）的侧翻临界值区间 | references/capabilities/rigid-rollover-threshold.md | references/capabilities/superelevation-and-neutral-speed.md、references/capabilities/suspension-threshold-correction.md、references/capabilities/slide-vs-trip-diagnosis.md、references/capabilities/fmvss-1-2-screening.md |
| 有超高的弯道上门槛变多少；中性车速是什么、是不是最安全车速；道路设计该取多少超高；出路面/路肩外倾时门槛是升还是降 | references/capabilities/superelevation-and-neutral-speed.md | references/capabilities/rigid-rollover-threshold.md、references/capabilities/suspension-threshold-correction.md、references/capabilities/tripped-rollover-energy.md |
| 轮子离地算不算翻；离地之后还能救回来吗；预警阈值该定在哪；侧翻开始与侧翻完成的判据 | references/capabilities/rollover-onset-staging.md | references/capabilities/rigid-rollover-threshold.md、references/capabilities/slide-vs-trip-diagnosis.md、references/capabilities/transient-threshold-damping.md |
| 这车是先甩尾还是先翻；门槛比摩擦极限高是不是就不会翻；为什么事故统计与理论相反；湿滑路面会不会连货车都先滑 | references/capabilities/slide-vs-trip-diagnosis.md | references/capabilities/rigid-rollover-threshold.md、references/capabilities/suspension-threshold-correction.md、references/capabilities/transient-threshold-damping.md、references/capabilities/tripped-rollover-energy.md |
| 算悬挂车辆的实际侧翻门槛；侧倾率/侧倾中心高度对门槛的影响；独立悬架是不是比整体桥更抗翻；理论 1.3 实测 1.2，差在哪 | references/capabilities/suspension-threshold-correction.md | references/capabilities/rigid-rollover-threshold.md、references/capabilities/precise-model-and-tilt-test.md、references/capabilities/transient-threshold-damping.md、references/capabilities/superelevation-and-neutral-speed.md |
| 手算够不够、要不要建模；侧倾响应折线上哪一点是门槛；倾斜平台测出来的数能不能用；侧翻试验该怎么做法、力加在哪 | references/capabilities/precise-model-and-tilt-test.md | references/capabilities/suspension-threshold-correction.md、references/capabilities/rigid-rollover-threshold.md、references/capabilities/rollover-onset-staging.md |
| 紧急避障和连续变道哪个更容易翻；该做阶跃还是蛇行/变道工况；为什么货车怕变道、轿车不怕；2 秒变道对应多少 Hz | references/capabilities/step-vs-sine-selection.md | references/capabilities/transient-threshold-damping.md、references/capabilities/model-tier-router.md、references/capabilities/phase-lag-and-four-wheel-steer.md |
| 紧急避障/突然打方向多少 g 会翻；留多少余量才够；阻尼器算不算安全件；瞬态门槛比准静态低多少 | references/capabilities/transient-threshold-damping.md | references/capabilities/step-vs-sine-selection.md、references/capabilities/suspension-threshold-correction.md、references/capabilities/rollover-onset-staging.md |
| 为什么大车反应迟钝、打方向要早；理论能出 0.8g 实际只有 0.5g；四轮转向是不是更安全；相位差对侧翻有什么影响 | references/capabilities/phase-lag-and-four-wheel-steer.md | references/capabilities/step-vs-sine-selection.md、references/capabilities/trailer-whip-and-roll-coupling.md、references/capabilities/transient-threshold-damping.md |
| 双节挂车为什么翻、怎么防；挂车侧翻是不是挂车自己的问题；侧倾耦合和刚性连接有什么区别；牵引车什么都没做挂车就翻了 | references/capabilities/trailer-whip-and-roll-coupling.md | references/capabilities/phase-lag-and-four-wheel-steer.md、references/capabilities/step-vs-sine-selection.md、references/capabilities/accident-statistics-reading.md |
| 侧滑撞路缘后是怎么翻的、能不能算；E(t) 曲线怎么看、这次翻不翻；提高抗绊倒能力该改哪个参数；23.075 是什么量 | references/capabilities/tripped-rollover-energy.md | references/capabilities/model-tier-router.md、references/capabilities/phase-lag-and-four-wheel-steer.md、references/capabilities/accident-statistics-reading.md |
| 两台车侧翻率能不能直接比；提高门槛能降多少事故率；SUV 侧翻率高是不是车的问题；怎么读侧翻率统计 | references/capabilities/accident-statistics-reading.md | references/capabilities/fmvss-1-2-screening.md、references/capabilities/rigid-rollover-threshold.md、references/capabilities/slide-vs-trip-diagnosis.md |
| 这车侧翻达标吗；FMVSS 1.2 是什么要求、有没有编号；货车要不要满足 1.2；合规了是不是就安全 | references/capabilities/fmvss-1-2-screening.md | references/capabilities/accident-statistics-reading.md、references/capabilities/rigid-rollover-threshold.md、references/capabilities/suspension-threshold-correction.md |
| 这个问题该用哪个模型/该不该建模；准静态公式什么时候不能用；用 t/2h 解释这次快速避障翻车行不行；要不要上 8 自由度模型 | references/capabilities/model-tier-router.md | references/capabilities/rigid-rollover-threshold.md、references/capabilities/transient-threshold-damping.md、references/capabilities/tripped-rollover-energy.md、references/capabilities/step-vs-sine-selection.md |

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

- 缺 $t$ 或 $h$ 时停止算门槛；不得用 $b/L$、$c/L$ 或轴距代替（$h$ 是整车重心距地高度）。
- 用户要求"这辆车多少 g 会翻"的确定性答案时停止：$t/2h$ 只能给上限，必须附三笔折扣（悬挂、轮胎、阶跃）与"需实测/建模"的说明。
- 缺 $R_\phi$ 的单位（rad/g 还是 deg/g）或 $h_r/h$ 时停止做悬挂修正；不得默认 6 或 0.1。
- 用户要求给"轿车/SUV 阶跃降幅"的具体百分比时停止：原文该处 OCR 断裂，只能写"低于 $t/2h$、降幅原文未说明"（G1），严禁从图 9.7 反推。
- 用户要求从图 9.2/9.4/9.7–9.15 读任何一个数时停止，声明只有曲线、只能给形状与读数口径。
- 用户要求给 1.2 补一个标准编号、或要 ECE/GB 合规结论时停止：原文无编号（严禁补 216），本章只覆盖作者所述的 FMVSS 要求。
- 用户要求"高于 1.2 就安全"或"提门槛能降多少事故率"的量化承诺时停止：同门槛事故率可差 3 倍，作者明言"过于草率"。
- 工况是绊倒（出路面/撞路缘）却要求用 $a_y$ 门槛判定时停止，改走能量判据；反之平路转向工况不得用能量判据。
- 用户把中性车速当最安全/推荐车速时停止，先纠正为"该半径+该超高下 $a_y=g\phi$ 的平衡点"。
- 出现"提高侧倾率以提高门槛"的表述时停止，按式(9-6) 纠正为"侧倾率尽可能低（高侧倾刚度）"，并标 ⚠️ 译文矛盾。
