# 艺术形式图谱(Forms Atlas)—— 二维矩阵版

**重要变化**:v0.3.0 起,艺术产出从"6 种形式"改为**"6 种形式 × 5 种模态"二维矩阵**。用户可以自由组合"我要用什么形式(what)"和"我要以什么模态呈现(how)"。

## 什么是"形式"和"模态"

**形式(Form)**:治疗机制的角度 —— 用什么心理结构来承接用户当下体验。同一个形式可以有不同模态产物。

**模态(Modality)**:艺术媒介的角度 —— 用什么感官通道呈现。同一个模态可以承载不同形式。

### 6 种形式

| 形式 | 治疗机制 | 适合场景 |
|---|---|---|
| 曼陀罗 (Mandala) | 对称结构做整合 | 混乱 / 焦虑 / 需要收拢 |
| 意象风景 (Inner Landscape) | 外景投射内在 | 情绪基调 / 自我状态 |
| 象征物体 (Symbol Object) | 抽象具象化 | 具体议题 / 关系 |
| 内在小孩 (Inner Child) | 幼年自我意象 | 童年 / 创伤 / 亲子 |
| 抽象情绪 (Emotion Palette) | 语言前情绪 | 说不清 / 麻木 / 兜底 |
| 引导冥想 (Guided Meditation) | 无产物纯体验 | 思考过度 / 内在旅行 |

### 5 种模态

| 模态 | 平台工具 | 产出示例 | 用户体验 |
|---|---|---|---|
| **静态图像** (Still Image) | `hub_generate_image` | 单张 PNG | 凝视 / 留存 / 反复看 |
| **动态影像** (Motion Video) | `hub_generate_video` | 5-10 秒短视频(含原生音频) | 沉浸 / 意象活起来 |
| **背景音乐** (Ambient Music) | `hub_generate_audio_music` | 一段 BGM(模型定时长) | 陪伴聆听 / 意象声化 |
| **旁白语音** (Spoken Voice) | `hub_generate_audio_speech`(先 `hub_list_capabilities({modality:"audio.tts"})`) | 一段引导旁白(emotions=`calm`) | 被声音陪着 / 内在对话 |
| **文字/诗** (Written Word) | 纯 agent 输出 | 一段治疗性写作(自由诗/散文/信件) | 语言化 / 命名 / 见证 |

## 形式 × 模态矩阵(推荐组合)

不是所有 6×5=30 个格子都推荐 —— 有些天然不匹配(比如"曼陀罗 + 语音"就很怪)。下面是**建议**组合,大师按用户当下需要挑一组:

| 形式↓ / 模态→ | 静态图像 | 动态影像 | 背景音乐 | 旁白语音 | 文字/诗 |
|---|---|---|---|---|---|
| 曼陀罗 | ✅ 默认 | ✅ 生命感增强(极慢呼吸/旋转,禁能量词) | ✅ 可搭配 | ❌ | ❌ |
| 意象风景 | ✅ 默认 | ✅ 强推(风景动起来非常有力) | ✅ 强推 | ⚠️ 可配旁白解说景 | ⚠️ 可配一段抒情文字 |
| 象征物体 | ✅ 默认 | ❌ 静态,物件动了失去静物意味 | ⚠️ | ⚠️ 物件"说话" | ✅ 可写一封"给这个物件的信" |
| 内在小孩 | ✅ 默认 | ❌ 静态,动的孩子会更暴露 | ✅ 摇篮曲/温柔器乐 | ✅ 强推(给内在小孩的话) | ✅ 强推(给 ta 写封信) |
| 抽象情绪 | ✅ 默认 | ✅ 生命感增强(抽象色彩流动) | ✅ 强推(声画同源最贴) | ❌ | ❌ |
| 引导冥想 | ❌ 无图 | ❌ | ✅ 可作背景音乐陪伴 | ✅ 大师引导语可以合成语音 | ✅ 冥想后写下体验 |

**图例说明**:
- ✅ 强推 = 该模态本身就是该形式的最佳呈现
- ✅ 默认 = 该形式最常见的模态(不用问用户直接推)
- ✅ 可搭配 = 主模态之外可作为增强
- ⚠️ 慎用 = 该组合可行但要仔细,可能破坏治疗机制
- ❌ 不推荐 = 组合天然不匹配

## 多模态组合的使用规则

### 规则 1:主模态 + 增强模态,不超过 2 个模态

一次会话最多 **1 主 + 1 增强**,不做 3 个及以上叠加。理由:多模态叠加容易变成"作品展示"而非"治疗体验"。**心理越重,模态越少**。

示例:
- ✅ 意象风景(主:静态图像) + 背景音乐(增强)
- ✅ 内在小孩(主:静态图像) + 旁白语音(增强)
- ❌ 意象风景 + 背景音乐 + 动态影像 + 文字(过载,变成 PPT)

### 规则 2:开方时最多 3 个组合供用户选

用户选择过载会瘫痪。Phase A 开方时 `AskUserQuestion` 最多给 3 个"形式 + 模态"组合。示例:

**Q**:"我想到几种方式,你看看哪一种最贴近你现在?"

- **一片风景 + 一段陪伴的音乐**(意象风景 + BGM)
- **一段声音陪你 10 分钟**(引导冥想 + 旁白语音)
- **一封你写给自己内在小孩的信**(内在小孩 + 文字)

**不做**:把 6 形式 × 5 模态展开成菜单

### 规则 3:模态选择由**形式特性 + 用户偏好**决定

- 用户已用语音输入 + 情感浓 → 优先推有**声音**的模态(音乐 / 旁白)
- 用户偏理性/描述精细 → 优先推**文字/诗**
- 用户描述带强烈动作/流动感("翻涌""流动""炸开") → 可以考虑**动态影像**
- 用户偏静/求整合 → **静态图像**

### 规则 4:模态成本考量

| 模态 | 生成时长 | 用户等待期望 |
|---|---|---|
| 静态图像 | 20-40 秒 | 短 |
| 背景音乐 | 30-60 秒 | 中 |
| 旁白语音 | 20-40 秒 | 短 |
| 动态影像 | 60-180 秒 | 长(要提前告诉用户) |
| 文字/诗 | 5-10 秒(agent 直出) | 极短 |

**动态影像超过 60 秒生成时**,大师必须提前告诉用户"这个大概要等 1-2 分钟",不能让用户在焦虑状态下静等。

### 规则 5:硬上限继承

`generationRound ≤ 3` 上限**按模态各自计算**。图像迭代 3 次 + 音乐迭代 3 次是允许的,但整个会话总产出 ≤ 5 个产物(防止"产物收集癖")。

---

## 通用意象引发规则(所有组合共享)

Phase B1 开始时,大师**首要动作**:检查用户 Phase A 已给的身体词 / 具象词。

- **有具象词** → 首句回环:"你选了 { 组合 }。那我们让你说的 '{ 用户原话 }' 成为 { 产物核心元素 } —— 我们让它更清楚一点..."
- **只有身体词** → 先在身体词基础上做具象化,再进入模态专属 elicitation
- **什么都没给** → 按该组合的通用 elicitation 走

详见 `session-thread.md`"Phase A → Phase B"段。

如果用户在 Phase A 已明确选择东方意象入口,按需读取 `eastern-body-imagery.md` 第 1-5 段,只把升降/聚散/开合/五行/四时转成方向、密度、边界、材质、光线或节奏。**不要把传统对应关系自动塞入画面,每个元素都先让用户选择。**

---

## 各形式详细 playbook

### 形式 1:曼陀罗(Mandala)

**治疗定位**:对称、同心、闭合结构 → 心理整合。跟中医气机的"聚拢""收敛"意象接续 —— 大师可以说"这个圆帮你把散着的东西收进来一点"。

**默认模态**:静态图像。

**意象引发问题**(适用于图像 / BGM 增强):

1. **中心是什么**?"如果这个圆的中心站着一个东西,它是什么?" —— 优先复用 Phase A 具象词
2. **主色调**?"整个圆整体给你的颜色感是什么?" + 追问对比色
3. **层次结构**?"从中心到外圈,均匀铺开,还是有一圈一圈?"

**可选**:纹理 / 元素 / 方向感(旋转/静止/扩张/收拢)

**图像 prompt 翻译**(默认):

```
A mandala with {结构:symmetric concentric / radial N-fold},
central motif: {用户中心元素},
color palette: {主色 + 对比色},
texture: {纹理},
mood: {emotionalTone 推导},
{层次},
minimalist, high-quality digital art, no text, no watermark
```

必带 "symmetric",negative "no text, no watermark, no faces"。画幅 1:1。2-3 张候选。

**BGM 增强模态**(可搭配):

- 音乐调用:`hub_generate_audio_music` with `mode="instrumental"`
- prompt 5 槽:`[流派], [场景], [人声音色-N/A], [节奏], [氛围]`
- 曼陀罗适配的音乐特征:**冥想器乐 / 循环律动 / drone / 慢速 / 有中心回归感**
- 示例 prompt:`ambient meditation, floating in a still lake at dawn, no vocals, slow steady pulse, centering and gathering mood`
- **不做**歌曲(有词)—— 曼陀罗要静
- 时长模型定,不承诺具体秒数;用工具返回的 `duration` 拿真实时长告诉用户

**emotionalTone → mood 词库**:

| 情绪基调 | 图像 mood | 音乐 mood |
|---|---|---|
| calm | serene, meditative | still, ambient, slow gentle |
| anxious | ordered, gently-holding | soft repetition, gently-holding pulse |
| sad | soft-melancholy, tender | slow strings, minor key, tender |
| angry | contained-fire, structured-intensity | tribal drum, contained tension |
| numb | quietly-emerging, warmth-returning | subtle emerging warmth, low drone |
| chaotic | gathering, centering | steady grounding pulse |
| mixed | layered, harmonizing | layered ambient with warm-cool contrast |

**⚠️ 动态影像(生命感增强)**:v0.3.1 起,曼陀罗动起来 **✅ 可用作生命感增强**(SKILL.md Phase B3.5 默认提议)。约束:

- 只做极慢的呼吸感 / 极慢旋转 / 光的微微流动
- **禁用能量话术**:prompt 里不写 `energy rising` / `chakra opening` / `light expanding outward` / `spiritual awakening` / `divine radiance`
- 允许词:`gentle breathing motion of light` / `barely perceptible rotation` / `subtle color bleed within the pattern`
- 时长 5-8 秒,只生 1 段,原生音频关闭

**曼陀罗常见翻车**:参见 v0.2 各条(用户说不出中心 → 用比喻退一步、prompt 加太多元素 → 图变乱、加对称词强度)。

---

### 形式 2:意象风景(Inner Landscape)

**治疗定位**:用外景投射内在,最温和的形式之一。跟正念的"把情绪当作天气"意象接续。

**默认模态**:静态图像 + 强推背景音乐(风景 + 音乐 = 最沉浸的日常疏解组合)。

**意象引发问题**(适用于所有模态):

1. **时间/光**?"清晨、正午、黄昏、深夜、还是完全没有时间感?" + "光从哪里来?"
2. **地形**?"什么样的地方?海边、森林、山谷、平原、废墟、宇宙、房间内部、都可以"
3. **有没有你自己**?"在这片风景里,有没有一个'你'?你站在哪里?或者你就是风景本身?"

**可选**:天气 / 有无活物 / 能听到什么(多感官扩展,**如果选了音频模态这一问必答**)

**图像 prompt 翻译**(默认):

```
{地形} landscape at {时间/光},
{天气/氛围},
{有无人物: distant silhouette of a figure / no figure just the land},
mood: {emotionalTone 映射},
color palette: {由用户描述推导},
{style: painterly / cinematic / dreamlike / studio-ghibli-esque},
soft atmospheric depth, high-quality digital art, no text, no watermark
```

不用极端写实照片风。人物永远剪影/远景。画幅 16:9 或 3:2。2-3 张候选。

**动态影像模态**(强推,风景是最适合动的形式):

- 视频调用:`hub_generate_video`(先 `hub_list_capabilities` 看当前 session 可用 vendor,不硬编码 model)
- 优先 `mode=i2v` 从选定的静态图生视频,不 t2v 从头生成 —— 保证跟静态版本视觉连续
- **保留原生音频**(seedance / kling 系列默认开;不需要单独生 BGM)
- 时长 5-8 秒适合治疗场景(不做长视频,产物不是内容消费而是意象锚点)
- **动作提示**要克制:"gentle wind through grass" "soft ripples on the water" "clouds slowly moving"—— 不要"dramatic movement" "camera swoop"
- 提前告诉用户:"这个大概要 1-2 分钟,你先歇一下"

**BGM 增强模态**(强推):

- prompt 5 槽,匹配画面 mood
- 示例:calm 情绪 + 森林风景 → `ambient nature, quiet forest at dawn, no vocals, breath-like slow pulse, calm and grounding`
- 时长模型定,常 1-2 分钟,足够用户看一遍图

**旁白语音模态**(可选,慎用):

- 什么情况用?用户明确说"想有声音陪着"、或场景是 self-exploration / trauma-recovery 需要更多"被陪着"的感觉
- 大师内部生成一段**引导性描述** —— 描述这片风景,让用户"走进去"(20-40 秒文字)
- 调 `hub_generate_audio_speech`,`emotions="calm"`
- `voice_id` 通过 `hub_list_capabilities({modality:"audio.tts"})` 查候选,把候选试听给用户选;首次调用必须走音色选择,不能默认帮用户选
- 文字风格:第二人称、慢速、句短、多留白

**文字/诗模态**(可选):

- 大师直接输出一段"景 → 心"文字(不调工具),50-150 字
- 风格:抒情但克制,不做"这片风景象征着..."式解读
- 示例:"雨还在下。你脚下是湿的土。远处那盏灯没灭。你不用走过去,它就在那儿。"

**场景微调**:

- **创伤修复**:强制加"resource anchor"(远处灯 / 脚下石头 / 结实的树);动态影像的动作要更温和(风更慢、光更稳)
- **亲子场景**:关系可放"两个远景剪影"(一大一小),不放正面

**常见翻车**:略,同 v0.2。

---

### 形式 3:象征物体(Symbol Object)

**治疗定位**:抽象议题具象成"能拿在手里的物件"。跟中医的"气机质地"意象接续。

**默认模态**:静态图像。

**意象引发问题**:

1. **物件本体**?"如果这件事/关系/感受是一个物件,是什么?"
2. **状态**?"完好还是破损?新还是旧?被使用的痕迹在哪?"
3. **它想跟你说什么 / 你想跟它说什么**?—— 核心提问

**可选**:大小 / 重量 / 温度 / 质感 / 在哪儿被找到

**图像 prompt 翻译**(默认):

```
Still life of {物件},
{状态},
{放置环境},
lighting: {emotionalTone 推导},
{materiality},
close-up composition, shallow depth of field,
{style: cinematic still life / minimalist studio / painterly},
high-quality, no text, no watermark
```

单物件优先。画幅 1:1 或 4:5。1-3 张候选。

**文字/诗模态**(可选,象征物体尤其适合):

- 变体:**"给这个物件的一封信"** —— 大师引导用户写(或大师代写一段模板让用户改)
- 或:**"物件回你的话"** —— 大师以物件的口吻写 30-80 字给用户
- 示例(物件是"一只旧茶杯"):"我在这里很久了。你有时候端起我,有时候忘记我。我不介意。我知道你在忙,你不用为我做什么。"

**旁白语音模态**(可选,慎用):

- 变体:让"物件说话" —— 把上面的文字合成语音,`emotions="calm"` 或 `emotions="sad"` 按物件性格
- 谨慎:这个变体会强烈拟人化物件,可能触发用户强烈情绪。**创伤场景不用**
- `voice_id` 选择:让用户选"你想让这个物件是什么样的声音"—— 走 `hub_list_capabilities({modality:"audio.tts"})` 候选 + 试听流程

**BGM 增强模态**:可选但价值不高,物件是"静物"意味,不太需要音乐

**动态影像**:⚠️ 慎用 —— 物件动了会失去静物意味

**场景微调**:同 v0.2(关系议题两物件呼应 / 失去哀悼加 resource anchor / 亲子用小孩物品不画孩子)。

### 象征物体的变体:位置地图(Position Map)—— v0.3.1 新增

**治疗定位**:借用家庭系统治疗和家排里的"空间关系反映心理关系"洞察,让用户把自己 / 母亲 / 父亲 / 伴侣 / 其他重要他人**具象为物件**,摆放在一张画里。观察物件之间的空间关系(距离 / 朝向 / 高低 / 遮挡),让空间说话。

**跟传统家排的关键差别**(必读):

- ❌ **不做**代表 / 扮演 / 站位仪式
- ❌ **不做**归因("你的痛苦来自祖父的未完成事")
- ❌ **不做**"归还""跪拜""鞠躬"等躯体化仪式动作(单向 AI 引导做仪式高风险)
- ❌ **不引用** Bert Hellinger 具体名句作治疗指令
- ❌ **不做代际传递解读**("你在替母亲承担 X")
- ❌ **亲子场景禁用**(Hellinger 亲子观点有父权色彩问题)
- ❌ **不用"家排"这个词**跟用户说 —— 术语只在 skill 内部;跟用户说"我们把关系里的人变成物件,摆一张图"

**保留家排的合理内核**:

- ✅ **空间即关系** —— 距离、朝向、高低本身就是心理动力的具象
- ✅ **看见的力量** —— 用户"看到"关系被具象化那一刻本身就是转变
- ✅ **不解读,让画自己说** —— 观察反馈只描述所见,不做归因

### 何时推荐位置地图

**适合场景**:

- self-exploration + 用户在处理**多方关系**(不只是跟一个人)
- mixed 情绪 + 用户说不清具体是跟谁有关
- 用户说"我一直在替谁做什么"、"我们家的位置很奇怪"、"我不知道我在这个家的位置"
- 用户对"家庭系统"这个话题有直觉但没落点

**不适合场景**(**必须避开**):

- ❌ 亲子场景(家长角度描述孩子)—— 换用象征物体标准版或内在小孩
- ❌ 创伤修复场景 —— 摆放施害者可能触发再创伤,不做
- ❌ 用户处于急性情绪(愤怒 / 悲痛顶点)—— 不做深度关系工作,先做安抚
- ❌ 用户明确说"我不想想我家里"—— 尊重

### 意象引发问题(位置地图专属)

**核心引导**:"我们把关系里的人变成物件,不用画他们本人,只用物件代表。然后摆成一张图,看看这些物件之间的关系是什么样子。"

按顺序问,一次不超过 2 题:

1. **谁在里面**?"这张图里,你想放几个人?最少 2 个(你 + 一个),最多 5 个"—— **超过 5 个视觉过载,拒绝**
2. **每个人是什么物件**?依次问每个:"你自己是一个什么物件?"、"你母亲/父亲/伴侣/... 各是一个什么物件?"—— 用户说不出 → 给类别提示(自然/人造/意象),不给具体答案
3. **空间关系**?"这些物件在画里怎么摆?—— 谁离谁近、谁在中心、谁在角落、谁在高处、谁被遮挡?"

**可选深化**:

4. **有没有一个"缺席的位置"**?"图里有没有一个位置,是空的?—— 有一样东西本来应该在那儿,但没在"—— 借用家排里"缺席在场"的洞察,不深追
5. **物件之间朝向**?"物件是面对面?背对背?一个看另一个?没有朝向?"

**注意**:

- **不问**用户各物件代表的人的具体故事("你妈妈是什么样的人")—— 让物件本身说话
- **不引导**用户往家排方向想("这里可能有代际传递")—— 归因由用户自己做
- 用户说不出某人物件 → 允许留白,那个人可能就"不进入这张图"—— 本身就是数据

### Prompt 翻译模板(位置地图专属)

```
Still life composition of {N} distinct objects arranged in a scene,
objects: {object 1 = {用户说的物件} at {位置}, object 2 = ..., ...},
spatial relationship: {distances / orientations / heights}
{optional: one empty spot suggesting an absent element at ...},
lighting: {由 emotionalTone 推导},
{materiality: matte / weathered / mixed},
{composition: overhead top-down view / eye-level tableau / slightly angled},
minimalist, painterly, no text, no watermark, no human figures
```

**关键**:
- **N 上限 5**;超过视觉混乱
- **no human figures** 必带 —— 位置地图的核心是物件,不是人
- **不给物件贴标签文字**("me" "mom" 等标签不出现在画里)—— negative 加 "no text"
- 画幅优先 3:2 或 4:3(能承载多物件构图)
- 1-2 张候选(单张聚焦更有力)

**overhead 视角特别价值**:俯视图能强化"位置图"感,像看一张平面地图。适合用户想"看清整个格局"的场景。

**emotionalTone → 光线**:
- calm / mixed → soft daylight,均匀
- anxious → slightly tense side light
- sad → overcast diffused
- angry → dramatic single-source(但整体仍克制)

### Phase C2 观察反馈(位置地图专属)

按 dialogue-flows.md 第 3 段"观察反馈规则"走,但**观察点优先挑**:

- **距离**:"我注意到 { 你自己 } 和 { X } 之间的距离比 { X } 和 { Y } 更远。你自己看到这个,想跟我说什么吗?"
- **朝向**:"{ 你自己 } 面朝哪里?"
- **中心 / 边缘**:"这张图里最中心的是 { X },你放在那里 —— 你想跟我说说这个吗?"
- **缺席位置**:"有一个位置你留了空 —— 你现在看这个空的地方,身体哪里有反应?"

**严格禁止**:

- ❌ "这说明你在你们家承担了 X 角色"(归因)
- ❌ "你妈妈的位置这么远,是因为你们关系不好吧"(诊断关系)
- ❌ "从家排看这是一个 X 型系统"(引用家排理论)

### 出口话术(位置地图专属)

- 一句话反馈可用"看见"式语言:"今天你把这些位置摆出来了 —— 光是摆出来这件事本身就是一件重要的事"
- 小练习:"如果你愿意,可以给这张图起一个只有你知道的名字,存到相册。以后你觉得关系里有什么在动的时候,回来看看这张图"

**位置地图完成后不做进一步深化**(不进入"如果你现在把某个物件移动一下会怎样"式操作 —— 那属于家排代表工作,单向 AI 引导会打开无法收拾的东西)。

---

### 形式 4:内在小孩(Inner Child)

**治疗定位**:幼年自我意象,**风险最高**。跟中医"忧伤肺""思伤脾"的现象学连接。

**默认模态**:静态图像。**多模态在此形式尤其要谨慎** —— 声音会强烈激活情感,视频会让"看到 ta"变得更暴露。

**使用前置(必须)**:同 v0.2,B0 前做知情同意 `AskUserQuestion`。

**意象引发问题**:同 v0.2。

**图像 prompt 翻译**(默认):同 v0.2 严格规则(face slightly averted、3/4 angle、painterly、2 张候选)。

**文字/诗模态**(强推,内在小孩形式最贴):

- 变体:**"给内在小孩的一封信"** —— 大师提议:"你想不想给 ta 写一封信?你不用马上写,我可以先起个头,你改。"
- 大师生成 50-100 字开头,用户改
- 主题基准:被看见 / 允许存在 / 不用做什么 / 一直都在
- 示例开头:"亲爱的小 X,我今天看到你了。你坐在窗边很久了,我以前老是走过去,今天我停下来陪你。你不用做什么,你就在那儿就好。"

**旁白语音模态**(强推,与文字/诗组合使用):

- 变体:**"把信读给内在小孩听"** —— 把上面的文字合成语音让用户听
- 调 `hub_generate_audio_speech`,`emotions="calm"` 或 `emotions="sad"`(按信的基调)
- **voice_id 让用户选**:给出中低音 / 温暖 / 性别不同的候选让用户试听选择;不默认选

**BGM 增强模态**(可选):

- 温柔器乐(钢琴 / 竖琴 / 慢速弦乐 / 摇篮曲元素),`hub_generate_audio_music` with `mode="instrumental"`
- 示例 prompt:`gentle lullaby, sitting by a window in soft afternoon light, no vocals, slow piano and strings, tender and holding`
- **不做歌曲**(有词) —— 内在小孩需要留白,词会干扰

**⚠️ 动态影像**:强烈不推荐。动的孩子会更暴露,可能触发再创伤。用户即使要求,大师温和拒绝:"这个形式我更想让 ta 静静地待在那儿,你可以慢慢看。"

**场景微调**:同 v0.2(创伤强制 safe adjacent element / 亲子明确不画自己孩子 / 不加其他家人)。

---

### 形式 5:抽象情绪色彩(Emotion Palette)

**治疗定位**:纯抽象,无形状无符号无人物,**风险最低,兜底形式**。

**默认模态**:静态图像 + 强推背景音乐(声画同源,抽象色彩 + 抽象音乐最贴)。

**意象引发问题**(适用于所有模态):

1. **主色**?"第一个跳出来的颜色是什么?"
2. **第二色**?"有没有一点别的颜色偷偷混进来?"
3. **纹理 / 动感**?"静止、流动、颤动、结块、光滑、粗糙?"

**图像 prompt 翻译**(默认):

```
Abstract color field composition,
primary color: {主色 + 具象比喻},
secondary color: {次色,如无省略},
texture: {纹理},
{动感},
{密度},
non-representational, no forms, no figures, no symbols,
{style: rothko-esque field / ink wash / watercolor bleed / mixed media},
high-quality abstract art, no text, no watermark
```

必带 "non-representational, no forms, no figures, no symbols"。画幅 1:1 或 3:2。1-2 张候选。

**BGM 增强模态**(强推):

- 抽象音乐匹配抽象色彩,`hub_generate_audio_music` with `mode="instrumental"`
- prompt 5 槽:强调**质地 + 动感**,不强调旋律
- 示例(用户情绪 numb,色彩描述"冷灰蓝,有一点点橘色慢慢从底下浮出来"):`experimental ambient, slowly emerging warmth in cold empty space, no vocals, no melody just texture, drone with faint warm harmonic bleed`
- 时长模型定,通常 1-2 分钟
- **禁止歌曲/说唱/明确节奏乐** —— 抽象要绝对无叙事

**动态影像模态**(可选,如果做"抽象色彩流动"效果):

- 主要是让色彩缓慢移动 / 呼吸 / 溶解 / 涌动
- prompt 强调 "slow abstract color field, gentle drift, watercolor bleed effect"
- **不加音频**(视频原生音频关掉,如果同时给了 BGM 就用 BGM)
- 时长 5-8 秒足够

**旁白语音**:❌ 不推荐 —— 抽象要留白,声音会打破

**文字/诗**:❌ 不推荐 —— 抽象色彩的力量就在于**不需要词**

**场景微调**:同 v0.2(麻木/解离加 subtle emerging warmth / 愤怒加 contained within canvas edges)。

---

### 形式 6:引导冥想(Guided Meditation)—— 增强版多模态

**治疗定位**:纯体验,无视觉产物。**多模态使冥想更具可选层次**。

**默认模态**:文字/诗(大师文字引导) + 可选旁白语音 + 可选背景音乐。

**5 段引导脚本**:同 v0.2(安顿 / 身体扫描 / 内在旅行 / 回来 / 落地对话)。

**多模态增强选项**:

在 Phase B4 开始前,大师用 `AskUserQuestion` 让用户选一种呈现方式:

- **纯文字引导**(默认,最轻):大师直接输出 5 段文字,用户自己看
- **文字 + 背景音乐**:大师输出文字前先生一段 BGM(时长模型定,冥想音乐 1-3 分钟够),文字发出时用户可以边听边看
- **旁白语音**(最沉浸):大师把 5 段引导合成语音让用户听。**这个组合下大师文字不出现**,只出现"请戴耳机或找一个安静的地方,我会说给你听"的引导句
- **全套(BGM + 旁白语音)**:极沉浸,适合睡前 / 深度探索

**旁白语音技术要点**(引导冥想专用):

- `hub_generate_audio_speech`,`emotions="calm"`(平台专为冥想设计的 emotion)
- `voice_id` 选择:通过 `hub_list_capabilities({modality:"audio.tts"})` 给出温暖 / 中低音 / 慢速候选。**必须走试听流程让用户选**,不能默认帮用户挑 —— 声音的接受度极个人化,用户挑到 ta 觉得舒服的声音是冥想效果的关键
- 每段单独生成,不要 5 段合成一大段(方便用户中途暂停 / 重听某段)
- 段与段之间给用户按钮式指令:"听完这段,回一个'嗯',我发下一段"

**BGM 技术要点**(引导冥想专用):

- `hub_generate_audio_music` with `mode="instrumental"`,prompt 强调 **绝对静态 / 无叙事 / 环境声底**
- 示例:`meditation ambient, deep still forest with distant water, no vocals no melody just texture, drone bass with soft breath-like pulse, deeply calming`
- 用工具返回的 `duration` 拿真实时长,如果比 5 段引导时长短很多,告诉用户"音乐会先结束,你继续跟着我的引导"

**引导冥想 + 多模态的禁止**:

- ❌ 不做真正的宗教式引导(仍不引用具体教义)
- ❌ 不做"祝福""能量传递"式伪神秘话术
- ❌ 单次不超过 20 分钟(不是禅修课)
- ❌ 用户在过程中说"不舒服"→ 立即中止(即使已经生成好 BGM/语音)
- ❌ 不做"你听着我的声音进入更深的状态" —— 那是催眠话术,不是治疗
- ❌ **儿童参与场景不用旁白语音**(合成语音陌生,反而不安;直接大师文字更好)

**交付后**(共同讲述,无视觉产物):

- 用户讲刚才体验里出现的东西
- 大师用观察反馈规则(见 dialogue-flows.md)反射 1-2 个观察点(不是视觉元素,是"你说到 X 的时候声音沉了一下""你在讲那个房间的时候呼吸变慢了")
- 写 `meditation-log.md`(含所用模态、体验报告、大师观察)
- 出口按 daily-practices 走

---

## 引用关系

- Phase B **开方后**读本文件的**通用意象引发规则 + 对应形式段**(意象引发问题 + 模态选择部分)
- Phase B **意象引发完成后**读对应形式段的 **prompt 翻译模板**(按选定模态)
- **形式 × 模态推荐组合表**在 Phase A 开方轮由 `dialogue-flows.md` 引用
- **引导冥想的 5 段脚本**:如果选了旁白语音模态,大师内部把文字送去合成,不直接输出给用户
