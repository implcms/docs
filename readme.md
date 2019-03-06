# Implcms

## 服务器配置
```
nginx config

location ~ ^/(?!(applications/.*/assets|system/assets)) {
    fastcgi_pass unix:/dev/shm/php-cgi.sock;
    include fastcgi_params;
    fastcgi_param  SCRIPT_FILENAME  $document_root/index.php;
}
```

## 模型

模型一般对应数据库里的一张表，在`implcms`模型又两个部分组成模型配置和模型接口。

### 模型配置示例: `movie.yaml`

```yaml

# 模型结构,包括字段以及关系
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

### 模型接口

所有的模型接口都要传`modelConfig`这个参数，以下模型配置都支持

- `akino@movie`
- `akino@movie.little`

#### 查询接口
```
model.one

model.all

model.list
```
可选参数
- `id` 模型主键
- `filter` 过滤器，例如：`filter[price]=0`
- `order` 排序，例如: `order[score]='DESC'`
- `having` 通过关系查询，例如: `having[artists]=14`

#### 更新和创建

```
model.create

model.update

```
