# 安装、调用与迭代

## 安装

此目录本身就是完整Skill；不依赖Rhino、图像生成、网络或第三方库。支持可读Markdown技能的环境；是否自动发现取决于宿主支持。本包不附带CAD建模、测绘或正式审图能力。

Codex本地安装：将整个 architecture-design 目录复制到 CODEX_HOME/skills/architecture-design；CODEX_HOME 未设置时使用用户目录下 .codex/skills/architecture-design。若目录已存在，先比较版本并备份，不覆盖项目文件。在新的聊天/重新加载技能后调用；未列入技能列表前不要声称已加载。无法安装时可直接要求AI读取本目录SKILL.md并遵循相对引用；这属于文件加载方式，不代表宿主已安装。

Windows PowerShell（从解压后父目录运行；仅首次安装，存在即停止）：

```powershell
$skillBase = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $env:USERPROFILE '.codex/skills' }
$skillTarget = Join-Path $skillBase 'architecture-design'
if (Test-Path -LiteralPath $skillTarget) { throw '目标已存在，请先比较版本并备份。' }
New-Item -ItemType Directory -Force -Path $skillBase | Out-Null
Copy-Item -LiteralPath './architecture-design' -Destination $skillTarget -Recurse
```

## 调用示例

“使用 $architecture-design。项目是咸阳设计博物馆；请先读取我给的任务书和底图，识别当前阶段，只询问最影响判断的缺项。”

“使用 $architecture-design，评审v3平面和剖面，重点检查展品运输、闭馆公共通行和跨层可达；不要重做已完成研究。”

“使用 $architecture-design，继续 project-state.md 中的院落分支，比较新增展厅后的面积和流线影响，重大决策先给我选项。”

## 文件与版本

Skill包保持通用，项目数据放在项目的 architecture-project/。复制templates后填写，保留E/P/S/O/V标识。所有未知值可保留，不用为了填满表格编造。文件只读时在聊天输出同结构记录。

v1.0.0为首次发布。语义版本：修正文案及不改变判断的规则为patch；增加兼容工作流/模板为minor；改变证据分类、记录格式或关键门槛为major并附迁移说明。每次以失败案例驱动最小修改，记录变更原因、兼容性、受影响文件和测试结果；不要把个别项目偏好升级成通用约束。

发布检查：运行创建器quick_validate.py（如宿主提供）；核对相对链接、七阶段字段、压缩包与源文件哈希；按tests/acceptance-tests.md做实际行为回归。格式通过不代表设计能力或合规性已获证明。


## GitHub安装与升级

维护仓库：[XLJFZ/skills](https://github.com/XLJFZ/skills/tree/main/skills/architecture-design)，安装源为仓库中的skills/architecture-design整个目录。只复制本Skill目录，不覆盖其他技能。

后续升级按[维护与同步流程](references/github-maintenance.md)执行。跨设备使用时比较本机与远端版本，保留未发布修改；不要用整仓覆盖本机skills目录。此流程不安装后台监听或定时任务。
