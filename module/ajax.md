# 跨域异步请求

> 需要加载的模块

```js
const eeui = app.requireModule('eeui');
```

## eeui.ajax

> 跨域请求

* 支持自定义headers
* 支持上传文件

```js
/**
 * @param params    详细参数
 * @param callback  回调事件
 */
eeui.ajax({params}, callback(result))
```

### params 参数说明

| 属性名 | 类型 | 必须 | 描述 | 默认值 |
| --- | --- | :-: | --- | --- |
| url | `String` | √ | 请求地址 | - |
| name | `String` | - | 请求名称，用于取消请求 | - |
| method | `String` | - | 请求类型，`get`、`post` | get |
| dataType | `String` | - | 返回数据类型，`json`、`text` | json |
| timeout | `Number` | - | 请求超时时间（单位：毫秒） | 15000 |
| cache | `Number` | - | 缓存时间，0不缓存（单位：毫秒） | 0 |
| beforeAfter | `Boolen` | - | 是否回调`前(ready)`、`后(complete)`事件 <Tag date="20191202" :value="['1.0.32+']"/> | false |
| headers | `Object` | - | 请求头部headers | - |
| data | `Object` | - | 发送数据 | - |
| files | `Object` | - | 提交文件  | - |


### callback 回调`result`说明

```js
{
    status: 'success',      //状态，详见：注①
    
    code: 200,              //请求结果状态码
    headers: { ... },       //请求结果headers信息
    result: '...',         //请求结果
    
    name: 'requestName',    //请求名称
    url: 'http://....',     //请求地址
    cache: false,           //请求结果是否为缓存
}
```

> 注①：

- `ready`就绪
- `success`请求成功
- `error`请求失败
- `complete`请求结束

回调过程：`ready` -> (`success` | `error`) -> `complete`；

注: `ready`和`complete`事件仅在`beforeAfter=true`时有回调 <Tag date="20191202" :value="['1.0.32+']"/>。

### 简单示例

```js
//示例①
eeui.ajax({
    url: 'http://....'
}, function(result) {
    //......
});

//示例②
eeui.ajax({
    url: 'http://....',
    method: 'post',
    headers: {
        token: 'x2eefhjb2h3rj'
    },
    data: {
        username: 'eeui'
    },
    files: {
        userimg: '/storage/sdcard/.....'
    }
}, function(result) {
    //......
});
```

## eeui.ajaxCancel

> 取消跨域请求

```js
/**
 * @param name    请求名称（留空则取消所有请求）
 */
eeui.ajaxCancel(name)
```

## eeui.getCacheSizeAjax

> 获取跨域请求缓存

```js
/**
 * @param callback  回调事件，{size:123123}，单位：字节B
 */
eeui.getCacheSizeAjax(callback(result))
```

## eeui.clearCacheAjax

> 清除跨域请求缓存

```js
eeui.clearCacheAjax()
```


