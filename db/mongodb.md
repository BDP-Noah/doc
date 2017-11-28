# MongoDB同步指南

同步客户端处理mongo复合数据类型（如: **ObjectId，ISODate，Timestamp** 等）时，采用**mongo strict**语法，与**robomongo**等第三方工具使用的**mongo shell**语法有区别.

## strict 语法文档

设有document如下：

```javascript
{
    "_id" : ObjectId("5492bfefa31053f0741a6a39"),
    "number" : 0,
    "string" : "COMPLETED",
    "lastUpdateTime" : ISODate("2015-01-27T13:39:49.824Z"),
    "timestamp_type" : Timestamp(12986507, 1),
}
```

### 语法对比

| 数据类型|mongo shell|mongo strict|
| -- | -- | -- |
| ISODate    |  `ISODate("2015-01-27T13:39:49.824Z")`     | `{"$date": "2015-01-27 13:39:49.824"}`   |
| ObjectId   |  `ObjectId("5492bfefa31053f0741a6a39")`    | `{"$oid": "5492bfefa31053f0741a6a39"}`   |
| Timestamp  |  `Timestamp(12986507, 1)`                  | `{"$timestamp":{"t":129986507, "i":1}}`  |

### 示例
```javascript
//基本类型
 {"number": 0} //查询number=0的documents
 {"number": {"$gte": 0}} //查询number>=0的documents
 {"number": {"$lte": 0}} //查询number<=0的documents
 {"number": {"$gt": 0}} //查询number>0的documents
 {"number": {"$lt": 0}} //查询number<0的documents

//复合类型
 {"lastUpdateTime" : {"$date":"2015-01-27 13:39:49.824"}}
 //查询lastUpdateTime="2015-01-27 13:39:49.824"的documents

 {"lastUpdateTime" : {"$gt":{"$date":"2015-01-27 13:39:49.824"}}}
 //查询lastUpdateTime>"2015-01-27 13:39:49.824"的documents

```
