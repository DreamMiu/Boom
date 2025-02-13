# Boom

[English](README_EN.md)

> 基于BukkitAPI的管理插件

支持`Bukkit`/`Spigot`/`Paper`/`Purpur`等`Bukkit`的分支核心

支持`1.13.x`及以上版本，`1.16.x`-`1.19.x`经过测试

提供完整语言文件, 欢迎pr其他的语言文件

**不支持`1.12`及以下版本, 不支持`Sponge`核心, 不支持`Mohist`/`Arclight`/`CatServer`等任何的添加了mod支持的服务端核心，不支持MOD实体的处理(你可以用, 但是遇到问题请不要在这儿反馈)**

[![Release](https://img.shields.io/github/v/release/4o4E/Boom?label=Release)](https://github.com/4o4E/Boom/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/4o4E/Boom/total?label=Download)](https://github.com/4o4E/Boom/releases)

## 支持功能

以下所有配置均可以按世界/WorldGuard区域单独配置(在`global`下的是全局设置，在`each.<世界名>`下的是单独世界的设置，`region.<区域名>`下的是区域设置，处理优先级：区域(`region`) -> 世界(`each`) -> 全局(`global`))
- 控制实体爆炸
- 阻止火焰蔓延
- 阻止火焰烧毁方块
- 保护耕地不被实体踩坏
- 阻止实体转换(村民, 女巫, 僵尸村民, 溺尸)
- 阻止末影人搬起方块
- 使盔甲架生成的时候摆正自己(使盔甲架默认有双手)
- 死亡时保留物品
- 死亡时保留等级
- 阻止使用床
- 阻止使用重生锚
- 阻止使用指令(指令转接的功能跳过此检测)
- 指令转接，输入指令a以使用指令b(可以触发多条指令)(支持控制台指令的转接)
- 限制实体生成(百分比)
- 阻止玩家点击实体/方块

## 配置文件

[config.yml](src/main/resources/config.yml)

## 语言文件

[lang.yml](src/main/resources/lang.yml)

欢迎pr其他的语言文件

## 如何配置

```yaml
# global下的配置是全局配置
global:
  explosion:
    CREEPER:
      enable: false
      cancel: false
  disable_fire_spread: false
  disable_fire_burn: false
  # 此处省略其他配置...

# each下的配置是单独世界的配置
each:
  # !! 实际处理时会优先寻找对应世界的配置, 若未找到则会使用global中的配置 !!
  # 此处只需要写不同于global的配置, 相同的可以省略
  # 此处用 example_world1 和 example_world2 作为世界名字, 实际使用时将其改成自己世界的名字
  # 比如 world 或者 world_nether 等
  # 世界名字区分大小写, 不能有多余空格
  # 不知道自己世界名字的可以用客户端(需要权限)执行 /bm world 查看当前所在的世界名字
  example_world1:
    explosion:
      CREEPER:
        enable: true
        cancel: false
    disable_fire_spread: false
    disable_fire_burn: false
  example_world2:
    explosion:
      CREEPER:
        enable: true
        cancel: false
    disable_fire_spread: true
    disable_fire_burn: true
  # 此处省略其他配置...

```

按照以上配置

在世界`example_world1`中, 苦力怕的爆炸不会破坏方块

在世界`example_world2`中, 火焰不会蔓延和烧坏方块

其他所有世界中则苦力怕的爆炸会破坏方块, 火焰会蔓延和烧坏方块

## 指令

> 插件主命令为`boom`，包括别名`bm`，如果与其他插件指令冲突，请使用`boom`
- `/bm reload` 重载插件
- `/bm debug` 切换debug消息的接受与否
- `/bm world` 查看当前世界名
- `/bm sun` 切换当前世界天气在接下来的10分钟内为晴
- `/bm sun <世界>` 切换指定世界天气在接下来的10分钟内为晴
- `/bm sun <世界> <时长>` 切换指定世界天气在接下来的指定时长内为晴
- `/bm rain` 切换当前世界天气在接下来的10分钟内为雨
- `/bm rain <世界>` 切换指定世界天气在接下来的10分钟内为雨
- `/bm rain <世界> <时长>` 切换指定世界天气在接下来的指定时长内为雨
- `/bm thunder` 切换当前世界天气在接下来的10分钟内为雷暴
- `/bm thunder <世界>` 切换指定世界天气在接下来的10分钟内为雷暴
- `/bm thunder <世界> <时长>` 切换指定世界天气在接下来的指定时长内为雷暴
- `/bm ls` 切换当前世界天气在接下来的一小时内为晴
- `/bm stick` 获取调试棒(用于修改盔甲架和展示框)

## 权限

- `boom.admin` 允许使用插件指令

- `boom.bypass.command` 允许跳过指令过滤

- `boom.weather` 允许使用所有天气指令

  **子权限节点**

  - `boom.weather.sun` 允许切换天气为晴

  - `boom.weather.rain` 允许切换天气为雨

  - `boom.weather.thunder` 允许切换天气为雷暴

- `boom.stick` 允许获取并使用调试棒修改盔甲架/展示框

- `boom.bypass.*` 允许跳过点击实体和方块的限制

  **子权限节点**

  - `boom.bypass.block` 允许跳过点击方块的限制
  
  - `boom.bypass.entity` 允许跳过点击实体的限制

## 下载

- [最新版](https://github.com/4o4E/Boom/releases/latest)

## 已知问题

- [ ] 盔甲架调试棒潜行点击盔甲架修改其碰撞箱时有时会连续触发两次

  解决方法: 潜行点击距离盔甲架相近的方块

- [x] ~~村民防雷击会阻止村民变成僵尸村民(被僵尸打死就是直接死了)~~ 已修复

## 更新记录

```log
2021.01.07 1.0.0 插件发布
2021.01.07 1.0.1 添加reload指令
2021.01.11 1.0.2 添加阻止时的粒子、音效自定义内容
2021.01.18 1.0.3 修复bug
2021.02.01 1.0.4 添加阻止蝙蝠生成的选项（主要是自己的空岛服要用XD）
2021.02.09 1.0.5 添加禁用指令的使用和tab补全
2021.02.14 1.0.6 移除单独的阻止蝙蝠生成选项，添加所有生物的概率生成/禁用生成
2021.02.21 1.1.0 重写部分代码，优化性能，添加农田保护，火焰蔓延开关，指令转接/指令简化
（更新必须删除配置文件，新版本配置文件完全不兼容旧版本
2021.02.22 1.1.1 添加保护村民不被雷击转化成女巫的保护
2021.02.23 1.1.2 添加展示框调整工具，允许使用调试棒切换可见/可交互
2021.02.25 1.2.0 修复bug，优化代码，调整默认配置文件
（更新必须删除配置文件，新版本配置文件完全不兼容旧版本
2021.02.25 1.2.1 新增盔甲架调试功能，允许使用调试棒切换可见/可交互
2021.03.02 1.2.2 修复bug，新增更新检查
2021.03.06 1.2.3 修复bug，新增天气控制
2021.03.07 1.2.4 修复bug，新增玩家使用禁用命令后控制台执行命令
2021.03.28 1.2.5 修复bug，修改禁用指令的格式，新增模糊匹配
2021.05.23 1.3.0 修复bug，新增按世界配置禁用指令，优化盔甲架调试功能，添加bstats统计数据
（更新必须删除配置文件，新版本配置文件完全不兼容旧版本）
2021.06.12 1.3.1 删除遗留的调试信息
2021.06.12 1.3.2 修复帮助信息不显示的问题
2021.11.07 1.3.3 修复help指令显示的错误内容
2022.06.23 2.0.0 用kotlin重写，并且修复高版本无法阻止使用床的问题，新增死亡掉落相关设置, 优化处理流程, 增加debug日志
（更新必须删除配置文件，新版本配置文件完全不兼容旧版本）
2022.06.23 2.0.1 修改未使用语言文件的内容使用语言文件以便修改语言
2022.07.01 2.0.2 修复实体爆炸时的debug信息错误显示的问题，修复配置文件中错误的不加载单独世界配置项的问题
2022.07.02 2.0.3 移除未移除的调试信息
2022.07.02 2.0.4 修复实体限制配置读取错误的问题
2022.07.02 2.0.5 添加阻止玩家点击实体/方块的配置项
2022.07.07 2.0.6 添加点击限制的跳过权限, 完善配置文件中的注释, 添加打掉展示框时的处理
2022.07.10 2.0.7 修复点击基岩会触发点击床的bug
2022.07.11 2.0.8 添加阻止玩家受到伤害的选项
2022.07.25 2.0.9 添加WorldGuard软依赖, 添加region配置项, 允许按区域检测
（更新必须删除配置文件，新版本配置文件完全不兼容旧版本）
```

## bstats

[![bstats](https://bstats.org/signatures/bukkit/Boom.svg)](https://bstats.org/plugin/bukkit/Boom/11445)
