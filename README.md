**注意：此仓库不在更新，最新版本的地址**
新版地址：https://github.com/mi-unity-qggame/unitytoqgame

**Unity转小米快游戏（小游戏）工具使用说明文档**

**视频教程**

地址：https://kpan.mioffice.cn/webfolder/ext/8EhBM8oTtYY%40?n=0.5625941541150863 

密码：0a9T

**更新日志**
**1.3.0 版本**
<ol>
    <li>支持分包打包模式，分包打包包体会变大，是因为内部有一个整包，两个分包的主包和副包。如果整包小于30M,即使打出来的包大于30M也可以正常提交</li>
    <li>其他优化</li>
</ol>

**1.5.0 版本**
<ol>
    <li>支持unity2022版本</li>
    <li>其他优化</li>
</ol>

**1.5.1 版本**
<ol>
    <li>修复2019 使用Getlaunch接口打包失败问题</li>
</ol>

**1.5.2 版本**
<ol>
    <li>支持webgl2.0</li>
</ol>

**1.5.4 版本**
<ol>
    <li>bugfix</li>
</ol>


**问题：**<br>
**1. 手机打开出现加载失败，请重试的页面**
<ol><li>检查包名是否在小米开发者平台注册过</li><li>如果确认包名没问题，可以用测试包名来测试 com.demo.ch.mini</li></ol>

**2. 手机打开游戏一直处于白屏状态，是什么原因？**
<ol><li>第一种解决办法：可以把wasm文件放在服务器上</li><li>第二种解决办法：检查手机是否是低端机，如果是低端机可以换成性能好的高端机，启动起来游戏，然后做wasm分包处理。</li><li>第三种解决办法：检查wasm是否过大，如果过大请优化，建议 **30M** 以下。</li>
</ol>

**一、转换工具链接**

http://tennews.cn/MiQGameConverter.unitypackage

支持的unity版本**2021**、**2020**，**2019**。

结构：

![](images/Unity转快游戏使用说明文档.001.png)

**二、使用步骤**

1. **点击菜单栏 小米快游戏/打包设置**

![](images/Unity转快游戏使用说明文档.002.png)

2. **弹出操作窗口**

![](images/Unity转快游戏使用说明文档.003.png)

参数说明：

1. 游戏名称：小米快游戏名称。
2. 包名：在小米快游戏中心申请的包名，一定要填写正确的包名，否则会导致加载失败。
3. 版本号：版本号。
4. 版本code：版本code。
5. 加载页面Url：游戏加载过程当中页面，用来
6. 输出目录：打包输出目录，此目录每次打包都会清空，请注意选择合适的目录。
7. 游戏方向：横屏或者竖屏。
8. 包类型：debug或者release包。release包需要release签名文件，请设定release签名文件所在的目录。
9. 包体超限：由于快游戏包体大小限定，unity游戏资源较多的情况下，可以使用此项，把打出来资源放在服务器上，使用远程资源加载。
10. 打包：执行打包操作。

3. **打包完成会打开打包目录。如下所示：**

![](images/Unity转快游戏使用说明文档.004.png)

MQGame即为**小米快游戏工程**。

转换完成会在dist目录下生成快游包：

![](images/Unity转快游戏使用说明文档.005.png)

在此目录下，也可以手动执行npm命令生成快游戏包。

1. npm install命令安装快游戏依赖包；
2. npm run build 或者npm run release生成对应的debug包和release包。
3. npm run server，可以生成启动调试服务器，使用快游戏调试器（下载地址：https://www.quickapp.cn/docCenter/post/69），扫描二维安装即可启动游戏。注意：需要把调试器环境切换为：com.miui.hybrid环境！！！

![](images/Unity转快游戏使用说明文档.006.png)

**三、优化建议**

1. 包体过大，或者遇见out of memory，可以把这两两项改为如下选项，优化包体和内存。

![](images/Unity转快游戏使用说明文档.007.png)

**注意！！！Unity基础功能使用说明**

unity转快游戏，有些unity功能是不能直接在快游戏里面使用的，需要在unity层使用的时候做一些适配工作。

1. **Websocket（可选）**

示例：WebSocket服务器搭建完成后，在客户端场景物体上挂载示例脚本Connection，并修改Connection脚本中的IP地址即可。

![](images/Unity转快游戏使用说明文档.008.png)

2. **InputField（必须）**

在挂载输入框组件的物体上，需手动挂载一个脚本。 如果使用的是 InputField (Legacy) 组件则手动挂载 WebglInput 脚本，使用的是 InputField (TMP)组件则手动挂载 WebglInputTMP 脚本。

![](images/Unity转快游戏使用说明文档.009.png)

![](images/Unity转快游戏使用说明文档.010.png)

**四、快游戏功能接入**

转换工具提供的快游戏功能有：登录、支付、广告、文件读写、创建游戏图标，key-value本地存储等功能。

**1、 初始化**

初始化需要在调用sdk功能之前调用，确保初始化完成，才能使用SDK功能。

例子：

|C#<br>//初始化<br>MiBridge.Instance.Init();|
| :- |
**2、 登录和获取用户信息**

|C#<br>//快游戏小米账号登录<br>MiBridge.Instance.Login((accountId, session) => {<br>`    `MiBridge.Instance.QGLog("login account id={0}, session={1}", accountId, session);<br>`    `MiBridge.Instance.GetUserInfo((nickName, avatarUrl, gender) =><br>`    `{<br>`        `MiBridge.Instance.QGLog("get user info nickName={0}, avatar={1}, gender={2}", nickName, avatarUrl, gender);<br>`    `}, (code, msg) =><br>`    `{<br>`        `MiBridge.Instance.QGLog("get user info error code={0}, msg={1}", code, msg);<br>`    `});<br>}, (code, msg) => {<br>`    `MiBridge.Instance.QGLog("login error code={0}, msg={1}", code, msg);<br>});|
| :- |
**3、支付**

支付接入需要服务器接入，具体服务器接入方式请查看小米开发者文档：https://dev.mi.com/distribute/doc/details?pId=1109。

|C#<br>//订单信息<br>OrderInfo orderInfo = new OrderInfo<br>{<br>`    `appId = "1",               // 游戏唯一ID<br>`    `appAccountId = 12,         // 与登录接口返回的appAccountId一致<br>`    `session = "1",             // 与登录接口返回的session一致<br>`    `cpOrderId = "1",           // 游戏订单号<br>`    `cpUserInfo = "",           // cp透传信息 (非空)<br>`    `displayName = "1",         // 支付的时候显示的商品名称<br>`    `feeValue = 100,            // 价格 单位分<br>`    `sign = "1",                // 签名 用于校验 具体生成方式，请查看：https://dev.mi.com/distribute/doc/details?pId=1109<br>};<br><br>//支付接口<br>MiBridge.Instance.Pay(orderInfo, (success, code, msg) => {<br>`    `MiBridge.Instance.QGLog("pay result success={0}, code={1}, msg={2}", success, code, msg);<br>});|
| :- |
**4、广告**

**4.1、Banner广告**

|C#<br>/// 创建banner广告<br>` `MiBridge.Instance.CreateBannerAd("81e6cbe35e56b53eebbc547fd1bc5614", new AdEventListener { <br>`    `onAdError = (code, msg) => {<br>`        `MiBridge.Instance.QGLog("c# ad error");<br>`    `},<br>    <br>`    `onAdClose = (isEnd) => {<br>`        `MiBridge.Instance.QGLog("c# ad close");<br>`    `},<br><br>`    `onAdLoad = (info) => {<br>`        `MiBridge.Instance.QGLog("c# ad load");<br>`    `},<br>});<br>/// 隐藏广告<br>MiBridge.Instance.HideAd("81e6cbe35e56b53eebbc547fd1bc5614");<br>/// 销毁广告，销毁后，如需重新显示，请先调用创建广告<br>MiBridge.Instance.DestroyAd("81e6cbe35e56b53eebbc547fd1bc5614");|
| :- |
**4.2、插屏广告**

|C#<br>/// 创建插屏广告<br><br>MiBridge.Instance.CreateInterstitialAd("f54f3dfc0ba63cf3dbf582816ee069d7", new AdEventListener<br>{<br>`    `onAdError = (code, msg) => {<br>`        `MiBridge.Instance.QGLog("c# insert ad error");<br>`    `},<br><br>`    `onAdClose = (end) => {<br>`        `MiBridge.Instance.QGLog("c# insert ad close");<br>`    `},<br><br>`    `onAdLoad = (info) => {<br>`        `MiBridge.Instance.QGLog("c# insert ad load");<br>`    `},<br>});<br><br>/// 展示插屏广告测试<br>MiBridge.Instance.ShowAd("f54f3dfc0ba63cf3dbf582816ee069d7");<br><br>/// 销毁插屏广告测试<br>MiBridge.Instance.DestroyAd("f54f3dfc0ba63cf3dbf582816ee069d7");|
| :- |
**4.3、Native广告**

|C#<br>/// 创建原生广告<br>MiBridge.Instance.CreateNativeAd("da11b7e8c582ee7d1acf16a627ea6b34", new AdEventListener<br>{<br>`    `onAdError = (code, msg) => {<br>`        `MiBridge.Instance.QGLog("c# native ad error");<br>`    `},<br><br>`    `onAdClose = (end) => {<br>`        `MiBridge.Instance.QGLog("c# native ad close");<br>`    `},<br><br>`    `onAdLoad = (info) => {<br>`        `MiBridge.Instance.QGLog("c# native ad load");<br>`    `},<br>});<br><br>/// 加载广告<br>MiBridge.Instance.LoadAd("da11b7e8c582ee7d1acf16a627ea6b34");<br><br>/// 展示广告<br>MiBridge.Instance.ShowAd("da11b7e8c582ee7d1acf16a627ea6b34");<br><br>/// 销毁广告，销毁后，如需重新显示，请先调用创建广告<br>MiBridge.Instance.DestroyAd("da11b7e8c582ee7d1acf16a627ea6b34");|
| :- |
**4.4、激励视频广告**

|C#<br>/// 创建激励视频广告<br>MiBridge.Instance.CreateRewardedVideoAd("77295ab0558fa54fc5cc9ed6a28b6da7", new AdEventListener<br>{<br>`    `onAdError = (code, msg) => {<br>`        `MiBridge.Instance.QGLog("c# reward ad error");<br>`    `},<br><br>`    `onAdClose = (end) => {<br>`        `string info = "success";<br>`        `if (!end) {<br>`            `// end == true 说明激励视频播放完毕，是正常结束<br>`            `info = "failure";<br>`        `}<br>`        `MiBridge.Instance.QGLog($"c# reward ad close end={info}");<br>`    `},<br><br>`    `onAdLoad = (info) => {<br>`        `MiBridge.Instance.QGLog("c# reward ad load");<br>`    `},<br>});<br><br>/// 加载广告<br>MiBridge.Instance.LoadAd("77295ab0558fa54fc5cc9ed6a28b6da7");<br><br>/// 展示广告<br>MiBridge.Instance.ShowAd("77295ab0558fa54fc5cc9ed6a28b6da7");|
| :- |
**4.5、互推盒子广告**

|C#<br>/// <summary><br>/// 展示互动盒子广告<br>/// 互动盒子广告介绍：https://dev.mi.com/distribute/doc/details?pId=1442<br>/// </summary><br>/// <param name="adId">广告id</param><br>/// <param name="type"><br>/// 广告类型: <br>/// 1. type=100，    互推盒子-九宫格 <br>/// 2. type=120，    互推盒子-横幅 <br>/// 3. type=130/140，互推盒子-抽屉，    白色背景为130，黑色背景为140<br>/// 4. type=150，    互推盒子-悬浮球<br>/// </param><br>/// <param name="listener">监听器</param><br>/// <returns></returns><br>MiBridge.Instance.ShowRecommendAd("da11b7e8c582ee7d1acf16a627ea6b34", 100, (success, msg) => <br>{<br><br>});<br><br>/// <summary><br>/// 关闭互动盒子广告<br>/// 互动盒子广告介绍：https://dev.mi.com/distribute/doc/details?pId=1442<br>/// </summary><br>/// <param name="adId">广告id</param><br>/// <param name="type"><br>/// 广告类型: <br>/// 1. type=100，    互推盒子-九宫格 <br>/// 2. type=120，    互推盒子-横幅 <br>/// 3. type=130/140，互推盒子-抽屉，    白色背景为130，黑色背景为140<br>/// 4. type=150，    互推盒子-悬浮球<br>/// </param><br>/// <param name="listener">监听器</param><br>MiBridge.Instance.CloseRecommendAd("da11b7e8c582ee7d1acf16a627ea6b34", 100, (success, msg) =><br>{<br><br>});|
| :- |
**5、文件操作**

**5.1、读文件**

|C#<br>MiBridge.Instance.ReadFile("log.txt", (data, len) =><br>{<br>`    `string test = System.Text.Encoding.ASCII.GetString(data);<br>`    `MiBridge.Instance.QGLog("MiBridge.Instance.ReadFile success {0}, {1}", len, test);<br>}, (msg) =><br>{<br>`    `MiBridge.Instance.QGLog("read file failure {0}", msg);<br>});|
| :- |
**5.2、写文件**

|C#<br>string myString = "Hello world!!!";<br>byte[] data = Encoding.UTF8.GetBytes(myString);<br>MiBridge.Instance.WriteFile("log.txt", data, false, (success, msg) =><br>{<br>`    `MiBridge.Instance.QGLog("write file {0}, {1}", success, msg);<br>});|
| :- |
**5.3、删除文件**

|C#<br>MiBridge.Instance.DeleteFile("log.txt", (success) => { <br>});|
| :- |
**6、游戏图标**

|JSON<br>MiBridge.Instance.HasShortcut( has => {<br>`        `if (has)<br>`        `{<br>`            `MiBridge.Instance.QGLog("has short cut");<br>`        `}<br>`        `else <br>`        `{<br>`            `MiBridge.Instance.QGLog("has not short cut");<br>`            `MiBridge.Instance.CreateShortcut("便于打开游戏", (success, code, msg) => {<br>`                `MiBridge.Instance.QGLog("create short cut {0}, {1}, {2}", success, code, msg);<br>`        `});<br>`    `}<br>});|
| :- |
**7、KV存储**

支持四种类型存储：int，float，double和string类型。

存和读操作：

|JSON<br>MiBridge.Instance.SetKVInt("int", 1);<br>var kvInt = MiBridge.Instance.GetKVInt("int");<br>MiBridge.Instance.QGLog("get int kv={0}", kvInt);<br><br>MiBridge.Instance.SetKVFloat("float", 2.0522222f);<br>var kvFloat = MiBridge.Instance.GetKVFloat("float");<br>MiBridge.Instance.QGLog("get float kv={0}", kvFloat);<br><br>MiBridge.Instance.SetKVDouble("dobule", 3.2656453453d);<br>var kvDouble = MiBridge.Instance.GetKVDouble("dobule");<br>MiBridge.Instance.QGLog("get dobule={0}", kvDouble);<br><br>MiBridge.Instance.SetKVString("string", " fsdfsdf ");<br>var kvString = MiBridge.Instance.GetKVString("string");<br>MiBridge.Instance.QGLog("get string={0}", kvString);|
| :- |
删除操作：

|C#<br>MiBridge.Instance.DeleteKV("int");|
| :- |
**8、日志打印到快游戏平台**

|JSON<br>MiBridge.Instance.QGLog("hello world！");|
| :- |
**五、调试**

快游戏只能**真机**调试

1. 小米手机开启USB调试模式
2. 浏览器调试
1. **edge**浏览器调试
1. 输入 edge://inspect/#devices
2. **chrome**浏览器调试
1. 输入 chrome://inspect/#devices
3. 点击 **inspect**进入调试页面

![](images/Unity转快游戏使用说明文档.012.png)

**六、生成证书**

1. [**下载快应用IDE**](https://www.quickapp.cn/)

![](images/Unity转快游戏使用说明文档.013.png)

2. **打开一个工程（任意一个工程）**

![](images/Unity转快游戏使用说明文档.014.jpeg)
