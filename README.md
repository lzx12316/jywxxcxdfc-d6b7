# 基于微信小程序的房产交易租赁服务平台设计与实现

> 🎓 **计算机毕业设计 · 基于微信小程序的房产交易租赁服务平台设计与实现**
>
> 本仓库只放**项目介绍 + 运行截图**（截图是站点带水印的原图，存在仓库 `images/` 里）。
>
> 👉 **完整可运行源码 / 数据库脚本 / 部署文档：[点我获取](https://geekcode.top/archives/%E5%9F%BA%E4%BA%8E%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E7%9A%84%E6%88%BF%E4%BA%A7%E4%BA%A4%E6%98%93%E7%A7%9F%E8%B5%81%E6%9C%8D%E5%8A%A1%E5%B9%B3%E5%8F%B0%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%AE%9E%E7%8E%B0?utm_source=github)**
>
> 💬 咨询微信：**ir9372**　|　🌐 更多项目：[极客代码 geekcode.top](https://geekcode.top/?utm_source=github)
>
> 📌 项目详情页：<https://geekcode.top/archives/%E5%9F%BA%E4%BA%8E%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E7%9A%84%E6%88%BF%E4%BA%A7%E4%BA%A4%E6%98%93%E7%A7%9F%E8%B5%81%E6%9C%8D%E5%8A%A1%E5%B9%B3%E5%8F%B0%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%AE%9E%E7%8E%B0?utm_source=github>


<table><td width="230" align="center"><a href="https://geekcode.top/?utm_source=github"><img src="images/02.jpg" alt="微信名片" width="220"></a><br><b>扫码加微信 ir9372</b></td><td valign="middle">📦 源码 = 项目介绍 + 全部运行截图 + 数据库 + 部署文档<br>👉 点上方任意截图，直接跳到 <b>极客代码 geekcode.top</b> 详情页</td></table>

---

<h1>基于微信小程序的房产交易租赁服务平台设计与实现</h1>
<h2>项目概述</h2>
<p>本项目名为“基于微信小程序的房产交易租赁服务平台设计与实现”，旨在构建一个集房产出售、租赁、预约看房及中介管理于一体的综合性服务平台。项目采用前后端分离架构，前端主要依托微信小程序提供移动端服务，后端基于 Java 技术栈构建核心业务逻辑与数据支撑。平台核心功能涵盖房源展示、在线预约（购房/租房）、中介信息管理、用户评论互动及后台统一管理。适用人群包括寻求购房或租房服务的普通用户、发布房源信息的房产中介人员以及负责系统运维的管理员。通过该平台，用户可便捷地浏览房源详情并完成预约操作，中介可高效管理房源与客户，管理员则能对全站数据进行集中监控与维护，有效提升了房产交易的透明度与服务效率。</p>
<h2>技术架构</h2>
<p>本项目采用典型的前后端分离架构设计。后端服务端使用 Spring Boot 框架作为基础容器，集成 MyBatis-Plus 进行持久层开发，利用 Shiro 框架实现权限认证与安全控制，数据库选用 MySQL 存储业务数据。前端分为两部分：面向用户的微信小程序端和面向管理员的 Web 后台管理端。小程序前端通过 HTTP 协议调用后端提供的 RESTful API 接口进行数据交互，实现了页面渲染与业务逻辑的解耦。Web 后台同样基于 Vue 技术栈（根据 vue-integrated 类型推断）构建界面，并通过相同的 API 网关与后端通信。这种架构确保了系统的高内聚低耦合，便于独立部署、扩展和维护。核心技术选型理由在于 Spring Boot 的快速开发与生态丰富性，MyBatis-Plus 简化了 CRUD 操作，Shiro 提供了成熟的权限解决方案，而微信小程序则保证了移动端的广泛覆盖与良好用户体验。</p>
<h2>功能模块</h2>
<h3>小程序用户端</h3>
<p>根据路由配置 <code>/fangyuanchushou</code>、<code>/fangwuleixing</code>、<code>/yudingfangzi</code> 等分析，小程序端主要包含以下功能模块：</p>
<ol>
<li><strong>房源浏览与检索</strong>：支持查看房产出售列表 (<code>/fangyuanchushou</code>) 和房产租赁信息 (<code>/zufangxinxi</code>, <code>/fangyuanchuzu</code>)，可按房屋类型 (<code>/fangwuleixing</code>) 筛选。</li>
<li><strong>预约服务</strong>：提供预约购房 (<code>/yuyuegoufang</code>) 和预约租房 (<code>/yuyuezufang</code>) 功能，支持提交预订单 (<code>/yudingfangzi</code>)。</li>
<li><strong>资讯与互动</strong>：展示新闻公告 (<code>/news</code>)，支持对出售房源 (<code>/discussfangyuanchushou</code>) 和租赁房源 (<code>/discussfangyuanchuzu</code>) 进行评论交流。</li>
<li><strong>个人中心</strong>：包含我的收藏 (<code>/storeup</code>)、我的资料 (<code>/yonghu</code>) 以及注册登录入口 (<code>/jingjirenRegister</code>)。</li>
<li><strong>门店与中介查询</strong>：可查看门店信息 (<code>/mendian</code>) 及经纪人中心 (<code>/jingjirenCenter</code>, <code>/jingjiren</code>)。</li>
</ol>
<h3>Web 后台管理端</h3>
<p>基于后台路由及代码上下文，Web 管理端主要功能包括：</p>
<ol>
<li><strong>系统登录与管理</strong>：管理员通过专用登录页进入系统，拥有最高权限。</li>
<li><strong>用户与角色管理</strong>：管理普通用户 (<code>/yonghu</code>) 和经纪人 (<code>/jingjiren</code>) 账户信息。</li>
<li><strong>房源内容管理</strong>：维护房产出售 (<code>/fangyuanchushou</code>) 和租赁 (<code>/fangyuanchuzu</code>) 的数据录入、审核与更新。</li>
<li><strong>业务数据监控</strong>：查看和管理预约记录 (<code>/yuyuegoufang</code>, <code>/yuyuezufang</code>)、订单状态 (<code>/yudingfangzi</code>) 及收藏数据 (<code>/storeup</code>)。</li>
<li><strong>系统配置与资讯</strong>：发布新闻 (<code>/news</code>)，管理房屋类型字典 (<code>/fangwuleixing</code>)，以及系统参数配置 (<code>/config</code>)。</li>
</ol>
<h2>用户角色与权限</h2>
<p>本系统主要划分为三种角色，各角色权限范围如下：</p>
<ol>
<li><p><strong>管理员 (Admin)</strong></p>
<ul>
<li><strong>访问端点</strong>：Web 后台管理系统。</li>
<li><strong>权限描述</strong>：拥有系统全部数据的增删改查权限。负责用户账号管理、房源信息发布与审核、预约订单处理、新闻公告发布、系统参数配置以及所有业务模块的最终控制权。</li>
</ul>
</li>
<li><p><strong>普通用户 (User)</strong></p>
<ul>
<li><strong>访问端点</strong>：微信小程序前端。</li>
<li><strong>权限描述</strong>：注册登录后，可浏览所有公开房源信息（出售/租赁），执行预约看房或下单操作，收藏感兴趣的房源，参与房源评论讨论，查看个人收藏记录及修改个人资料。无法发布房源或管理他人数据。</li>
</ul>
</li>
<li><p><strong>经纪人 (Agent/Jingjiren)</strong></p>
<ul>
<li><strong>访问端点</strong>：微信小程序前端（部分特定入口如 <code>/jingjirenCenter</code>）。</li>
<li><strong>权限描述</strong>：除具备普通用户的浏览和预约权限外，重点在于其专属的中心页面 (<code>/jingjirenCenter</code>)。通常用于展示个人业绩、接收客户咨询或管理自己名下的房源线索（具体深度权限依据后端 Controller 实现而定，此处仅基于路由存在性推断其有独立视图）。需通过注册流程 (<code>/jingjirenRegister</code>) 成为合法经纪人身份。</li>
</ul>
</li>
</ol>
<h2>项目特色与创新点</h2>
<ol>
<li><strong>全链路交易闭环</strong>：整合了从房源发现、类型筛选、查看详情到最终预约（购房/租房）的完整业务流程，打通了线上信息与线下服务的连接。</li>
<li><strong>双向互动社区化运营</strong>：引入评论机制 (<code>discuss...</code>)，允许用户对房源进行评价和交流，增加了平台的活跃度与信息参考价值，区别于传统单向展示型房产网站。</li>
<li><strong>多角色协同管理</strong>：设计了用户、经纪人、管理员三级体系，既满足了C端用户的便捷需求，又为B端经纪人提供了工作入口，同时保证后台管理的规范性。</li>
<li><strong>轻量化移动端体验</strong>：依托微信小程序无需下载、即用即走的特性，降低了用户使用门槛，结合 RESTful API 的高效数据交互，提升了响应速度与用户体验。</li>
</ol>
<h2>部署环境</h2>
<p>为确保项目正常运行，需准备以下软件环境：</p>
<ol>
<li><p><strong>后端运行环境</strong>：</p>
<ul>
<li>JDK 版本：建议 JDK 8 或 JDK 11（兼容 Spring Boot 主流版本）。</li>
<li>Maven：用于依赖管理和项目构建。</li>
<li>MySQL：数据库服务器，版本建议 5.7 或 8.0，需创建对应数据库并导入初始化脚本。</li>
</ul>
</li>
<li><p><strong>前端运行环境</strong>：</p>
<ul>
<li>Node.js：用于编译 Vue 相关资源及包管理（npm/yarn）。</li>
<li>微信开发者工具：用于调试、预览和上传微信小程序代码。</li>
</ul>
</li>
<li><p><strong>其他依赖</strong>：</p>
<ul>
<li>Tomcat：若未使用 Spring Boot 内置容器，需独立部署；通常 Spring Boot 打包 jar 即可直接运行。</li>
<li>IDE：IntelliJ IDEA (后端), VS Code (前端)。</li>
</ul>
</li>
</ol>
<h2>五、技术特性</h2>
<ul>
<li>前后端集成部署，前端资源打包至后端 static 目录</li>
<li>使用 MyBatis-Plus 简化数据访问层开发</li>
<li>集成 Shiro 权限框架实现角色权限控制</li>
</ul>
<h2>六、功能模块截图</h2>
<h3>后台管理端</h3>
<h4>后台-登录页</h4>
<p><a href="https://geekcode.top/archives/%E5%9F%BA%E4%BA%8E%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E7%9A%84%E6%88%BF%E4%BA%A7%E4%BA%A4%E6%98%93%E7%A7%9F%E8%B5%81%E6%9C%8D%E5%8A%A1%E5%B9%B3%E5%8F%B0%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%AE%9E%E7%8E%B0?utm_source=github" title="查看完整源码"><img src="images/01.jpg" alt="后台-登录页"></a></p>

---

## 获取完整源码

| 项目 | 说明 |
| --- | --- |
| 项目名 | 基于微信小程序的房产交易租赁服务平台设计与实现 |
| 运行截图 | 本文 1 张（站点带水印原图，仓库 `images/` 目录） |
| 完整源码 | [https://geekcode.top/archives/%E5%9F%BA%E4%BA%8E%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E7%9A%84%E6%88%BF%E4%BA%A7%E4%BA%A4%E6%98%93%E7%A7%9F%E8%B5%81%E6%9C%8D%E5%8A%A1%E5%B9%B3%E5%8F%B0%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%AE%9E%E7%8E%B0?utm_source=github](https://geekcode.top/archives/%E5%9F%BA%E4%BA%8E%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E7%9A%84%E6%88%BF%E4%BA%A7%E4%BA%A4%E6%98%93%E7%A7%9F%E8%B5%81%E6%9C%8D%E5%8A%A1%E5%B9%B3%E5%8F%B0%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%AE%9E%E7%8E%B0?utm_source=github) |
| 咨询微信 | **ir9372**（备注：jingpin-yuanma） |
| 更多项目 | [极客代码 geekcode.top](https://geekcode.top/?utm_source=github) |

> 需要源码、部署、改配置、跑不起来等问题，加微信 ir9372 沟通，说明项目名即可。
