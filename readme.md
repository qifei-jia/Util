# Util应用框架介绍
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://mit-license.org/)

Util是一个.net core平台下的应用框架，旨在提升小型团队的开发输出能力，由常用公共操作类(工具类)、分层架构基类、Ui组件，第三方组件封装，第三方业务接口封装，配套代码生成模板，权限等组成。

## 引子

几年前我在博客园写了一个 [应用程序框架实战](https://www.cnblogs.com/xiadao521) 的系列文章，受到不少.net同学的青睐，不过由于种种原因（想写的范围过大，技术更新过快，工作忙，人越来越懒，好吧，我承认主要是最后一点）而烂尾。

我在博客中放出过一些示例代码，由于未正式开源，修复过的bug也未能更新，所以将博客中提供的示例项目都删除了。

一些同学将这些代码应用在项目上，当碰到问题时，由于没有技术支持，也没有相关教程，苦不堪言。而另外一些同学没有下载到示例项目。

虽然博客断更2年，但时常有同学通过加QQ或发EMAIL的方式联系我，希望能够得到最新代码，并对用法和设计思路进行讲解。

.net core发展迅猛，它为.net提供了更广阔的竞争力，同时也意味着新一轮的学习与代码移植工作开始，我也在这个大潮中跌跌撞撞的摸索着。

几位好友（[AlexLEWIS](https://github.com/alexinea "刘怡") [Kiler](https://github.com/kiler398 "谢炀") [Lemon](https://github.com/liuhaoyang "刘浩杨") ）发起了.net core学习小组，并打算为国内.net core开源大业作出贡献，我果断加入了队伍进行学习，并决定对Util应用框架进行开源。

经讨论，大家决定将各自的开源项目统一发布到 [.NET China Foundation](https://github.com/dotnetcore) 之下，以方便国内.net core开源项目的推广，同时也欢迎国内.net core开源项目作者的加入。

## 技术框架与应用框架

框架是一种可复用的基础代码库，如果它只解决纯技术问题，可以认为是技术框架，如果它与你的业务相关，则可认为是应用框架（框架，应用框架均没有标准定义，我在此以个人理解描述术语含义，以方便后续讨论，并非权威定义）。

.net提供的基础类库是最基础的技术框架，它提供了进行.net开发所需要的基础API，这些API都比较原始。完全使用原始API进行项目开发，会导致高昂的学习成本，更多的Bug，难以维护的重复代码，低效的开发进度。

为了完成某项特定的技术需求，比如写日志，你可以使用原始API进行简单实现，并在多个地方复制粘贴进行调用。这很快会让你厌烦，除了冗余代码以外，你发现还需要经常扩展日志操作的功能，于是你想把日志操作封装成库来调用。

等等，不要再重复造轮子了(为了学习目的造轮子，这绝对是值得肯定的，但确实准备拿来使用的，如果不是真有几把刷子，比如 [Lemon](https://github.com/liuhaoyang "刘浩杨") 同学，建议还是省省吧)，一些前辈已经做了这些基础工作，并且他们的工作已经在全球大范围的使用，非常成熟，并且持续维护。

这些能够解决特定技术问题的类库暂时统称为第三方技术框架,在项目上使用第三方技术框架是项目成功的必要保障。从此，你不再为如何实现某项技术问题而烦恼，也不需要为持续扩展的技术需求而疲于奔命，更多的精力被用在业务上，这才是你应该干的事。

对于你的项目，每当碰到某种技术障碍时，你会四处打听有没有某个第三方技术框架解决了你的问题，找到以后，你通过调试一些Demo代码，简单的用起来了。每当需要这个功能的时候，你会从以前的代码复制粘贴，由于第三方技术框架已经高度封装，所以冗余代码不是特别显著，你没有理会它。

如果你的团队并不经常沟通，处理同一问题的过程将在团队中反复发生，这将导致对于某个问题的技术实现不一致，并且付出高昂的学习成本。当调用代码被大量的复制粘贴后，如果发现调用代码有Bug，或需要增加一些健壮性，你才意识到虽然第三方技术框架已经比较完善，但对它的调用依然有封装的必要。

你开始封装一些经常需要操作的代码，这些代码可能是用.net原始Api封装的，也可能是封装了第三方技术框架的调用，这些封装好的代码被称为公共操作类，也叫工具类。

对于最基础的Crud和业务代码的结构，你发现也可以抽取出来，形成分层架构基类。

你的项目可能需要在网页上进行开发，采用原始的html,css,js技术，将面临界面美观，浏览器兼容性,开发效率低下等问题，有第三方技术框架提供了相关的解决方案，比如EasyUi,Bootstrap,Angularjs,ReactJs等。将第三方UI框架集成并封装起来，能够显著提升开发效率。

如果在项目中，你需要实现支付等业务功能，你可以对这些第三方业务接口进行封装。

对于常规的项目，总是需要一些通用模块，比如权限，将它作为后续项目的起点是一个好主意。

当这些基础代码被高度封装后，常规的Crud代码变得非常简洁，但你还是需要复制这些基础结构，通过反复整理，可以得到一个代码模板，通过代码生成工具将基础的Crud代码生成出来，可以大幅提升生产力。

这个持续封装过程演变为一套项目开发模式，支持这套模式的所有基础代码库，我将它称之为应用框架。

应用框架为你项目的所有方面提供支持，你需要不断的完善它。

## Util的由来

Util是我在.net开发生涯中不断积累而成的一套应用框架，最初的名字叫CommonUtilities，这是一个基本由公共操作类构成的类库。

随着经验和水平的上升，我根据自己的习惯，逐步实现了经典图书中某些概念（比如规约），并吸收了一些流行应用框架( 比如 [ABP](https://github.com/aspnetboilerplate/aspnetboilerplate) [Nop](https://www.nopcommerce.com) )的部分代码。

Util并不是一个完善的应用框架，我总是根据自己项目上的需求来扩展它，所以它基本只是为了满足我个人习惯和项目的产物。

由于技术更新异常迅速，多年来大量的代码被持续重构，还有更多的代码被抛弃，这也是Util不完善的一个重要原因。

发布Util的目的，是希望帮助技术还比较落后的.net小型团队能够搭建出自己的应用框架，提供一个示范，同时也希望它成为跟我有相似开发习惯和偏好的.net同学的重要工具。

## 愿景

让开发更简单

## 承诺

不必担心再次断更，代码会持续更新，使用文档将由Util核心开发团队成员编写，我会补充一些设计方面的文档上来。

## 特点

**简单易用**的傻瓜式API设计，让你的团队能够快速上手进行开发。对于简单操作，通常采用静态方法或扩展方法进行调用，对于更加复杂的操作，尽量封装为链式API。

**强类型(静态类型)**化风格，将UI组件封装为asp.net core razor组件，充分发挥VS开发工具的优势，比如智能提示，编译时检查。

**代码整洁**，Util开发小组成员都有着代码洁癖，每行代码都经过反复斟酌。

地道的**中国味**，Util开发小组成员的英文水平比较菜，命名充满国风，并以中文注释进行补充。

## 面向群体

Util应用框架面向的是*架构初学者*，但不是.net初学者。

如果你是.net初学者，基本的Crud（增删改查）尚且完成不了，请缓一年再来。

你可能已经有了一些项目经验，甚至已经开发多年，但你的项目开发依然进度缓慢，很难按时交付，代码质量糟糕，难以继续维护，你迫切希望找到一种方法来改善这个过程，Util就是为你准备的。

如果你手里没有任何积累，Util将是你搭建自己框架的一个很好的起点。

如果你已经身经百战，自己的框架也比较成熟，Util对你的帮助不会太大。

如果你对API的英文语法要求很高，Util可能无法达到你的要求，请自行修改命名或远离它。

## 使用方式

## 开发环境

## 框架开发流程

  *搜集* - *整理* - *集成* - *封装*

## 项目开发流程

  

## 作者

**何镇汐**

## 核心开发团队

[何镇汐](https://github.com/utilcore) [程序喵](https://github.com/program-meow "胡雲鹏")

## 技术顾问团队

[AlexLEWIS](https://github.com/alexinea "刘怡") [Kiler](https://github.com/kiler398 "谢炀") [Lemon](https://github.com/liuhaoyang "刘浩杨") [Savorboard](https://github.com/yuleyule66 "杨晓东") [Lyrics](https://github.com/lyricsyo "娄宇")

## 贡献与反馈

## 交流方式

 Util应用框架交流QQ群(一群)：24791014

## 免责申明

## 开源地址

https://github.com/dotnetcore/util/

## License

**MIT**

## 参考

## 更新计划

## 更新列表