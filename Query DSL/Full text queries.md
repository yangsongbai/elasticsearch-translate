# [Full text queries](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/full-text-queries.html)
高级全文查询通常用于对全文字段（如电子邮件。他们了解如何分析正在查询的字段，并在执行之前将每个字段的分析器（或搜索分析器）应用于查询字符串。
`The high-level full text queries are usually used for running full text queries on full text fields like the body of an email.
 They understand how the field being queried is analyzed and will apply each field’s analyzer (or search_analyzer) 
 to the query string before executing.`
 查询可以分为以下几组：  
 * [x] [匹配查询](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query.html)
   用于执行全文查询的标准查询，包括模糊匹配和短语或邻近查询。  
 * [x] [短语查询](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query-phrase.html)
   类似于匹配查询，但用于匹配精确的短语或单词邻近匹配。  
 * [x] [匹配短语前缀查询](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query-phrase-prefix.html)  
    类似于匹配短语查询，但对最后一个单词进行通配符搜索。  
 * [x] [匹配短语前缀查询](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-multi-match-query.html) 
    匹配查询的多字段版本   
 * [x] [常用术语查询](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-common-terms-query.html)
  更专业的查询，它更倾向于使用不常用的词。
 * [x] [query_string query](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-query-string-query.html)  
 支持压缩Lucene查询字符串语法，允许您在单个查询字符串中指定AND | OR | NOT条件和多字段搜索。仅供专业用户使用
 * [x] [simple_query_string query](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-simple-query-string-query.html)  
  更简单、更健壮的查询字符串语法版本，适合直接向用户公开         
 ```
The queries in this group are:

match query
The standard query for performing full text queries, including fuzzy matching and phrase or proximity queries.
match_phrase query
Like the match query but used for matching exact phrases or word proximity matches.
match_phrase_prefix query
The poor man’s search-as-you-type. Like the match_phrase query, but does a wildcard search on the final word.
multi_match query
The multi-field version of the match query.
common terms query
A more specialized query which gives more preference to uncommon words.
query_string query
Supports the compact Lucene query string syntax, allowing you to specify AND|OR|NOT conditions and multi-field search within a single query string. For expert users only.
simple_query_string query
A simpler, more robust version of the query_string syntax suitable for exposing directly to users.
```
