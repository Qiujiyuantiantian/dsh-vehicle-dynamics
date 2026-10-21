# 能力索引（完整版）

| capability_id | 标题 | 重要度 | 意图 | 关键词 | 能力卡 |
|---|---|---|---|---|---|
| cap.gillespie-ch7.structure-family-selection | 悬架结构选型：先定两族，再按「存在理由 ↔ 代价」逐条核对 | critical | 为一台车选悬架结构并说明代价；麦弗逊/双 A 臂/多连杆/整体桥怎么选；某结构有什么缺点、我漏了什么 | 悬架选型、整体式车轴、独立悬架、solid axle、MacPherson、multi-link | capabilities/structure-family-selection.md |
| cap.gillespie-ch7.active-suspension-ladder | 主动悬架分级选型：按性能模式查能力矩阵，取最低够用等级 | high | 空气悬架算不算主动悬架；半主动够不够、要不要上全主动；主动悬架能不能控侧倾/点头 | 主动悬架、半主动、自调水平、active suspension、semi-active、load leveling | capabilities/active-suspension-ladder.md |
| cap.gillespie-ch7.virtual-point-method | 虚拟作用点法：把任意杆系折算成绕一点摆动的单摆臂 | critical | 这套杆系的虚拟作用点在哪；三连杆的上控制臂要不要算进去；虚拟作用点和瞬心是不是一回事 | 虚拟作用点、虚拟铰接点、virtual point、instantaneous center、三连杆 | capabilities/virtual-point-method.md |
| cap.gillespie-ch7.parallel-arm-infinite-point | 平行杆的无穷远极限法：交点在无穷远时方向由杆件斜率决定 | medium | 上下摆臂平行时侧倾中心怎么算；叶片弹簧的侧倾中心在哪；水平/倾斜平行杆的侧倾中心一样吗 | 平行杆、无穷远、parallel arm、infinite virtual point、叶片弹簧 | capabilities/parallel-arm-infinite-point.md |
| cap.gillespie-ch7.full-compensation-veto | 满额几何补偿的否决检查：把 e/d 调到 100% 之前先过 8 条 | high | 抗后蹲/抗点头做到 100% 行不行；为什么原厂只做一半；完全消除点头有什么代价 | 满额补偿、抗点头上限、100% anti-dive、trade-off、零俯仰 | capabilities/full-compensation-veto.md |
| cap.gillespie-ch7.jacking-risk | 举升（jacking）风险判定：条件齐发才成立，防治只有一条 | critical | 摆动轴为什么会翻车/甩尾；举升（jacking）是什么、怎么防治；加粗防倾杆能不能治举升 | 举升、jacking、tuck under、摆动轴、侧翻 | capabilities/jacking-risk.md |
| cap.gillespie-ch7.equivalent-trailing-arm-ed | 等效拖曳臂归一化：纵向力比只由几何决定 F_z/F_x=e/d | critical | 纵向力和垂向力之比怎么算；等效拖曳臂是什么、没有纵臂能不能用；e 和 d 从哪里量 | 等效拖曳臂、e/d、equivalent trailing arm、Fz/Fx、虚拟铰接点 | capabilities/equivalent-trailing-arm-ed.md |
| cap.gillespie-ch7.anti-squat-100 | 100% 抗后蹲判据：e/d=h/L，与弹簧刚度无关（独立后驱用 (e−r)/d） | critical | 100% 抗后蹲的铰接点放在哪；后悬架加速时下沉多少；独立后悬架为什么按整体式公式算不对 | 抗后蹲、anti-squat、e/d=h/L、独立后悬、(e-r)/d | capabilities/anti-squat-100.md |
| cap.gillespie-ch7.anti-squat-percent | 抗后蹲百分率：(e/d)÷(h/L)，一个不含弹簧刚度的几何比例 | medium | 这台车现在是几成抗后蹲；抗后蹲率怎么算、能不能超过 100%；60% 抗后蹲的分母是什么 | 抗后蹲百分率、percent anti-squat、抗后蹲率、几何比例 | capabilities/anti-squat-percent.md |
| cap.gillespie-ch7.anti-pitch-up-precision | 完全抗前仰：e/d=h/L+(h/L)(K_r/K_f)，2h/L 只作速算 | high | 加速时车身要完全水平需要多大 e/d；2h/L 到底能不能用；抗前仰和抗后蹲差多少 | 抗前仰、anti-pitch、2h/L、刚度比、K_r/K_f | capabilities/anti-pitch-up-precision.md |
| cap.gillespie-ch7.front-drive-anti-lift | 前驱动整体式轴：零前仰条件 e/d=−h/L−(h/L)(K_f/K_r)，支点落在前轴后方 | high | 前驱车加速抬头怎么消；前轴抗提升怎么做、e/d 为负是什么意思；前驱和后驱的抗前仰公式是不是反的 | 抗提升、anti-lift、前驱、FWD、负 e/d | capabilities/front-drive-anti-lift.md |
| cap.gillespie-ch7.five-e-quick-rule | h/L≈0.2 速算：完全抗后蹲约需 5 倍 e 的有效拖曳臂长度 | medium | 完全抗后蹲要留多长的拖曳臂；布置空间不够怎么办；拖曳臂多短算短 | 5倍臂长、有效拖曳臂长度、packaging、power hop、布置 | capabilities/five-e-quick-rule.md |
| cap.gillespie-ch7.pitch-rate-theta-p | 俯仰角变化率 θ_p/a_x：三项结构与 rad/(in/s²)→rad/g→deg/g 单位链 | high | 加速抬头多少度每 g；俯仰角变化率怎么算；我的结果和例题 1.43 对不上 | 俯仰角变化率、pitch gradient、theta_p、deg/g、1.43 | capabilities/pitch-rate-theta-p.md |
| cap.gillespie-ch7.roll-center-solid-axle | 整体式车轴侧倾中心：三步作图，四种结构只换「谁承受侧向力」 | high | 四连杆/三连杆后悬的侧倾中心在哪；整体桥侧倾中心怎么画；侧倾中心高度多少合适 | 侧倾中心、roll center、四连杆、三连杆、侧倾轴线 | capabilities/roll-center-solid-axle.md |
| cap.gillespie-ch7.roll-center-independent | 独立悬架侧倾中心：单侧虚拟点→接地点连线→与中心线求交，外加正/负摆动臂命名 | high | 麦弗逊/双 A 臂的侧倾中心怎么画；正摆动臂/负摆动臂是什么意思；降车身后侧倾中心变多少 | 独立悬架侧倾中心、roll center independent、正摆动臂、麦弗逊、swing arm | capabilities/roll-center-independent.md |
| cap.gillespie-ch7.active-mode-signals | 主动悬架六种性能模式与各自的传感信号 | medium | 主动悬架控制策略用什么信号；侧倾控制怎么触发；能不能只靠软件解决点头 | 主动悬架控制、传感信号、roll control、anti-dive control、接地性 | capabilities/active-mode-signals.md |
| cap.gillespie-ch7.example1-anchors | 例题 1 的三个数值锚点：0.189 / 0.301 / 1.43 deg/g 的回归自检 | high | 例 1 的 1.43 怎么算出来的；0.301 和 0.378 哪个对；我的结果和例题差两倍/差 12 倍 | 例题 1、数值锚点、0.189、0.301、1.43 | capabilities/example1-anchors.md |
| cap.gillespie-ch7.example2-anti-lift-anchors | 例题 2 的两个锚点：4.2 / 2.61 deg/g，比值 1.606 是自检式 | medium | 4.2 和 2.61 是怎么来的；完全抗提升能降低多少抬头；抗提升到底是省略哪一项 | 例题 2、抗提升、4.2、2.61、1.606 | capabilities/example2-anti-lift-anchors.md |
