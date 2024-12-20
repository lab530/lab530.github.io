+++
slug = "Dev_C++6.3 output Chinese garbled code solution"
title = '关于 Dev_C++ 6.3 版本中输出中文乱码问题的解决方案'
date = 2024-09-09T23:49:57+08:00
weight=3

categories = [
    "环境配置"
]


+++

# 关于 Dev_C++ 6.3 版本中输出中文乱码问题的解决方案

![img](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting2022-10-24-1.png))

对于刚入门的新生来说 Dev_C++ 6.3 编译器版本中存在一个令人头疼的问题，就是输出中文乱码的问题。

如何解决这个问题呢？

请跟着进行如下操作。

+ 第一步，点击工具栏的 `工具` 选项
+ 第二步，点击 `编译选项` 选项
+ 第三步，在第一个输入框中加入命令 `-fexec-charset=gbk` 
+ 第四步，勾选 `编译时加入以下命令:`
+ 第五步，重新编译并运行即可

操作图片如下:

![img](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting2022-10-24-2.png)

![img](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting2022-10-24-3.png)

![img](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting2022-10-24-4.png)

![img](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting2022-10-24-5.png)