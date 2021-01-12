---
title:  如何使用RStudio+Hugo+Netlify搭建个人主页
author: Peng Wang
date: '2021-01-11'
slug: []
categories:
  - blog
tags: [hugo]
authors: [Peng Wang]
description: ''
externalLink: ''
series: []
---


- 本文尽量用最简单直接的语言搭配直接上手的代码来讲清楚如何搭建个人主页
- 必备软件：[R](https://cran.r-project.org/mirrors.html) (下载最新版本），[RStudio](https://rstudio.com/products/rstudio/download/#download)（下载最新版本的IDE）
- 必备网站：[Netlify](https://www.netlify.com) （用于将搭载好的网站承载在上面并进行发布）
- 可选网站：[GitHub](https://github.com) （用于和Netlify同步，方便经常更新个人网站的内容）

1. 打开RStudio，在console输入下列代码
```R
install.packages("blogdown")   #安装blogdown包
blogdown::install_hugo(force=TRUE)  #安装hugo
```
2. 在RStudio的菜单栏里进行如下操作
  - File - New Project - New Directory - New Project
  - 在Directory Name中输入你想起的名字，例如“kw”
  - 在路径下拉菜单中选择你想把这个新的project放在哪里，建议选一个最容易找到的地方，例如就放在Downloads文件夹
  - 点击创建，RStudio会自动跳到你创建的新项目
3. 选择你喜欢的主题
  - [Hugo Themes](https://themes.gohugo.io)
  - 我们以[“aafu”](https://themes.gohugo.io/aafu/)为例 
  - 点击“download”，跳转到GitHub页面（不要慌，不需要你懂GitHub）
  - 记住主题的路径名，例如aafu，在GitHub上（用户名/库名）为“darshanbaral/aafu“
  - 一个劝告，小白不要选择太复杂的主题，例如那些有菜单，点击会有各种页面，甚至会有文章或者推文什么的
  - 这种主题比较麻烦，就算你成功搭出来了，你以后更新也很麻烦
4. 打开RStudio，在console里输入下列代码（点击回车以后，你会看到“index.md”和一个Viewer跳出来）
```R
blogdown::new_site(theme = "darshanbaral/aafu")
```
5. 关于config
  - 在viewer那个区域内，点击Files，你会看到在你这个项目里的所有文件
  - 点击config.toml
    - 了解一下这个文件的结构
    - baseURL：这个先不要管，除非你已经购买了个人域名，否则你目前还不能确定这个URL会是什么
    - languageCode：Hugo支持18钟语言，这里强调两个，en-us（英语）和zh-cn（简体中文）
    - theme：不要动这个
    - [params]：主页参数，里面有很多元素，包括主题背景、图标、菜单、以及主页页面各元素
  - 具体了解一下aafu主题所具有的参数部分
    - 整个页面（颜色应该是可以调整的）
    - 两个主菜单按钮Home和Blog（你可以在viewer里点击看看有什么变化）
    - 主页内容栏，About Me、Experiens等
    - 头像、姓名、简介、社交账号连接
6. 修改config.toml的参数
  - languageCode：我个人想保留英文，不过我看了一下，这个主页吧，也没设置多语言，其实没啥区别，改不改都一样
  - [params]下面：
    - title = "KW的主页"　
    - author = "Kin Wang"
    - description = "KW的个人网站"
    - copyright = "Kin Wang"
  - [params.theme]下面：
    - mainTheme = "dark"；这个我改成了“dark”
    - showAttribute = false；这个改成false，可以让底下那个“by aaa”消失掉
    - singlePage = true；这个改成true，就只有一个单独页面，没有home和blog了，你也可以不改
  - [params.favicons]
    - use = false；这个用处不大，直接设置成false就行了
  - [params.profile]
    - name = "Kin Wang"；资料部分，你的姓名
		- tagline = "折腾青年"；这个你想写啥写啥
		- location = "火星"；你想些啥写啥
    - photo = "IMG_7377.JPG"；这一步很关键
      - 首先，你要先把你想放的照片先放到指定路径“/kw/themes/aafu/static/images"
      - 我放了一张名为“IMG_7377.JPG”的照片进去
  - [params.social]
    - title这个无所谓，不要管
    - [[params.social.list]]总共有6个，你可以修改，你也可以删，你也可以用#来变成comments
    ```
        [[params.social.list]]
            class = "fab"
            icon = "fa-linkedin-in"
            url = "http://linkedin.com/kkww"  #这个地方写你的LinkedIn地址
            title = "LinkedIn"		
        #[[params.social.list]]      #我不想要这个部分，所以我前面都加了“#”
        #    class = "fab"
        #    icon = "fa-stack-overflow"
        #    url = "#"
        #    title = "StackOverflow"
        [[params.social.list]]
            class = "fab"
            icon = "fa-github"
            url = "#"
            title = "GitHub"
        [[params.social.list]]
            class = "fab"
            icon = "fa-twitter"
            url = "#"
            title = "Twitter"
		   #[[params.social.list]]    #不想要这个
       #        class = "ai"
       #        icon = "ai-google-scholar"
       #        url = "#"
       #        title = "Google Scholar"
		    [[params.social.list]]     #改成知乎
            class = "fab"    #把ai改成fab
            icon = "fa-zhihu"   #改成fa-zhihu
            url = "#"        #你的知乎地址
            title = "Zhihu"   #改成Zhihu
    ```
  - [[params.showInAccordion]]有好几个呢，我觉得这些都算很实用的，我除了想删掉Hobbies，其他都留着
    ```
      [[params.showInAccordion]]
          item = "aboutme"
          expand = true   # true for the section that is initially expanded
      [[params.showInAccordion]]
          item = "experience"
      [[params.showInAccordion]]
          item = "education"
      [[params.showInAccordion]]
          item = "publication"
      [[params.showInAccordion]]
          item = "project"
      [[params.showInAccordion]]
          item = "skill"
      #[[params.showInAccordion]]    #不想要
      #    item = "hobby"
    ```
  - [params.aboutme]以及后面的，看情况改就行了，我是这样改的
    ```
        [params.aboutme]
          title = "关于我"
          icon = "fas fa-user"
          description = "就一逗比青年，没啥可介绍的"  #你想些啥写啥
      # Experience section
      [params.experience]
          title = "工作经验"
          icon = "fas fa-briefcase"

          [[params.experience.list]]
              position = "做梦师"   #你的职位
              dates = "2019 - *Present*"    #时间
              company = "做梦工厂"   #公司
              details = "负责个人做梦，同时也负责让别人做梦"  #工作内容
          [[params.experience.list]]
              position = "咸鱼"
              dates = "2018 - 2019"
              link = "#"    #你公司的网页地址，你要是不想，可以删掉
              company = "阿里wawa"   #公司名
              #你要是想加个details，就复制上面那个
              details = "尽一切努力不做拼夕夕人！"

      # Education section
      [params.education]
          title = "教育经历"
          icon = "fas fa-graduation-cap"

          [[params.education.list]]
              degree = "做梦学博士"    #你的学位
              college = "做梦大学"   #学校
              dates = "2013 - 2018"   #时间
              #thesis_title = "Effect of humans on other humans: a study of human behavior."
              #thesis_link = "#"
          [[params.education.list]]
              degree = "咸鱼学硕士"
              college = "咸鱼大学"
              dates = "2013 - 2018"
              #thesis_title = "Effect of humans on other humans: a study of human behavior."
              #thesis_link = "#"
          [[params.education.list]]
              degree = "不知道学了啥的学士"
              college = "不知道大学"
              dates = "2004 - 2009"
           #写这个代码的人真无聊，毕业论文题目和链接都给
      # Publication section
      [params.publication]
          title = "发表情况"   #发表文章情况
          icon = "fas fa-book"
          #The order below determines the order in which the items appear in "Publications" section
          format = ["date", "authors", "title", "journal"]
          #If you don't want to group publications, comment the line below by adding # at the beginning
          types = ["期刊文章", "会议"]

          [[params.publication.list]]
              title = "写到这才发现，这个主题的coder写的不是英文"   #文章名
              authors = "K Wang, Y Wang"     #作者
              date = "2018"    #日期
              journal = "Journal of Field 52 (16), 9033-9044"    #期刊
              link = "#"      #链接
              type = "期刊文章"     #文章类型

          #[[params.publication.list]]
          #    title = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
          #    authors = "F Last, F Second, P secondary"
          #    date = "2018"
          #    journal = "Journal of Field 52 (16), 9033-9044"
          #    link = "#"
          #    type = "Journal Articles"
		
          [[params.publication.list]]
              title = "论如何做梦"
              authors = "K Wang"
              date = "2018"
              journal = "世界做梦大会"
              link = "#"
              type = "会议"

      # Project section
      [params.project]
          title = "项目"     #项目
          icon = "fas fa-project-diagram"

          [[params.project.list]]
              title = "做梦一天"   #项目名称
              url = "#"     #链接
              description = "就做梦一天呗"    #描述
          [[params.project.list]]
              title = "做梦一周"     #项目
              url = "#"
              description = "就做梦一周啊"
          [[params.project.list]]
              title = "做梦一个月"
              url = "#"
              description = "就一个月都做梦哎"
          [[params.project.list]]
              title = "一直做梦"
              url = "#"
              description = "活到老，梦到老"            

    # Skill section
    [params.skill]
        title = "技能"
        panelId = "skill-panel"
        icon = "fas fa-cogs"

        [[params.skill.list]]
            skill = "好吃懒做, 做梦"     #名称
            skillrating = 90             #评级
        [[params.skill.list]]
            skill = "咸鱼"
            skillrating = 80
        [[params.skill.list]]
            skill = "吃"
            skillrating = 50

    # Hobby section
    #[params.hobby]
     #   title = "Hobbies"
      #  icon = "fas fa-gamepad"
		#
     ##   [[params.hobby.list]]		
		   # hobby = "Cooking"
        #[[params.hobby.list]]		
		#    hobby = "Hiking"
     #   [[params.hobby.list]]		
		  #  hobby = "Baking"
    ```
7. 可以选择同步到GitHub上面，然后再同步到Netlify上面。这样做，你可以方便更新你的个人主页。当然，你如果不准备更新，那直接投到Netlify上也没关系。
8. 打开GitHub客户端，把刚才创建好的文件夹拖进来，然后确认创建新的repository，然后点publish repository
9. 在Netlify上创建账户，并且绑定Github账号。
10. 点击New site from git，选择对应的Github上的repository。build command是hugo，publish directory是public，environment variable中设置Key为HUGO_VERSION，value为0.73.0
11. 然后点击deploy
12. 我的[demo](https://kwhugodemo.netlify.app)




