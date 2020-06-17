## [Query and filter context](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-filter-context.html#query-filter-context)
查询子句的行为依赖于是否使用查询上下文或者赛选上下文
```The behaviour of a query clause depends on whether it is used in query context or in filter context: ```
## 查询上下文

`Query context
 A query clause used in query context answers the question 
 “How well does this document match this query clause?” 
 Besides deciding whether or not the document matches, 
 the query clause also calculates a _score representing how well the document matches, 
 relative to other documents.
 Query context is in effect whenever a query clause is passed to a query parameter, 
 such as the query parameter in the search API.`
 
 