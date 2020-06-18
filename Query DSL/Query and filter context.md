## [Query and filter context](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-filter-context.html#query-filter-context)
查询子句的行为依赖于是否使用查询上下文或者赛选上下文
```The behaviour of a query clause depends on whether it is used in query context or in filter context: ```
## 查询上下文
查询上下文中使用的查询子句回答了“此文档与此查询子句的匹配程度如何”的问题？“，
除了决定文档是否匹配外，query子句还计算一个表示文档与其他文档匹配程度的分数。  
 当查询子句传递一个查询参数时，查询上下文起作用，列如在[search](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/search-request-query.html) API中的参数查询。
`Query context
 A query clause used in query context answers the question 
 “How well does this document match this query clause?” 
 Besides deciding whether or not the document matches, 
 the query clause also calculates a _score representing how well the document matches, 
 relative to other documents.
 Query context is in effect whenever a query clause is passed to a query parameter, 
 such as the query parameter in the search API.`
## 过滤上下文  
在过滤上下中，一个子查询解决的问题是“这个文档是否匹配这个查询语句”，需要的答案很简单 yes  or no ,不需要计算评分。
过滤上下文查询，通常是用来过滤结构化数据，比如：时间数据是否落在【2015，2016】之间；状态字段是否设置为“publish”?
当传递过滤参数时过滤查询起作用，例如 filter 或者 moust_not 参数在[bool](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-bool-query.html)查询中，
过滤参数在 [constant_score](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-constant-score-query.html) 查询，
或者 聚合 [过滤](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/search-aggregations-bucket-filter-aggregation.html)。
 `Filter context
  In filter context, a query clause answers the question 
  “Does this document match this query clause?” The answer is a simple Yes or No — no scores are calculated. 
  Filter context is mostly used for filtering structured data, e.g.
  Does this timestamp fall into the range 2015 to 2016?
  Is the status field set to "published"?
  Frequently used filters will be cached automatically by Elasticsearch, to speed up performance.
  Filter context is in effect whenever a query clause is passed to a filter parameter,
  such as the filter or must_not parameters in the bool query, 
  the filter parameter in the constant_score query, or the filter aggregation.`
 下面是在搜索API的查询和筛选上下文中使用的查询子句的示例。此查询将匹配满足以下所有条件的文档：
 `Below is an example of query clauses being used in query and filter context in the search API. 
 This query will match documents where all of the following conditions are met:`
 
 `The title field contains the word search.
  The content field contains the word elasticsearch.
  The status field contains the exact word published.
  The publish_date field contains a date from 1 Jan 2015 onwards.`
  
  `GET /_search
   {
     "query": {  1
       "bool": {  2
         "must": [
           { "match": { "title":   "Search"        }}, 2
           { "match": { "content": "Elasticsearch" }}  2
         ],
         "filter": [ 3
           { "term":  { "status": "published" }}, 4
           { "range": { "publish_date": { "gte": "2015-01-01" }}} 4
         ]
       }
     }
   }`
   
   `	
1 The query parameter indicates query context.
2 The bool and two match clauses are used in query context, which means that they are used to score how well each document matches.
3 The filter parameter indicates filter context.
4 The term and range clauses are used in filter context. They will filter out documents which do not match, but they will not affect the score for matching documents.`

建议
`
Use query clauses in query context for conditions which should affect the score of matching documents
 (i.e. how well does the document match), 
and use all other query clauses in filter context.`