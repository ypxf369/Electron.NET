# Electron.NET
使用Electron的C#版本开发Net Core桌面应用程序

## 1.介绍  
Electron是由Github上的一支团队和一群活跃贡献者维护。用HTML，CSS和JavaScript来构建跨平台桌面应用程序的一个开源库。 Electron通过将Chromium（谷歌浏览器引擎）和Node.Js合并到同一个运行时环境中，并将其打包为Mac，Windows和Linux系统下的应用来实现这一目的。官方地址：https://electronjs.org。
## 2.搭建流程  
a、Electron.NET是基于Electron和Node.js的，因此在你开撸之前需要做点准备工作。  
b、安装Node.js 去https://nodejs.org/en/下载  
c、打开node.js命令行注册一个配置文件，敲命令：npm config set registry xxx （xxx随便写）  
d、上面那个命令运行完会生成一个.npmrc文件。找到它(c:\user\你的用户名\.npmrc)，找不到就搜索吧。  
f、继续敲命令 npm install -g electron  
g、继续敲命令npm install electron-packager --global  
h、分别敲node -v和electron -v，看看装没装上  
i、如下所示：  
Microsoft Windows [版本 10.0.14393]
(c) 2016 Microsoft Corporation。保留所有权利。

C:\Users\yp252>node -v

v5.4.1

C:\Users\yp252>electron -v

v1.8.2

C:\Users\yp252>

## 4.开发
a、创建net core mvc项目  
b、安装ElectronNET软件包 Install-Package ElectronNET.API  
c、在Program.cs中Build()方法之前加上.UseElectron(args)
d、在Startup.cs中Configure方法中UserMvc下面加入下面的代码：
```
var browserWindow = await ElectronNET.API.Electron.WindowManager.CreateWindowAsync(new BrowserWindowOptions  
{ 
                Width = 1152,
                Height = 864,
                Show = true,
                Center = true,
                Transparent = true
            }, $"http://localhost:{ BridgeSettings.WebPort }/1.html");//App打开的时候 显示的页面，BridgeSettings.WebPort获取你这个mvc绑定在本地的端口  
            browserWindow.OnReadyToShow += () => browserWindow.Show();
            browserWindow.SetTitle("Electron.NET API Demos");//这是App的标题 
 }
 ```
 e、开始开发你的网站，测试完了之后再项目根目录中找的.csproj文件，更改如下配置节点：  
 
 ```
 <ItemGroup>
      <DotNetCliToolReference Include="ElectronNET.CLI" Version="*" />
 </ItemGroup>
  ```
f、在你的 程序包管理控制台 中找到你的项目路径，cd进去，dir能看到 program.cs就行了。
g、然后运行 dotnet electronize init,它会在项目根目录下商城一个electron.manifes.json文件
h、继续 net electronize start,可能会报错，没关系，只要控制台不强制关闭就行。
i、注意：有时候会报”***不是内部或外部命令，也不是可运行的程序”的错误，一般就是npm等等，遇到这样的错误直接在cmd中cd到错误目录直接在cmd中敲之地你那个命令就行。
j、如果没有意外的话，程序也就跑起来了。

            
