---
layout:     post
title:      "电脑配置"
subtitle:   " \"整理的 Win10 配置\""
date:       2018-10-6 16:00:00
author:     "丢手圈"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 生活
---

# 浏览器

## 1. Chrome 浏览器
### 1.1 更改安装位置
chrome默认安装路径为 C:\Program Files (x86)\Google\Chrome，要确定 C:\Program Files (x86)\Google\ 下面没有chrome这个文件夹，因为这个要由mklink来创建。而文件夹 D:\Chrome 要先建立好。

win10 符号链接制作命令方法，cmd命令行(管理员)中输入
`mklink /d "C:\Program Files (x86)\Google\Chrome" "D:\Chrome"` 然后回车。

### 1.2 更改缓存位置
只需要三步:

1. 关闭正在运行的Chrome,删除C:\Users\用户\AppData\Local\Google\Chrome目录下的User Data文件夹
2. 在非系统盘符新建个文件夹,比如D:\Chrome
3. 打开cmd输入，`mklink /d "C:\Users\g\AppData\Local\Google\Chrome\User Data" "D:\browser userdate\chromeuser"`，回车执行

不管怎么升级,用户数据,缓存什么的全部保存在了 D:\Chrome 文件夹下

原理：mklink给D:\Chrome目录 在  C:\Users\用户\AppData\Local\Google\Chrome\User Data目录下创建了映射,当chrome在操作user data文件夹的时候其实是在操作D盘的Chrome文件夹。

## 2. 百分浏览器缓存位置更改
`mklink /d "C:\Users\g\AppData\Local\CentBrowser\User Data" "D:\browser userdate\centuser"`

恢复直接删除 C 盘，user data> d的目录，把 D 盘文件夹 user data copy 复制到 C 盘

## 3. 火狐浏览器更改缓存位置
1. 打开firefox，地址栏输入 about:config
2. 右键新建一个字符串： browser.cache.disk.parent_directory
3. 然后输入希望的位置。如 D:\browser userdate\firefoxcache
4. 保存并推出重启浏览器即可。

注意：browser.cache.disk.enable，这个必须要设定为 true。重启后，键入：about:cache即可观察修改情况。

# Win10 系统配置
## 资源管理器导航栏
### 1. Onedrive 图标
注册表定位到：`HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6} `，在右边双击System.IsPinnedToNameSpaceTree ，将其数值数据改为“0”。设置完成后重启文件夹（或重启一次计算机），然后打开文件夹，OneDirve 就删除了。

### 2. 网络图标
注册表定位到：`HKEY_CLASSES_ROOT\CLSID\{F02C1A0D-BE21-4350-88B0-7367FC96EF3C}\ShellFolder`，右键点击ShellFolder项，在弹出的菜单栏选择【权限】选项，进入权限管理界面，点击选中当前电脑用户名称，H/Administrators，然后在下方权限处勾上【完全控制】，设置完毕，在右方找到Attributes值，双击或右键点击选择【编辑】，将其数值数据更改为 b0940064，点击保存。

若要恢复显示，将上述数据数值改回“b0040064”。
完成上述修改后注销或者重启系统，导航面板里就不会再显示网络了。

## 系统右键菜单

### 1. 用3D画图编辑
删除方法：打开记事本，复制下面内容，以reg格式保存，双击运行即可。

    Windows Registry Editor Version 5.00
    [-HKEY_LOCAL_MACHINE\SOFTWARE\Classes\SystemFileAssociations\.jpg\Shell\3D Edit]
    [-HKEY_LOCAL_MACHINE\SOFTWARE\Classes\SystemFileAssociations\.jpeg\Shell\3D Edit]
    [-HKEY_LOCAL_MACHINE\SOFTWARE\Classes\SystemFileAssociations\.bmp\Shell\3D Edit]
    [-HKEY_LOCAL_MACHINE\SOFTWARE\Classes\SystemFileAssociations\.png\Shell\3D Edit]


### 2. 还原以前的版本
打开注册表后，点击“编辑”-“查找”，在查找目标中 输入： `{596AB062-B4D2-4215-9F74-E9109B0A8153}` ，取消勾选值和数据；将查找到的文件夹全部删除。（删一个后，再查找下一个，直到没有）之后你就会发现右键中 还原到以前的版本 选项消失了。（大概有7-8个比较多耐心删，别删错了）

### 3. 向右旋转向左旋转
删除图片右键菜单中的向右旋转、向左旋转，编辑。
删除方法：打开记事本，复制下面内容，以reg格式保存，双击运行即可。

    Windows Registry Editor Version 5.00
    [-HKEY_CLASSES_ROOT\SystemFileAssociations\.jpg\ShellEx\ContextMenuHandlers\ShellImagePreview]
    [-HKEY_CLASSES_ROOT\SystemFileAssociations\.bmp\ShellEx\ContextMenuHandlers\ShellImagePreview]
    [-HKEY_CLASSES_ROOT\SystemFileAssociations\.png\ShellEx\ContextMenuHandlers\ShellImagePreview]
    [-HKEY_CLASSES_ROOT\SystemFileAssociations\.gif\ShellEx\ContextMenuHandlers\ShellImagePreview]
    [-HKEY_CLASSES_ROOT\SystemFileAssociations\.tif\ShellEx\ContextMenuHandlers\ShellImagePreview]
    [-HKEY_CLASSES_ROOT\SystemFileAssociations\image\shell\edit]  


### 4. 照片查看器文件关联的方法如下：
方法：打开记事本，复制下面内容，以reg格式保存，双击运行即可。

    Windows Registry Editor Version 5.00
    
    ; Change Extension's File Type 
    
    [HKEY_CURRENT_USER\Software\Classes\.jpg] 
    
    @="PhotoViewer.FileAssoc.Tiff" 
    
    ; Change Extension's File Type 
    
    [HKEY_CURRENT_USER\Software\Classes\.jpeg] 
    
    @="PhotoViewer.FileAssoc.Tiff" 
    
    ; Change Extension's File Type 
    
    [HKEY_CURRENT_USER\Software\Classes\.gif] 
    
    @="PhotoViewer.FileAssoc.Tiff" 
    
    ; Change Extension's File Type 
    
    [HKEY_CURRENT_USER\Software\Classes\.png] 
    
    @="PhotoViewer.FileAssoc.Tiff" 
    
    ; Change Extension's File Type 
    
    [HKEY_CURRENT_USER\Software\Classes\.bmp] 
    
    @="PhotoViewer.FileAssoc.Tiff" 
    
    ; Change Extension's File Type 
    
    [HKEY_CURRENT_USER\Software\Classes\.tiff] 
    
    @="PhotoViewer.FileAssoc.Tiff" 
    
    ; Change Extension's File Type 
    
    [HKEY_CURRENT_USER\Software\Classes\.ico] 
    
    @="PhotoViewer.FileAssoc.Tiff"


### 5. 设置为桌面背景
删除方法：打开记事本，复制下面内容，以reg格式保存，双击运行即可。
```
Windows Registry Editor Version 5.00
[-HKEY_CLASSES_ROOT\SystemFileAssociations\.jpg\Shell\setdesktopwallpaper]
[-HKEY_CLASSES_ROOT\SystemFileAssociations\.jpeg\Shell\setdesktopwallpaper]
[-HKEY_CLASSES_ROOT\SystemFileAssociations\.png\Shell\setdesktopwallpaper]
```

### 6. Windows Media Player
方法一：打开记事本，复制下面内容，以reg格式保存，双击运行即可。
```
Windows Registry Editor Version 5.00
[-HKEY_CLASSES_ROOT\SystemFileAssociations\audio\shell\Enqueue]
[-HKEY_CLASSES_ROOT\SystemFileAssociations\audio\shell\Play]
[-HKEY_CLASSES_ROOT\SystemFileAssociations\Directory.Audio\shell\Enqueue]
[-HKEY_CLASSES_ROOT\SystemFileAssociations\Directory.Audio\shell\Play]
[-HKEY_CLASSES_ROOT\SystemFileAssociations\Directory.Image\shell\Enqueue]
[-HKEY_CLASSES_ROOT\SystemFileAssociations\Directory.Image\shell\Play]
```
方法二：卸载 Windows Media Player

### 7. 播放到设备
注册表定位到：`HKEY_CLASSES_ROOT\CLSID\{7AD84985-87B4-4a16-BE58-8B72A5B390F7}` ，属性-高级，将该主键的所有者设置为 Administrators 组，同时将 Administrators 组设置为完全控制权限。然后再把下面的一个主键InProcServer32也照上述方法设置权限，就能删除或更改这个主键。

可以重命名该主键（等同于删除），比如将{7AD84985-87B4-4a16-BE58-8B72A5B390F7}更名为{7AD84985-87B4-4a16-BE58-8B72A5B390F7}1234567

### 8. 左侧 6 个文件夹
隐藏方法：打开记事本，复制下面内容，以reg格式保存，双击运行即可。
```
Windows Registry Editor Version 5.00
;图片
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{0ddd015d-b06c-45d5-8c4c-f59713854639}\PropertyBag]
"ThisPCPolicy"="Hide"

;视频
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{35286a68-3c57-41a1-bbb1-0eae73d76c95}\PropertyBag]
"ThisPCPolicy"="Hide"

;下载
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{7d83ee9b-2244-4e70-b1f5-5393042af1e4}\PropertyBag]
"ThisPCPolicy"="Hide"

;音乐
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{a0c69a99-21c8-4671-8703-7934162fcf1d}\PropertyBag]
"ThisPCPolicy"="Hide"

;桌面
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}\PropertyBag]
"ThisPCPolicy"="Hide"

;文档
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions\{f42ee2d3-909f-4907-8871-4c22fc0bf756}\PropertyBag]
"ThisPCPolicy"="Hide"
```

### 9. 3D对象
注册表定位到：`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{0DB7E03F-FC29-4DC6-9020-FF41B59E513A}` ，右击 `{0DB7E03F-FC29-4DC6-9020-FF41B59E513A}` 删除

## 其他软件右键菜单
### Adobe Acrobat 
- 文件右键菜单（文件右键）：`HKEY_CLASSES_ROOT\*\shellex\ContextMenuHandlers`  下，找到 Adobe.Acrobat.ContextMenu 一项，删除
- 合并"右键菜单（文件夹的右键）：`HKEY_CLASSES_ROOT\Folder\ShellEx\ContextMenuHandlers\Adobe.Acrobat.ContextMenu`，删除

### 显卡右键菜单
注册表定位到：`HKEY_CLASSES_ROOT\Directory\Background\shellex\ContextMenuHandlers`，在该选项下面的对象项的介绍：AMD/ATI显卡--“ACE”、intel显卡--“igfxcui”、NVIDIA显卡--“NvCplDesktopContext”
删除对应文件夹，但千万别动“new”项，该项是系统默认项，删除后会引起右键菜单消失的
