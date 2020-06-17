原文地址     
https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl.html
### 原文
Elasticsearch provides a full Query DSL (Domain Specific Language) 
based on JSON to define queries. Think of the Query DSL as an AST (Abstract Syntax Tree) of queries,
 consisting of two types of clauses:
### 翻译   
Elasticsearch 基于json格式提供了一种全文查询的DSL(领域特定语言) 。 我们可以将查询DSL看成是AST(抽象语法树)查询 ，
它由以下两种类型组成：  
  叶子查询子句  
    叶子查询子句，在特定的字段特定的查找特定值，例如[match](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query.html)、
    [term](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-term-query.html)或者[range](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-range-query.html)等查询，这些查询可以单独使用。
  `Leaf query clauses
   Leaf query clauses look for a particular value in a particular field, 
   such as the match, term or range queries. These queries can be used by themselves.`  
   复合查询子句  
    复合查询子句包装其他叶查询或复合查询，并用于以逻辑方式组合多个查询（例如[bool](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-bool-query.html)
    或[dis_max](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-dis-max-query.html)查询），或更改它们的行为（例如[constant_score](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-constant-score-query.html)查询）
   `Compound query clauses
    Compound query clauses wrap other leaf or compound queries and 
    are used to combine multiple queries in a logical fashion (such as the bool or dis_max query), 
    or to alter their behaviour (such as the constant_score query).`
查询子句的行为不同，这取决于它们是在[查询上下文](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-filter-context.html)中使用还是在[筛选上下文](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-filter-context.html)中使用。    
`Query clauses behave differently depending on whether they are used in query context or filter context.`
