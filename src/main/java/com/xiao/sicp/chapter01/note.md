### 1.1 The Element of Programming

When we describe a language, we should pay particular attention to the means that the language provides for combining simple ideas to form more complex ideas.

Every powerful language has three mechanisms for accomplishing this:

    1. primitive expression, which represent the simplest entities the language is concerned with,
    2. means of combination, by which compound elements are built from simpler ones, and
    3. means of abstraction, by which compound elements can be named and manipulated as units.    

### 1.1 程序设计的基本元素

一个强有力的程序设计语言，不仅是一种只会计算机执行任务的方式，它还应该成为一种框架，使我们能够在其中组织自己有关计算过程的思想。每一种强有力的语言都为此提供了三种机制：

- **基本表达形式**，用于表示语言所关心的最简单的个体。
- **组合的方法**，通过它们表达从较简单的东西出发构造出复合的元素。
- **抽象的方法**，通过它们可以为复合对象命名，并将它们当作单元去操作。

#### 过程定义
`例如定义求一个整数的立方的过程cube：
(define (cube x) (* x x x))`

一般形式为：(define (\<name> \<formal parameters>)  \<body>)
 
 \<name>是一个符号；\<formal parameters>（形式参数）是一些名字；\<body>是一个表达式。
 
 \<name>和\<formal parameters>被写在一对括号里，成为一组，就像是实际调用被定义过程时的写法。`

#### 正则序和应用序

"完全展开而后归约"的求值模型称为正则序求值，与之对应的是现在解释器里实际使用的"先求值参数而后应用"的方式，它称为应用序求值。

Lisp采用应用序求值，部分原因在于这样做可以避免对于表达式的重复求值 (例如square ( * 2 5 ) )，从而提高一定的效率。更重要的是，在超出了可以采用替换方式模拟的过程范围之后，正则序的处理将变得更复杂得多。
#### 条件表达式和谓词

在Lisp中针对这种分情况分析的特殊形式，称为cond（表示"条件"）。其使用形式如下：

(define (abs x) (cond ((> x 0) x) ((< x 0) (- x)) ((= x 0) 0)))

条件表达式的一般形式为：(cond (\<p1> \<e1>) (\<p2> \<e2>) … (\<pn> \<en>))

if表达式的一般形式为：(if \<predicate> \<consequent> \<alternative>)

### 1.2 过程和它们所产生的计算

一个过程也就是一种模式，它描述了一个计算过程的局部演化方式，描述了这一计算过程中的每个步骤是怎样基于前面的步骤建立起来的。

#### 线性递归过程

要执行这种计算过程，解释器就需要维护好那些以后将要进行执行的操作的轨迹。（先逐步展开而后收缩的形状）

#### 线性迭代过程

一般来说，迭代计算过程就是那种其状态可以用固数目的状态`变量`描述的计算过程；而与此同时，又存在着一套固定的规则，描述了计算过程在从一个状态到下一状态转换时，这些变量的更新方式；还有一个（可能有的）结束检测，它描述了这一计算过程应该终止的条件。

#### 树形递归过程

### 1.3 用高阶函数做抽象

### 过程作为参数

查看书籍，理解(define (sum term a next b)) 含义为：实现从a到b进行term运算后的值求和（next表示a到b之间的变化规律）。

#### 用lambda构造过程

一般而言，lambda使用与define同样的方式创建过程，除了不为有关过程提供名字之外：( lambda ( \<formal parameters> \<body> ) )

这样得到的过程与通过define创建的过程完全一样，仅有的不同之处，就是这种过程没有与环境中的任何名字相关联。

事实上：(define (plus4 x) (+ x 4)) 等价于 (define plus4 (lambda (x) (+ x 4)))

一般说：(define ()) 相当于 (define (lambda () ))

#### "一等"元素 first-class object

使用限制最少的元素称为语言中的“一等”元素，是语言的“一等公民”，
具有最高特权（最普遍的可用性）。常见的包括：

-  可以用变量命名（在常规语言里，可存入变量，取出使用）
-  可以作为参数传给过程
-  可以由过程作为结果返回
-  可以放入各种数据结构
-  可以在运行中动态地构造