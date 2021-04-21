# Hgserver 使用说明文档

## 目录

1. [基本指令](#1-基本指令)

   1. [指令简介](#11-指令简介)
   2. [普通指令](#12-普通指令)
      1. [跑图服务器](#121-跑图服务器)
      2. [滑翔服务器](#122-滑翔服务器)
      3. [*各服务器地图列表](#123-*各服务器地图列表)
3. [管理员指令](#13-管理员指令)
2. [进阶控制](#2-进阶控制)
   1. [Rcon](#21-rcon)
   2. [绑定按键](#22-绑定按键)
   3. [cfg 的使用](#23-cfg的使用)
   4. [额外的知识](#24-额外的知识)
3. [版本信息](#3-版本信息)

## 正文

### 1 基本指令

#### 1.1 指令简介

当前所有的 CS:GO 服务器 (甚至包括大型比赛的服务器) 都使用了一款叫做 Sourcemod 的插件。当然这款插件并非专为 CS:GO 设计，从名字上可以看出它是专为起源引擎的游戏设计的。这款插件允许你在游戏中几乎能做到任何你想做的操作，你可以在其中加入自己或他人开发的插件从而获得自己想要得到的效果，下面我简称这款插件为 sm。

sm 插件监听了游戏内的 `对话框` 和 `控制台` 。这意味着普通的玩家也可以方便地在游戏内进行由简单到繁琐的插件控制与操作，而无需了解服务器的复杂知识 (这部分也取决于插件提供的操作方式，但一般的插件都会为游戏内的操作提供方便)。

在 `控制台` 中，所有与 sm 插件相关的指令，均由 `sm_` 开头，例如：

```
sm_admin
sm_map
sm_rtv
```

这意味着你在 `控制台` 输入带 `sm_` 前缀的命令，服务器就会判断这是 sm 插件的命令，从而在服务器中寻找存在的指令进行执行。

在 `对话框` 中，所有与 sm 插件相关的指令，均由 `!` 或者 `/` 开头，例如：

```
!admin
!map
!rtv
/admin
/map
/rtv
```

这意味着你在 `对话框` 输入带 `!` 或者 `/` 前缀的命令，服务器就会判断这是 sm 插件的命令，从而在服务器中寻找存在的指令进行执行 (在这里 ! 与 / 作用基本相同，但在[之后的内容](#24-额外的知识)会提到它们之间的细微区别)。

事实上在控制台输入的 `sm_` 效果与在对话框中输入的 `!` 和 `/` 是相同的，也可以说是等价的。这一点可以用于在某些防止刷屏的服务器中反复执行一些指令，比如滑翔服中快速输入多个 `!r` 会被服务器认为是刷屏，但是在控制台快速输入多个 `sm_r` 则不会被认为是刷屏行为。

对于某些特定的插件，在聊天框中以 `.` 为前缀的、甚至没有前缀的指令也会被识别。比如：

```
.setup
.guns
.ready
.pause
guns
rtv
```

#### 1.2 普通指令

**此处提到的指令仅为本服务器包含的，在其它服务器可能失效**

##### 1.2.1 跑图服务器

`.setup`

> 进入服务器时默认是竞技模式的热身，如果要进入跑图则需要在聊天框输入 `.setup` ，左侧会弹出菜单。按数字 1 进入跑图模式。

`!diy`

> 服务器自定义聚合菜单，包括 皮肤、刀具、贴纸、手套、探员、音乐盒、布章。也可以使用 `!menu` 呼出。快捷键使用键盘上的句号呼出（前提是句号键绑定在 `buyammo2` 命令上）

`!ws`

> 自定义皮肤菜单，可设置磨损。快捷键使用键盘上的逗号呼出（前提是逗号键绑定在 `buyammo1` 命令上）

`!knife`

> 自定义刀具类型菜单

`!s`

> 自定义贴纸菜单，也可以使用 `!stickers` 呼出

`!glove`

> 自定义手套菜单

`!agents`

> 自定义探员菜单

`!music`

> 自定义音乐盒菜单

`!patch`

> 自定义布章菜单

`!weather`

> 显示当前天气

`!fakecase`

> 假开箱菜单，可以假装开到了一把刀

`!wiki`

> CSGOWIKI 菜单，可以快速查询当前图的道具。更多信息可以到 [csgowiki](csgowiki.top) 官网查看。

`!maps`

> 显示换图菜单

`!inspect`

> 显示特殊检视菜单

##### 1.2.2 滑翔服务器

**由于本人服务器使用的滑翔插件为 Surftimer ，与主流滑翔社区中使用的插件基本相同，因此下列所有的指令基本也都可以在其它滑翔服务器使用**

`!surftimer`

> 滑翔显示菜单，控制屏幕上显示的一些信息与内容

`!r`

> 回到起点。在无关卡图里直接回到起点，在关卡图中会需要二次确认，防止直接误触直接回到第一关起点

`!back`

> 回到当前关卡的起点

`!b`

> 传送到奖励关

`!saveloc`

> 保存当前的位置与速度，可以在除起点与终点的任何地方使用，包括观察别人的时候也可以保存当前位置，可用于练习

`!practice`

> 传送到保存的位置并保持保存的速度，可用于练习

`!mi`

> 查看地图信息与分数

`!m`

> 在公屏显示地图名和难度

`!rank`

> 在公屏显示排名

`!showzones`

> 地图中将会显示起点与终点的界线

**以下指令不确保其它服务器都能使用**

`!nv`

> 开启夜视模式，提高视野亮度

`!nvs`

> 调整夜视的模板与强度

`!mhud`

> MovementHUD 菜单。MovementHUD 是专业的显示速度与按键的插件

##### 1.2.3 *各服务器地图列表

主服务器( hgserver.xyz )

```
de_mirage
de_inferno
de_train
de_dust2
de_cache
de_nuke
de_cbble
de_anubis
de_overpass
de_vertigo
de_mirage_parkour
de_overpass_cyberpunk
de_inferno_destruct
mini_mirage_rooftops
mini_inferno
mini_train
de_dust2_mirror
de_mirage_cyberpunk
am_must2
am_water
am_grass2
```

滑翔服务器( surf.hgserver.xyz )

```
surf_aircontrol_fixed
surf_ameliorate
surf_aser2
surf_asrown
surf_benevolent
surf_beyond
surf_cartoon1
surf_colum_2
surf_duggywuggy
surf_easy
surf_eclipse_fix
surf_ecosystem
surf_fortum
surf_frost
surf_garden_go
surf_gleam
surf_golden_a
surf_hades2
surf_helloworld
surf_highlands
surf_hourglass
surf_how2surf
surf_imagine_fix
surf_inferno
surf_ivory
surf_kitsune
surf_lovetunnel
surf_me
surf_methadone
surf_milkyway
surf_minigolf
surf_not_so_beginner
surf_not_so_disaster
surf_nyx
surf_oasis
surf_olympics_sns
surf_piano
surf_proximity_final
surf_reytx
surf_rooftopsv2
surf_rookie
surf_sandtrap2
surf_simpsons_go_rc2
surf_spaceship_ksf
surf_squirrelsonvacation
surf_sundown_njv
surf_sunnyhappylove
surf_voteforthisone1
surf_premium
surf_ethereal1
surf_interference_csgo
surf_borderlands
surf_korn
surf_serenity
```

 查看最近更新的地图请到 <https://web.hgserver.xyz/map.txt> 

#### 1.3 管理员指令

`!admin`

> 管理员菜单，提供许多服务器控制选项

### 2 进阶控制

#### 2.1 Rcon

首先解释一下游戏服务器的概念。

我们所说的服务器实际上是一个模糊的概念。服务器可以指真正在机房中运行的计算机，也可以指网络上虚拟的游戏房间。基本上来说，远程机房中的计算机才是真正的服务器。搭建游戏服务器的原理实际上就是在远程机房的计算机上安装游戏软件（可能是服务器专用版的游戏版本），然后运行，建立房间，但是特殊的地方在于这个“房主”并不会占用服务器的玩家位，也就是说用远程服务器搭建的房间默认是一个空房间，游戏里的时间也是停止的(这样的状态称为 hibernation)，直到有真正的玩家进入，服务器才会进入运行状态。

回忆一下我们自己建立房间的经历，我们可以在控制台输入一些代码改变服务器的属性，比如 `mp_warmup_end` 可以结束热身。那么同样的我们是否可以用游戏中的控制台控制远程服务器的属性呢？确实可以，这就涉及到了这一章的关键词：`Rcon`

`Rcon` 是被 source 专用服务器使用的一种协议，可以使得玩家在不直接接触服务器的情况下控制服务器。简单讲下它的用法：只要在你想要输入的指令前加一个 `rcon` 即可，比如：

```shell
rcon mp_warmup_end
rcon mp_restartgame 1
```

当然，如果每个人都能使用这种方法修改服务器的属性的话，势必会造成混乱，因此 Rcon 的使用需要密码来限制。比如，我在游戏服务器的设置里规定 Rcon 密码为：`12345678` ，为了使用 Rcon 指令，首先需要在控制台里输入 Rcon 密码，形式如下：

```shell
rcon_password 12345678
```

这之后就可以使用 Rcon 指令了。

**_本服务器的 Rcon 密码请联系服主获得。_**

#### 2.2 绑定按键

绑定按键的基本指令还是很简单的，下面分享我在滑翔服使用的按键绑定：

```
bind "r" "sm_r"
bind "b" "sm_b"
bind "v" "sm_back"
bind "x" "sm_mi"
bind "z" "sm_m"
bind "j" "sm_nv"
bind "mouse5" "sm_saveloc"
bind "mouse4" "sm_practice"
bind "CAPSLOCK" "+voicerecord"
```

进阶一些的设置，可以使用 `alias` 进行宏定义：

```
alias +r "+right;+moveright"
alias -r "-right;-moveright"
alias +l "+left;+moveleft"
alias -l "-left;-moveleft"

bind "q" "+l"
bind "e" "+r"
```

这段指令的目的是在左转和右转时做到 100% 同步，滑翔转圈的时候有时能用到。

#### 2.3 cfg 的使用

待补充，可以在 [Hg's Blog](https://hgcp10.rinue.top/?p=105) 获取。

#### 2.4 额外的知识

- `!` 与 `/` 的区别

  默认情况下，服务器在聊天框中接收到 `!` 开头的指令时，会执行对应的命令，同时玩家发送的消息也会打在公屏上。但是如果接受到的是 `/` 开头的指令时，不但会执行对应的命令，同时也会隐藏该消息。这可以使其它玩家无法察觉该玩家发出的具体指令。当然这个属性可以由服务器或插件修改，比如跑图服务器里本人将 `!` 开头的指令也隐藏了，又比如手套插件在编写时默认就隐藏了 `!glove` 指令。

### 3 版本信息

当前文档版本：**0.2 Alpha**

- 更新了一些指令
- 更新了服务器地图列表方便查询

**_0.1 Alpha_**

- 初步搭建了文档框架，完成了基本的内容