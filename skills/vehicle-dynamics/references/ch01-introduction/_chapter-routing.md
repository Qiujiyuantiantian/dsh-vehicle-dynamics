---
name: vehicle-dynamics-base
description: |
  当用户处理车辆动力学「最底层」问题时调用：由两轴载荷反求重心纵向位置（b、c）、算静态轴荷、
  算含空气阻力与拖钩力的动态轴荷一般式、算加速/减速的载荷转移、算坡道轴荷与坡度 %↔° 换算、
  判断"坡上两轴载荷之和为什么小于总重"、拆拖挂两体解拖钩力并判 FWD/RWD/4WD 的爬坡优劣、
  选定建模自由度与自由体图、核对 SAE 符号与力矩正方向。
  
  输出一律附**口径声明**：全章英制（lb、in、ft/s²，g=32.2 ft/s²）；**b = 前轴→重心、c = 重心→后轴**
  （与很多英文文献相反）；$W_f$、$W_r$ 为**垂直力、取正**；$\theta$ 上坡正下坡负、小角度式用弧度；
  坡度按**正切**；轴荷为**准静态**（无俯仰角加速度）。
  
  强制声明五个全局前提：①式(1-5) 的惯性项**必须取 +**（OCR 作 −，照抄得 $W_r$=1119.4 而非 1347.3）；
  ②恒等式 $W_f+W_r=W\cos\theta+R_{hz}$ 是唯一收尾自检（无拖车时 = $W\cos\theta$）；
  ③例题 3 的 10.18%/11.42%/19.44% 只能作**原书报告值**，不可当基准（独立重建 10.9%/11.6%/20.7%）；
  ④本卡集覆盖的是**准静态、单质量刚体**，不含瞬态与横向；⑤图 1.2 正文无逐点数值，不得给具体车速。
  
  不适用于：功率/扭矩受限的爬坡能力、不具备完全防滑功能的 4WD、瞬态轴荷与点头/抬头
  （需 $I_{yy}\dot q$，本章未给）、横向载荷转移与侧倾、轮胎力学与 $\mu(V,T,p)$、
  货车/挂车多体与 >2 自由度的判据、欧拉角的旋转矩阵与三个角位移符号（正文未印）、
  小角度近似失效的定量边界（原文未给）、FWD/RWD 爬坡闭式解（OCR 残缺，不可引用）。
  
  Triggers: 轴荷/轴重/前轴载荷/后轴载荷/axle load/weight distribution/重心位置/CG location/b、c/
  载荷转移/load transfer/weight transfer/加速轴荷/制动轴荷/坡度/坡道/grade/爬坡度/%
  arctan/sin tan 换算/轴荷之和/为什么少了 6 磅/拖钩/拖挂/hitch/towing/爬坡能力/gradeability/
  FWD/RWD/4WD/附着力/adhesion/单质量/两质量/lumped mass/簧上簧下/自由体图/FBD/法向力/垂直力/
  normal force/vertical force/力矩正方向/SAE J670e/符号约定
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch1-introduction
  cangjie.capability-count: 8
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 1 章 绪论 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 功率或扭矩受限的爬坡能力、最高车速（本章只有附着受限上限）
- 不具备完全防滑功能的 4WD 的驱动力分配（原文明确"需要更复杂的方法"）
- 瞬态轴荷、俯仰角加速度 $I_{yy}\dot q$、点头/抬头（dive/squat）的定量
- 横向载荷转移、侧倾刚度与侧倾力矩分配
- 轮胎力学：$\mu$ 随滑移率/速度/温度/胎压的变化，轮胎侧偏角 $\alpha$ 与侧偏刚度
- 货车、挂车、多体与 >2 自由度的自由度判据
- 欧拉角的旋转矩阵、三个角位移符号与转角正负号；$\nu=\psi\pm\beta$ 的关系式
- 小角度近似失效的定量界线（原文只暗示 10%–12% 仍在使用）
- 图 1.2 的逐点车速（正文无逐点数值，只能给趋势与轴量程）

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 全章只有一根主链：坐标系与符号 → 自由体（六类力）→ 对另一轴接地点取矩 → 轴荷一般式 → 退化三特例 → 拖挂两体 → 附着判据。跳步得到的只是算术结果，不是可交付结论。
2. 轴荷不是常数：它随加速度、坡度、空气阻力（及其高度）、拖钩力（两个力臂）变化；静载荷只是 $a_x=\theta=D_A=R_h=0$ 的特例，用静值算性能会系统性错。
3. 一切轴荷结果都必须用 $W_f+W_r=W\cos\theta+R_{hz}$ 收尾；坡上"和小于总重"是物理（$W(1-\cos\theta)$），照抄式(1-5) 的负号则会让和少 $2(W/g)a_xh/L$——这两种差必须分开。
4. 符号是本章的主战场：$b/c$ 与多数文献相反、法向力向下而垂直力向上、同一章两处力矩正方向相反、$p/r$ 被 OCR 互换过。约定错一次，整条链反号而不报错。
5. 拖挂必须先拆两体解拖钩力，整车取矩会把它当内力解不出；爬坡能力只判"驱动轴是不是被卸载的那一轴"，绝对百分比原书不可复现。
6. 建模第一步是选自由度（求解量是否依赖车身—车轮相对运动），第二步是核对假设；假设不满足时误差不报错，只给出"看起来像对的数"。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 由两轴载荷反求重心纵向位置；算水平静止时的前后轴静载荷；核对某本书或某软件的重心位置算法；判断对方资料的 b、c 是否与本章相反 | references/capabilities/static-axle-load-and-cg-location.md | references/capabilities/dynamic-axle-load-general-form.md、references/capabilities/acceleration-load-transfer.md、references/capabilities/grade-axle-load-and-grade-angle.md、references/capabilities/axle-load-sum-diagnostic.md |
| 坡上加速时前后轴载荷各多少；拖挂之后轴荷怎么变；空气阻力对轴荷的影响；有坡又有加速度用哪个公式；核对某条轴荷式子是否漏项或符号错 | references/capabilities/dynamic-axle-load-general-form.md | references/capabilities/static-axle-load-and-cg-location.md、references/capabilities/acceleration-load-transfer.md、references/capabilities/grade-axle-load-and-grade-angle.md、references/capabilities/axle-load-sum-diagnostic.md、references/capabilities/towing-gradeability-analysis.md、references/capabilities/sign-convention-and-moment-direction-check.md |
| 加速时前轴会轻多少；制动时前轴加载多少；0.3g 会转移多少载荷；前驱起步为什么打滑 | references/capabilities/acceleration-load-transfer.md | references/capabilities/static-axle-load-and-cg-location.md、references/capabilities/dynamic-axle-load-general-form.md、references/capabilities/grade-axle-load-and-grade-angle.md、references/capabilities/axle-load-sum-diagnostic.md |
| 12% 坡是多少度；坡上前后轴载荷多少；上坡时载荷往哪移；下坡时前轴是不是更重；为什么坡上轴荷之和小于总重 | references/capabilities/grade-axle-load-and-grade-angle.md | references/capabilities/acceleration-load-transfer.md、references/capabilities/dynamic-axle-load-general-form.md、references/capabilities/axle-load-sum-diagnostic.md、references/capabilities/towing-gradeability-analysis.md |
| 前后轴载荷加起来不等于总重；坡上少了 6 磅是不是算错了；轴荷之和对不上怎么查；交付前的轴荷校核 | references/capabilities/axle-load-sum-diagnostic.md | references/capabilities/dynamic-axle-load-general-form.md、references/capabilities/grade-axle-load-and-grade-angle.md、references/capabilities/acceleration-load-transfer.md、references/capabilities/static-axle-load-and-cg-location.md |
| 这车能不能把船从坡上拖上来；为什么前轴更重的前驱车爬坡反而差；拖钩载荷随坡度怎么变；FWD/RWD/4WD 爬坡能力对比；书里的 10.18% 能不能当基准 | references/capabilities/towing-gradeability-analysis.md | references/capabilities/dynamic-axle-load-general-form.md、references/capabilities/grade-axle-load-and-grade-angle.md、references/capabilities/model-setup-fbd-and-assumptions.md、references/capabilities/sign-convention-and-moment-direction-check.md |
| 该用单质量还是两质量模型；簧上簧下要不要分开；自由体图怎么画、有没有漏力；这个公式的假设在本题成立吗；为什么改了悬架参数结果不变 | references/capabilities/model-setup-fbd-and-assumptions.md | references/capabilities/dynamic-axle-load-general-form.md、references/capabilities/sign-convention-and-moment-direction-check.md、references/capabilities/static-axle-load-and-cg-location.md、references/capabilities/acceleration-load-transfer.md |
| 法向力和垂直力有什么区别；轮胎支撑力该取正还是负；力矩正方向怎么定；为什么算出来轴荷是负的；跨标准资料怎么对接符号 | references/capabilities/sign-convention-and-moment-direction-check.md | references/capabilities/model-setup-fbd-and-assumptions.md、references/capabilities/dynamic-axle-load-general-form.md、references/capabilities/towing-gradeability-analysis.md、references/capabilities/axle-load-sum-diagnostic.md |

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

- 缺两轴载荷、只给总重与轴距时停止反求 b、c——两个未知量一个方程，无解。
- 缺重心高 h 时停止一切载荷转移计算；原书例题 2 的 h=20 in 是"因缺数据而假设"，不得当实测值传播。
- 缺 $h_a$（风压中心高）、$h_h$（拖钩高）、$d_h$（拖钩距后轴）时停止把它们默认为 0，改为记"信息不足"并给出偏差方向。
- 当式出现 $R_{hz}$ 而未给拖钩垂直力时停止求和自检，改用 $W_f+W_r=W\cos\theta$ 版本并声明无拖挂。
- 用户要求 FWD/RWD 的绝对爬坡百分比时停止给出精确值，只能给"原书报告值 + 独立重建值（±3%–7%）"两列并标注不自洽。
- 用户要求引用 FWD/RWD 爬坡闭式解时停止：OCR 残缺、分子与"前轴静载"自相矛盾。
- 用户要求把 $\mu$ 当随载荷/滑移/温度变化的量时停止：本章三式的前提是 $\mu$ 为常数。
- 工况为瞬态（急加速、急制动、过坎、拖挂纵向冲击）时停止套用准静态轴荷式，声明出界。
- 用户把例题 3 的"前驱（AWD）"当第四种配置时停止，按 FWD 处理并标注原文笔误。
- 坡道结果的两轴之和小于总重时停止"修正公式"，先按 $W(1-\cos\theta)$ 判正常。
