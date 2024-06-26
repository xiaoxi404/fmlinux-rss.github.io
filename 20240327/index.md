# 今日开源新闻汇总2024-3-27
## 新闻1
开源的 Panthor DRM 驱动程序支持更新的 Arm Mali GPU，已在 3 月初排队进入 drm-misc-next，准备合并到 Linux 6.9。但最终没有在 Linux 6.9 合并窗口前被拉入 DRM-Next，因此被推迟到 Linux 6.10 周期。不过，本周该驱动程序和其他更改开始为 Linux 6.10 排队。
<br>
首次为 Linux 6.10 准备的 drm-misc-next 拉取已完成。这次拉取使得支持新型 Mali 图形“Gen10”的 Panthor DRM 驱动程序落地，这些图形依赖于命令流前端（CSF）。与此同时，Mesa 24.1 也进行了 Gallium3D 驱动程序的更改，以支持这个新的内核图形驱动程序。Mali GPU 支持也有新的固件要求。
<br>
除了引入 Panthor 驱动程序外，这次 drm-misc-next 拉取还包括改进 TTM 缓冲对象在空闲/繁忙处理中的放置、一个新的 CONFIG_DRM_WERROR 选项用于将 DRM 子系统代码的警告设置为错误，以及其他各种核心改进。较小的直接渲染管理器驱动程序也进行了一些小修复。
<br>
在组织方面，DRM-Misc 现已过渡到使用 GitLab 和 FreeDesktop.org 托管。
<br>
请查看这次拉取，了解初步为 Linux 6.10 准备的 DRM-Misc-Next 材料，预计在今年夏天。
<br>
## 新闻2
Intel维护的通用VA-API库"libva"的工程师们今天发布了2.21版本，为这个视频加速API支持带来了几项修复和添加。
<br>
通用的libva 2.21库增加了一个驱动程序名称映射，以支持新的Intel Xe内核模式驱动程序。Intel Xe已合并到Linux 6.8中，并且是Lunar Lake之前几代的实验性驱动选项。现在，随着libva 2.21的发布，为使用Xe驱动程序的用户提供了适当的映射，而不是现有的i915驱动程序。
<br>
![图片暂时迷路了！！:(](img/2.png)
<br>
Libva 2.21还在AV1编码代码中添加了allow_content_tools和force_intger_mv，各种针对Windows平台的特定修复/添加，当所有Wayland后端失败时的修复，持续集成（CI）更新，以及各种构建更新。
<br>
通过GitHub下载和查看libva 2.21 VA-API库更改的完整列表。
<br>
## 新闻3
在Linux 6.6版本中，作为Intel控制流执行技术（CET）的一部分，Shadow Stack支持终于被合并。这项历经数年的努力使得新一代Intel处理器能更好地防御ROP攻击。对于Linux 6.10版本，Shadow Stack的支持将扩展到x32。
<br>
尽管x32 ABI并不十分常见，但它仍然存在。作为提醒，这个Linux ABI提供了x86_64的好处，同时仍然依赖于32位指针。它相对于x86 32位的优势在于能够利用x86_64增加的寄存器集、浮点改进等，但仍然依赖于32位指针，并且每个进程的内存限制为4GB。
<br>
十年前，x32 ABI听起来非常不错，但如今在实际应用中很少听到有关x32的消息，大多数用户对x86_64感到满意。甚至偶尔有人呼吁是否应该弃用x32。不过，令人惊讶的是，我们现在看到Shadow Stack支持x32。
<br>
![图片暂时迷路了！！:(](img/3.png)
<br>
目前在TIP.git的"x86/shstk"分支中排队的是为x32添加shadow stack支持。这一支持已经在使用Intel Tiger Lake系统的x32上成功测试，由Intel工程师H.J. Lu进行。现在它已经在TIP分支中，很可能会在今年夏天提交到Linux 6.10内核周期。总之，看到Intel在2024年为Linux x32支持做出改进，这确实有些意外。
<br>
## 新闻4
Intel今天发布了驱动程序补丁，为其Xe和i915 Linux内核图形驱动程序的DG2/Alchemist系列添加了两个新的PCI ID。
<br>
在过去两年多的时间里，他们的开源Linux图形驱动程序代码中已经积累了各种DG2 PCI ID，今天早上又有两个新的PCI ID以补丁形式出现，用于i915和Xe Linux DRM驱动程序。
<br>
新的PCI ID是0x56BE和0x56BF。经过一些搜索，在Intel Compute Runtime代码中找到了这两个ID，0x56BE是Intel Arc Graphics A750E变体，而0x56BF是Intel Arc Graphics A580E。关于Arc Graphics A580E和A750E变体，公开的信息不多，所以我们可能很快就会随着驱动程序支持的出现而了解更多。
<br>
![图片暂时迷路了！！:(](img/4.png)
<br>
对于i915和Xe内核图形驱动程序，根据补丁，只需要新的PCI ID，无需在现有的DG2/Alchemist代码路径上进行其他驱动更改。通常，PCI ID的添加被视为当前（v6.9）内核周期的“修复”的一部分，是比较安全的，或者可能会推迟到v6.10，这取决于Intel是否急于推出新的硬件支持。
<br>
## 新闻5
AMD今天发布了本季度的第三个也是最后一个开源Vulkan驱动程序更新。
<br>
AMDVLK 2024.Q1.3作为Radeon图形的官方开源Vulkan驱动程序的最新版本，今天发布了。AMDVLK 2024.Q1.3版本针对Vulkan API 1.3.279头文件进行了更新，增加了一些面板设置选项，并修复了各种错误。这次修复的内容包括Vulkan Conformance Test Suite（VKCTS）的失败、与之前驱动版本相比Quake II RTX性能回退，以及一些应用程序中的分段线问题。
<br>
![图片暂时迷路了！！:(](img/5.png)
<br>
这是一个相当小的更新，并且仍然没有看到像由Valve和其他方支持的Mesa RADV驱动程序那样的活动水平或爱好者/游戏玩家的兴趣。对AMDVLK 2024.Q1.3 Vulkan驱动程序感兴趣的人可以在GitHub上找到今天的发布版本，无论是源代码形式还是Ubuntu和RHEL二进制文件。
<br>
## 新闻6
Linux 6.9版本在带来许多重大变化和新功能/硬件支持的同时，也宣布了对经典的EXT2文件系统驱动程序的弃用。
<br>
EXT2文件系统已经存在了三十年，自从EXT3出现已经过去了二十多年，而自从EXT4在Linux内核中稳定运行也已经有十五年了。EXT2的使用一直在下降，可能只用于访问旧的存储设备或遗留的Linux发行版安装。
<br>
现在之所以弃用EXT2，是因为该文件系统驱动程序不支持2038年之后的日期，这是Y2038问题的一部分。由于不能正确支持2038年1月19日之后的时间戳，Linux开发者现在鼓励任何剩余的EXT2用户升级到使用EXT4驱动程序来访问他们的文件系统。EXT4驱动程序能够处理EXT2文件系统，同时正确支持Y2038问题之后的日期。
<br>
![图片暂时迷路了！！:(](img/6.png)
<br>
因此，目前EXT2驱动程序已被弃用，其代码仅作为参考目的保留，但很可能在未来几年内被移除。更多关于EXT2驱动程序弃用的详细信息，请查看Bootlin博客。
<br>
## 新闻7
SDL库广泛用于跨平台游戏，当前的SDL 3.0开发代码更倾向于使用Wayland而不是X11，但一个新的拉取请求可能会暂时撤销这一偏好，因为Wayland生态系统仍然不够完善。
<br>
两年前，在尝试默认支持Wayland之后，由于出现了一些错误和生态系统问题，SDL撤销了这一变更。随着正在开发中的SDL 3.0版本的推进，它再次尝试优先选择Wayland而不是X11，但这个周末有一个新的拉取请求被打开，该请求将撤销对Wayland的偏好。
<br>
Valve的Linux图形团队的Joshua Ashton发起了这个拉取请求，该请求将撤销对Wayland的优先选择。Ashton在合并请求中提出了以下观点： 
<br>
"Wayland存在许多未解决的问题，例如表面暂停阻塞呈现和FIFO（垂直同步）实现基本上是破碎的，导致GPU绑定性能降低。
<br>
这并不是说’我们应该在Mesa/其他驱动程序中修复FIFO’，而是在没有额外协议的情况下，这是完全无法修复的，这种情况下是fifo-v1。
<br>
没有这个协议，vkQueuePresent或glSwapBuffers在呈现图像后必须等待’帧’回调。我们在SteamOS上能够避免这种情况的唯一原因是因为Gamescope实现了本质上是fifo-v1的东西，我们在那里使用它。
<br>
另一方面是表面暂停——与上述帧回调的使用方式和阻塞问题非常相似。如果SDL窗口被遮挡，vkQueuePresent将在FIFO中阻塞，这是游戏通常不喜欢的。这可以通过fifo-v1和commit-timing-v1的组合来解决。
<br>
目前，游戏和普通应用程序更倾向于使用Wayland而不是X11，并没有任何优势——只有严重的性能和不可用性退步。因此，我们必须撤销这一变更，直到fifo-v1和commit-timing-v1发布，并至少在主要合成器的稳定版本中发布。"
<br>
这个问题现在正在拉取请求内部激烈讨论，一些人认为Wayland对游戏有优势。还有一些建议应该检查fifo-v1和commit-timing-v1协议，以决定Wayland的支持，而不是完全撤销。
<br>
![图片暂时迷路了！！:(](img/7.png)
<br>
目前这个拉取请求还没有合并，但看起来SDL 3.0至少在FIFO和Commit Timing协议在上游完成并获得Wayland合成器支持之前，可能会发生撤销或部分禁用。这个可能的撤销发生在SDL 3.0预览版发布几天后。讨论仍在进行中，请继续关注。
<br>
