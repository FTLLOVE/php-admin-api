​	

# 													ThinkPHP5笔记

## 1. 路由配置

### 1.1 路由位置

```php
application/route.php
```

### 1.2 动态路由的定义

#### 1. 任意请求方式的定义(不严格定义的前提下推荐使用)

```PHP
Route::any("api/v1/index", "api/IndexController/index");
Route::rule("api/v1/index", "api/IndexController/index");
```

#### 2. GET

```php
Route::get("api/v1/index", "api/IndexController/index");
```

#### 3. POST

```php
Route::post("api/v1/index", "api/IndexController/index");
```

#### 4. PUT

```php
Route::put("api/v1/index", "api/IndexController/index");
```

#### 5. DELETE

```php
Route::delete("api/v1/index", "api/IndexController/index");
```

### 1.3 路由分组(推荐使用)

```php
Route::group("api/v1", function () {
	Route::any("index", 'api/IndexController/index');
   ...
});
```

## 2. 请求

#### 2.1  通用获取请求参数（直接实例化对象）

```php
$params = Request::instance()->params();
```

#### 2.2 作为方法的参数传递获取(推荐使用)

```php
public function index(Request $request) {
  $keyword = $request->param("keyword");
}
```

#### 2.3 获取特定方法的请求参数

```php
$request->get("keyword"); //GET
$request->post("keyword"); //POST
$request->put("keyword"); //PUT
$request->delete("keyword"); //DELETE
```

#### 2.4 获取文件(通过超全局变量)

```php
$file = $_FILES['file'];
```

## 3. 数据库

#### 3.1 原生SQL

```php
Db::query("select * from user where id = ?", [$request -> param("id")]);
```

#### 3.2 DB方式

```php
$data = Db::table("banner b")->field("b.*")
			->join("banner_item bi", "b.id = bi.banner_id")
			->where("bi.id", "=", $request->param("id"))
			->find();
```

#### 3.3 ORM(推荐)

> 所有的关联关系都定义在model层

##### 3.3.1  一对一（belongsTo）

> belongsTo($model, $foreignKey = '', $localKey = '', $alias = [], $joinType = 'INNER')
>
> 参数说明: 
>
> ​	model: 关联的模型名称
>
> ​	foreignKey:	关联外键
>
> ​	localKey： 关联主键
>
> ​	joinType: join类型，默认INNER，还有left,right	

```php
namespace app\api\model;

class BannerItemModel extends BaseModel
{
	protected $table = "banner_item";
	protected $visible = ["banner_id", "image"];
   
	public function image()
	{	
		return $this->belongsTo("ImageModel", "img_id", "id");
	}
}
```

##### 3.3.2 一对多(hasMany)

> hasMany($model, $foreignKey = '', $localKey = '')
>
> 参数说明:
>
> ​		model: 关联模型
>
> ​		foreignKey:	关联外键
>
> ​		localKey： 关联主键		

```php
namespace app\api\model;

use think\model;

class BannerModel extends BaseModel
{
	protected $table = "banner";
	protected $hidden = ["delete_time", "update_time"];

	public function items()
	{
		return $this->hasMany("BannerItemModel", "banner_id", "id");
	}

}
```

##### 3.3.3 多对多(belongsToMany)

> belongsToMany($model, $table = '', $foreignKey = '', $localKey = '')
>
> 参数说明:
>
> ​	model: 当前模型
>
> ​	table: 中间表
>
> ​	foreignKey: 关联外键
>
> ​	localKey: 当前模型关联键	

```php	
public function products()
{
		return $this->belongsToMany("ProductModel", "theme_product",
			"product_id", "theme_id");
}
```

##### 3.3.4 or和and查询

```php
return self::with(["categorys", "tags"])
			->where('title|content', 'like', "%$keyword%")
			->where("status", "=", 2)
			->paginate($size, false, ['page' => $page]);
```

##### 3.3.5 新增

```php
$params = Request::instance()->param();
$user = new UserModel();
$user->data($params);
$user->allowField(true)->save();
```

##### 3.3.6 更新

```php
$params = Request::instance()->param();
$user = new UserModel();
$user->data($params);
$id = Request::instance()->param("id");
$user->allowField(true)->save($params, ["id" => $id]);
```

##### 3.3.7 批量删除

```php
ArticleCategoryModel::where("article_id", "=", $articleId)->delete();
```

##### 3.3.8 批量新增

```php
$originCategoryIds = array();
$articleCategory = new ArticleCategoryModel();
   foreach ($categoryIds as $categoryId) {
      array_push($originCategoryIds, [
         "article_id" => $articleId,
         "category_id" => $categoryId
      ]);
   }
$articleCategory->saveAll($originCategoryIds);
```

##### 3.3.9 多表联查

```php
/**
	 * 根据角色获取菜单列表
	 * @param array $roleIds
	 * @return array
	 */
	public static function getMenuListByRoleList($roleIds) {
		return Db::table("role_menu rm")
			->field(['m.id', 'm.name', 'm.pid', 'm.icon', 'm.sort', 'm.url'])
			->join("role r", "rm.role_id = r.id", "left")
			->join("menu m", "rm.menu_id = m.id", "left")
			->where("rm.role_id", "in", $roleIds)
			->select();
	}
```



## 4. 拓展

### 4.1 七牛云

#### 4.1.1 配置文件

```php
	// application/config.php
	//七牛云空间配置
	'qiniu' => [
		'accesskey' => '3BrP3J9dfq2j6jF7Avk7qFNeitlmxEFV3_hpBxi8',
		'secretkey' => 'P_J1DOSPE2OeQbYB3LM1yFHRq3vxFXSbE9_B8KLU',
		'bucket' => 'qihuishou',
		'DOMAIN' => 'http://qn.qihuishou.club/'
	]
```

#### 4.1.2 封装公用上传&删除方法

```php
<?php
/**
 * @fileName QiniuUtil.php
 * @author sprouts <1139556759@qq.com>
 * @date 2020/5/21 00:50
 * @description 七牛云存储
 */
namespace app\util;

use app\enum\ScopeEnum;
use app\exception\CustomException;
use Qiniu\Auth;
use Qiniu\Storage\BucketManager;
use Qiniu\Storage\UploadManager;
use think\Request;

class QiniuUtil
{

	/**
	 * 上传图片
	 *
	 * @return string 图片的url
	 * @throws CustomException
	 */
	public static function uploadImage()
	{
		if (empty($_FILES['file']['tmp_name'])) {
			throw new CustomException(ScopeEnum::IMAGE_ERROR);
		}
		$file = $_FILES['file']['tmp_name'];
		$pathInfo = pathinfo($_FILES['file']['name']);
		$ext = $pathInfo['extension'];


		$auth = new Auth(config("qiniu.accesskey"), config("qiniu.secretkey"));
		$bucket = config("qiniu.bucket");
		$token = $auth->uploadToken($bucket);

		$fileName = date('Y') . '/' . date('m') . '/' .
			substr(md5($file), 8, 5) . date('Ynd') . rand(0, 9999) . '.' . $ext;

		$uploadMgr = new UploadManager();

		list($res, $err) = $uploadMgr->putFile($token, $fileName, $file);

		if ($err != null) {
			throw new CustomException(ScopeEnum::UPLOAD_ERROR);
		} else {
			return $fileName;
		}
	}

	/**
	 * 删除图片
	 * @param $originFile 原图片
	 * @return bool
	 * @throws CustomException
	 */
	public static function deleteImage($originFile)
	{
		$isImage = preg_match('/.*(\.png|\.jpg|\.jpeg|\.gif)$/', $originFile);
		if (!$isImage) {
			throw new CustomException(ScopeEnum::IMAGE_ERROR);
		}
		$auth = new Auth(config('qiniu.accesskey'), config('qiniu.secretkey'));
		$bucketManager = new BucketManager($auth);

		$res = $bucketManager->delete(config("qiniu.bucket"), $originFile);

		if (is_null($res)) {
			return true;
		}
		return false;
	}
}
```

## 5. 分页

### 5.1 模型分页(推荐使用)

```php
return self::where("name", "like", "%$name%")
			->where("flag", "=", $flag)
			->paginate($size, false, ['page' => $page]);
```

> 结果集隐藏

```php
$data = $list ->hidden(['id']);
```

## 6. 跨域

> 修改`application/tags.php`文件

```php
'app_init'     => [
   'app\\common\\CORS'
],
```

 ```php
<?php
/**
 * @fileName CORS.php
 * @author sprouts <1139556759@qq.com>
 * @date 2020/6/5 14:44
 * @description 跨域处理
 */

namespace app\common;

class CORS {

	public function appInit() {
		header('Access-Control-Allow-Origin: *');
		header("Access-Control-Allow-Headers: token,Origin, X-Requested-With, Content-Type, Accept");
		header('Access-Control-Allow-Methods: POST,GET');
		if (request()->isOptions()) {
			exit();
		}
	}
}
 ```

## 	7. MYSQL

> 创建表

```mysql
CREATE TABLE `student` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(30) NOT NULL COMMENT '用户名',
  `age` int(11) NOT NULL COMMENT '年龄',
  `status` tinyint(1) DEFAULT NULL COMMENT '状态 0:删除 1:正常',
  `create_time` datetime DEFAULT NULL,
  `update_time` datetime DEFAULT NULL,
  PRIMARY KEY (`id`,`username`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='学生表';
```

> 创建字段

```mysql
alter table student
	add class_id int not null;
```

> 修改字段

```mysql
alter table student change school_id school_no int null;

alter table student modify age varchar(255) not null comment '年龄';
alter table student modify status int null comment '状态 0:删除 1:正常';
```

> 删除字段

```mysql
alter table student drop column school_no;
```

> 查看数据库表的状态

```mysql
show table status ;
```

> 删除表

```mysql
drop table test;
```

> 修改表的备注

```mysql
alter table test comment '测试';
```



### 数据库模型设计:

|           参数说明            |                       参数类型                       |
| :---------------------------: | :--------------------------------------------------: |
|        名称  col_name         |                       varchar                        |
|         类型 col_type         |  tinyint,int,varchar,double,datetime,longtext,text   |
|      属性长度 col_length      | int (**只有类型是tinyint,int,varchar,double才需要**) |
|      小数点 col_decimal       |           int(**只有类型是double才需要**)            |
|     是否为空 col_is_null      |                         int                          |
|      是否为键 col_is_key      |                         int                          |
| 是否自增 col_is_auto_increase |           int(**只有是主键的时候才需要**)            |
|   默认值 col_default_value    |                        object                        |
|       备注 col_comment        |                       varchar                        |

