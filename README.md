# bigbosscyb.github.io
多版本dll共存
bigbosscyb
WPF技术
2021-12-22 20:50
一个项目引用不同版本的dll
问题描述
一个项目引用不同版本的同一dll，会引发以下报错：
未能加载文件或程序集“xxx, Version=x.x.x.x, Culture=neutral, PublicKeyToken=xxxxxxxxxxxx”或它的某一个依赖项。系统找不到指定的文件
这里来解决项目中同一dll的多版本问题。
解决方式
通过配置web.config配置文件（app.config或web.config）增加配置节点
不同场景有不同的解决方式，下面说明
场景一   以高版本兼容
1
2
3
4
5
6
7
8
<runtime>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <dependentAssembly>
      <assemblyIdentity name="Newtonsoft.Json" publicKeyToken="30AD4FE6B2A6AEED" culture="neutral"/>
      <bindingRedirect oldVersion="0.0.0.0-6.0.0.0" newVersion="6.0.0.0"/>
    </dependentAssembly>
  </assemblyBinding>
</runtime>
场景二   同一dll两种版本共存
例如：项目自己引用log4net.dll 版本1.2.13.0 。添加第三方某个dll，第三方依赖log4net.dll版本1.2.9.0，项目中需要两种版本共存。
这里还分两种情况，dll的publicKeyToken相同还是不同 （publicKeyToken查询见说明1）
publicKeyToken相同，配置方法：
1
2
3
4
5
6
7
8
9
<runtime>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <dependentAssembly>
      <assemblyIdentity name="log4net" publicKeyToken="669e0ddf0bb1aa2a" />
      <codeBase version="1.2.13.0" href="bin\log4netdll\1_2_13\log4net.dll" />
      <codeBase version="1.2.9.0" href="bin\log4netdll\1_2_9\log4net.dll" />
    </dependentAssembly>
  </assemblyBinding>
</runtime>
publicKeyToken不同，配置方法：
1
2
3
4
5
6
7
8
9
10
11
12
<runtime>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <dependentAssembly>
      <assemblyIdentity name="log4net" publicKeyToken="669e0ddf0bb1aa2a" />
      <codeBase version="1.2.13.0" href="bin\log4netdll\1_2_13\log4net.dll" />
    </dependentAssembly>
    <dependentAssembly>
      <assemblyIdentity name="log4net" publicKeyToken="b32731d11ce58905" />
      <codeBase version="1.2.9.0" href="bin\log4netdll\1_2_9\log4net.dll" />
    </dependentAssembly>
  </assemblyBinding>
</runtime>
说明
1.publicKeyToken获取方式：使用vs的Tools Command Prompt命令行工具，输入:SN -T "path",例如：
1
2
3
4
5
6
C:\Program Files (x86)\Microsoft Visual Studio 11.0>SN -T "D:\project\liberary\External\log4net.dll"
 
Microsoft(R) .NET Framework 强名称实用工具 版本 4.0.30319.17929
版权所有(C) Microsoft Corporation。保留所有权利。
 
公钥标记为 b32731d11ce58905
参考：
未能加载程序集