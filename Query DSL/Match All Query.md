# Match All Query
The most simple query, which matches all documents, giving them all a _score of 1.0.
查询所有文档是最简单的查询，所有 _score 给评分 1.0。
`GET /_search
 {
     "query": {
         "match_all": {}
     }
 }`
 The _score can be changed with the boost parameter:
 评分可以通过 boost参数进行修改：
 `GET /_search
  {
      "query": {
          "match_all": { "boost" : 1.2 }
      }
  }`
 # Match NONE Query
 This is the inverse of the match_all query, which matches no documents.
 `GET /_search
  {
      "query": {
          "match_none": {}
      }
  }`
  
  