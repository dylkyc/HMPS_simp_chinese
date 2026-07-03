# HMPS Mod - 本地化与界面修复日志

> 日期：2026-07-04
> 适用版本：Victoria 3 HMPS Mod

---

## 一、本地化工程

### 1.1 文件本地化完成度：98.4%

对所有 localization/english/ 中的 .yml 文件进行了中文本地化处理，
对应的 localization/simp_chinese/ 文件已全部创建并翻译。

### 1.2 已翻译的关键内容

| 分类 | 文件 | 说明 |
|------|------|------|
| 政治/法律 |  _HMPS_politics_l_*.yml | 政府类型、法律描述、制度框架 |
| 日志条目 |  _HMPS_journal_entries_l_*.yml | 事件条件、进度条、工具提示 |
| 事件 |  _HMPS_events_l_*.yml | FAQ、GM操作、赠款事件 |
| 决议 |  _HMPS_decisions_l_*.yml | 各国决议描述 |
| 文化 |  _HMPS_cultures_l_*.yml | 混合文化名称（非裔德意志人、华裔英国人等） |
| 修正 |  _HMPS_modifiers_l_*.yml | 各类修正名称和描述 |
| 产业 |  _HMPS_industry_text_l_*.yml | 建筑、生产方法 |
| 外交行动 |  _HMPS_diplomatic_actions_l_*.yml | 赠款、关税豁免等 |
| 动员选项 |  _HMPS_mobilization_options_l_*.yml | 巧克力、化学武器、喷火器 |
| 界面 |  _HMPS_interfaces_l_*.yml | 工具提示、界面文本 |

### 1.3 修复的缺失本地化键

| 键名 | 中文翻译 |
|------|----------|
| DATA_MILITARY_FORMATION_UNITS | 部队 |
| DATA_MILITARY_FORMATION_NAME | 名称 |
| DATA_MILITARY_FORMATION_TYPE | 类型 |
| DATA_MILITARY_FORMATION_SHIP_HITPOINTS | 生命值 |
| DATA_MILITARY_FORMATION_SHIP_CREW | 船员 |
| DATA_MILITARY_FORMATION_ORGANIZATION | 组织度 |
| DATA_MILITARY_FORMATION_MORALE | 士气 |
| DATA_MILITARY_FORMATION_COLUMN_ONE_ARMY | 陆军信息 |
| DATA_MILITARY_FORMATION_COLUMN_ONE_FLEET | 舰队信息 |

### 1.4 新增州名中文本地化

| 英文名 | 中文名 |
|--------|--------|
| Greater Massachusetts | 大马萨诸塞 |
| Amur | 阿穆尔 |
| Northern Manchuria | 北满洲 |
| Southern Manchuria | 南满洲 |
| Outer Manchuria | 外满洲 |
| Maior Rio do Norte | 北大河 |
| Transjordan | 外约旦 |
| Greater Maryland | 大马里兰 |
| Greater Syria | 大叙利亚 |

---

## 二、界面修复

### 2.1 多部队选中时动员按钮偏移

**问题表现：** 框选多支部队时，指挥官指令按钮排满一行后向左偏移，带动员选项一起偏移，部分按钮无法点击。

**根本原因：** gui/military_formation_panel.gui 中选中多支部队时的指挥官指令按钮容器（flowcontainer，第1335行）没有设置 wrap_count（换行数限制）。MOD新增了3个条件性指挥官指令后，当选中部队满足条件时，按钮过多，容器水平扩展超出面板宽度。

**修复方法：** 在 flowcontainer 中添加 wrap_count = 7，限制每行最多显示7个按钮，超出部分自动换行。
- 修改文件：gui/military_formation_panel.gui
- 修改位置：原 spacing = 5 行后添加 wrap_count = 7

### 2.2 已恢复为原版的GUI文件

为确保与原版行为一致，以下文件已从原版游戏复制覆盖：
- gui/right_click_menu.gui
- gui/custom_tooltip.gui
- gui/ingame_hud.gui
- gui/military_formation_panel.gui
- gui/military_panel_formations.gui
- gui/map_list_panel.gui
- gui/front_panel.gui

---

## 三、游戏文件修复

### 3.1 冗余动员选项清理

**修改文件：** common/mobilization_options/HMPS_00_mobilization_option.txt

| 操作 | 选项 | 说明 |
|------|------|------|
| 保留 | mobilization_option_chocolate | 恢复率 +5% |
| 保留 | mobilization_option_chemical_weapons | 进攻 -15 |
| 保留 | mobilization_option_flamethrowers | 进攻 -10，士气损失 +5% |
| 移除 | mobilization_option_tobacco | 与 chocolate 效果完全相同 |
| 移除 | mobilization_option_liquor | 与 chocolate 效果完全相同 |
| 移除 | mobilization_option_opium | 与 chocolate 效果完全相同 |

### 3.2 war_exhaustion_values.txt 语法错误

**问题：** common/script_values/war_exhaustion_values.txt 第148行有一个多余的闭括号 }，会导致脚本解析错误。

**修复：** 删除了多余的 } 行。

### 3.3 其他已清理

- 删除了重复的本地化文件：localization/english/0_HMPS_units_and_commander_orders_l_english - Copy.yml

---

## 四、全面检查结果

| 检查项目 | 结果 |
|----------|------|
| GUI文件括号匹配（21个文件） | ✅ 全部正常 |
| Common .txt文件括号匹配 | ✅ 全部正常 |
| 本地化文件配对（EN↔CN） | ✅ 完整配对 |
| ON_ACTION引用的日志条目 | ✅ 全部存在 |
| 事件引用的效果/触发器文件 | ✅ 全部存在 |

---

## 五、剩余未翻译条目说明

剩余 59 条未翻译键（占总数1.6%），均为无需翻译的内容：

| 类别 | 数量 | 说明 |
|------|------|------|
| 货币金额 | 44 | £10,000,000 等，数字与符号通用 |
| 变量引用 | 12 | \\$ 格式，自动解析为其他键值 |
| 专有名词 | 1 | Ahmad bin Abdullah bin Fahal（人名） |
| 空字符串 | 1 | " "（仅为空格） |
| 变量作用域 | 1 | [ROOT.GetCharacter.GetFullName]（代码引用） |

---

*本日志自动生成*
