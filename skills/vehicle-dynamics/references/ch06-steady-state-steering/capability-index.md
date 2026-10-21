# 能力索引（完整版）

| capability_id | 标题 | 重要度 | 意图 | 关键词 | 能力卡 |
|---|---|---|---|---|---|
| cap.gillespie-ch6.steer-character-k | 转向特性判定：由轴荷与整轴侧偏刚度算 K，再判三态 | critical | 判断一辆车是推头还是甩尾；由轴荷与轮胎侧偏刚度算不足转向梯度 K；校核算出的 K 是否差了两倍（口径错） | 不足转向梯度、推头、甩尾、understeer gradient、cornering stiffness、转向特性 | capabilities/steer-character-k.md |
| cap.gillespie-ch6.axle-rule-direction | 前后轴对置判据：任何效应只看它把哪个轴的侧偏角做大 | high | 某个改装动作会让车更推头还是更甩尾；手头没有系数但需要一个可靠的方向结论；六项分项符号互相矛盾需要一个仲裁判据 | 轴别判据、方向判断、axle rule、不足转向方向、过多转向方向 | capabilities/axle-rule-direction.md |
| cap.gillespie-ch6.roll-chain-kphi-phi-dfz | 侧倾链：悬架侧倾刚度→侧倾率→前后轴侧倾力矩→轮荷差 | high | 由弹簧刚度与间距算侧倾刚度、侧倾率与轮荷差；前后轴各分到多少侧倾力矩；加了稳定杆侧倾率能降多少 | 侧倾刚度、侧倾率、侧倾力矩、轮荷差、roll stiffness、lateral load transfer | capabilities/roll-chain-kphi-phi-dfz.md |
| cap.gillespie-ch6.camber-thrust-k | 外倾推力对 K 的贡献：外倾梯度×侧倾率 | medium | 外倾对不足转向梯度贡献多少 deg/g；外倾梯度与侧倾率怎么接进 K；整体轴要不要算外倾项 | 外倾推力、外倾梯度、camber thrust、camber gain、K_camber | capabilities/camber-thrust-k.md |
| cap.gillespie-ch6.compliance-steer-k | 侧向力柔顺转向：横摆中心判方向，A 系数算幅值 | medium | 换衬套后转向特性会往哪边变；柔顺转向 K_lfcs 贡献多少；横摆中心位置怎么判不足还是过多 | 柔顺转向、横摆中心、衬套、compliance steer、K_lfcs | capabilities/compliance-steer-k.md |
| cap.gillespie-ch6.drive-force-steering | 驱动力影响的三项式读法：前驱/后驱/四驱方向 | medium | 前驱/后驱/四驱加油门时车头往哪偏；扭矩分配怎么影响转向特性；用三项式解释前驱出弯表现 | 驱动力、前驱、后驱、四驱、torque vectoring、power oversteer | capabilities/drive-force-steering.md |
| cap.gillespie-ch6.constant-radius-test | 等半径法实测 K：选法、执行流程与 δ–a_y 曲线判读 | high | 设计并执行一次定圆稳态回转试验；从 δ–a_y 数据读不足转向梯度；判断曲线在大侧向加速度处是否变号 | 等半径法、定圆试验、constant radius、skid pad、稳态回转 | capabilities/constant-radius-test.md |
| cap.gillespie-ch6.constant-speed-test | 等速法实测 K：用阿克曼梯度线做基准 | medium | 用等速法测不足转向梯度；固定车速打方向的数据怎么算 K；与阿克曼梯度线怎么比 | 等速法、constant speed test、阿克曼梯度、横摆角速度、实测 K | capabilities/constant-speed-test.md |
| cap.gillespie-ch6.understeer-tuning | 设计调校决策链：改哪个零件→动哪一项→K 往哪个方向（限定版） | critical | 把过多转向的车调成不足转向；这套改装方案的方向对不对；除了改弹簧还能动什么 | 调校、改装方案、稳定杆、tuning、understeer fix、转向特性调整 | capabilities/understeer-tuning.md |
| cap.gillespie-ch6.low-speed-geometry | 低速转向几何：阿克曼角与偏离轮迹 | high | 算某半径下的阿克曼角与内外轮转角差；算货车/客车的偏离轮迹（内轮差）；判断停车场刮胎是不是几何问题 | 阿克曼角、偏离轮迹、内轮差、Ackerman、off-tracking、转弯半径 | capabilities/low-speed-geometry.md |
| cap.gillespie-ch6.understeer-gradient-definition | 不足转向梯度 K 的定义式与「每轴两轮」口径 | critical | 侧偏刚度要不要乘 2、每轴两轮还是单胎；算出的 K 是别人的两倍，怀疑口径；只有单胎侧偏刚度，要接进整车公式 | 每轴两轮、侧偏刚度口径、单胎、per axle、cornering stiffness | capabilities/understeer-gradient-definition.md |
| cap.gillespie-ch6.characteristic-speed | 特征车速 V_char（只对不足转向） | high | 算特征车速；这车多少速度转向最敏感；为什么特征车速很高反而不安全 | 特征车速、characteristic speed、V_char、灵敏度峰值 | capabilities/characteristic-speed.md |
| cap.gillespie-ch6.critical-speed | 临界车速 V_crit（只对过多转向） | high | 算临界车速并说明含义；过多转向的车开到多快会失控；甩尾是不是车的问题而不是技术问题 | 临界车速、critical speed、V_crit、方向不稳定、oversteer instability | capabilities/critical-speed.md |
| cap.gillespie-ch6.cg-sideslip-angle | 质心侧滑角 β 的定义式与 SAE 符号 | medium | 算质心侧滑角 β；判断某工况下车尾会不会外甩；与实车测得的 β 对比 | 侧滑角、质心、sideslip angle、body slip、β | capabilities/cg-sideslip-angle.md |
| cap.gillespie-ch6.beta-zero-speed | β=0 的车速（与转向半径无关） | low | 什么速度下侧滑角为零；车尾什么时候开始外甩；β=0 车速与转弯半径有关系吗 | β=0、侧滑角零点、sideslip zero、姿态变号 | capabilities/beta-zero-speed.md |
| cap.gillespie-ch6.static-margin | 静态裕度 e/L 与符号判据 | high | 算静态裕度 e/L；中性转向点在哪里；静态裕度 0.8% 是不是不安全 | 静态裕度、储备系数、static margin、中性转向点 | capabilities/static-margin.md |
| cap.gillespie-ch6.ackerman-angle | 阿克曼角（内外轮分开，小转向角） | high | 算某半径下的内外轮转角；阿克曼误差有多大；平行转向有什么问题 | 阿克曼角、内外轮转角差、Ackerman、平行转向 | capabilities/ackerman-angle.md |
| cap.gillespie-ch6.off-tracking | 偏离轮迹 Δ 与一次近似 | medium | 算偏离轮迹/内轮差；大车转弯扫过多宽；一次近似能用吗 | 偏离轮迹、内轮差、off-tracking、tractrix、扫掠宽度 | capabilities/off-tracking.md |
| cap.gillespie-ch6.two-wheel-preconditions | 两轮（自行车）模型的假设清单——代入任何公式前逐条核对 | critical | 这个公式/工况适不适用；为什么我的仿真与公式差很多；报告里要写模型适用域与局限 | 两轮模型、假设清单、bicycle model、linear tire、稳态假设、适用域 | capabilities/two-wheel-preconditions.md |
| cap.gillespie-ch6.roll-stiffness-formula | 悬架侧倾刚度 K_φ=0.5K_s s² 及三种代入口径 | high | 由弹簧刚度与间距算侧倾刚度；稳定杆刚度怎么叠加；in·lb/rad 与 in·lb/deg 怎么换 | 侧倾刚度、roll stiffness、K_phi、稳定杆、弹簧刚度 | capabilities/roll-stiffness-formula.md |
| cap.gillespie-ch6.load-transfer-two-mechanisms | 轮荷差双机制拆分（瞬时项/可调项） | high | 加稳定杆能减少多少载荷转移；轮荷差怎么拆成两部分；为什么调了悬架轮胎还是偏磨 | 轮荷差、载荷转移、几何项、弹性项、load transfer | capabilities/load-transfer-two-mechanisms.md |
| cap.gillespie-ch6.roll-rate | 侧倾率 R_φ 及 rad/deg 口径陷阱 | high | 每 g 侧倾几度；侧倾率算出负的怎么办；10.5 deg/g 正常吗 | 侧倾率、侧倾角、roll rate、roll gradient | capabilities/roll-rate.md |
| cap.gillespie-ch6.roll-moment-front-bias | 侧倾力矩偏前的四条理由 + 稳定杆布置规则 | high | 防倾杆装前轴还是后轴；只加后稳定杆行不行；为什么原厂前防倾杆更粗 | 稳定杆、防倾杆、侧倾力矩分配、sway bar、偏前 | capabilities/roll-moment-front-bias.md |
| cap.gillespie-ch6.camber-angle-composition | 地面外倾角合成与含外倾的侧偏力叠加 | medium | 地面外倾角怎么算；外倾等效多少侧偏角；两个外倾角要不要相加 | 外倾角合成、地面外倾、camber、参考系 | capabilities/camber-angle-composition.md |
| cap.gillespie-ch6.camber-magnitude-screen | 外倾量级三条分流判据 | medium | 这辆车要不要算外倾项；外倾对 K 影响大不大；改外倾能治推头吗 | 外倾量级、camber、斜交胎、子午胎、整体轴 | capabilities/camber-magnitude-screen.md |
| cap.gillespie-ch6.aligning-torque-k | 回正力矩项 K_at：恒为正、通常 <0.5 deg/g | medium | 回正力矩对 K 有多大影响；能不能靠主销后倾把车调向过多；K_at 恒正是好事吗 | 回正力矩、拖距、aligning torque、K_at、pneumatic trail | capabilities/aligning-torque-k.md |
| cap.gillespie-ch6.sae-k-definition | SAE 对不足转向梯度的定义（转向盘口径） | medium | 我的 K 和厂家差 10% 正常吗；hand-wheel 还是 road-wheel；转向盘转角除以传动比对不对 | SAE、转向盘口径、hand-wheel、road-wheel、传动比、转向系统柔度 | capabilities/sae-k-definition.md |
| cap.gillespie-ch6.test-method-choice | 四种试验法只取两种：K 测量方法选型 | medium | 用哪种方法测 K；等半径还是等速；只有油门和方向盘可控能测吗 | 试验方法、等半径法、等速法、等转向角法、test method | capabilities/test-method-choice.md |
| cap.gillespie-ch6.units-constants-checklist | 单位与常数口径清单（全章英制，含 r 的双单位） | critical | 这些公式用英制还是 SI、怎么换算；为什么算出负的侧倾率/异常半径；结果数量级不对，先查什么 | 单位换算、英制、57.3、ft/s、rad/s、口径清单 | capabilities/units-constants-checklist.md |
| cap.gillespie-ch6.olley-criterion | Olley 判据：由扰动后的走向判定不足/过多转向 | medium | 不用公式怎么判推头还是甩尾；侧风/路面凸起后车头往哪偏说明什么；为什么甩尾会越来越严重 | Olley、扰动判据、侧向扰动、disturbance、正反馈 | capabilities/olley-criterion.md |
| cap.gillespie-ch6.design-lever-inventory | 设计入口原则：能动侧偏力的都是旋钮（七通道穷举） | high | 这车推头，除了改弹簧还能动什么；改装方案有没有漏掉某条通道；调校从哪儿入手 | 设计入口、旋钮、七通道、design lever、调校手段 | capabilities/design-lever-inventory.md |
| cap.gillespie-ch6.load-transfer-only-distributed | 横向载荷转移的转向效应不可消除，只能分配 | high | 能不能消除横向载荷转移；调前后侧倾刚度比会让车往哪边变；为什么加硬弹簧没用 | 横向载荷转移、不可消除、load transfer、只能分配、平方律 | capabilities/load-transfer-only-distributed.md |
