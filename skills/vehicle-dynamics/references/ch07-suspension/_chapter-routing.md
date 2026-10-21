---
name: vehicle-suspension-geometry
description: |
  当用户处理乘用车/商用车「悬架结构与几何」问题时调用：选悬架结构（整体式/独立式/第迪安/叶片弹簧/四连杆/三连杆/SLA/麦弗逊/多连杆/拖曳臂/半拖曳臂/摆动轴）并列出代价、
  用等效拖曳臂（虚拟作用点/虚拟铰接点）把任意杆系归一化、由 e/d 与 h/L 算 100% 抗后蹲与完全抗前仰、算抗后蹲百分率、
  算俯仰角变化率 θ_p/a_x（deg/g）、求整体式车轴与独立悬架的侧倾中心（含正/负摆动臂、平行杆无穷远退化）、
  判断举升（jacking）风险、按性能模式选主动/半主动悬架等级并写传感信号、判断满额几何补偿该不该做。
  输出一律是**几何量**（e/d、比值、高度、deg/g、结构 + 代价清单），强制声明结构分支、单位口径（全章英制，g=386 in/s²）与姿态前提（零侧倾/准静态）。
  不适用于：瞬态与极限工况、衬套柔度定量修正、成本/重量/寿命量化比较、侧倾中心「该取多高」的目标值、制动抗点头的数值计算（式 7-28 符号待核）、
  四驱 θ_p（式 7-26 与 7-12 符号相反，分支不可用）、独立后驱 θ_p（式 7-18 不可恢复）。
  Triggers: 悬架选型/整体桥/独立悬挂/麦弗逊/双A臂/多连杆/摆动轴/等效拖曳臂/虚拟作用点/抗后蹲/抗前仰/抗点头/抗提升/e over d/侧倾中心/正摆动臂/负摆动臂/举升/jacking/主动悬架/半主动/空气悬架/俯仰角变化率/θp
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch7-suspension
  cangjie.capability-count: 18
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 7 章 悬架 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 瞬态与极限工况（俯仰/侧倾动力学、横摆阻尼、附着极限非线性、举升-侧翻的定量阈值）
- 衬套柔度、车身变形、轮胎垂向柔度的定量修正（作者只在多连杆一处承认刚体假设被破）
- 成本、重量、寿命、制造工艺的量化比较（本章只有定性代价）
- 侧倾中心的目标高度、抗前仰百分率、抗点头百分率的定义（原文均未给出）
- 制动抗点头的数值计算、四驱 θ_p、独立后驱 θ_p 与完全抗前仰（依赖待核或不可恢复的式子）
- 具体零部件选型、供应商报价、法规认证、控制器的功率/带宽/失效策略

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 悬架是几何机构而不是「弹簧+减振器」：改一个铰接点，同时改变抗后蹲、抗前仰、侧倾中心与转向特性——所以任何单项指标都不能单独调。
2. 全章只有一个公共分析工具：把任意杆系折算为绕虚拟作用点摆动的等效单臂；纵向用它得 F_z/F_x=e/d，侧向用它得侧倾中心。
3. 抗后蹲是纯几何（e/d=h/L，与弹簧刚度无关）；抗前仰要后轴抬升（e/d=h/L+(h/L)(K_r/K_f)），两者差一个刚度比项，绝不互为「加强版」。
4. 侧倾中心是「侧向力的作用点」，只在零侧倾位形下确定，随位形移动、可为负；本章**没有**「该取多高」的经验值，任何目标值都不得补造。
5. 工程上极少做满额补偿：作者给出 8 条否决理由与「抗点头很少超过 50%」的经验上限；满额前必须逐条过否决门。
6. 主动悬架只改变垂直方向的**力**，不改变**运动学**（不能改侧倾中心/外倾曲线），且在 ≈10 Hz 车轮模态处无明显优势且会反噬乘适性。
7. 全章英制（in、lb、g=386 in/s²）且无 SI 换算表；K 为左右两侧之和、e 从接地点量起、d 是有效臂长——口径错不会自曝。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 为一台车选悬架结构并说明代价；麦弗逊/双 A 臂/多连杆/整体桥怎么选；某结构有什么缺点、我漏了什么 | references/capabilities/structure-family-selection.md | references/capabilities/roll-center-solid-axle.md、references/capabilities/roll-center-independent.md、references/capabilities/jacking-risk.md、references/capabilities/active-suspension-ladder.md |
| 空气悬架算不算主动悬架；半主动够不够、要不要上全主动；主动悬架能不能控侧倾/点头 | references/capabilities/active-suspension-ladder.md | references/capabilities/active-mode-signals.md、references/capabilities/structure-family-selection.md、references/capabilities/full-compensation-veto.md |
| 这套杆系的虚拟作用点在哪；三连杆的上控制臂要不要算进去；虚拟作用点和瞬心是不是一回事 | references/capabilities/virtual-point-method.md | references/capabilities/parallel-arm-infinite-point.md、references/capabilities/equivalent-trailing-arm-ed.md、references/capabilities/roll-center-solid-axle.md |
| 上下摆臂平行时侧倾中心怎么算；叶片弹簧的侧倾中心在哪；水平/倾斜平行杆的侧倾中心一样吗 | references/capabilities/parallel-arm-infinite-point.md | references/capabilities/virtual-point-method.md、references/capabilities/roll-center-solid-axle.md、references/capabilities/roll-center-independent.md |
| 抗后蹲/抗点头做到 100% 行不行；为什么原厂只做一半；完全消除点头有什么代价 | references/capabilities/full-compensation-veto.md | references/capabilities/anti-squat-100.md、references/capabilities/anti-pitch-up-precision.md、references/capabilities/five-e-quick-rule.md、references/capabilities/active-suspension-ladder.md |
| 摆动轴为什么会翻车/甩尾；举升（jacking）是什么、怎么防治；加粗防倾杆能不能治举升 | references/capabilities/jacking-risk.md | references/capabilities/roll-center-independent.md、references/capabilities/structure-family-selection.md |
| 纵向力和垂向力之比怎么算；等效拖曳臂是什么、没有纵臂能不能用；e 和 d 从哪里量 | references/capabilities/equivalent-trailing-arm-ed.md | references/capabilities/virtual-point-method.md、references/capabilities/anti-squat-100.md、references/capabilities/roll-center-solid-axle.md |
| 100% 抗后蹲的铰接点放在哪；后悬架加速时下沉多少；独立后悬架为什么按整体式公式算不对 | references/capabilities/anti-squat-100.md | references/capabilities/anti-squat-percent.md、references/capabilities/anti-pitch-up-precision.md、references/capabilities/five-e-quick-rule.md、references/capabilities/full-compensation-veto.md |
| 这台车现在是几成抗后蹲；抗后蹲率怎么算、能不能超过 100%；60% 抗后蹲的分母是什么 | references/capabilities/anti-squat-percent.md | references/capabilities/anti-squat-100.md、references/capabilities/full-compensation-veto.md |
| 加速时车身要完全水平需要多大 e/d；2h/L 到底能不能用；抗前仰和抗后蹲差多少 | references/capabilities/anti-pitch-up-precision.md | references/capabilities/anti-squat-100.md、references/capabilities/pitch-rate-theta-p.md、references/capabilities/front-drive-anti-lift.md、references/capabilities/full-compensation-veto.md |
| 前驱车加速抬头怎么消；前轴抗提升怎么做、e/d 为负是什么意思；前驱和后驱的抗前仰公式是不是反的 | references/capabilities/front-drive-anti-lift.md | references/capabilities/anti-pitch-up-precision.md、references/capabilities/example2-anti-lift-anchors.md、references/capabilities/anti-squat-100.md |
| 完全抗后蹲要留多长的拖曳臂；布置空间不够怎么办；拖曳臂多短算短 | references/capabilities/five-e-quick-rule.md | references/capabilities/anti-squat-100.md、references/capabilities/full-compensation-veto.md、references/capabilities/anti-squat-percent.md |
| 加速抬头多少度每 g；俯仰角变化率怎么算；我的结果和例题 1.43 对不上 | references/capabilities/pitch-rate-theta-p.md | references/capabilities/example1-anchors.md、references/capabilities/example2-anti-lift-anchors.md、references/capabilities/anti-squat-100.md |
| 四连杆/三连杆后悬的侧倾中心在哪；整体桥侧倾中心怎么画；侧倾中心高度多少合适 | references/capabilities/roll-center-solid-axle.md | references/capabilities/roll-center-independent.md、references/capabilities/virtual-point-method.md、references/capabilities/parallel-arm-infinite-point.md、references/capabilities/jacking-risk.md |
| 麦弗逊/双 A 臂的侧倾中心怎么画；正摆动臂/负摆动臂是什么意思；降车身后侧倾中心变多少 | references/capabilities/roll-center-independent.md | references/capabilities/roll-center-solid-axle.md、references/capabilities/virtual-point-method.md、references/capabilities/jacking-risk.md、references/capabilities/parallel-arm-infinite-point.md |
| 主动悬架控制策略用什么信号；侧倾控制怎么触发；能不能只靠软件解决点头 | references/capabilities/active-mode-signals.md | references/capabilities/active-suspension-ladder.md、references/capabilities/full-compensation-veto.md |
| 例 1 的 1.43 怎么算出来的；0.301 和 0.378 哪个对；我的结果和例题差两倍/差 12 倍 | references/capabilities/example1-anchors.md | references/capabilities/anti-squat-100.md、references/capabilities/anti-pitch-up-precision.md、references/capabilities/pitch-rate-theta-p.md |
| 4.2 和 2.61 是怎么来的；完全抗提升能降低多少抬头；抗提升到底是省略哪一项 | references/capabilities/example2-anti-lift-anchors.md | references/capabilities/front-drive-anti-lift.md、references/capabilities/pitch-rate-theta-p.md、references/capabilities/example1-anchors.md |

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

- 缺「结构判定」（整体式/独立式、是否驱动、是否独立后驱）时停止计算，只给方法与所需数据清单——结构决定用 e 还是 (e−r)、用两点法还是一点法。
- 用户要求「侧倾中心该取多高」或「抗点头率算到 X%」时停止：前者全章无判据，后者式(7-28) 的负号与 β 基准未定义，一律标「需纸书复核」。
- 工况为瞬态/极限（跳动、冲击、接近附着极限的动态过程）时停止套用本章准静态公式，声明出界。
- 涉及四驱俯仰（式 7-26/27）或独立后驱俯仰（式 7-18）时停止给数值，声明该分支不可用。
- 用户要求按 2h/L 给抗前仰定量结论时停止，先给精确式 0.301 并说明速算仅在 K_r/K_f 与 1 的偏差 ≤10% 时可用。
