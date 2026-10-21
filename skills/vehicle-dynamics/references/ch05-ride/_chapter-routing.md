---
name: vehicle-ride-comfort
description: |
  当用户处理乘用车/商用车「乘适性（ride comfort）」问题时调用：把主观抱怨（颠、晃、抖、麻手、
  过坎顶到底）先归到「输入—传递—判据」三段并按频率窗分诊；把路面谱按 $f=\nu V$ 换成时间谱、
  给出 $a\propto V^2$ 的倍数与轮辙和/差（侧倾通道）；算乘适刚度 $RR$、跳动/俯仰固有频率、
  静挠度尺与车轮 hop 频率；校核行程预算（1 Hz 需 5 in 吸收 0.5 g）与阻尼可用上限（ζ=0.2/0.4 只降 2%/8%）；
  评减振器阀配置、判线性谱方法何时失效；算主动 vs 被动的成对收益（−30% / 约束 20% 后 −10%）；
  算轴距滤波零点（跳动奇次倍、俯仰偶次倍）；算跳动/俯仰双模态频率与两个运动中心；
  做 Olley 四准则 + 动态指数 $DI$ 的前后悬架匹配校核；定位车上激振源（轮胎/传动系/发动机）的阶次；
  以及判读人体容许界限曲线（只给形状与出处，不给限值）与乘适性谱的呈现规范（线性-线性）。
  
  输出一律附口径声明：全章英制（lb/in、in、ft、mph、cyc/ft，$g=386$ in/s²，$0.159=1/(2\pi)$ 绑英制）、
  $W$ 是单轮荷、$W_a$ 是车轴重、跳动串联 $RR$ / hop 并联 $K_t+K_s$、$Z/\theta$ 只给区间（±6%）。
  强制声明五个全局前提：①线性粘性阻尼（与 5.2.7 的非线性自证冲突）；
  ②式(5-11) 整条缺失，ζ 由式(5-19c) 重构（非原文）；③式(5-15)(5-16) 损坏 ⇒ 力通道 $F_w/F_b$ 不可复现；
  ④41 张图全为 PNG 占位 ⇒ 零读数；⑤$G_0$ 绝对标度与图5.2 刻度差约两个数量级 ⇒ 只给形状/拐点/波数窗。
  
  不适用于：任何以 m/s² 或 g 表示的舒适性数值限值（本章没有）、ISO 2631-1:1997 的 $W_k/W_d$ 加权与
  VDV/EU 限值、5.3 的"人的感受"做成可算能力（只作判据/警告）、路面 PSD 的绝对数值（H-1）、
  被动悬架工作点选点（图5.23 无数表，H-2）、接地性/轮胎动载的传递函数（G-1）、
  车身结构模态（>25 Hz 仅一句提及）、离散冲击的峰值指标（只到频域）、半主动/天棚/预瞄控制律。
  
  Triggers: 乘适性/平顺性/ride comfort/ride quality/颠/晃/抖/麻手/发飘/过坎顶到底/某车速才抖/
  乘适刚度/ride rate/跳动固有频率/bounce frequency/静挠度/static deflection/行程预算/suspension travel/
  限位块/bump stop/阻尼比/damping ratio/200% 阻尼/减振器/valving/车轮 hop/wheel hop/簧下质量/unsprung mass/
  路面谱/PSD/wavenumber/侧倾输入/roll excitation/车速平方/主动悬架/active suspension/30%/10%/
  轴距滤波/wheelbase filter/零点/双模态/运动中心/center of oscillation/Zθ/Olley/欧雷准则/动态指数/DI/
  阶次/order/传动轴不平衡/万向节/点火频率/发动机悬置/容许界限/等舒适度曲线/1/3 倍频带/线性-线性
metadata:
  cangjie.generated-by: cangjie-tools v2.5.0
  cangjie.variant: single
  cangjie.bundle-id: bundle.gillespie-ch5-ride
  cangjie.capability-count: 13
  cangjie.entrypoint-count: 1
---
# 《车辆动力学基础》第 5 章 乘适性 — 全书能力入口

## 触发与不触发

**适用**：与本书能力域相关的咨询与任务（见下方路由表的意图列）。
**不适用**：
- 任何以 m/s² 或 g 表示的舒适性数值限值（本章没有；ISO 只有"第二版"且标准号 OCR 缺失）
- ISO 2631-1:1997 的 $W_k/W_d$ 加权、VDV（$a_w^4T$）剂量、EU 2002/44/EC 的 0.5 / 1.15 m/s² 行动值与限值（本章完全无剂量概念）
- 5.3「人的感受」做成可算能力（硬性约束：只作判据/警告；不得输出单一加权 RMS 当 KPI）
- 路面 PSD 的绝对数值 $G_z$（H-1：$G_0$ 标度与图5.2 刻度差约两个数量级，单位口径未交代）
- 被动悬架工作点的选点计算（H-2：图5.23 无数表、$S_0$ 未给、纵轴单位不清）
- 接地性/轮胎动载的传递函数（G-1：式(5-15)(5-16) 损坏，$F_w/F_b$ 不可复现）
- 车身结构模态（>25 Hz 只有 p124 一句定性）、离散冲击的峰值指标（只到频域）
- 半主动（CDC/磁流变）、天棚阻尼、预瞄与路面感知控制律；主动悬架的成本/可靠性/能耗
- 侧倾刚度与力矩分配、侧倾中心（属第 6/7 章；本章全文未出现"侧倾中心"）
- 轮胎包络（enveloping）解析模型、$K_t$ 的频率/胎压/载荷依赖、多轴/挂车的轴距滤波

## 核心原则（常驻速览，概览类问题读到这里即可回答）

1. 乘适性是一条三段链（输入 → 传递 → 判据）：输入＝路面 1 类 + 车上旋转件 3 类，传递＝四分之一车辆 → 刚体双模态 → 非线性 → 主动，判据＝人体容许界限；归错段，后面每一步都白算。
2. 全章只有两根几何杠杆：纵向的 $f=\nu V$（把波数换成频率、再微分两次给 $a\propto V^2$）与横向的轮辙和/差（平均喂跳动/俯仰，差值喂侧倾，长波处只 10%）。
3. 低频可算部分只有三个数：串联乘适刚度 $RR$、由它来的跳动频率 $f_n=0.159\sqrt{RR/(W/g)}$、以及等价表述静挠度（10 in↔1 Hz、5↔1.4、1↔3.13）——"软不软"可以只用一把尺子量；而这两个天花板挡住了"越软越好"：行程（1 Hz 需 ≥5 in 吸收 0.5 g，量产锁在 1–1.5 Hz）与阻尼（ζ=0.2/0.4 只把频率拉低 2%/8%，但峰高成倍变；200% = ζ=2.0 过阻尼）。
4. 高频端有两处不可忽视：hop（并联 $K_t+K_s$，10.36 Hz，含摩擦 12–15 Hz，簧下质量是唯一纯收益杠杆）与车上旋转件的阶次线族（峰随车速移动的才是旋转件）。
5. 整车级只有两条可算结论：轴距滤波（跳动零点 $V/2L$ 奇次倍、俯仰偶次倍 ⇒ 高速只剩跳动）与双模态（$\alpha,\beta,\gamma$ ⇒ 两个 Hz + 两个运动中心，$Z/\theta$ 病态只给区间）。
6. 调校的经验法则（Olley 四准则 + $DI$）能筛不能定：1930s 单车单人无样本、"低 30%"与"后移 6.5%L"不等价（8.8% vs 23%）、四条互相不独立，原文末句"最佳频率比要由实验确定"。
7. 判据端没有公认换算尺：全章无以 m/s² 或 g 表示的限值，ISO 只到"第二版"（标准号缺失），加权被 Healey 反证为未验证工具——所以交付物是"谱形整形"，不是"RMS 最小"。

## 能力路由（先读本表，按意图加载 1 张能力卡）

| 用户意图 | 先读 | 补读/备注 |
|---|---|---|
| 用户给一句主观抱怨，判断这是哪一类乘适性问题、该改哪里；判断某个频谱峰属于哪一段（输入/传递/判据）；决定下一笔钱花在弹簧、减振器、轮胎、悬置还是转向盘隔振上；解释为什么高速反而比低速舒服（或反过来） | references/capabilities/ride-triage-and-resonance-windows.md | references/capabilities/road-input-spectrum-and-track-split.md、references/capabilities/ride-rate-and-bounce-frequency.md、references/capabilities/wheel-hop-and-unsprung-mass.md、references/capabilities/onboard-excitation-orders.md |
| 同一段烂路车速翻倍颠几倍；路面谱（cyc/ft）怎么换成车内谱（Hz）；水泥路和沥青路哪个更颠、过接缝的冲击能不能用谱算；4×4 低速为什么晃、高速为什么不晃；只有单侧轮辙数据，能不能代表整车垂直输入 | references/capabilities/road-input-spectrum-and-track-split.md | references/capabilities/quarter-car-gain-and-spectrum-product.md、references/capabilities/wheelbase-filter-zeros.md、references/capabilities/ride-triage-and-resonance-windows.md |
| 有路面谱和悬架参数，预测车内加速度谱；有实测车内谱，反推"是输入大还是传递差"；隔振为什么低频放大、高频衰减、共振最差；轮胎动载/接地性能不能算 | references/capabilities/quarter-car-gain-and-spectrum-product.md | references/capabilities/road-input-spectrum-and-track-split.md、references/capabilities/ride-rate-and-bounce-frequency.md、references/capabilities/wheel-hop-and-unsprung-mass.md、references/capabilities/damper-valving-and-hysteresis.md |
| 由弹簧/轮胎刚度与轮荷算跳动固有频率；想"把悬架调软一点"，先知道现在多少 Hz；只有静态压缩量（或只有频率），两者互换；换软胎能不能变舒服 | references/capabilities/ride-rate-and-bounce-frequency.md | references/capabilities/travel-budget-and-damping-limits.md、references/capabilities/wheel-hop-and-unsprung-mass.md、references/capabilities/olley-criteria-and-dynamic-index.md |
| 想调到 1 Hz，行程够不够、会不会撞限位块；为什么量产车做不到 1 Hz、豪华车为什么能更软；阻尼比 0.3 够不够、能不能用无阻尼频率算共振；100%/200% 阻尼是什么意思 | references/capabilities/travel-budget-and-damping-limits.md | references/capabilities/ride-rate-and-bounce-frequency.md、references/capabilities/damper-valving-and-hysteresis.md、references/capabilities/active-vs-passive-paired-gain.md |
| 审一份减振器规格/调校方案，判断缺什么；为什么平路反而更颠、烂路反而舒服；能不能用频域方法算这辆车的响应；换了减振器为什么 hop 频率没按预期变 | references/capabilities/damper-valving-and-hysteresis.md | references/capabilities/travel-budget-and-damping-limits.md、references/capabilities/quarter-car-gain-and-spectrum-product.md、references/capabilities/wheel-hop-and-unsprung-mass.md |
| 要不要上主动/半主动悬架，需要可比的收益；宣传里的"主动降 30%"能不能引用；为什么主动悬架在烂路/10 Hz 附近提升有限；隔振、行程、接地性三个指标能不能合成一个分数 | references/capabilities/active-vs-passive-paired-gain.md | references/capabilities/travel-budget-and-damping-limits.md、references/capabilities/damper-valving-and-hysteresis.md、references/capabilities/quarter-car-gain-and-spectrum-product.md |
| 换铝转向节/轻轮毂/碳纤维轮有没有用、能提升多少；为什么几乎所有车的 hop 都在 10–12 Hz；有 GAWR 没有称重数据，怎么估非悬挂质量；减速带过后车轴发抖/轮胎离地 | references/capabilities/wheel-hop-and-unsprung-mass.md | references/capabilities/ride-rate-and-bounce-frequency.md、references/capabilities/quarter-car-gain-and-spectrum-product.md、references/capabilities/onboard-excitation-orders.md |
| 某个车速才抖，是什么坏了；区分轮胎、传动轴、万向节、发动机；做动平衡有没有用、换胎能改善多少；怠速抖动、加速轰鸣、发动机悬置怎么定 | references/capabilities/onboard-excitation-orders.md | references/capabilities/wheel-hop-and-unsprung-mass.md、references/capabilities/ride-triage-and-resonance-windows.md、references/capabilities/road-input-spectrum-and-track-split.md |
| 高速为什么只剩跳动、俯仰去哪了；为什么某个频率在某些车速下消失；路谱采集传感器装哪里；这个峰是跳动还是俯仰 | references/capabilities/wheelbase-filter-zeros.md | references/capabilities/pitch-bounce-bimodal-and-centers.md、references/capabilities/olley-criteria-and-dynamic-index.md、references/capabilities/road-input-spectrum-and-track-split.md |
| 算整车级跳动/俯仰两个模态频率；判断哪个模态主导（跳动还是俯仰）；读例 5.2.11-2 的载荷扫描表；这个 Z/θ 值能不能引用 | references/capabilities/pitch-bounce-bimodal-and-centers.md | references/capabilities/olley-criteria-and-dynamic-index.md、references/capabilities/ride-rate-and-bounce-frequency.md、references/capabilities/wheelbase-filter-zeros.md |
| 做前后悬架匹配校核，要一张通过/不通过清单；前簧该比后簧软多少、6.5% 轴距是什么意思；DI 是什么、等于 1 有什么好处；Olley 准则还算不算数、能不能当标准 | references/capabilities/olley-criteria-and-dynamic-index.md | references/capabilities/pitch-bounce-bimodal-and-centers.md、references/capabilities/ride-rate-and-bounce-frequency.md、references/capabilities/wheelbase-filter-zeros.md |
| 这张实测谱哪个频带最值得改；乘适性报告的结论段能写到什么程度；网上流传的"ISO 限值 0.315 m/s²"能不能挂到本书名下；谱该用线性-线性还是双对数；主观评价试验怎么设计才不被污染 | references/capabilities/human-limit-and-spectrum-presentation.md | references/capabilities/ride-triage-and-resonance-windows.md、references/capabilities/quarter-car-gain-and-spectrum-product.md、references/capabilities/active-vs-passive-paired-gain.md |

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

- 用户要求"这车舒适不舒适 / 给个合格线 / 多少 m/s² 算超标"时停止：本章任何位置都没有数值限值，只能给形状性结论、1/3 倍频带最差带与出处。
- 用户要求"按 ISO 2631-1:1997 算加权 RMS / VDV 剂量"时停止：本章只有"第二版"且无标准号，不得代写标准条文。
- 用户要求"某路面某波数的 $G_z$ 绝对数值"时停止：$G_0$ 标度与图5.2 刻度差约两个数量级（H-1），只能给形状/拐点/波数窗/"两档差 10 倍"。
- 用户要求"在加速度—行程平面上选最优 ζ / 给最优工作点"时停止：图5.23 无数表、$S_0$ 未给、纵轴单位不清（H-2），只能给定性排序。
- 用户要求"轮胎动载/接地性的定量改善"时停止：式(5-15)(5-16) 损坏，力通道不可复现（G-1），只能给方向与 ζ_un 约束。
- 缺单轮荷 $W$、$K_s$、$K_t$ 任一而要求固有频率时停止：用 $K_s$ 代 $RR$ 会高估约 6%，用轴荷代单轮荷会低估约 29%。
- 缺轴距 $L$ 或缺车速 $V$ 而要求"某频率会不会共振/零点在哪"时停止：全部频率都经 $f=\nu V$ 与车速绑定。
- 缺 $k^2$ 或 $DI$ 而要求双模态频率与运动中心时停止：$k^2$ 不可从本章其他量推得，例题是由 $DI$ 反求（假设）。
- 只拿到主动悬架"降 30%"一个数时停止：必须成对取得约束后的数（ζ_un=20% → −10%）与架构限定，否则拒绝给收益。
- 用户要求把"消掉某个振动"当验收标准时停止：原文明确消除一个会暴露下一个、且振动是路感反馈；输出必须是"谱形目标 + 必须保留的频带"。
