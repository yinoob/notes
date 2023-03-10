#### SQL中的NULL

1．NULL不是值。

2．因为NULL不是值，所以不能对其使用谓词。

3．对NULL使用谓词后的结果是unknown。

4．unknown参与到逻辑运算时，SQL的运行会和预想的不一样。

5．按步骤追踪SQL的执行过程能有效应对4中的情况。最后说明一下，要想解决NULL带来的各种问题，最佳方法应该是往表里添加NOT NULL约束来尽力排除NULL。

NULL惹人讨厌的原因，一般来说有以下5个。

1．在进行SQL编码时，必须考虑违反人类直觉的三值逻辑。

2．在指定IS NULL、IS NOT NULL的时候，不会用到索引，因而SQL语句执行起来性能低下。

3．如果四则运算以及SQL函数的参数中包含NULL，会引起“NULL的传播”。

4．在接收SQL查询结果的宿主语言中，NULL的处理方法没有统一标准。

5．与一般列的值不同，NULL是通过在数据行的某处加上多余的位（bit）来实现的。因此NULL会使程序占据更多的存储空间，使得检索性能变差。

#### 消除NULL

1. 编号：使用异常编号
2. 名字：使用“无名氏”
3. 数值：用0代替
4. 日期：用最大值或最小值代替

#### SQL理论

支撑SQL和关系数据库的基础理论主要有两个：一个是数学领域的集合论，另一个是作为现代逻辑学标准体系的谓词逻辑（predicate logic），准确地说是“一阶谓词逻辑”。

#### 全称量词和存在量词

谓词逻辑中有量词（限量词、数量词）这类特殊的谓词。我们可以用它们来表达一些这样的命题：“所有的x都满足条件P”或者“存在（至少一个）满足条件P的x”。前者称为“全称量词”，后者称为“存在量词”，分别记作∀、∃。

#### 使用EXISTS谓词表达全称量词

使用EXISTS谓词来表达全称量化，这是EXISTS的用法中很具有代表性的一个用法。通过这一部分内容的学习，希望大家能习惯从全称量化“所有的行都××”到其双重否定“不××的行一行都不存在”的转换。

SQL中没有与全称量词相当的谓词，可以使用NOT EXISTS代替。

#### WHERE和HAVING

如果实体对应的是表中的一行数据，那么该实体应该被看作集合中的元素，因此指定查询条件时应该使用WHERE子句。如果实体对应的是表中的多行数据，那么该实体应该被看作集合，因此指定查询条件时应该使用HAVING子句。

1．在SQL中指定搜索条件时，最重要的是搞清楚搜索的实体是集合还是集合的元素。

2．如果一个实体对应着一行数据→那么就是元素，所以使用WHERE子句。

3．如果一个实体对应着多行数据→那么就是集合，所以使用HAVING子句。

4．HAVING子句可以通过聚合函数（特别是极值函数）针对集合指定各种条件。

#### 使用EXISTS更快

使用EXISTS时更快的原因有以下两个。

- 如果连接列（id）上建立了索引，那么查询Class_B时不用查实际的表，只需查索引就可以了。
- 如果使用EXISTS，那么只要查到一行数据满足条件就会终止查询，不用像使用IN时一样扫描全表。在这一点上NOT EXISTS也一样。
- 当IN的参数是子查询时，数据库首先会执行子查询，然后将结果存储在一张临时的工作表里（内联视图），然后扫描整个视图。很多情况下这种做法都非常耗费资源。使用EXISTS的话，数据库不会生成临时的工作表。

#### 尽量避免排序

会进行排序的代表性的运算有下面这些。

- GROUP BY子句
- ORDER BY子句
- 聚合函数（SUM、COUNT、AVG、MAX、MIN）
- DISTINCT
- 集合运算符（UNION、INTERSECT、EXCEPT）
- 窗口函数（RANK、ROW_NUMBER等）

不管是减少排序还是使用索引，抑或是避免中间表的使用，都是为了减少对硬盘的访问。

[SQL进阶教程-MICK-微信读书 (qq.com)](https://weread.qq.com/web/bookDetail/bd632340718ff622bd6a540)