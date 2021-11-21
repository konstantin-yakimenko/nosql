## Базовые возможности mongodb

##### 1. скачать и запустить mongodb через докер, команды:
```shell
> docker run -it --rm --name mongodb -d mongo
> docker exec -it mongodb mongo
```

##### 2. создать базу hw
```shell
> use hw
```

##### 3. добавить записи
```shell
> db.stud.insert([
   {"_id":0,"name":"aimee Zank","scores":[{"score":1.463179736705023,"type":"exam"},{"score":11.78273309957772,"type":"quiz"},{"score":35.8740349954354,"type":"homework"}]},
   {"_id":1,"name":"Aurelia Menendez","scores":[{"score":60.06045071030959,"type":"exam"},{"score":52.79790691903873,"type":"quiz"},{"score":71.76133439165544,"type":"homework"}]},
   {"_id":2,"name":"Corliss Zuk","scores":[{"score":67.03077096065002,"type":"exam"},{"score":6.301851677835235,"type":"quiz"},{"score":66.28344683278382,"type":"homework"}]},
   {"_id":3,"name":"Bao Ziglar","scores":[{"score":71.64343899778332,"type":"exam"},{"score":24.80221293650313,"type":"quiz"},{"score":42.26147058804812,"type":"homework"}]},
   {"_id":4,"name":"Zachary Langlais","scores":[{"score":78.68385091304332,"type":"exam"},{"score":90.2963101368042,"type":"quiz"},{"score":34.41620148042529,"type":"homework"}]},
   {"_id":5,"name":"Wilburn Spiess","scores":[{"score":44.87186330181261,"type":"exam"},{"score":25.72395114668016,"type":"quiz"},{"score":63.42288310628662,"type":"homework"}]},
   {"_id":6,"name":"Jenette Flanders","scores":[{"score":37.32285459166097,"type":"exam"},{"score":28.32634976913737,"type":"quiz"},{"score":81.57115318686338,"type":"homework"}]},
   {"_id":7,"name":"Salena Olmos","scores":[{"score":90.37826509157176,"type":"exam"},{"score":42.48780666956811,"type":"quiz"},{"score":96.52986171633331,"type":"homework"}]},
   {"_id":8,"name":"Daphne Zheng","scores":[{"score":22.13583712862635,"type":"exam"},{"score":14.63969941335069,"type":"quiz"},{"score":75.94123677556644,"type":"homework"}]},
   {"_id":9,"name":"Sanda Ryba","scores":[{"score":97.00509953654694,"type":"exam"},{"score":97.80449632538915,"type":"quiz"},{"score":25.27368532432955,"type":"homework"}]},
   {"_id":10,"name":"Denisha Cast","scores":[{"score":45.61876862259409,"type":"exam"},{"score":98.35723209418343,"type":"quiz"},{"score":55.90835657173456,"type":"homework"}]},
   {"_id":11,"name":"Marcus Blohm","scores":[{"score":78.42617835651868,"type":"exam"},{"score":82.58372817930675,"type":"quiz"},{"score":87.49924733328717,"type":"homework"}]},
   {"_id":12,"name":"Quincy Danaher","scores":[{"score":54.29841278520669,"type":"exam"},{"score":85.61270164694737,"type":"quiz"},{"score":80.40732356118075,"type":"homework"}]},
   {"_id":13,"name":"Jessika Dagenais","scores":[{"score":90.47179954427436,"type":"exam"},{"score":90.3001402468489,"type":"quiz"},{"score":95.17753772405909,"type":"homework"}]},
   {"_id":14,"name":"Alix Sherrill","scores":[{"score":25.15924151998215,"type":"exam"},{"score":68.64484047692098,"type":"quiz"},{"score":24.68462152686763,"type":"homework"}]}])

BulkWriteResult({
"writeErrors" : [ ],
"writeConcernErrors" : [ ],
"nInserted" : 15,
"nUpserted" : 0,
"nMatched" : 0,
"nModified" : 0,
"nRemoved" : 0,
"upserted" : [ ]
})
```

##### 4. убеждаемся что существует коллекция
```shell
> show collections
stud
```

##### 5. выбрать 5 записей:
```shell
> db.stud.find().limit(5)

{ "_id" : 0, "name" : "aimee Zank", "scores" : [ { "score" : 1.463179736705023, "type" : "exam" }, { "score" : 11.78273309957772, "type" : "quiz" }, { "score" : 35.8740349954354, "type" : "homework" } ] }
{ "_id" : 1, "name" : "Aurelia Menendez", "scores" : [ { "score" : 60.06045071030959, "type" : "exam" }, { "score" : 52.79790691903873, "type" : "quiz" }, { "score" : 71.76133439165544, "type" : "homework" } ] }
{ "_id" : 2, "name" : "Corliss Zuk", "scores" : [ { "score" : 67.03077096065002, "type" : "exam" }, { "score" : 6.301851677835235, "type" : "quiz" }, { "score" : 66.28344683278382, "type" : "homework" } ] }
{ "_id" : 3, "name" : "Bao Ziglar", "scores" : [ { "score" : 71.64343899778332, "type" : "exam" }, { "score" : 24.80221293650313, "type" : "quiz" }, { "score" : 42.26147058804812, "type" : "homework" } ] }
{ "_id" : 4, "name" : "Zachary Langlais", "scores" : [ { "score" : 78.68385091304332, "type" : "exam" }, { "score" : 90.2963101368042, "type" : "quiz" }, { "score" : 34.41620148042529, "type" : "homework" } ] }
```

##### 6. найти запись с полем name = Aurelia Menendez
```shell
> db.stud.find({"name" : "Aurelia Menendez"})
{ "_id" : 1, "name" : "Aurelia Menendez", "scores" : [ { "score" : 60.06045071030959, "type" : "exam" }, { "score" : 52.79790691903873, "type" : "quiz" }, { "score" : 71.76133439165544, "type" : "homework" } ] }
```

##### 7. Обновить запись с _id = 1
```shell
> db.stud.update({"_id" : 1}, {"name": "Ivan Ivanov"})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

##### 8. выбрать запись с _id = 1
```shell
> db.stud.find({"_id" : 1})
{ "_id" : 1, "name" : "Ivan Ivanov" }
```

##### 9. создание индекса по полю "name"
```shell
> db.stud.createIndex( { name: 1 } )
{
"numIndexesBefore" : 1,
"numIndexesAfter" : 2,
"createdCollectionAutomatically" : false,
"ok" : 1
}
```

##### 10. запрос по полю "name" : "Bao Ziglar"
```shell
> db.stud.find({"name" : "Bao Ziglar"})
{ "_id" : 3, "name" : "Bao Ziglar", "scores" : [ { "score" : 71.64343899778332, "type" : "exam" }, { "score" : 24.80221293650313, "type" : "quiz" }, { "score" : 42.26147058804812, "type" : "homework" } ] }
```
