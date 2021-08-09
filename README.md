# faker

To response a fake data for struct

## tag快速入门

所有fake数据通过tag标签来控制生成，其组成形式为： `fake:$expression`

- `fake` 为固定标志，代表该字段需要生成一个fake数据，不声明则不生成，或者写作`fake:"-"`
- `$expression` 为fake生成规则表达式，详情见下文

|功能|expression|示例|示例说明|备注|
|---|---|---|---|---|
|返回常量值|const=$value|const=true|返回固定boolean值为true|常量值仅适用于基础数据类型|
|返回随机值|rand$suffix|randBool|返回一个boolean的随机值|该随机表达式仅适用于基础数据类型|
|返回指定长度的数组|arr($length,$itemPression)|arr(3,randBool)|返回一个长度为3的boolean数组|该随机表达式仅适用于切片和数组|
|返回指定长度的map|map($length,$keyExpression,$valueExpression)|map(3,randInt,randString)|返回一个长度为3,key为int随机值，value为字符串随机值的map数据|该随机表达式仅适用于map结构|
|返回指定范围(闭区间)的随机整数|randInt[$lowBound,$highBound]|randInt[1,100]|返回在1-100之间的随机整数|该随机表达式仅适用于整型|
|返回指定长度随机整数|randId($length)|randId(5)|返回长度为5的随机无符号整数|该随机表达式仅适用于无符号整型|
|返回指定长度字符串|randStr($length)|randStr(20)|返回长度为20的随机字符串|该随机表达式仅适用于字符串类型|
|返回随机名称|randName($type,$lang)|randName(person,cn)|返回一个随机中文人名|该随机表达式仅适用于字符串类型|
|返回随机ObjectHexId|objectHex|objectHex|返回一个随机ObjextHexId|该随机表达式仅适用于字符串类型|
|返回随机手机号|mobile|mobile|返回一个随机手机号|该随机表达式仅适用于字符串类型|
|返回随机国内座机|phone|phone|返回一个随机国内座机|该随机表达式仅适用于字符串类型|
|返回枚举随机|enum[$value,$value...]|enum[1,2,3]|从1,2,3中返回一个随机值|该随机表达式仅适用于基本数据类型|
|...|...|...|...|...|


## 示例
```go
package types

type Fake struct{
	Id int64 `json:"id" fake:"randId"`
	Name string `json:"name" fake:"randName(persion,cn)"`
	Mobile string `json:"mobile" fake:"mobile"`
	Gender string `json:"gender" fake:"enum[男,女]"`
	Hobby []string `json:"hobby" fake:"arr(3,randStr)"`
}
```

```json
{
  "id": 1,
  "name": "张三",
  "mobile": "136xxxx001",
  "gender": "男",
  "hobby": ["footbal","swimming","learning"]
}
```

## 详细用法
TODO(anqiansong)