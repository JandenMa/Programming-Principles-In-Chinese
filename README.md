# 程序设计法则

> Translated by Janden.Ma at 2019-01
>
> From https://github.com/webpro/programming-principles
>
> 翻译自英文，如有翻译不准确的地方，请指正



每个程序员都可以从理解程序设计法则和模式中受益。这个对我来说也仅仅是一个参考，我只是把它放在这里，也许在设计，讨论或评阅读过程中对您有所帮助。 需要注意的是，它并非完整，您经常需要在与之冲突的原则之间进行权衡。

这么文档列表的灵感来自 [The Principles of Good Programming](https://www.artima.com/weblogs/viewpost.jsp?thread=331531)，但我觉得它过于紧凑，并不完全符合我个人的观点。另外，我需要有更多的论证、细节，以及其他资源的链接。如果您有任何改进的建议或意见，请让我知道。

---



## 目录

#### 通用类

- [KISS法则](#KISS法则)
- [YAGNI法则](#YAGNI法则)
- [尽可能做可运行的最简单的事](#尽可能做可运行的最简单的事)
- [关注点分离](#关注点分离)
- [遵循不写重复代码](#遵循不写重复代码)
- [作为代码的维护者](#作为代码的维护者)
- [避免过早优化](#避免过早优化)
- [童子军规则](#童子军规则)

#### 模块/类之间

- [低耦合](#低耦合)
- [迪米特法则](#迪米特法则)
- [优先使用组合而非继承](#优先使用组合而非继承)
- [正交性](#正交性)
- [健壮性法则](#健壮性法则)
- [控制反转](#控制反转)

#### 模块/类

- [高内聚](#高内聚)
- [里氏替换原则](#里氏替换原则)
- [开闭原则](#开闭原则)
- [单一职责原则](#单一职责原则)
- [隐藏接口实现细节](#隐藏接口实现细节)
- [柯里定律](#柯里定律)
- [封装经常修改的代码](#封装经常修改的代码)
- [接口隔离原则](#接口隔离原则)
- [命令查询分离原则](#命令查询分离原则)

---



#### KISS法则

*KISS —— Keep it Simple Stupid(保持简单愚蠢）*

大多数系统在保持简单而不是复杂的时候，大都能达到最佳性能。

**原因**：

- 更少的代码需要花费在编程的时间更少，相对来说BUG也会更少，并且更容易去改动。
- Simplicity is the ultimate sophistication.——简单就是终极的复杂（大道至简，至繁归于至简）。
- 一个东西看似达到完美时，不在于无法再往里边加任何东西，而是无法从里边拿走任何东西。

**参考来源**

- [KISS principle](https://en.wikipedia.org/wiki/KISS_principle)
- [Keep It Simple Stupid (KISS)](http://principles-wiki.net/principles:keep_it_simple_stupid)



---



#### YAGNI法则

*YAGNI——you aren't gonna need it（不要实现没有必要的东西）*

**原因**

- 当你将工作量仅仅用于一个明天才需要的功能上，那意味着你将失去为当前需要迭代的功能所付出的时间。
- 它会导致代码膨胀，软件变得更大，更复杂。

**参考来源**

- [You Arent Gonna Need It](http://c2.com/xp/YouArentGonnaNeedIt.html)
- [You’re NOT gonna need it!](http://www.xprogramming.com/Practices/PracNotNeed.html)
- [You ain't gonna need it](http://en.wikipedia.org/wiki/You_ain't_gonna_need_it)



---



#### 尽可能做可运行的最简单的事

**原因**

- 我们只要专注于解决真正的问题所在，我们就能取得最大进展。

**怎么做**

- 问问自己：”最简单的事情是什么“

**参考来源**

- [Do The Simplest Thing That Could Possibly Work](http://c2.com/xp/DoTheSimplestThingThatCouldPossiblyWork.html)



---



#### 关注点分离

*Separation of Concerns, SoC*

关注点分离，是将计算机程序分为不同部分的一种设计原则，这样做可以是每个部分都解决一个单独的问题。举个例子，程序的业务逻辑是一个点，而用户界面又是另一个点。更改用户界面的时候，不应该要求更改业务逻辑，反之亦然。

引用 [Edsger W. Dijkstra](https://en.wikipedia.org/wiki/Edsger_W._Dijkstra) （1974）

> It is what I sometimes have called "the separation of concerns", which, even if not perfectly possible, is yet the only available technique for effective ordering of one's thoughts, that I know of. This is what I mean by "focusing one's attention upon some aspect": it does not mean ignoring the other aspects, it is just doing justice to the fact that from this aspect's point of view, the other is irrelevant.
>
> 「有时候我将它称之为”关注点分离“，即使并不完全可能，但它是我仅能了解到的可以有效地排列一个人想法的技术。这就是我所说的”将注意力集中在某些方面“：它不意味着忽视其他方面，只是事实上，从这方面的观点出发，其他的无关紧要。」

**原因**

- 简化软件应用的开发和维护
- 当关注点被很好地分离，则每个部分可以被复用，也可以独立的开发和更改。

**怎么做**

- 将程序按功能划分为尽可能少相互重叠的单独模块

**参考资源**

- [Separation of Concerns](https://en.wikipedia.org/wiki/Separation_of_concerns)



---



#### 遵循不写重复代码

*Keep Things DRY——Don't Repeat Yourself*

在系统中，每一块知识点都应该有一个单一的、明确的、权威的表示。

在程序中，每一个重要的功能，在源码中都应该只有一个实现的地方。当出现不同的代码实现相似的功能时，通过抽离变化的部分，将他们组合在一起，通常是有利的。

**原因**

- 代码复制/重复（有意或无意），将会导致维护噩梦，不好分解和逻辑矛盾。
- 对系统任何单一元素进行修改的时候，不应该修改其他逻辑上无关的元素。
- 另外，逻辑相关的元素，都应该可以被预测并统一改变来保持同步。

**怎么做**

- 只在一个地方放置业务规则、长表达式、if语句、数学公式、元数据等。
- 确定系统中使用的每一个知识点单一、权威的来源，然后使用它生成该知识的可用实例（代码，文档，测试等）。
- 应用 [Rule of three](http://en.wikipedia.org/wiki/Rule_of_three_(computer_programming))

**参考资源**

- [Dont Repeat Yourself](http://c2.com/cgi/wiki?DontRepeatYourself)
- [Don't repeat yourself](http://en.wikipedia.org/wiki/Don't_repeat_yourself)
- [Don't Repeat Yourself](http://programmer.97things.oreilly.com/wiki/index.php/Don't_Repeat_Yourself)

**相关知识**

- [Abstraction principle](http://en.wikipedia.org/wiki/Abstraction_principle_(computer_programming))（抽象原则）
- [Once And Only Once](http://c2.com/cgi/wiki?OnceAndOnlyOnce) （是DRY的子集，也成为重构的目标）.
- [Single Source of Truth](http://en.wikipedia.org/wiki/Single_Source_of_Truth)（单一来源的真理）
- A violation of DRY is [WET](http://thedailywtf.com/articles/The-WET-Cart) （违反DRY原则的是WET(Write Everything Twice)）



---



#### 作为代码的维护者

**原因**

- 维护是任何项目最昂贵的一个阶段

**怎么做**

- 成为维护者
- 时刻编码，就好像最终维护你代码的人是一个知道你住在哪儿的狂暴精神病患者一样
- 时刻以这样一种方式去编码和注释：假设有不同能力级别的人去翻阅你的代码，他们会乐意去阅读并从中学习
- [别让我思考](http://www.sensible.com/dmmt.html)
- 使用最小惊讶原则 [Principle of Least Astonishment](http://en.wikipedia.org/wiki/Principle_of_least_astonishment)

**相关资源**

- [Code For The Maintainer](http://c2.com/cgi/wiki?CodeForTheMaintainer)
- [The Noble Art of Maintenance Programming](http://blog.codinghorror.com/the-noble-art-of-maintenance-programming/)



---



#### 避免过早优化

引用 [Donald Knuth](http://en.wikiquote.org/wiki/Donald_Knuth)：

> Programmers waste enormous amounts of time thinking about, or worrying about, the speed of noncritical parts of their programs, and these attempts at efficiency actually have a strong negative impact when debugging and maintenance are considered. We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil. Yet we should not pass up our opportunities in that critical 3%.
>
> 「程序员花大量的时间在思考或担心他们程序中不重要部分的速度上，然而事实上，企图考虑这些效率，在调试和维护上会产生很大的负面影响。我们97%的时间应该忘记那些小的效率，但是也不应该放弃那关键的3%的机会。」

理解”过早“与否是至关重要的。

**原因**

- 我们事先无法知道瓶颈在哪里
- 优化之后可能难以阅读，并因此需要维护

**怎么做**

- [让它正确并且快速地运行](http://c2.com/cgi/wiki?MakeItWorkMakeItRightMakeItFast)
- 不要在不需要的时候去优化，只有在分析后发现瓶颈再去优化它

**相关资源**

- [Program optimization](http://en.wikipedia.org/wiki/Program_optimization)（程序优化）
- [Premature Optimization](http://c2.com/cgi/wiki?PrematureOptimization)（不成熟的优化）



---



#### 童子军规则

美国童子军有一个简单的规则，可以适用于我们的职业：“离开营地时让它比你发现它时更干净”。 童子军规则规定我们应该始终保持代码比我们发现的更干净。【这意味着团队中每一个成员都有义务去改善代码】

**原因**

- 对现有代码库进行更改时，代码的质量往往会很低，从而会积攒很多技术债务。根据童子军规则，我们应该考虑每次提交的代码质量。技术债务是由于遭受连续的重构，无论多么小。

**怎么做**

- 每次提交都要确保不会降低代码的质量
- 每当有人看到一段不太清晰的代码时，他们应该抓住机会修正它。

**相关资源**

- [Opportunistic Refactoring](http://martinfowler.com/bliki/OpportunisticRefactoring.html)



---



#### 低耦合

模块/组件之间的耦合指的是是它们相互依赖的程度，较低的耦合效果会更好。 换句话说，耦合是在对代码单元“A”做出未知改变之后导致代码单元"B"将“破坏”的概率。

**原因**

- 一个模块中的一个改变，通常会导致其他模块产生连锁反应般的变化
- 由于模块间依赖性增加，模块的组装可能需要更多的努力和（或）时间
- 特定模块可能更难以重用和（或）测试，因为必须包含依赖模块
- 开发人员可能害怕更改代码，因为他们不确定可能会影响到什么

**怎么做**

- 消除，最小化并减少必要关系的复杂性
- 通过隐藏实现细节，降低耦合度
- 使用[迪米特法则](#迪米特法则)

**相关资源**

- [Coupling](http://en.wikipedia.org/wiki/Coupling_(computer_programming))（耦合）
- [Coupling And Cohesion](http://c2.com/cgi/wiki?CouplingAndCohesion)（耦合和内聚）



---



#### 迪米特法则

*Law of Demeter, LoD*

*Don't talk to strangers.——不要和陌生人说话*

**原因**

- 通常情况下，耦合度很高
- 可能会透露太多的实现细节

**怎么做**

一个对象的方法只能调用以下对象的方法：

- 对象本身
- 方法的一个参数对象
- 在方法中被创建的任意对象
- 对象的任意属性或字段

**相关资源**

- [Law of Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter)（迪米特法则）
- [The Law of Demeter Is Not A Dot Counting Exercise](http://haacked.com/archive/2009/07/14/law-of-demeter-dot-counting.aspx/)



---



#### 优先使用组合而非继承

**原因**

- 减少类之间的耦合
- 使用继承，子类容易想当然，并且破坏里氏替换原则（LSP）

**怎么做**

- 通过测试LSP（里氏替换原则，可替代性）来决定何时继承
- 在存在“有”（或“使用”）的关系时使用组合，在存在“是”时使用继承。

**相关资源**

- [Favor Composition Over Inheritance](http://blogs.msdn.com/b/thalesc/archive/2012/09/05/favor-composition-over-inheritance.aspx)



---



#### 正交性

> The basic idea of orthogonality is that things that are not related conceptually should not be related in the system.
>
> 「正交性的基本思想是，概念上不相关的事物在系统中不应该有关联」

来源：[Be Orthogonal](http://www.artima.com/intv/dry3.html)

> It is associated with simplicity; the more orthogonal the design, the fewer exceptions. This makes it easier to learn, read and write programs in a programming language. The meaning of an orthogonal feature is independent of context; the key parameters are symmetry and consistency.
>
> 「它与简单相关联，设计越正交，异常越少。这使得编程语言更容易学习，阅读和编写程序。 正交特征的含义与上下文无关，关键在于对称性和一致性。」

来源：[Orthogonality](http://en.wikipedia.org/wiki/Orthogonality_(programming))



---



#### 健壮性法则

>  Be conservative in what you do, be liberal in what you accept from others
>
>  「保守你的所作所为，豁达地接纳他人」

协作服务依赖于彼此的接口。 通常接口需要进化，这就会导致另一端接收到未指定的数据。 如果收到的数据不严格遵循规范，那么原本的接口实现就拒绝协作。 一个更复杂的接口实现会忽略它无法识别的数据并继续运行。

**原因**

- 为了能够进化服务，您需要确保供应商可以进行更改以支持新需求，同时最大限度地减少对现有客户的破坏。

**怎么做**

- 将命令或数据发送到其他机器（或同一台机器上的其他程序）的代码应完全符合规范，但接收输入的代码就应接受尽量长的不符合要求但含义明确的输入。

**相关资源**

- [Robustness Principle in Wikipedia](https://en.wikipedia.org/wiki/Robustness_principle)
- [Tolerant Reader](http://martinfowler.com/bliki/TolerantReader.html)



---



#### 控制反转

*Inversion of Control, IoC*

控制反转也被称为”好莱坞原则“——「不要打电话给我们，我们会打电话给你」。这是一种设计法则，其中计算机程序的定制编写部分从通用框架接收控制流。控制反转带有强大的含义，即可重用代码和特定于问题的代码是独立开发的，即使它们在应用程序中一起运行。

**原因**

- 控制反转是用来增加程序的模块化并使其具有可扩展性
- 将任务的执行与实现分离
- 模块应该被设计为专注于它的任务
- 使模块免于假设其他系统如何做他们所做的事情，而是依赖契约
- 更换模块时要防止副作用

**怎么做**

- 使用工厂模式
- 使用服务定位模式
- 使用依赖注入
- 使用上下文查找
- 使用模板方法模式
- 使用策略模式

**相关资源**

- [Inversion of Control in Wikipedia](https://en.wikipedia.org/wiki/Inversion_of_control)
- [Inversion of Control Containers and the Dependency Injection pattern](https://www.martinfowler.com/articles/injection.html)



---



#### 高内聚

单个模块/组件的聚合度是指其职责构成有意义单元的程度，聚合度更高更好。

**原因**

- 理解模块的困难度增加
- 维护系统的难度增加，因为域中的逻辑更改会影响多个模块，并且因为一个模块中的更改需要更改相关模块
- 重用模块的难度增加，因为大多数应用程序不需要模块提供随机操作集

**怎么做**

- 分组相关功能在一个单一的责任体系中（例如在一个类中）

**相关资源**

- [Cohesion](http://en.wikipedia.org/wiki/Cohesion_(computer_science))
- [Coupling And Cohesion](http://c2.com/cgi/wiki?CouplingAndCohesion)



---



#### 里氏替换原则

*Liskov Substitution Principle, LSP*

里氏替换原则完全与对象的预期行为有关

> Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.
>
> 「程序中的对象应该可以替换为其子类型的实例，而不会改变该程序的正确性。」

**相关资源**

- [Liskov substitution principle](http://en.wikipedia.org/wiki/Liskov_substitution_principle)
- [Liskov Substitution Principle](http://www.blackwasp.co.uk/lsp.aspx)



#### 开闭原则

*Open/Closed Principle, OCP*

软件实体（例如类）的扩展性应该是开放，但是修改应该是闭合的。也就是说这样的实体可以允许修改其行为而不改变其源代码。

**原因**

- 通过对现有代码的最小程度的更改来提高可维护性和稳定性

**怎么做**

- 编写可扩展的类（与可修改的类相对）
- 仅暴露需要更改的移动部件，隐藏其他所有部件

**相关资源**

- [Open Closed Principle](http://en.wikipedia.org/wiki/Open/closed_principle)
- [The Open Closed Principle](https://8thlight.com/blog/uncle-bob/2014/05/12/TheOpenClosedPrinciple.html)



---



#### 单一职责原则

*Single Responsibility Principle, SRP*

一个类不应该有多个被改变的理由

长版本：每个类都应该承担一个责任，并且该责任应该由该类完全封装。 责任可以被定义为改变的理由，因此一个类或模块应该只有一个改变的理由

**原因**

- 可维护性：仅在一个模块或类中需要进行更改

**怎么做**

- 使用柯里化

**相关资源**

- [Single responsibility principle](http://en.wikipedia.org/wiki/Single_responsibility_principle)



---



#### 隐藏接口实现细节

软件模块通过提供接口来隐藏信息（即实现细节），而不泄漏任何不必要的信息。

**原因**

- 当接口实现更改时，使用的接口客户端不必更改

**怎么做**

- 尽可能减少类和成员的可访问性
- 不要在public中暴露成员数据
- 避免将私有实现细节放在类的接口中
- 减少耦合以隐藏更多实现细节

**相关资源**

- [Information hiding](http://en.wikipedia.org/wiki/Information_hiding)



---



#### 柯里定律

柯里定律是指为任何特定的代码选择一个明确定义的目标：只做一件事

- [Curly's Law: Do One Thing](http://blog.codinghorror.com/curlys-law-do-one-thing/)
- [The Rule of One or Curly’s Law](http://fortyplustwo.com/2008/09/06/the-rule-of-one-or-curlys-law/)



---



#### 封装经常修改的代码

一个好的设计可以识别最有可能改变的热点，并将它们封装在API之后。 当发生预期的变化时，将修改保持在本地

**原因**

- 在发生更改时把所需的修改降到最低

**怎么做**

- 在一个接口封装不同的概念
- 尽可能将不同的概念封进它自己的模块

**相关资源**

- [Encapsulate the Concept that Varies](http://principles-wiki.net/principles:encapsulate_the_concept_that_varies)
- [Encapsulate What Varies](http://blogs.msdn.com/b/steverowe/archive/2007/12/26/encapsulate-what-varies.aspx)
- [Information Hiding](https://en.wikipedia.org/wiki/Information_hiding)



---



#### 接口隔离原则

将臃肿的接口减少为多个更小、更具体的客户端特定接口。 接口应该更多地依赖于调用它的代码而不是实现它的代码。

**原因**

- 如果一个类实现了不需要的方法，则调用者需要知道该类的方法实现。 例如，如果一个类实现一个方法但只是抛出，那么调用者需要知道实际上不应该调用此方法

**怎么做**

- 避免臃肿接口。 类不应该存在违反单一责任原则的实现方法。

**相关资源**

- [Interface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle)



#### 命令查询分离原则

*Command Query Separation, CQS*

命令查询分离原则指的是每个方法应该是一个命令执行一个动作，或一个查询返回数据给他的调用者，而不是二者兼备。 提出问题的人不应该修改答案。

应用此原则后，程序员可以更自信地编写代码。 查询方法可以在任何地方以任何顺序使用，因为它们不会改变状态。 但使用命令必须更加小心。

**原因**

- 通过将方法将查询和命令明确地分离，程序员可以在不知道每个方法的实现细节的情况下自信地编码

**怎么做**

- 将每个方法实现为查询或命令的一种
- 通过命名约定来定义方法名，以此来暗示该方法是查询还是命令

**相关资源**

- [Command Query Separation in Wikipedia](https://en.wikipedia.org/wiki/Command%E2%80%93query_separation)
- [Command Query Separation by Martin Fowler](http://martinfowler.com/bliki/CommandQuerySeparation.html)