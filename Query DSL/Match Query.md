# [Match Query](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query.html#query-dsl-match-query)
&nbsp;&nbsp;匹配查询接受文本/数字/日期，对其进行分析，并构造查询。例如：
`match queries accept text/numerics/dates, analyzes them, and constructs a query. For example:`
`GET /_search
 {
     "query": {
         "match" : {
             "message" : "this is a test"
         }
     }
 }`
 注意，消息是字段的名称，您可以替换任何字段的名称。
 `Note, message is the name of a field, you can substitute the name of any field instead.`
 ## [Match](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query.html#query-dsl-match-query-boolean)
  匹配查询属于布尔类型。这意味着对提供的文本进行分析，分析过程从提供的文本构造一个布尔查询。运算符标志可以设置为or 或 and 来控制布尔子句（默认为or）。
  可以通过使用[minimum_should_match](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-minimum-should-match.html)参数，设置should子句最少匹配的数目。  
  分析器可以设置为控制哪个分析器将对文本执行分析过程。它默认为字段显式映射定义或默认搜索分析器。  
   可以将`lenient`参数设置为true，以忽略由数据类型不匹配导致的异常，例如尝试使用文本查询字符串查询数值字段。默认为false。
 ```The match query is of type boolean. It means that the text provided is analyzed and the analysis 
process constructs a boolean query from the provided text. 
The operator flag can be set to or or and to control the boolean clauses (defaults to or). 
The minimum number of optional should clauses to match can be set using the minimum_should_match parameter.
    
    The analyzer can be set to control which analyzer will perform the analysis process on the text. 
It defaults to the field explicit mapping definition, or the default search analyzer.
    
    The lenient parameter can be set to true to ignore exceptions caused by data-type mismatches, 
such as trying to query a numeric field with a text query string. Defaults to false.
```  

## [Fuzziness](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query.html#query-dsl-match-query-fuzziness)
&nbsp;&nbsp;模糊性允许根据所查询字段的类型进行模糊匹配。有关允许的设置，请参见模糊性。
&nbsp;&nbsp;在这种情况下，可以设置`prefix_length`前缀长度和`max_expansions`最大扩展来控制模糊过程.
&nbsp;&nbsp;如果设置了fuzzy选项，则查询将使用`top_terms_blended_freqs${max_expansions}`作为其[rewrite method](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-multi-term-rewrite.html)重写方法fuzzy_rewrite参数允许控制如何重写查询.
&nbsp;&nbsp;默认情况下允许模糊换位（ab→ba），但可以通过将模糊换位设置`fuzzy_transpositions`为false禁用。
&nbsp;&nbsp;注意，模糊匹配不适用于同义词，因为在引擎盖下，这些词被扩展为一个特殊的同义词查询，它混合了不支持模糊扩展的词频率。
```
   fuzziness allows fuzzy matching based on the type of field being queried. See Fuzziness for allowed settings.

   The prefix_length and max_expansions can be set in this case to control the fuzzy process. 
   If the fuzzy option is set the query will use top_terms_blended_freqs_${max_expansions} 
   as its rewrite method the fuzzy_rewrite parameter allows to control how the query will get rewritten.

   Fuzzy transpositions (ab → ba) are allowed by default but can be disabled by setting fuzzy_transpositions to false.

   Note that fuzzy matching is not applied to terms with synonyms, 
   as under the hood these terms are expanded to a special synonym query that blends term frequencies, 
   which does not support fuzzy expansion.
```

## [zero_terms_query](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query.html#query-dsl-match-query-zero) 
如果分析器使用移除了在一个查询停用词过滤器的所有token,默认情况下不会匹配文档。
为了更改是否可以使用zero_terms_query选项，该选项接受none（默认值）和 all（与match_all查询相对应）。
```
If the analyzer used removes all tokens in a query like a stop filter does, the default behavior is to match no documents at all. 
 In order to change that the zero_terms_query option can be used, which accepts none (default) and all which corresponds to a match_all query.
```

```
GET /_search
{
    "query": {
        "match" : {
            "message" : {
                "query" : "to be or not to be",
                "operator" : "and",
                "zero_terms_query": "all"
            }
        }
    }
}
```

## [cutoff_frequency](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/query-dsl-match-query.html#query-dsl-match-query-cutoff)
&nbsp;&nbsp;&nbsp;&nbsp;匹配查询支持截止频率，该截止频率允许指定一个绝对或相对文档频率，其中高频项移动到可选子查询中，
并且仅当低频项（低于截止频率）中的一个（对于or运算符）或所有低频项（对于and运算符）匹配时才进行评分

&nbsp;&nbsp;&nbsp;&nbsp;此查询允许在运行时动态处理stopwords，与域无关，不需要stopword文件。
`The match query supports a cutoff_frequency that allows specifying an absolute or 
relative document frequency where high frequency terms are moved into an optional subquery 
and are only scored if one of the low frequency (below the cutoff) 
terms in the case of an or operator or all of the low frequency terms in the case of an and operator match.
 
 This query allows handling stopwords dynamically at runtime, is domain independent and doesn’t require a stopword file. 
 It prevents scoring / iterating high frequency terms and only takes the terms into account 
 if a more significant / lower frequency term matches a document. 
 Yet, if all of the query terms are above the given cutoff_frequency the query is automatically transformed into 
 a pure conjunction (and) query to ensure fast execution.
 
 The cutoff_frequency can either be relative to the total number of documents if in the range [0..1) 
 or absolute if greater or equal to 1.0.
 
 Here is an example showing a query composed of stopwords exclusively:` 
 
 `GET /_search
  {
      "query": {
          "match" : {
              "message" : {
                  "query" : "to be or not to be",
                  "cutoff_frequency" : 0.001
              }
          }
      }
  }`
  
  `
The cutoff_frequency option operates on a per-shard-level. 
This means that when trying it out on test indexes with low document numbers 
you should follow the advice in Relevance is broken.`
  