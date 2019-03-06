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
    
```


### 模型接口

所有的模型接口都要传`modelConfig`这个参数。modelConfig 有三个部分组成分别为：应用名称


#### 返回单个记录

```
model.one
```
参数
字段 | 解释 | 必填
-- | -- | --
`modelConfig` | 模型配置,应有名@模型名称 [配置] | 是



