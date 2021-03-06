# 模型

模型一般对应数据库里的一张表，在`implcms`模型又两个部分组成模型配置和模型接口。

## 模型配置
`applications/akino/models/movie.yaml`
```yaml

# 模型结构,包括字段以及关系。schema 用于创建数据库表
schema:
    title: longString
    poster: longString
# 除了schema之外其他的都是模型配置,例如：

default:
    columns:
    - title
    - poster
# 上面的配置用可以通过 akino@movie 参数来访问

little:
    columns:
    - title
# 上面的配置用可以通过 akino@movie.little 参数来访问
```
上面的模型配置非常简单，为了更复杂的应用场景你也可以[深入了解](model-more.md)。

## 模型接口

所有的模型接口可以`modelConfig`这个参数,比如：`little`，默认`default`

### 查询接口
```
akino@movie.one

akino@movie.all

akino@movie.list
```
可选参数
- `id` 模型主键 例如: `id=13`
- `filter` 过滤器，例如：`filter[price]=0`
- `order` 排序，例如: `order[score]='DESC'`

### 更新和创建

```
akino@movie.create

akino@movie.update
```
现在我们创建一个`movie`模型

json数据类型
```javascript
{
    impl:{
        api: akino@movie.create
    },
    movie:{
        title: "另一城",
        poster: "default.png"
    },
}
```
html表单
```html
<form method="post" action="">
    <input name="impl[api]" value="akino@movie.create" type="hidden">
    <input name="movie[title]" value="另一城" type="text">
    <input name="movie[poster]" value="default.png" type="text">
    <button>提交</button>
</form>
```

> 在html和原生js环境下我们提供了[impl.js](../frontend/impl.js.md)库，通过该库你很容易实现请求。

对应的我们需要更新记录的话增加`id`参数就可以了

```javascript
movie:{
    title: "另一城",
    poster: "default.png",
    id: 2
}
```
```html
<input name="movie[id]" value="2" type="hidden">
```


#### 删除记录
```
model.delete
```
可选参数(二选一)
- `id` 模型主键 例如: `id=13`
- `filter` 过滤器，例如：`filter[price]=2`
