# 移植教程

## 前言

本教程适用对象是刚接触C++移植Python的开发人员。适用项目是Archicad cAPI扩展为pyAPI，在移植过程中涉及C++及python相关理论不做过多释义。编写此教程的目的是通过查阅本教程，使开发人员能快速掌握移植的基本操作。若需要提升移植技巧，请详细阅读[pybind11](https://pybind11.readthedocs.io/en/stable/)官方文档

本教程将以移植DGLib项目为例，带领初学者逐步将ACPyModuleTutorials基础项目迁移为DGLib项目。

## 下载模板

基础项目为ACPyModuleTutorials（内含子模块ACExport），后续的所有移植项目，如DGLib、GSRoot、ACTextEngine和Graphix等都是以该基础项目为模板。项目地址为https://github.com/graphisoft-python/ACPyModuleTutorials.git。

本教程以git命令方式为例，打开任意命令行工具（安装VisualStudio 2017或使用VisualStudio Code的内置命令行工具），键入命令 ```git clone --recursive https://github.com/graphisoft-python/ACPyModuleTutorials.git```，等待克隆成功结束即可，如下图所示：

<image src="./images/0.png"></image>

<image src="./images/1.png"></image>

## 修改模板

### 修改文件夹及文件名

打开基础项目文件夹，搜索所有以```ACPyModuleTutorials```命名的文件或文件夹，将```ACPyModuleTutorials```替换为```DGLib```（注：修改文件名时，勿将文件后缀名修改）。如下图所示：

<image src="./images/2.png"></image>

<image src="./images/3.png"></image>

### 修改文件内容

使用Notepad++或VisualStudio Code等编辑工具,依次打开下列文件： ```DGLib.sln```,```DGLib.cpp```,```DGLib.vcxproj```,```DGLib.vcxproj.filters```
并将以上文件内的```ACPyModuleTutorials```全部替换为```DGLib```。如下图所示：

<image src="./images/4.png"></image>

## 编译项目

使用VisualStuido 2017打开修改后的项目，编译模式须调整为**Release**模式。然后点击“生成-生成解决方案”。如无错误方式，且生成xxx.pyd文件，则证明项目修改成功。如下图所示：

<image src="./images/5.png"></image>

<image src="./images/8.png"></image>

<image src="./images/6.png"></image>

## 测试项目

在搭建测试环境之前，请务必安装ArhiCAD 22。以本教程为例，该软件安装于默认位置C:\Program Files。

### 搭建测试环境

要对项目编译生成的python库进行测试，须在ArchiCAD 22的安装目录中安装VirtualPyEnv插件。而安装该插件，只需到 [VirtualPyEnv](https://github.com/graphisoft-python/VirtualPyEnv) 下载zip文件，并解压至```C:\Program Files\GRAPHISOFT\ARCHICAD 22\Add-Ons``` 即可。如下图所示，是解压VirtualPyEnv后的位置及文件夹结构

<image src="./images/7.png"></image>

### 测试移植库

在```C:\Program Files\GRAPHISOFT\ARCHICAD 22\Add-Ons\VirtualPyEnv\APPS``` 文件夹下，新建任意文件夹（如wsTest），然后新建vapp.py文件。按下图所示写入测试代码，完成后保存。

<image src="./images/9.png"></image>

### 查看测试结果

打开ArchiCAD 22，等待iMonitor窗口弹出调试信息。如下图所示：

<image src="./images/10.png"></image>

至此，你已完成ACPyModuleTutorials向DGLib的迁移。接下来的工作便是根据pybind11，将c++库移植为python库。