以撒的结合 SpiderMod 版本插件，用于修复刷新道具时游戏崩溃以及道具池相关问题

SpiderMod 官网：http://spidermod.spiderland.net/

### Roll 崩 Bug
关于游戏会被 Roll 崩这个 Bug，首先我们来简单的了解一下以撒这个游戏中道具的刷新机制。
1. 不同的房间有不同的道具列表，所以我们能在不同的房间刷出各种类别的道具，游戏崩溃这个 Bug 出现在普通房间 / 宝物房道具列表中
2. 在普通房间 / 宝物房生成道具或刷新道具时会从道具列表中随机抽取一个出来
3. 验证这个道具是否曾经捡过，如果没捡过继续第 4 步，否则跳到第 5 步
4. 把这个道具从道具列表里删除
5. 假如道具列表剩余道具数小于等于 5 个，恢复道具列表（满满的道具，相当于刚开始游戏时的状态）
6. 假如第 3 步的道具没捡过的话就生成或刷新出这个道具，否则跳回第 2 步
这个 Bug 的关键是当道具列表恢复过一次以后，我们曾经捡过的道具也在里面，那么第 3 步这些道具就会被跳过不会从道具列表里删除，而假如我们捡过的道具超过 5 个，这时就会与第 6 步组成无限循环，于是就卡死了。


这样修复这个 Bug 的关键是，曾经捡过的道具必须从道具列表里删除。我们只需要在第 3 步检查到曾经捡过的道具时，将其从道具列表中删除即可。当然实际代码中有许多细节需要兼顾，这里就不赘述了。


### 另外还修复了两个 Bug
1. Boss 房 / 普通隐藏房 / Boss 挑战房有可能会出现未定义道具（不吃这些房间的任何道具，用 SpiderMod 进这些房间后狂按 F6 就能看到这个 Bug 了）
2. 商店道具列表最后一个道具永远不会出现的问题（同样用 SpiderMod 进商店狂按 F6，然后菜单 - 内置 - 道具列表中可以查看还剩一个道具在里面，如果是修女服就哭吧）


### 使用说明：
下载解压到 SpiderMod 的 Plugins 目录中，启动 SpiderMod，菜单 - 插件 - 启用，重启 SpiderMod，菜单 - 插件 - 设置，在想启用的插件前打上勾，重新启用 SpiderMod 即可。
记得同时启用 PhD Bug 修复插件，这样才能确保游戏不会像陆夫人那样崩掉。