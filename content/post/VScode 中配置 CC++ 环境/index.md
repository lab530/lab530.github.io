+++
slug = "VScode-C-C++-environment"
title = 'VScode 中配置 C/C++ 环境'
date = 2024-09-09T23:49:57+08:00
weight=3

categories = [
    "环境配置"
]


+++

转载自 @零流 @火星动力猿 on [bilibili](https://www.bilibili.com/video/BV1Cu411y7vT?share_source=copy_web)  
由 lazarus 在原文基础上进行修改

- [1. 下载编辑器VScode](#1-下载编辑器vscode)
- [2. 下载编译器MinGW并解压](#2-下载编译器mingw并解压)
- [3. 将MinGW添加至环境变量](#3-将mingw添加至环境变量)
- [4. 配置VScode插件](#4-配置vscode插件)
- [5. 运行代码](#5-运行代码)
- [6. 提示](#6-提示)
- [7. 例行格式条款](#7-例行格式条款)

## 1. 下载编辑器VScode
- 官网：[VSCode 官网](https://code.visualstudio.com/)（点链接时按下Ctrl，不会覆盖当前页面哦^-^）
![下载VSCode](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingvscode%E4%B8%8B%E8%BD%BD.png)  

- 安装VScode（建议附加任务全部勾选）
![VSCode安装](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingvscode%E5%AE%89%E8%A3%85.gif)  

## 2. 下载编译器MinGW并解压
- 官网页面：[MingW 官网](https://www.mingw-w64.org/)

- 下载页面：[MingW 下载地址](https://sourceforge.net/projects/mingw-w64/files/)

    > 你可以进入官网自行寻找  
      你也可以直接点击为你找好的下载页面

- 下载页面中选择 `x86_64-win32-seh` 下载
![mingw下载](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingmingw%E4%B8%8B%E8%BD%BD.png)
    > 如果你因为网络环境限制无法下载  
    不限速下载，请笑纳^-^：[mingW 网盘下载](https://wwn.lanzouh.com/iLOip031ku6b) 密码:1234


- 在C盘中解压文件  
![解压 mingW](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting%E8%A7%A3%E5%8E%8Bmingw.gif)
    > 理论上你可以在任何地方解压，但注意路径不能包含中文，至于特殊字符请自行测试  
    **请你务必记住 mingw 的路径**！

## 3. 将MinGW添加至环境变量
- 进入mingw64下的bin文件夹，复制当前路径，Win + i唤起系统设置，输入高级系统设置并进入，点击环境变量，选择path，编辑，新建，粘贴路径，按下三个确定
![将 mingW 添加至环境变量](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting%E9%85%8D%E7%BD%AE%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F.gif)

- 可以按 win + r 呼出运行窗口，在其中输入 cmd 打开终端，在终端输入 gcc -v 验证环境变量是否配置好。出现如下内容则配置正确
![gcc](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettinggcc.png)

## 4. 配置VScode插件
- 打开 VScode 安装插件 Chinese, C/C++ 和 **CodeRunner** ，等待安装完毕后重启VScode
![安装 VSCode 插件](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting%E5%AE%89%E8%A3%85%E6%8F%92%E4%BB%B6.gif)  
CodeRunner 选图中这个  
![CodeRunner](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingcoderunner.png)

- 创建一个用于存放代码的文件夹，建议目录为 C:\\MyCode。用 VSCode 打开 MyCode 文件夹。

- 使用 VSCode 在 MyCode 文件夹下新建一个 .vscode 文件夹，并在其中创建以下四个 json 文件，并在 VSCode 或记事本中进行修改
    - launch.json 文件，**须将注释处表明的路径和参数改为你自己电脑上的**
        ```json
            {
            // 使用 IntelliSense 了解相关属性。 
            // 悬停以查看现有属性的描述。
            // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
            "version": "0.2.0",
            "configurations": [
                {
                    "name": "gcc.exe - 生成和调试活动文件",
                    "type": "cppdbg",
                    "request": "launch",
                    "program": "${fileDirname}\\bin\\$  {fileBasenameNoExtension}.exe",
                    "args": [],
                    "stopAtEntry": false,
                    "cwd": "${fileDirname}",
                    "environment": [],
                    "externalConsole": false,
                    "MIMode": "gdb",
                
                    // 此处更改为你自己的 mingw 下 bin 目录，保留 gdb.exe
                    "miDebuggerPath": "\\mingw64\\bin\\gdb.exe",

                    "setupCommands": [
                        {
                            "description": "为 gdb 启用整齐打印",
                            "text": "-enable-pretty-printing",
                            "ignoreFailures": true
                        },
                        {
                            "description": "将反汇编风格设置为  Intel",
                            "text": "-gdb-set disassembly-flavor    intel",
                            "ignoreFailures": true
                        }
                    ],
                    "preLaunchTask": "C/C++: gcc.exe 生成活动文件"
                }
            ]
        }
        ```
    - C/C++ 头文件路径 c_cpp_properties.json **须将注释处表明的路径和参数改为你自己电脑上的**
        ```json
            {
                "configurations": [
                    {
                        "name": "Win32",
                        "includePath": [
                            // 此处更改为你自己的 mingw 下 include 目录
                            "\\mingw64\\x86_64-w64-mingw32\\include"
                        ],
                        "defines": [
                            "_DEBUG",
                            "UNICODE",
                            "_UNICODE"
                        ],
                        "intelliSenseMode": "gcc-x64"
                    }
                ],
                "version": 4
            }
        ```

    - tasks.json
        ```json
        {
            "tasks": [
                {
                    "type": "cppbuild",
                    "label": "C/C++: gcc.exe 生成活动文件",
                    // 此处更改为你自己的 mingw 下 bin 目录，保留 gcc.exe
                    "command": "\\mingw64\\bin\\gcc.exe",
                    "args": [
                        "-fdiagnostics-color=always",
                        "-g",
                        "${file}",
                        "-o",
                        "${fileDirname}\\${fileBasenameNoExtension}.exe"
                    ],
                    "options": {
                        "cwd": "${fileDirname}"
                    },
                    "problemMatcher": [
                        "$gcc"
                    ],
                    "group": {
                        "kind": "build",
                        "isDefault": true
                    },
                    "detail": "调试器生成的任务。"
                }
            ],
            "version": "2.0.0"
        }
        ```
    完成这一步时你的 /MyCode/.vscode 文件夹下应该有上述三个 json 文件且内容符合你的 mingw 路径，**代码无法运行大概率和此处配置文件以及 mingw 环境变量配置有关！**  
![.vscode](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingvscode.png)

- 将 `CodeRunner` 设置成在终端中输出  
    右键拓展列表中的 `CodeRunner`，选择拓展设置。在打开的窗口中下翻，找到 `Run in Terminal` 并勾选。
    ![CodeRunnerSetting](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingCodeRunnerTerminal.png)


## 5. 运行代码
- 在 MyCode 下新建一个文件，英文命名且扩展名为 .c 例如 test.c

- 编写相关代码

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    int main()
    {
        printf("Hello World!\n");
        printf("你好世界！\n");
        system("pause");    // 防止运行后自动退出，需头文件stdlib.h
        return 0;
    }
    ```
点击软件左上角的运行按钮，或者按下快捷键 Ctrl + alt + n，即可在输出窗口看到输出结果


## 6. 提示
- 若源代码文件夹含有中文路径，将会无法编译程序。
- 若你的Windows用户名使用了中文，可能无法运行。
- 若无法运行代码，请检查第三第四步。

## 7. 例行格式条款
- 本文以自身分享为主，文中的提到的包括但不限于电脑操作、软件安装、点击链接，作者不保证有效性和可能发生的不利后果。
- 如需转载请在开头注明作者和出处
- 本文由 lazarus 在原基础上进行修改
