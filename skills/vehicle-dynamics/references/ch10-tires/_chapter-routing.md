---
name: vehicle-tires
description: |
  当用户处理乘用车/商用车「轮胎」问题时调用：判 SAE 轮胎坐标系与符号约定（$F_z$ 取负、$W=-F_z$、
  $C_\alpha$ 取正、外倾角两套正方向、系数是 /deg 不是 /rad）；按用途与路面选附着系数
  （$\mu_p$ 干 0.70–0.90 / 湿 0.25–0.50 / 冰 0.10–0.15；$\mu_s$ 只在抱死；滑动数 SN=100$\mu_s$，
  干 81 / 波特兰水泥 45–50 / 湿 30 / Jennite 20–25）；算滑动率 $s=(1-r\omega/V)\times100$ 并读
  "斜率共、峰值分"；算载荷与气压对 $\mu$ 的修正（近额定 +10% → −0.01；50%→125% 降 >20%，两段不得衔接）；
  由 $\alpha$ 与 $F_z$ 求 $F_y$ 三区段（线性 0–5/10°、峰值 15–20°、大角 $\mu_sW\sin\alpha$）；
  由侧偏系数（斜交 0.12 / 子午线 ≈0.15 / 低高宽比 0.25–0.30 $\mathrm{deg^{-1}}$）反算 $C_\alpha$；
  估外倾刚度与推力（$C_\gamma$=(0.10–0.20)$C_\alpha$，子午线再 ×0.40–0.50）；执行 0.0175 车辙判据
  （0.0175 = 1/57.3 = $\sin1°$，左边必须是 $C_\gamma/W$）；算回正力矩三来源（侧偏 0.033/0.043、
  外倾 0.003/0.001、路径曲率）；判复合滑动方向（制动与驱动不对称、4° 反常项、0.3g 最不利点、抱死顺序）；
  用正反滚动半差/平均分离圆锥度与帘布层转向（都要 /2）；估台阶冲击 $\Delta F_z\approx h k_t$ 与两个纵向机制；
  判轮胎模态与反共振（60 Hz 传、90/110 Hz 图注值不传、<20 Hz 轮轴跳动、反共振才是传力峰）；
  判前后轴 $C_\alpha/W$ 平衡（不足/过多转向）；以及"结构定 $C_\alpha$/$C_\gamma$、摩擦副定 $\mu$"的归因。
  
  输出一律是**系数 + 区间 + 适用域 + 判据**，并附口径声明：全章英制（lb、ft、in、deg、r/s，
  g=32.2 ft/s²）、$W=-F_z>0$、系数一律 /deg（per-rad ×57.3）、外倾角逐轮声明基准、
  $\mu$ 必带"峰值/滑动/滑动数"身份与"轮胎+路面+载荷"三件套。
  强制声明四个全局前提：①本章是"经验系数归类章"，正文只有 4 条定义式、30 张图，无一条拟合式；
  ②所有 carpet plot 无数据表，凡需读图斜率/截距处只能定性；③数据为 1970s–80s 样本、以斜交胎为主；
  ④文本与附录 A 的三处定义冲突以正文为准（滑动率用式(10-1)、传递率用 p278、外倾角用 p266 定量）。
  
  不适用于：$C_\alpha$ 绝对值的原始数据（本章不给，只能反算）、$\mu(F_z)$ 的 a/b 系数（全书缺值）、
  复合滑动的 $F_y(F_x)$ 解析式（本章无）、雪/砂石/赛道胶与胎温效应（全章零覆盖）、5–20 Hz 瞬态传递函数
  （只有松弛长度与 0.05 s 单例）、椭圆摩擦参数、驻波、轮胎设计（配方/带束角/帘线材料）、
  ECE R117 / EU 标签 / FMVSS 139、ABS 阈值与循环频率。
  
  Triggers: 轮胎/tyre/tire/附着系数/摩擦系数/μ/峰值附着/滑动摩擦/滑动数/skid number/SN 81/
  滑动率/slip ratio/μ-s 曲线/ABS 与附着/侧偏角/slip angle/侧偏刚度/cornering stiffness/C_alpha/
  侧偏系数/1-per-deg/外倾角/camber/外倾刚度/C_gamma/外倾推力/camber thrust/车辙/rut/tramlining/0.0175/
  回正力矩/aligning moment/M_z/拖距/pneumatic trail/原地打方向/转向手感/复合滑动/combined slip/
  摩擦圆/friction circle/弯道制动/0.3g/抱死顺序/圆锥度/conicity/帘布层转向/ply steer/跑偏/pull/drift/
  台阶冲击/impact force/轮胎垂直刚度/包容/enveloping/轮胎模态/tire mode/60 Hz/90 Hz/110 Hz/
  反共振/anti-resonance/轮轴跳动/axle hop/轮迹刚度/footprint stiffness/传递率/transmissibility/
  不足转向/understeer/过多转向/oversteer/前后侧偏刚度平衡/载荷敏感性/load sensitivity/胎压与抓地/
  换胎选型/子午线/斜交/radial/bias/高宽比/aspect ratio
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch10-tires
  cangjie.capability-count: 15
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 10 章 轮胎 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- $C_\alpha$ 的绝对典型值（lb/deg）的原始数据——本章未给，只能反算或读图（G1）
- $\mu(F_z)$ 的 a、b 多项式系数——全书缺值（G2）
- 复合滑动的 $F_y(F_x)$ 解析式与摩擦椭圆参数（G3）
- 胎温对 $\mu$ 的影响（全章 0 次）、雪/砂石/赛道胶路面
- 5–20 Hz 瞬态传递函数（只有松弛长度与 10 r/s 单例）、ABS 阈值/升压率/循环频率
- 驻波（本章全文未出现，不得挂在本章名下）
- 轮胎设计：配方、带束角优化、帘线材料、花纹设计
- ECE R117 / EU 轮胎标签 / FMVSS 139 / 胎压监测
- 圆锥度对气压的灵敏度系数、轮胎垂直刚度 $k_t$ 的典型值（本章均未给）
- 30 张 carpet plot 的逐点读数（全部无数据表）

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 本章是「接口章」：把一块橡胶圆环体翻译成整车方程能吃下的系数与符号约定，只给量级与符号，不给模型——所以卡片的交付物是"数值 + 适用域 + 判据"，不是推导。
2. 符号先行：$F_z$ 取负、$W=-F_z>0$、$C_\alpha$ 取正、$C_\gamma$ 无负号、外倾角逐轮定号、系数是 /deg。符号错一次，第 6 章的 $K$ 会整体反号，而数值看起来仍合理。
3. 结构定系数、摩擦副定附着：帘布角/带束层/高宽比决定 $C_\alpha$（0.12/0.15/0.25–0.30）与 $C_\gamma$（10%–20%，子午线再 ×40%–50%）；路面/胶料/载荷决定 $\mu$。所以"换胎能改转向平衡，不一定改极限附着"。
4. 本章最有用的数都可自证：0.0175=1/57.3=$\sin1°$、0.12→12% 载荷、8.60 $\mathrm{rad^{-1}}$、60 Hz、15%–20% 峰位；最不可靠的都要读图：$C_\alpha$ 绝对值、$\mu(F_z)$ 的 a/b、$C_\gamma$ 绝对值。按这条线把卡切成"可复算"与"只能定性"两类。
5. 载荷敏感性是两条互不相容的口径（局部斜率与全域割线），$C_\alpha$ 与 $\mu$ 随载荷的方向相反（$C_\alpha$ 绝对值升、$C_\alpha/W$ 与 $\mu$ 降）——混用会让载荷转移的效果反号。
6. 三个硬缺口（$C_\alpha$ 绝对值、$\mu(F_z)$ 的 a/b、复合滑动解析式）一律标 needs_review 或"不可算"，任何补数都是编造。
7. 时代边界：1970s–80s 样本、以斜交胎为主、高宽比停在 0.60、无温度/雪/砂石/赛道胶、无现代轮胎品类。用于现代低扁平/EV 胎必须重取数。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 判断一组轮胎力/刚度数据的符号是否正确；垂直载荷该取正还是取负；侧偏刚度能不能是负值；左右轮外倾角符号怎么定、按哪套定义；侧偏刚度与侧偏系数的单位与量纲换算 | references/capabilities/tire-sign-and-unit-gate.md | references/capabilities/cornering-stiffness-from-coefficient.md、references/capabilities/rut-criterion-0175.md、references/capabilities/lateral-force-three-regimes.md |
| 制动/驱动/极限工况的摩擦系数取多少；湿路、冰面附着系数是多少；滑动数怎么换算成摩擦系数；有 ABS 与无 ABS 该用哪个摩擦系数；路面摩擦等级怎么对标法规 | references/capabilities/mu-surface-selection.md | references/capabilities/longitudinal-slip-and-mu-s-curve.md、references/capabilities/mu-load-and-pressure-sensitivity.md、references/capabilities/combined-slip-and-friction-circle.md |
| 滑动率怎么算、ABS 什么时候介入；峰值附着出现在第几% 滑动率；换胎或换路面后制动变差，是峰值变了还是斜率变了；滑动率与滑动数有什么区别；冰面为什么一点就滑 | references/capabilities/longitudinal-slip-and-mu-s-curve.md | references/capabilities/mu-surface-selection.md、references/capabilities/mu-load-and-pressure-sensitivity.md、references/capabilities/combined-slip-and-friction-circle.md |
| 载荷增加后摩擦系数降多少；超载/满载工况 $\mu$ 怎么修正；50% 到 125% 载荷峰值附着降幅；胎压能不能提高抓地、干湿有何不同；前后轴载荷不同能不能用一个 $\mu$ | references/capabilities/mu-load-and-pressure-sensitivity.md | references/capabilities/mu-surface-selection.md、references/capabilities/understeer-balance-by-normalized-stiffness.md、references/capabilities/camber-stiffness-magnitude.md |
| 侧偏角 1° 能出多少侧向力；侧偏角 10°/20° 时轮胎还有多少力、是否已饱和；轮胎饱和的侧偏角是多少；转向响应滞后多久、松弛长度是什么；烂路/颠簸路面为什么抓地变差 | references/capabilities/lateral-force-three-regimes.md | references/capabilities/cornering-stiffness-from-coefficient.md、references/capabilities/combined-slip-and-friction-circle.md、references/capabilities/tire-sign-and-unit-gate.md |
| 这胎的侧偏刚度是多少 lb/deg；侧偏系数 0.15 换算成绝对刚度；换低高宽比胎转向会灵敏多少；1/deg 与 lb/deg 怎么换算、per rad 多少；拟合侧偏刚度要不要先扣残差 | references/capabilities/cornering-stiffness-from-coefficient.md | references/capabilities/tire-sign-and-unit-gate.md、references/capabilities/lateral-force-three-regimes.md、references/capabilities/understeer-balance-by-normalized-stiffness.md |
| 外倾能出多少侧向力；只有侧偏刚度，怎么估外倾刚度；子午线外倾刚度比斜交小多少；胎压对外倾刚度的影响；0.25 lb/deg per psi 是谁的系数 | references/capabilities/camber-stiffness-magnitude.md | references/capabilities/rut-criterion-0175.md、references/capabilities/cornering-stiffness-from-coefficient.md、references/capabilities/aligning-moment-three-sources.md |
| 车在车辙路上会不会被拽进辙里、会不会爬出车辙；0.0175 这个判据怎么来的、能不能推导；横坡 2° 时阈值是多少；换子午线胎后高速发飘/找辙是不是外倾推力不够；外倾项要不要算进不足转向梯度 | references/capabilities/rut-criterion-0175.md | references/capabilities/camber-stiffness-magnitude.md、references/capabilities/understeer-balance-by-normalized-stiffness.md、references/capabilities/conicity-and-ply-steer.md |
| 回正力矩怎么算、系数取多少；原地打方向为什么很沉；外倾产生的回正力矩有多大；M_z 对整车横摆影响大不大；换胎后转向手感变化 | references/capabilities/aligning-moment-three-sources.md | references/capabilities/camber-stiffness-magnitude.md、references/capabilities/combined-slip-and-friction-circle.md、references/capabilities/aligning-moment-three-sources.md |
| 弯道制动还剩多少侧向力；为什么制动入弯比驱动出弯更危险；摩擦圆怎么用、能不能算；侧向加速度多大时制动性能最差；先抱死哪个轮、甩尾还是推头 | references/capabilities/combined-slip-and-friction-circle.md | references/capabilities/mu-surface-selection.md、references/capabilities/lateral-force-three-regimes.md、references/capabilities/aligning-moment-three-sources.md |
| 换胎后跑偏、定位数据却合格；松手往一边跑是轮胎问题还是悬架问题；圆锥度和帘布层转向怎么区分；正反滚动测出的侧向力怎么分离；调气压能不能修跑偏 | references/capabilities/conicity-and-ply-steer.md | references/capabilities/rut-criterion-0175.md、references/capabilities/cornering-stiffness-from-coefficient.md、references/capabilities/tire-sign-and-unit-gate.md |
| 过坎/坑洞冲击力多大；耐久载荷谱的幅值怎么定；高速过接缝为什么伤悬架；低速过减速带能不能用同一个公式；轮胎能不能吸收冲击 | references/capabilities/step-impact-and-longitudinal-forces.md | references/capabilities/tire-modes-and-anti-resonance.md、references/capabilities/lateral-force-three-regimes.md |
| 某个频率的抖动是不是轮胎共振、会不会传到轮轴；60/90/110 Hz 各是什么振型；反共振是什么意思、为什么传递率峰值在那里；轮轴跳动和轮胎模态怎么分；换子午线胎后 NVH 为什么变化 | references/capabilities/tire-modes-and-anti-resonance.md | references/capabilities/step-impact-and-longitudinal-forces.md、references/capabilities/tire-structure-coefficient-map.md |
| 换胎后车会推头还是甩尾；前后侧偏刚度怎么比、谁该更大；为什么不能直接用侧偏刚度绝对值比较；载荷转移会不会让侧向力变小；前轮侧偏刚度越大越好吗 | references/capabilities/understeer-balance-by-normalized-stiffness.md | references/capabilities/cornering-stiffness-from-coefficient.md、references/capabilities/rut-criterion-0175.md、references/capabilities/aligning-moment-three-sources.md |
| 换胎能改转向吗、能改极限吗；低扁平胎为什么转向更灵敏；胎压/花纹/轮辋宽度对侧偏刚度的影响方向；子午线和斜交的系数差异从哪来；1992 年的数据能不能用于现代胎 | references/capabilities/tire-structure-coefficient-map.md | references/capabilities/cornering-stiffness-from-coefficient.md、references/capabilities/understeer-balance-by-normalized-stiffness.md、references/capabilities/camber-stiffness-magnitude.md |

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

- 用户要求"本章给出的 $C_\alpha$ 绝对值"时停止：本章无该数据，只能由侧偏系数 × 载荷反算并标"反算值"。
- 用户要求"给定 $F_x$ 下还剩多少 $F_y$"的定量答案时停止：本章无解析式（G3），只能给摩擦圆包络与方向。
- 用户要求"湿路峰值滑动率"时停止：原文只说"湿路最大摩擦力是载荷的 25%–50%"（$\mu_p$），湿路 $s_p$ 未给。
- 用户要求"$\mu(F_z)$ 的曲线/公式"时停止：只有局部斜率与全域割线两条互不相容的口径，禁止插值。
- 用户要求"每 psi 提高多少 $\mu$"或"$C_\alpha$ 的气压系数"时停止：本章无 $\mu$ 的气压系数；0.25 lb/deg per psi 只属斜交外倾刚度。
- 用户要求"圆锥度多少 psi 抵多少 lb"时停止：原文只给方向，无灵敏度。
- 用户要求"反共振频率是多少 Hz"时停止：原文未给数值，只给"共振之间的波峰"。
- 用户要求弯道制动的最不利侧向加速度按路面缩放（如 0.12g）时停止：本章无此规则，0.3g 是干路轿车经验值。
- 用户要求用本章数据讨论驻波或高速极限时停止：本章无驻波、无高速/瞬态数据。
- 用户要求把附录 A 的公式代入计算时停止：附录 A 是术语表，且 7.3.3.14（cos→sin）与 7.3.3.6（乘→除、ν→γ）有硬伤。
