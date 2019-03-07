# 比较复杂的模型

模型一般对应数据库里的一张表，在`implcms`模型又两个部分组成模型配置和模型接口。

## 模型配置
`applications/akino/models/movie.yaml`
```yaml

# 模型结构,包括字段以及关系。schema 用于创建数据库表
schema:
    title: 
        type: longString
        null: false
    poster: 
        type: string
        null: false
        default: default.png
    author:
        type: string
        null: false
    _indexs: 
        - title
        - author
        - poster
    _uniques:
        - title
    _relations:
        artists:
            modelConfig: akino@artists
            type: relation
            select: name
```
内置字段

`_indexs` 需要创建索引的字段列表
如果单个字段直接写一位数组就可以，例如：
```yaml
_indexs: 
    - title
    - author
    - poster

#多个字段创建索引

_indexs: 
    title_and_author: 
        - title
        - author
```

`_uniques` 跟`_indexs` 非常类似

```yaml
_uniques: 
    - title
    - author
    - poster

#多个字段创建索引
_uniques: 
    title_and_author: 
        - title
        - author

```

我们的模型肯定会关联很多其他模型，这些关系结构我们存到`_relations`字段里
```yaml
_relations:
    tags: 
        modelConfig: category@category
        type: relation
        select: name
    episode:
        modelConfig: akino@episode
        type: hasMany
    company:
        modelConfig: akino@company
        type: belongsTo
```

除了`schema`之外其他的都是模型配置,可以说查询配置。通过此配置我们不仅起到查询效果之外，我们还可以通过此配置来生成我们界面，具体用法在官方发布的`admin`应用文档里做了详细解释。

其中`default`配置是直接通过`应用名@模型名`来访问的，例如: 下面的配置可以通过`akino@movie`访问

```yaml
default:
    columns:
    - title(myTitle) #字段别名
    - poster
    - artists
all:
    columns:
    - title
    - poster
    - author
    - artists
    - tags
```
在上面的配置里面除了常规字段之外还有一个`artists`字段，该字段在上面的`_relations`里面定义的，通过上面的配置我们可以获取一个电影和它的演员。更多用法等你挖掘哦~

## 模型接口

所有的模型接口都要传`modelConfig`这个参数，例如：`akino@movie or akino@movie.all`

### 查询接口
```
model.one

model.all

model.list
```
可选参数
- `id` 模型主键 例如: `id=13`
- `filter` 过滤器，例如: `filter[price]=0`
- `order` 排序，例如: `order[score]='DESC'`
- `having` 通过关系过滤，例如: `having['artists']=12`

### 更新和创建
```
model.create

model.update
```
现在我们创建一个`movie`模型

>更新记录需要增加`id`参数就可以了
json数据类型
```javascript
{
    impl:{
        api: model.create
    },
    modelConfig: 'akino@movie',
    movie:{
        title: "另一城",
        poster: "default.png"
    },
}
```
html表单
```html
<form method="post" action="">
    <input name="impl[api]" value="model.create" type="hidden">
    <input name="modelConfig" value="akino@movie" type="hidden">
    <input name="movie[title]" value="另一城" type="text">
    <input name="movie[poster]" value="default.png" type="text">
    <button>提交</button>
</form>
```
> 在html和原生js环境下我们提供了[impl.js](../frontend/impl.js.md)库，通过该库你很容易实现请求。

#### 删除记录
```
model.delete
```
可选参数(二选一)
- `id` 模型主键 例如: `id=13`
- `filter` 过滤器，例如：`filter[price]=2`

#### 附加/移除关系
```
model.attach
```
参数
- `relation[关系名]=目标模型ID` 必填
- `relation[remark]=关系备注参数` 可选

#### 移除关系
```
model.detach
```

参数(二选一)
- `relation[关系名]=目标模型ID` 
- `id=关系ID` 
