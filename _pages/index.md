---
layout: defaults/page
permalink: index.html
narrow: true
title: Welcome to Hiram's Personal Page
---

## About Me

{% include components/intro.md %}

[//]: # ([Here's the full feature list and some quick examples of what it can do.]&#40;{{ site.baseurl}}{% link _pages/about.md %}&#41;)

<br />

## Education Background

|         Year          |                        Institute                        | <img width=20/> Degree                              |
|:---------------------:|:-------------------------------------------------------:|:----------------------------------------------------|
|      2024.2-now       |     <img width=20/> Australian National University      | <img width=20/>Master of Computing                  |
|     2018.9-2022.6     |    <img width=20/>  Beijing Institute of Technology     | <img width=20/>B.S. Computer Science and Technology |

<br />

## Experience
- AOI Algorithmic Engineer at Shenzhen Image Technology Co,.Ltd. (2023.3- 2023.12)
- Research Assistant at BIT supervised by [Prof. Jianwei Gong](https://me-english.bit.edu.cn/people/facultydept/vehiclee2/xs3/b125047.htm) and [Prof. Chao Lu](https://scholar.google.com/citations?user=0Jv8_7MAAAAJ&hl=zh-CN) ( 2022.7- 2023.1)
- Internship in ByteDance as Algorithm Engineer develop [Fastbot](https://github.com/bytedance/Fastbot_Android)( 2021.10-2022.3)
- Summer Research Internship with [Prof. Lili Su](https://lilisu3.sites.northeastern.edu/) on autonomous trajectory prediction (2021.7-2021.9)
- Autonomous System group of [BITFSD](http://www.bitfsd.com/) ( 2020-2022 )

<br />

### News
- **\[Feb.2024\]** I begin the Master of Computing at Australian National University, specializing in Artificial Intelligent!
- **\[Nov.2023\]** The paper about Multi-stream Information Fusion in Low-illumination Scenarios is accepted by IEEE T-ITS!
- **\[July.2023\]** Our research work on Online Risk Assessment for Human-robot Interaction is accepted by ITSC 2024!
- **\[Mar.2023\]** I join in Shenzhen Image Technology Co.,Ltd as full-time Algorithm Engineer, developing and optimizing algorithms for defect detection!
<br />

### Contact
I am happy to share and discuss the previous projects, technology details and research interests with everybody, please feel free to drop me an [email](mailto:hailong.gong@anu.edu.au).
<hr />

Views:&nbsp;<span id="" class="leancloud_visitors" data-flag-title=""> - </span>.

<!-- 同时兼容http与https -->
<script src="//unpkg.com/leancloud-storage@4.12.2/dist/av-min.js"></script>
<script>
    // 第一个参数是appid，第二个参数是appkey，此处的只是示例
    AV.init({
      appId: "MWwmGe7vgL0O6EFFKeDImBkD-gzGzoHsz",
      appKey: "VQeBsSS0pFds2P7BcE95mCsd",
      serverURL: "https://leancloud.api.whuzfb.cn"
    });
    // 自己创建的Class的名字
    var name='Counter';
    function createRecord(Counter){
      // 设置 ACL
      var acl = new AV.ACL();
      acl.setPublicReadAccess(true);
      acl.setPublicWriteAccess(true);
      // 获得span的所有元素
      var elements=document.getElementsByClassName('leancloud_visitors');
      // 一次创建多条记录
      var allcounter=[];
      for (var i = 0; i < elements.length ; i++) {
        // 若某span的内容不包括 '-' ，则不必创建记录
        if(elements[i].textContent.indexOf('-') == -1){
          continue;
        }
        var title = elements[i].getAttribute('data-flag-title');
        var url = elements[i].id;
        var newcounter = new Counter();
        newcounter.setACL(acl);
        newcounter.set("title", title);
        newcounter.set("url", url);
        newcounter.set("time", 0);
        allcounter.push(newcounter);
        // 顺便更新显示span为默认值0
        elements[i].textContent=0;
      }
      AV.Object.saveAll(allcounter).then(function (todo) {
        // 成功保存记录之后
        console.log('创建记录成功！');
      }, function (error) {
        // 异常错误 
        console.error('创建记录失败: ' + error.message);
      });
    }
    function showCount(Counter){
      // 是否需要创建新纪录的标志（添加一篇新文章）
      var flag=false;
      var query = new AV.Query(name);
      query.greaterThanOrEqualTo('time', 0);
      query.find().then(function (results) {
        // 当获取到的记录为0时置默认值
        if(results.length==0){
          $('.leancloud_visitors').text('-');
          flag=true;
          console.log('返回查询记录为空');
          // 如果获取到空记录就创建新记录
          createRecord(Counter);
          return;
        }
        // 将获取到的数据设置为text
        for (var i = 0; i < results.length; i++) {
          var item = results[i];
          var url = item.get('url');
          var time = item.get('time');
          var element = document.getElementById(url);
          element.textContent = time;
        }
        // 当某个span含有默认值时说明需要创建记录
        if($('.leancloud_visitors').text().indexOf("-") != -1){
          flag=true;
        }
        // 当获取的记录数与span个数不吻合时
        if(results.length != $('.leancloud_visitors').length){
          flag=true;
        }
        if(flag){
          createRecord(Counter);
        }
      }, function (error) {
        console.log('query error:'+error.message);
      });
    }
    $(function() {
      var Counter = AV.Object.extend(name);
      showCount(Counter);
    });
</script>


