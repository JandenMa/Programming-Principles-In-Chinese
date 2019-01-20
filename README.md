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
- [Do the simplest thing that possibly work（尽可能做可运行的最简单的事）](#Do the simplest thing that possibly work（尽可能做可运行的最简单的事）)
- [Separation of Concerns（SoC，关注点分离）](#Separation of Concerns（SoC，关注点分离）)
- [Keep Things DRY（遵循不写重复代码）](#Keep Things DRY（遵循不写重复代码）)
- [Code For The Maintainer（作为代码的维护者）](#Code For The Maintainer（作为代码的维护者）)
- [Avoid Premature Optimization（避免过早优化）](#Avoid Premature Optimization（避免过早优化）)
- [Boy-Scout Rule（童子军规则）](#Boy-Scout Rule（童子军规则）)

#### 模块/类之间

- [Minimise Coupling（低耦合）](#Minimise Coupling（低耦合）)
- [Law of Demeter（LoD，迪米特法则）](#Law of Demeter（LoD，迪米特法则）)
- [Composition Over Inheritance（优先使用组合而非继承）](#Composition Over Inheritance（优先使用组合而非继承）)
- [Orthogonality（正交性）](#Orthogonality（正交性）)
- [Robustness Principle（健壮性法则）](#Robustness Principle（健壮性法则）)
- [Inversion of Control（IoC，控制反转）](#Inversion of Control（IoC，控制反转）)

#### 模块/类

- [Maximise Cohesion（高内聚）](#Maximise Cohesion（高内聚）)
- [Liskov Substitution Principle（LSP，里氏替换原则）](#Liskov Substitution Principle（LSP，里氏替换原则）)
- [Open/Closed Principle（OCP，开闭原则）](#Open/Closed Principle（OCP，开闭原则）)
- [Single Responsibility Principle（SRP，单一职责原则）](#Single Responsibility Principle（SRP，单一职责原则）)
- [Hide Implementation Details（隐藏接口实现细节）](#Hide Implementation Details（隐藏接口实现细节）)
- [Curly's Law（柯里定律）](#Curly's Law（柯里定律）)
- [Encapsulate What Changes（封装经常修改的代码）](#Encapsulate What Changes（封装经常修改的代码)
- [Interface Segregation Principle（接口隔离原则）](#Interface Segregation Principle（接口隔离原则）)
- [Command Query Separation（CQS，命令查询分离原则）](#Command Query Separation（CQS，命令查询分离原则）)

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



#### Do the simplest thing that possibly work（尽可能做可运行的最简单的事）

**原因**

- 如果我们只有专注于解决真正的问题，我们才能取得最大进展。

**怎么做**

- 问问自己：”最简单的事情是什么“

**参考来源**

- [Do The Simplest Thing That Could Possibly Work](http://c2.com/xp/DoTheSimplestThingThatCouldPossiblyWork.html)



---



#### Separation of Concerns（SoC，关注点分离）

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



#### Keep Things DRY（遵循不写重复代码）

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



#### Code For The Maintainer（作为代码的维护者）

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



#### Avoid Premature Optimization（避免过早优化）

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



#### Boy-Scout Rule（童子军规则）

美国童子军有一个简单的规则，可以适用于我们的职业：“离开营地时让它比你发现它时更干净”。 童子军规则规定我们应该始终保持代码比我们发现的更干净。【这意味着团队中每一个成员都有义务去改善代码】

**原因**

- 对现有代码库进行更改时，代码的质量往往会很低，从而会积攒很多技术债务。根据童子军规则，我们应该考虑每次提交的代码质量。技术债务是由于遭受连续的重构，无论多么小。

**怎么做**

- 每次提交都要确保不会降低代码的质量
- 每当有人看到一段不太清晰的代码时，他们应该抓住机会修正它。

**相关资源**

- [Opportunistic Refactoring](http://martinfowler.com/bliki/OpportunisticRefactoring.html)



#### Minimise Coupling（低耦合）



#### Law of Demeter（LoD，迪米特法则）



#### Composition Over Inheritance（优先使用组合而非继承）



#### Orthogonality（正交性）



#### Robustness Principle（健壮性法则）



#### Inversion of Control（IoC，控制反转）



#### Maximise Cohesion（高内聚）



#### Liskov Substitution Principle（LSP，里氏替换原则）



#### Open/Closed Principle（OCP，开闭原则）



#### Single Responsibility Principle（SRP，单一职责原则）



#### Hide Implementation Details（隐藏接口实现细节）



#### Curly's Law（柯里定律）



#### Encapsulate What Changes（封装经常修改的代码）



#### Interface Segregation Principle（接口隔离原则）



#### Command Query Separation（CQS，命令查询分离原则）