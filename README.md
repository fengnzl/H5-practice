# H5-practice
混合模式 app 开发中通过 javascript 结合 html5+SDK 进行原生组件调用的相关实例。本示例 `demo` 根据[hbuilder开发移动app视频教程mui视频教程html5视频教程](https://edu.csdn.net/course/play/2949/48552)编写，相关api[文档地址](https://www.dcloud.io/docs/api/zh_cn/accelerometer.html)

## 1[手机加速感应器]

其应用场景有：

1. 摇一摇
2. 步数统计
3. 速度感应系统等

> Accelerometer模块管理设备加速度传感器，用于获取设备加速度信息，包括x（屏幕水平方向）、y（垂直屏幕水平方向）、z（垂直屏幕平面方向）三个方向的加速度信息

![](https://raw.githubusercontent.com/recoveryMonster/HexoImages/master/blog/20190909183212.png)

### 方法：

- [getCurrentAcceleration](https://www.dcloud.io/docs/api/zh_cn/accelerometer.html#plus.accelerometer.getCurrentAcceleration): 获取当前设备的加速度信息

  `void plus.accelerometer.getCurrentAcceleration( successCB, errorCB );`

- [watchAcceleration](https://www.dcloud.io/docs/api/zh_cn/accelerometer.html#plus.accelerometer.watchAcceleration): 监听设备加速度变化信息

  `Number plus.accelerometer.watchAcceleration( successCB, errorCB, option );
  Option:{frequency:1000}`

- [clearWatch](https://www.dcloud.io/docs/api/zh_cn/accelerometer.html#plus.accelerometer.clearWatch): 关闭监听设备加速度信息

  `void plus.accelerometer.clearWatch( watchId );`

首先新建一个包含`mui`的H5+目录

![](https://raw.githubusercontent.com/recoveryMonster/HexoImages/master/blog/20190909184556.png)

相关代码见文件

## 2[手机录音和播放]

Audio模块用于提供音频的录制和播放功能，可调用系统的麦克风设备进行录音操作，也可调用系统的扬声器设备播放音频文件。通过plus.audio获取音频管理对象。

应用场景：

1. 音频录制
2. 语音聊天
3. 语音留言
4. 音频播放

### 调用接口

对象

1. `AudioRecorder`

   ```js
   void recorder.record( option, successCB, errorCB );
   Option:{filename:"_doc/audio/"}
   ```

2. `AudioPlayer`

   ```js
   void play( successCB, errorCB );
   void pause(); 
   void resume(); 
   void stop(); 
   void seekTo( position ); 
   Position:100 //单位为秒
   Number getDuration(); //单位为秒
   Number getPosition(); //单位为秒
   void setRoute( route );
   Route：//数字，常量ROUTE_SPEAKER（扬声器模式）ROUTE_EARPIECE（听筒模式）
   ```

方法:

1. `getRecorder()`//获取录音设备

   ```js
   AudioRecorder plus.audio.getRecorder();
   ```

2. `createPlayer()`//创建播放器

   ```js
   AudioPlayer plus.audio.createPlayer( path )
   ```

## 3[手机二维码]

Barcode模块管理条码扫描，提供常见的条码（二维码及一维码）的扫描识别功能，可调用设备的摄像头对条码图片扫描进行数据输入。通过plus.barcode可获取条码码管理对象。

应用场景：

1. 扫码关注
2. 扫码支付
3. 扫码登录

调用方式：

1. 图片识别
2. 摄像头扫描

常用的为[QR](https://www.dcloud.io/docs/api/zh_cn/barcode.html#plus.barcode.QR): QR二维码，数值为0和[EAN13](https://www.dcloud.io/docs/api/zh_cn/barcode.html#plus.barcode.EAN13): EAN条形码标准版，数值为1。

### 调用接口

1. `Barcode = new plus.barcode.Barcode( id, filters, styles );`

   ```js
   Id // html 对象id用户识别控件的初始化
   Filter //要识别的条码类型过滤器，为条码类型常量数组
   Styles //条码识别控件样式
       String frameColor; //扫描框颜色
       String scanbarColor; //扫描条颜色
       String background;//条码识别控件背景颜色
   ```

2. `Barcode`

   ```js
   //Method
   void start( options ); 
   	Options: 
           Boolean conserve; //是否保存截图，默认false
           String filename; //截图保存路径
           Boolean vibrate; //成功后是否震动,默认true
           String sound;//成功后的提示音,可取none|default,默认default
   void cancel(); 
   void close(); 
   void setFlash( open ); 
   	Open: true/false//默认false
   // Events 
   void onmarked();// 识别成功后的回调 
   void onerror();
   ```

方法： `void plus.barcode.scan( path, successCB, errorCB, filters );`

## 4[手机摄像头]

Camera模块管理设备的摄像头，可用于拍照、摄像操作，通过plus.camera获取摄像头管理对象。

应用场景：

1. 保存自拍
2. 保存照片
3. 上传照片
4. 保存视频
5. 上传视频

### 调用接口

1. Camera

   ```js
   readonly attribute String[] supportedImageResolutions; 
   readonly attribute String[] supportedVideoResolutions; 
   readonly attribute String[] supportedImageFormats; 
   readonly attribute String[] supportedVideoFormats; 
   function void captureImage( successCB, errorCB, option ); 
           void onSuccess( capturedFile ) { // Caputre image/video file code. } 
           void onError( error ) { // Handle camera error 
               var code = error.code; // 错误编码 
               var message = error.message; // 错误描述信息
            }
           CameraOption { 
               attribute String filename; //拍照或摄像文件保存的路径, 以“/”结尾是路径，自动生成文件名
               attribute String format; //拍照或摄像的文件格式
               attribute String index; //1主摄像头，2辅摄像头
               attribute Number videoMaximumDuration // 视频长度 默认值为0（不限定视频长度）单位为秒（s） 仅在startVideoCapture时有效。
               attribute Boolean optimize // true - 自动调整图片方向； false - 不调整。 默认值为true。 设置为false则可避免延迟问题 ios不支持
               attribute PopPosition popover; //拍照或摄像界面弹出指示区域,仅ipad{top:"10px",left:"10px",width:"200px",height:"200px"}
           }
   function void startVideoCapture( successCB, errorCB, option ); 
   	参数同captureImage
   function void stopVideoCapture();
   ```

方法：`Camera plus.camera.getCamera( index ); `//1主摄像头，2辅摄像头,

## 5[手机联系人]

Contacts模块管理系统通讯录，用于可对系统通讯录进行增、删、改、查等操作。通过plus.contacts获取系统通讯录管理对象

应用场景：

1. 查找联系人
2. 导入联系人
3. 通讯录备份
4. 通讯录同步

### 调用接口

1. `AddressBook`

   ```js
   Contact create(); 
   void find(contactFields, successCB, errorCB, findOptions);
       contactFields //查找返回联系人中需要包含的信息
      	// 可取Contact对象的属性名称
       void onSuccess(contacts){ // Find contact success. }//数组，查找到的联系人对象
       findOptions :
           ContactFindFilte[] filter; // [{logic:"or",field:"displayNam",value:"*王*"},{logic:"or",field:"nickname",value:"*王*"}]
           Boolean multiple; //是否查找多个联系人，默认值为true
   
   ```

2. `Contact`

方法：

```js
void plus.contacts.getAddressBook( type, succesCB, errorCB );
    Type://常量plus.contacts.ADDRESSBOOK_PHONE， plus.contacts.ADDRESSBOOK_SIM
    void onSuccess( addressbook ){ // Code AddressBook here }
```

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

## 9 [手机相册管理]

Gallery模块管理系统相册，支持从相册中选择图片或视频文件、保存图片或视频文件到相册等功能。通过plus.gallery获取相册管理对象。

### 应用场景

1. 朋友圈发照片
2. QQ空间发视频
3. 添加图片附件
4. 添加视频附件

### 接口调用

[相关文档](http://www.html5plus.org/doc/zh_cn/gallery.html)

