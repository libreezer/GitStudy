# Preface
libcurl目前支持<mark>http、https、ftp、gopher、telnet、dict、file和ldap协议</mark>。libcurl同时也支持HTTPS认证、HTTP POST、HTTP PUT、 FTP 上传(这个也能通过PHP的FTP扩展完成)、HTTP 基于表单的上传、代理、cookies和用户名+密码的认证。
PHP中使用cURL实现Get和Post请求的方法
这些函数在PHP 4.0.2中被引入。
# Function
|   |   |
|---|---|
|[curl_close()](https://www.runoob.com/php/func-curl_close.html)|关闭一个cURL会话。|
|[curl_errno()](https://www.runoob.com/php/func-curl_errno.html)|返回最后一次的错误号。|
|[curl_error()](https://www.runoob.com/php/func-curl_error.html)|返回一个保护当前会话最近一次错误的字符串。|
|[curl_escape()](https://www.runoob.com/php/func-curl_escape.html)|返回转义字符串，对给定的字符串进行URL编码。|
|[curl_exec()](https://www.runoob.com/php/func-curl_exec.html)|执行一个cURL会话。|
|[curl_getinfo()](https://www.runoob.com/php/func-curl_getinfo.html)|获取一个cURL连接资源句柄的信息。|
|[curl_init()](https://www.runoob.com/php/func-curl_init.html)|初始化一个cURL会话。|
|[curl_pause()](https://www.runoob.com/php/func-curl_pause.html)|暂停及恢复连接。|
|[curl_reset()](https://www.runoob.com/php/func-curl_reset.html)|重置libcurl的会话句柄的所有选项。|
|[curl_setopt_array()](https://www.runoob.com/php/func-curl_setopt_array.html)|为cURL传输会话批量设置选项。|
|[curl_setopt()](https://www.runoob.com/php/func-curl_setopt.html)|设置一个cURL传输选项。|
|[curl_strerror()](https://www.runoob.com/php/func-curl_strerror.html)|返回错误代码的字符串描述。|
|[curl_unescape()](https://www.runoob.com/php/func-curl_unescape.html)|解码URL编码后的字符串。|
|[curl_version()](https://www.runoob.com/php/func-curl_version.html)|获取cURL版本信息。|

# GET
```
$curl_init = curl_init();  
// 设定链接  
curl_setopt($curl_init, CURLOPT_URL, $url_get);  
// GET请求方式 / 不设定方式默认GET  
curl_setopt($curl_init, CURLOPT_CUSTOMREQUEST, "GET");  
// 转换为变量  
curl_setopt($curl_init, CURLOPT_RETURNTRANSFER, true);  
// 执行  
$curl_exec = curl_exec($curl_init);  
// 关闭  
curl_close($curl_init);
```

# POST
```
$curl_init = curl_init();  
// 设定链接  
curl_setopt($curl_init, CURLOPT_URL, $url_get);  
// POST请求方式 / 不设定方式默认GET  
curl_setopt($curl_init, CURLOPT_CUSTOMREQUEST, "POST");  
// 传递数据  
curl_setopt($curl_init, CURLOPT_POSTFIELDS, $post_data);  
// 设置头信息 / 例子为发送json数据  
// curl_setopt($curl_init, CURLOPT_HTTPHEADER,  
//             array("Content-Type: multipart/form-data"));  
// 转换为变量  
curl_setopt($curl_init, CURLOPT_RETURNTRANSFER, true);  
// 执行  
$curl_exec = curl_exec($curl_init);  
// 关闭  
curl_close($curl_init);
```

>[! ] Tips:
>**注意：** POST上传数据只能有两种形式
>1. array("name"=>"breeze") 数组形式
>2. name=breeze 文本形式
>两种形式都不用设定header
## POST 上传文件
```
$url_get = "http://www.libreeze.top/temp/file_test.php";  
$file_path = "aaa";  
  
/**  
 * $data = array('images'=>'@'.$file_path.";type=image/jpeg"); // 老版用法  
 * $data = array('images'=>new CURLFile($file_path));        // php5.5以上推荐用法
 */  
  
// 上传文件 - 最好先检查文件权限以及路径  
$upload_file = array('upload' => new CURLFile($file_path));  
// 初始化curl  
$curl_init = curl_init();  
// 设定链接  
curl_setopt($curl_init, CURLOPT_URL, $url_get);  
// POST请求方式 / 不设定方式默认GET  
curl_setopt($curl_init, CURLOPT_CUSTOMREQUEST, "POST");  
// 传递数据  
curl_setopt($curl_init, CURLOPT_POSTFIELDS, $upload_file);  
// 设置头信息 / 可有可无  
curl_setopt($curl_init, CURLOPT_HTTPHEADER,  
    array("Content-Type: multipart/form-data"));  
// 转换为变量  
curl_setopt($curl_init, CURLOPT_RETURNTRANSFER, true);  
// 执行  
$curl_exec = curl_exec($curl_init);  
// 关闭  
curl_close($curl_init);
```
