# Similar url demo

## Steps
1. Install docker and docker-compose
2. cd into the root path and `docker-compose up`
3. get elk ip from `docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' similarurldemo_elk_1`
4. create indice: `curl -XPUT "http://[similarurldemo_elk_1 ip]:9200/similar-url" -d @similar-url-index-mapping.json`
5. add docs: `mv similar-url-example.csv input/similar-url-example.csv`
6. wait for index complete(it should have 10_000 docs): `curl -XGET "http://[similarurles_elk_1 ip]:9200/_cat/indices"`
7. make a simple query and verify the top records
```
curl -XGET "http://$(docker-ip similarurles_elk_1):9200/similar-url/_search?pretty" -d'                       *[master] 
{
  "query": {
    "terms": {
      "uberIds": [470334253, 505036857, 508380618, 516067213, 521105150, 539593897, 628296709, 640691803, 641260727, 641720782, 642211402, 644036565, 644178640, 644195300, 644207497, 646417903, 646417913, 646417936, 648598106, 660109214, 660935774, 660935788, 660935815, 660935826, 660936808, 661324228, 661740808, 661740814, 661740825, 661740834, 661740859, 661740892, 661740915, 662410419, 662410502, 662410590, 671047720, 674005942, 674013304, 674022297
      ]
    }
  },
  "_source": ["canonicalUrl", "uberIds"],
  "min_score": 22
}'
```
