# 控制器

在开发过程中除了模型数据之外我们我还要处理其他数据，此时我们需用通过控制器来编写我们的业务逻辑。控制器内可以有公开接口也可以有控制器内部用的私有函数。例如：
```php
// applications/akino/controllers/MovieController.php
<?php namespace Applications\Akino\Controllers;

/**
 * 电影控制器 
 */
class MovieController{

    /**
    * 电影统计数据
    */

    //此方法通过接口 akino@movie.statistics调用
    public function apiStatistics($param){
        $movieCount = $this->movieCount();
        $episodeCount = $this->episodeCount();

        $data = [
            'movieCount'=>$movieCount,
            'episodeCount'=>$episodeCount,
        ];

        return mr($data);
    }

    /**
    * 电影总数
    */
    private function movieCount(){
        return model('akino@movie')->count();
    }

    /**
    * 电影选集总数
    */
    private function episodeCount(){
        return model('episode')->count();
    }

}
```
在上面的代码中出现了几个全局函数`model()`, `mr()` ，这些函数在我们的[帮助函数](helpers.php)里做了详细的解释。