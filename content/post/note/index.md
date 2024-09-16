+++
title = '博客须知！！！'
date = 2024-09-16T15:49:28+08:00
weight=1

draft = true

+++

# !!! 写博客前先看此文

## 创建一篇新的博客

**如何创建一篇新的博客？**

- 首先要先运用 hugo 的语法在 post 目录下创建一个文件, 并在文件下创建 index.md 文件

  ```
  hugo new xxx/xxx/post/<文件夹名>/index.md
  
  ```

- 修改文件头部信息

  - 创建出来的文件一般开始时包含以下四个信息

    ```markdown
    ### 文章标题，默认与文件夹名称一致，可以修改
    title = '2022 10 11 CodingStyle'
    
    ### 文章创建时间
    date = 2024-09-09T23:49:57+08:00
    
    ###  draft 的指令是草稿的意思，如果沒有在上线前改成 false，是不會在正式网站中渲染的。
    draft = true
    ```

  - 可自行添加信息

    ```markdown
    ### 文章权重等级，数字越小越优先展示
    weight=5
    
    ### 文章标签分类
    categories = [
        "Test"
    ]
    ```

  

- 添加作者信息(为方便统一样式，恳请大家均采用以下样式)

  ```html
  <div style="text-align: center;">
      <img src="https://cdn.jsdelivr.net/gh/Ahaitang/PicGo@master/Images/ACM.jpg" alt="Yestercafe" style="zoom: 10%;" />
  </div>
  <div style="text-align: center;">
      <strong>Yestercafe</strong>
  </div>
  ```
  
  - 修改头像
  
    `将 src="图片链接" 换成自己的图片链接即可`
  
  - 修改作何名称
  
    `将<strong>作者名称</strong> 换成个人名称即可`
  
- 正文内容采用 Markdown 语法进行书写即可
