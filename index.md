> 服务端地址: http://192.168.1.104:8888

### 1. 登录

##### 接口地址

> api/login/login

##### 请求方式

> POST

##### 请求参数

| 请求参数 | 必传 | 参数说明 |
| :------: | :--: | :------: |
| username |  ✅   |  用户名  |
| password |  ✅   |   密码   |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

### 2. 用户管理

#### 2.1 获取用户列表

##### 接口地址

> api/user/getUserList

##### 请求方式

> GET

##### 请求参数

|   请求参数    | 必传 |      参数说明      |
| :-----------: | :--: | :----------------: |
|   username    |      |       用户名       |
|   telephone   |      |       手机号       |
| department_id |      |       部门ID       |
|    status     |      | 状态 0:下架 1:上架 |
|     page      |      |        页码        |
|     size      |      |        页数        |

##### 响应示例

```json
	{
    "code": 200,
    "message": "成功",
    "data": {
        "total": 1,
        "per_page": 15,
        "current_page": 1,
        "last_page": 1,
        "data": [
            {
                "id": 1,
                "nickname": "豆芽菜不爱吃豆芽", // 昵称
                "telephone": "15850796186",  // 手机号
                "email": "15850796186@163.com", // 邮箱
                "sex": 1, // 性别 0:未知 1:男 2：女
                "username": "1", // 用户名
                "remark": "我是备注", // 备注
                "status": 0, // 状态 1：有效 0：无效
                "create_time": "2020-06-01 20:46:18",
                "update_time": "2020-06-01 23:21:44",
                "department": {
                    "department_name": "测试部" // 部门名称
                }
            }
        ]
    }
}
```

#### 2.2 新增用户

##### 接口地址

> **api/user/addUser**

##### 请求方式

> POST

##### 请求参数

|   请求参数    | 必传 |        参数说明        |
| :-----------: | :--: | :--------------------: |
|   username    |  ✅   |         用户名         |
| department_id |  ✅   |         部门ID         |
|   telephone   |  ✅   |         手机号         |
|     email     |  ✅   |          邮箱          |
|    remark     |  ✅   |          备注          |
|   password    |  ✅   |          密码          |
|    status     |  ✅   |   状态 0:下架 1:上架   |
|      sex      |  ✅   | 性别,0:未知 1:男 2：女 |
|   nickname    |      |          昵称          |
|    post_id    |      |         岗位ID         |
|    roleIds    |      |       角色ID数组       |

###### 请求示例

```json
{
	"username": "张三", // 用户名
	"department_id": 1, // 部门ID
	"telephone": "15850791686", // 手机号
	"email": "111@qq.com", // 邮箱
	"sex": 1,  // 性别 0:未知 1:男 2：女
	"remark": "", // 备注
	"status": 1, // 状态 1：有效 0：无效
   "nickname": "",  // 昵称
   "post_id": 1, // 岗位ID
   "roleIds": [1,2,3] // 角色ID
}
```

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 2.3 更新用户，删除用户

> **当status=0的时候视为删除用户**

##### 接口地址

> api/user/updateUser

##### 请求方式

> PUT

##### 请求参数

|   请求参数    | 必传 |        参数说明        |
| :-----------: | :--: | :--------------------: |
|      id       |  ✅   |         用户ID         |
|   username    |  ✅   |         用户名         |
| department_id |  ✅   |         部门ID         |
|   telephone   |  ✅   |         手机号         |
|     email     |  ✅   |          邮箱          |
|    remark     |  ✅   |          备注          |
|   password    |  ✅   |          密码          |
|    status     |  ✅   |   状态 0:下架 1:上架   |
|      sex      |  ✅   | 性别,0:未知 1:男 2：女 |
|   nickname    |  ✅   |          昵称          |
|    post_id    |  ✅   |         岗位ID         |
|    roleIds    |  ✅   |       角色ID数组       |

###### 请求示例

```json
{	
   "id": 1,
	"username": "张三",
	"department_id": 1,
	"telephone": "15850791686",
	"email": "111@qq.com",
	"sex": 1,
	"remark": "",
	"password": "",
	"status": 1,
   "nickname": "",
   "post_id": 1,
   "roleIds": [1,2,3]
}
```

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 2.4 重置密码

##### 接口地址

> api/user/resetPassword

##### 请求方式

> PUT

##### 请求参数

| 请求参数 | 必传 | 参数说明 |
| :------: | :--: | :------: |
|    id    |  ✅   |  用户ID  |
| password |  ✅   |   密码   |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 2.5 获取用户详情

##### 接口地址

> api/user/getUserDetail

##### 请求方式

> GET

##### 请求参数

| 请求参数 | 必传 | 参数说明 |
| :------: | :--: | :------: |
|    id    |  ✅   |  用户ID  |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": {
        "id": 1,
        "nickname": "豆芽菜不爱吃豆芽",
        "department_id": 2,
        "telephone": "15850796186",
        "email": "15850796186@163.com",
        "sex": 1,
        "username": "1",
        "remark": "我是备注",
        "post_id": null,
        "menus": [
            {
                "id": 1,
                "name": "系统管理",
                "pid": 0,
                "icon": "icon1",
                "sort": 1,
                "url": null,
                "children": [
                    {
                        "id": 2,
                        "name": "用户管理",
                        "pid": 1,
                        "icon": "icon1-1",
                        "sort": 1,
                        "url": null,
                        "children": [
                            {
                                "id": 5,
                                "name": "新增用户",
                                "pid": 2,
                                "icon": "icon1-1-1",
                                "sort": 1,
                                "url": null
                            },
                            {
                                "id": 6,
                                "name": "删除用户",
                                "pid": 2,
                                "icon": "icon1-1-2",
                                "sort": 2,
                                "url": null
                            }
                        ]
                    }
                ]
            },
            {
                "id": 7,
                "name": "系统工具",
                "pid": 0,
                "icon": "icon2",
                "sort": 2,
                "url": null,
                "children": [
                    {
                        "id": 8,
                        "name": "数据表管理",
                        "pid": 7,
                        "icon": "icon2-1",
                        "sort": 1,
                        "url": null
                    }
                ]
            }
        ],
        "roles": [ // 角色列表
            {
                "id": 1,
                "name": "管理员",
                "status": 1,
                "remark": null
            },
            {
                "id": 2,
                "name": "访问角色",
                "status": 1,
                "remark": null
            }
        ]
    }
}
```

### 3. 角色管理

#### 3.1 获取角色列表

##### 接口地址

> api/role/getRoleList

##### 请求方式

> GET

##### 请求参数

| 请求参数 | 必传 |      参数说明      |
| :------: | :--: | :----------------: |
|   name   |      |      角色名称      |
|  status  |      | 状态 0:下架 1:上架 |
|   page   |      |        页码        |
|   size   |      |        页数        |

##### 响应示例

```json
	{
    "code": 200,
    "message": "成功",
    "data": {
        "total": 2,
        "per_page": 15,
        "current_page": 1,
        "last_page": 1,
        "data": [
            {
                "id": 1, 
                "name": "管理员", // 角色名称
                "status": 1, // 状态
                "remark": null // 备注
            },
            {
                "id": 2,
                "name": "访问角色",
                "status": 1,
                "remark": null
            }
        ]
    }
}
```

#### 3.2 新增角色

##### 接口地址

> api/role/addUser

##### 请求方式

> POST

##### 请求参数

| 请求参数 | 必传 |      参数说明       |
| :------: | :--: | :-----------------: |
|   name   |  ✅   |        昵称         |
|  status  |  ✅   | 状态 0:下架 1：正常 |
| menuIds  |  ✅   |     菜单ID数组      |
|  remark  |      |        备注         |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 3.3  更新角色,删除角色

> 当status=0的时候视为删除角色

##### 接口地址

> api/role/updateRole

##### 请求方式

> PUT

##### 请求参数

| 请求参数 | 必传 |      参数说明       |
| :------: | :--: | :-----------------: |
|    id    |  ✅   |       角色ID        |
|   name   |  ✅   |        昵称         |
|  status  |  ✅   | 状态 0:下架 1：正常 |
| menuIds  |  ✅   |     菜单ID数组      |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 3.4  获取角色详情

##### 接口地址

> api/role/getRoleDetail

##### 请求方式

> GET

##### 请求参数

| 请求参数 | 必传 | 参数说明 |
| :------: | :--: | :------: |
|    id    |  ✅   |  角色ID  |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": {
        "id": 1,
        "name": "管理员",
        "status": 1,
        "remark": null,
        "menu": [ // 菜单列表
            {
                "id": 1, // 菜单ID
                "pid": 0, // 菜单上级ID 0：顶级 !0: 有上级 
                "name": "系统管理", // 菜单名称
                "icon": "icon1", // 菜单图标
                "sort": 1, // 排序
                "status": 1, // 状态 0:下架 1：正常
                "remark": null, // 备注
                "url": null, // 页面组件url
                "children": [
                    {
                        "id": 2,
                        "pid": 1,
                        "name": "用户管理",
                        "icon": "icon1-1",
                        "sort": 1,
                        "status": 1,
                        "remark": null,
                        "url": null,
                        "children": [
                            {
                                "id": 5,
                                "pid": 2,
                                "name": "新增用户",
                                "icon": "icon1-1-1",
                                "sort": 1,
                                "status": 1,
                                "remark": null,
                                "url": null
                            }
                        ]
                    }
                ]
            }
        ]
    }
}
```

### 4. 菜单管理

#### 4.1 新增菜单

##### 接口地址

> api/menu/addMenu

##### 请求方式

> POST

##### 请求参数

| 请求参数 | 必传 |              参数说明              |
| :------: | :--: | :--------------------------------: |
|   pid    |  ✅   |       父级菜单： 顶级菜单=0        |
|   name   |  ✅   |                名称                |
|   icon   |      |                图标                |
|   sort   |  ✅   |                排序                |
|  status  |  ✅   |        状态 0:下架 1：正常         |
|   url    |      | 菜单组件路径,如果status=1，url必传 |
|  remark  |      |                备注                |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 4.2 更新菜单，删除菜单

> 当status=0的时候视为删除菜单

##### 接口地址

> api/menu/updateMenu

##### 请求方式

> PUT

##### 请求参数

| 请求参数 | 必传 |              参数说明              |
| :------: | :--: | :--------------------------------: |
|    id    |  ✅   |               菜单ID               |
|   pid    |  ✅   |       父级菜单： 顶级菜单=0        |
|   name   |  ✅   |                名称                |
|   icon   |      |                图标                |
|   sort   |  ✅   |                排序                |
|  status  |  ✅   |        状态 0:下架 1：正常         |
|   url    |      | 菜单组件路径,如果status=1，url必传 |
|  remark  |      |                备注                |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 4.3 获取菜单列表

##### 接口地址

> api/menu/getMenuList

##### 请求方式

> GET

##### 请求参数

| 请求参数 | 必传 |      参数说明      |
| :------: | :--: | :----------------: |
|   name   |      |      菜单名称      |
|  status  |      | 状态 0:下架 1:上架 |
|   page   |      |        页码        |
|   size   |      |        页数        |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": [
        {
            "id": 1,
            "pid": 0,
            "name": "系统管理",
            "icon": "icon1",
            "sort": 1,
            "status": 1,
            "remark": null,
            "url": null,
            "children": [
                {
                    "id": 2,
                    "pid": 1,
                    "name": "用户管理",
                    "icon": "icon1-1",
                    "sort": 1,
                    "status": 1,
                    "remark": null,
                    "url": null,
                    "children": [
                        {
                            "id": 5,
                            "pid": 2,
                            "name": "新增用户",
                            "icon": "icon1-1-1",
                            "sort": 1,
                            "status": 1,
                            "remark": null,
                            "url": null
                        }
                    ]
                },
                {
                    "id": 3,
                    "pid": 1,
                    "name": "角色管理",
                    "icon": "icon1-2",
                    "sort": 2,
                    "status": 1,
                    "remark": null,
                    "url": null
                }
            ]
        },
        {
            "id": 7,
            "pid": 0,
            "name": "系统工具",
            "icon": "icon2",
            "sort": 2,
            "status": 1,
            "remark": null,
            "url": null,
            "children": [
                {
                    "id": 8,
                    "pid": 7,
                    "name": "数据表管理",
                    "icon": "icon2-1",
                    "sort": 1,
                    "status": 1,
                    "remark": null,
                    "url": null
                }
            ]
        }
    ]
}
```

### 5. 部门管理

#### 5.1 新增部门

##### 接口地址

> api/department/addDepartment

##### 请求方式

> POST

##### 请求参数

|    请求参数     | 必传 | 参数说明 |
| :-------------: | :--: | :------: |
| department_name |  ✅   | 部门名称 |
|      sort       |  ✅   |   排序   |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 5.2 更新部门，删除部门

> 当status=0的时候视为删除部门

##### 接口地址

> api/department/updateDepartment

##### 请求方式

> PUT

##### 请求参数

|    请求参数     | 必传 | 参数说明 |
| :-------------: | :--: | :------: |
|       id        |  ✅   |  部门ID  |
| department_name |  ✅   | 部门名称 |
|      sort       |  ✅   |   排序   |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 5.3 获取部门详情

##### 接口地址

> api/department/getDepartmentDetail

##### 请求方式

> GET

##### 请求参数

| 请求参数 | 必传 | 参数说明 |
| :------: | :--: | :------: |
|    id    |  ✅   |  部门ID  |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": {
        "id": 1,
        "department_name": "开发1部", // 部门名称
        "sort": 1,
        "status": 0,
        "create_time": "2020-06-04 22:44:40",
        "update_time": "2020-06-04 23:26:53"
    }
}
```

#### 5.4 获取部门列表

##### 接口地址

> api/department/getDepartmentList

##### 请求方式

> GET

##### 请求参数

|    请求参数     | 必传 |      参数说明      |
| :-------------: | :--: | :----------------: |
| department_name |      |      部门名称      |
|     status      |      | 状态 0:下架 1:上架 |
|      page       |      |        页码        |
|      size       |      |        页数        |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": {
        "total": 4,
        "per_page": "2",
        "current_page": 2,
        "last_page": 2,
        "data": [
            {
                "id": 3,
                "department_name": "运维部",
                "sort": 1,
                "status": 1,
                "create_time": "2020-06-04 22:55:55",
                "update_time": "2020-06-04 22:55:55"
            },
            {
                "id": 4,
                "department_name": "大数据部",
                "sort": 1,
                "status": 1,
                "create_time": "2020-06-04 22:56:14",
                "update_time": "2020-06-04 22:56:14"
            }
        ]
    }
}
```

### 6. 岗位管理

#### 6.1 新增岗位

##### 接口地址

> api/post/addPost

##### 请求方式

> POST

##### 请求参数

| 请求参数  | 必传 | 参数说明 |
| :-------: | :--: | :------: |
| post_name |  ✅   | 岗位名称 |
| post_code |  ✅   | 岗位编码 |
|   sort    |  ✅   |   排序   |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 6.2 更新岗位，删除岗位

> 当status=0的时候视为删除岗位

##### 接口地址

> api/post/updatePost

##### 请求方式

> PUT

##### 请求参数

| 请求参数  | 必传 | 参数说明 |
| :-------: | :--: | :------: |
|    id     |  ✅   |  岗位ID  |
| post_name |  ✅   | 岗位名称 |
| post_code |  ✅   | 岗位编码 |
|   sort    |  ✅   |   排序   |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 6.3 获取岗位详情

##### 接口地址

> api/post/getPostDetail

##### 请求方式

> GET

##### 请求参数

| 请求参数 | 必传 | 参数说明 |
| :------: | :--: | :------: |
|    id    |  ✅   |  部门ID  |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": {
        "id": 1,
        "post_name": "开发",
        "post_code": "develope",
        "sort": 1,
        "status": 1,
        "create_time": "2020-06-10 14:54:58",
        "update_time": "2020-06-10 14:55:00"
    }
}
```

#### 6.4 获取部门列表

##### 接口地址

> api/post/getPostList

##### 请求方式

> GET

##### 请求参数

| 请求参数  | 必传 |      参数说明      |
| :-------: | :--: | :----------------: |
| post_name |      |      岗位名称      |
| post_code |      |      岗位编码      |
|  status   |      | 状态 0:下架 1:上架 |
|   page    |      |        页码        |
|   size    |      |        页数        |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": {
        "total": 1,
        "per_page": 15,
        "current_page": 1,
        "last_page": 1,
        "data": [
            {
                "id": 1,
                "post_name": "开发",
                "post_code": "develope",
                "sort": 1,
                "status": 1,
                "create_time": "2020-06-10 14:54:58",
                "update_time": "2020-06-10 14:55:00"
            }
        ]
    }
}
```

### 7. 数据库管理

#### 7.1 获取数据库表列表

##### 接口地址

> api/database/showTables

##### 请求方式

> GET

##### 请求参数

无

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": [
        {
            "Name": "department", // 数据库表名
            "Engine": "InnoDB",
            "Version": 10,
            "Row_format": "Compact",
            "Rows": 4, // 数量
            "Avg_row_length": 4096,
            "Data_length": 16384,
            "Max_data_length": 0,
            "Index_length": 0,
            "Data_free": 0,
            "Auto_increment": 5,
            "Create_time": "2020-06-05 00:40:09", // 创建时间
            "Update_time": null, // 更新时间
            "Check_time": null,
            "Collation": "utf8_general_ci",
            "Checksum": null,
            "Create_options": "",
            "Comment": "部门" // 表备注
        }
    ]
}
```

#### 7.2 删除数据库表

##### 接口地址

> api/database/deleteTable

##### 请求方式

> DELETE

##### 请求参数

|  请求参数  | 必传 | 参数说明 |
| :--------: | :--: | :------: |
| table_name |  ✅   |   表名   |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": ""
}
```

#### 8.2 删除数据库表

##### 接口地址

> api/database/getTableDetail

##### 请求方式

> GET

##### 请求参数

|  请求参数  | 必传 | 参数说明 |
| :--------: | :--: | :------: |
| table_name |  ✅   |   表名   |

##### 响应示例

```json
{
    "code": 200,
    "message": "成功",
    "data": [
        {
            "TABLE_CATALOG": "def",
            "TABLE_SCHEMA": "tp5-admin",
            "TABLE_NAME": "user",
            "COLUMN_NAME": "id", // 字段名
            "ORDINAL_POSITION": 1,
            "COLUMN_DEFAULT": null,
            "IS_NULLABLE": "NO",
            "DATA_TYPE": "int",
            "CHARACTER_MAXIMUM_LENGTH": null,
            "CHARACTER_OCTET_LENGTH": null,
            "NUMERIC_PRECISION": 10,
            "NUMERIC_SCALE": 0,
            "DATETIME_PRECISION": null,
            "CHARACTER_SET_NAME": null,
            "COLLATION_NAME": null,
            "COLUMN_TYPE": "int(11) unsigned", // 字段类型
            "COLUMN_KEY": "PRI",
            "EXTRA": "auto_increment",
            "PRIVILEGES": "select,insert,update,references",
            "COLUMN_COMMENT": "" // 字段备注
        }
    ]
}
```

#### 