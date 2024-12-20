+++
slug = "PicGo configuration tutorial and blog image upload specifications"
title = 'PicGo 配置教程及博客图片上传规范'
date = 2024-09-09T23:49:57+08:00
weight=5

categories = [
    "博客开发"
]

+++

## Before reading
为避免让项目仓库变得日益臃肿同时也为了优化开发和访问网站的体验，~~加快图片加载速度~~，现规定将图片嵌入方式统一改为图床链接。目前受国内~~欣欣向荣的~~网络环境影响，暂决使用指定 GitHub 仓库作为博客专用图床。

## PicGO 的安装与图床配置

1. 通过访问 [PicGo releases](https://github.com/Molunerfinn/PicGoreleases) 来下载软件。你也可以访问 [PicGo 中文文档](https://picgo.github.io/PicGo-Doc/zh/guide/) 以了解 PicGo 的操作以及插件等内容。
2. 生成 GitHub 的个人 token 用以访问仓库。
    - 打开个人设置，点击 **Developer Settings**。
    ![Developer Settings](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingDevelopS.png)  
    - 点击 **Personal access tokens** 选择 **Tokens (Classic)** 然后点击 **Generate new token**, 在下拉菜单中选择 **(Classic)** 标记的选项。此时会要求你验证账号。
    ![ClassicToken](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingClassicToken.png)  
    - 在页面中填写 note, 选择 token 的有效时间（不建议设置为永久有效），并勾选仓库下相关权限。然后在页面的最下方点击生成 token。
    ![PicGoSettingTokenSettings](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingTokenSettings.png)
    - 接下来就能看到生成的 token 了，这里记住一定要复制下 token，一旦这个页面关闭后就无法再获取 token 的值了。
    ![CopyToken](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingCopyToken.png)

3. PicGo 设置
    - 在设置里面**打开上传重命名**并关闭**使用内置剪贴板上传**，显示的图床只用勾选自己需要的，这里只勾选了 GitHub。
    ![PicGoSet](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingPicGoSet.png)
    - 打开图床设置，选择 GitHub，仓库名为 `UserName/RepoName` 的格式，本博客为 `lab530/assets_images_storage`，分支填 **main**，将刚才生成的 token 填入，**token 过期后需要重新生成 token 并更新 PicGo 这里的设置**。存储路径遵循 `Post/PostName` 的格式，每次创建与修改帖子时要保证图片的存储路径符合规范。自定义域名暂时不填（寻找可行的加速方案中）。
    ![GitHub](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingPicGo.png)
4. 上传图片
    - 点击上传区，有多种图片上传方式，可以将现有的文件拖入框中或浏览并选择图片来进行上传。也支持将剪贴板内的图片直接上传，链接格式选择 markdown。
    ![UploadArea](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingUpLoadArea.png)
    - 以任一方式上传后，会弹出重命名框，确认后等待上传完成时会跳出通知，并且自动将 markdown 格式的 URL 复制到剪贴板，如下例子所示。将 URL 嵌入文章即可完成图片插入。
        ``` markdown
        ![Demo](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting20221023184655.png)
        ```
        ![Demo](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSetting20221023184655.png)

    - 之前上传的图片可以在 **相册** 内找到，可以编辑与复制链接，也可进行批量删除操作。
    ![History](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingHistory.png)


最后贴一张 Lucy 的照片，侵删。
![Lucy](https://raw.githubusercontent.com/lab530/assets_images_storage/main/Post/PicGoSettingLucy)