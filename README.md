# H5-practice
H5 + interface call demo

## 1[手机加速感应器](https://github.com/recoveryMonster/H5-practice/blob/master/accelerometer.html)

## 2[手机录音和播放](https://github.com/recoveryMonster/H5-practice/blob/master/audio.html)

## 3[手机二维码](https://github.com/recoveryMonster/H5-practice/blob/master/barcode.html)

## 4[手机摄像头](https://github.com/recoveryMonster/H5-practice/blob/master/camera.html)

## 5[手机联系人](https://github.com/recoveryMonster/H5-practice/blob/master/contact.html)

## 6[手机设备管理]

Device模块管理设备信息，用于获取手机设备的相关信息，如IMEI、IMSI、型号、厂商等。通过plus.device获取设备信息管理对象。

###  应用场景

1. 打电话
2. 铃声提醒
3. 震动提醒
4. 音量设置
5. 查看设备属性信息

### 接口调用

[详见官方文档](http://www.html5plus.org/doc/zh_cn/device.html)

## 7.[Downloader下载管理器]

Downloader模块管理网络文件下载任务，用于从服务器下载各种文件，并支持跨域访问操作。通过plus.downloader获取下载管理对象。Downloader下载使用HTTP的GET/POST方式请求下载文件，符合标准HTTP/HTTPS传输协议。

### 应用场景

1. 音频下载
2. 视频下载
3. 文件下载
4. 数据缓存

### 接口调用

[详见官方文档](http://www.html5plus.org/doc/zh_cn/downloader.html)

## 8[系统事件管理]

Events模块管理客户端事件，包括系统事件，如扩展API加载完毕、程序前后台切换等。

### 应用场景

1. 等待事件完成
2. 应用从前台转入后台时停止占用资源
3. 应用从后台转到前台时开启一些服务
4. 断网时提示用户
5. 加载错误时提示用户

### 接口调用

[相关文档](http://www.html5plus.org/doc/zh_cn/events.html)