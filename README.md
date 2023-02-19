# php2go

[![MIT licensed][3]][4]

[3]: https://img.shields.io/badge/license-MIT-blue.svg
[4]: LICENSE

#### 介绍
基于 reflect 的应用，实现 go 语言 Array(Slice/Map) 常用工具函数的封装，具体的函数方式下面有详细内容讲解。

#### 安装
```shell
// github
go get github.com/lihao1988/go-array

// gitee
go get gitee.com/lihao1988/go-array
```

## 版本要求
Go 1.15 or above.

## Array(Slice/Map) Functions
#### In(value, array interface{}) bool
```go
// 用于检查Array(Slice/Map)中是否存在指定的值
value = "a"
dataMap := []string{"a", "b", "c"}
isExist := In(value, dataMap)
fmt.Println(isExist)
```
#### Keys(array interface{}, &keys interface{})
```go
// 获取数组中所有的键名
dataMap := map[string]string{
    "a": "this is 'A'",
    "b": "this is 'B'",
}

var keys []string
Keys(dataMap, &keys)
fmt.Println(keys)
```
#### Values(array interface{}, &values interface{})
```go
// 获取数组中所有的值
dataMap := map[string]string{
    "a": "this is 'A'",
    "b": "this is 'B'",
}

var values []string
Values(dataMap, &values)
fmt.Println(values)
```
#### Merge(&array interface{}, dArr ...interface{})
```go
// 把一个或多个数组合并为一个数组
dataMap := map[string]string{
    "a": "this is 'A'",
    "b": "this is 'B'",
}

dataOne := map[string]string{
    "c": "this is 'C'",
}
dataTwo := map[string]string{
    "d": "this is 'D'",
}

Merge(&dataMap, dataOne, dataTwo)
fmt.Println(dataMap)
```
#### Unique(&array interface{})
```go
// 删除数组中的重复值
dataMap := map[int]string{
    "a": "this is 'A'",
    "b": "this is 'B'",
    "a": "this is 'A'",
}
Unique(&dataMap)
fmt.Println(dataMap)
```
#### Column(&dest, input interface{}, columnKey, indexKey string)
```go
// 返回输入数组中某个单一列的值
dataMap := map[string]map[string]string{
    "a": {"key": "a1", "value": "A"},
    "b": {"key": "b1", "value": "B"},
}

// key 使用子数组字段 'key'，column 为子数组内容
dest := map[string]map[string]string{}
Column(&dest, dataMap, "", "key")
fmt.Println(dest)

//key 使用子数组字段 'key'，column 使用子数组字段 'value'
dest := map[string]string{}
Column(&dest, dataMap, "value", "key")
fmt.Println(dest)

//key 为空则为 list，column 使用子数组字段 'value'
dest := []map[string]string{}
Column(&dest, dataMap, "value", "")
fmt.Println(dest)
```
#### Diff(&array interface{}, dArr ...interface{})
```go
// 比较数组,返回差集(只比较键值)
dataMap := map[int]string{
    "a": "this is 'A'",
    "b": "this is 'B'",
	"c": "this is 'C'",
}

dataOne := map[int]string{
    "b": "this is 'B'",
    "d": "this is 'D'",
}

dataTwo := map[int]string{
    "c": "this is 'C'",
    "e": "this is 'E'",
}

Diff(&dataMap, dataOne, dataTwo)
fmt.Println("dataMap", dataMap)
```
#### Intersect(&array interface{}, dArr ...interface{})
```go
// 比较数组，返回交集(只比较键值)
dataMap := map[int]string{
    "a": "this is 'A'",
    "b": "this is 'B'",
}

dataOne := map[int]string{
    "b": "this is 'B'",
    "d": "this is 'D'",
}

dataTwo := map[int]string{
    "c": "this is 'C'",
    "e": "this is 'E'",
}

Intersect(&dataMap, dataOne, dataTwo)
fmt.Println("dataMap", dataMap)
```