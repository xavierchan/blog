---
title: Studio
toc: true
date: 2019-08-20 16:12:55
tags:
categories:
 - openedx
---

### 前言

Studio是用于构建课程的edX工具。您可以使用Studio创建课程结构，然后为学习者添加问题，视频和其他资源。您还可以管理课程安排，确定课程团队成员，设置评分政策，发布课程等。

### 一、技术栈

- django
- python2.7
- memcache
- mongodb
- pymongo
- edx-ora2
- xblock

[参考社区网站](https://www.edustack.org/manual/edx/open-edx-ebook%E4%B8%AD%E6%96%87%E7%89%88/)

## 二、运行环境

docker-compose.yml
环境变量设置： /edx/app/edxapp/edxapp_env
settings配置文件： --settings = devstack_docker
安装依赖关系： /edx/app/edxapp/edx-platform/requirements

## 三、相关功能

studio涉及的表：
API_ADMIN:
    - Api access configs
        Configuration for API management.
    - Api access requests
        Model to track API access for a user.
ASSESSMENT:
    - Assessment feedbacks
    - Assessments
    - Peer workflows
    - Rubrics
ora相关功能表。

ora的功能介绍 。

GitHub： [https://github.com/edx/edx-ora2](https://github.com/edx/edx-ora2)

文档： https://edx.readthedocs.io/projects/edx-partner-course-staff/en/latest/exercises_tools/open_response_assessments/index.html

功能分析：
  Open Response Assessments , EdX完全支持此问题类型。
  
  开放式反应评估（ORA），有时也称为同伴评估，是一种灵活的分配类型，学习者可以在其中回答可能没有明确答案的问题。 学习者提交文字回复或短文。 您还可以要求学员提交图像或其他类型的文件以附带他们的书面回复。

在提交原始回复后，学习者将被引导通过一系列评估步骤，包括培训步骤，同伴评估，自我评估和员工评估。

AUTHENTICATION AND AUTHORIZATION:
    - Groups
    - Users
身份认证和授权

BLOCK_STRUCTURE:

    - Block structure configurations
Configuration models for Block STructures

    
CATALOG:

    - Catalog integrations
    
管理配置以连接到目录服务并使用其API。
    
CELERY_UTILS:
    - Failed tasks
    
记录celery失败的任务。
    
CONTENTSERVER:

    - Cdn user agents configs
    - Course asset cache ttl configs

Configuration for the user agents we expect to see from CDNs.

Configuration for the TTL of course assets.

    
    
CONTENTSTORE

    - Push notification configs
    - Video upload configs
移动推送通知的配置。

配置上传功能。

COURSE MODES

    - Course mode expiration configs
    - Course modes
从课程结束到自动使课程模式过期的时间段的配置   
Course modes 提供各种模式的课程

COURSE OVERVIEWS

    - Course overview image configs
    - Course overview image sets
    - Course overviews
    
1，课程缩裂图配置 

2，课程缩裂图生成（前置条件1）

3，存储和缓存课程基本信息的模型

COURSE_CREATORS

    - Course creators
    

COURSEWARE

    - Course dynamic upgrade deadline configurations
    动态升级期限 每个课程运行配置
    此模型控制每个课程运行级别的动态升级截止日期，允许课程运行有不同的截止日期或完全退出功能
    - Dynamic upgrade deadline configurations
    动态升级截止日期配置：
    控制自定进度课程的动态升级截止日期的行为。
    - Offline computed grade logs
    计算离线成绩时的日志
    使用此功能可以再完成最后一次计算成绩时显示教室
    - offline computed grades
    为给定用户和课程离线计算的成绩表
    - Org dynamic upgrade deadline configurations
    动态升级每个组织的期限配置， 控制每个组织级别的动态升级截止日期，组织可以有不同的截止日期或完全退出功能
    - Student modules
    保持特定学生在特定课程的特定模块状态

CRAWLERS

    - Crawlers configs
    Django APP的配置抓取器具
    
CREDIT

    - Credit configs
    管理信用配置
    - Credit courses
    跟踪学分课程模型
    - Credit eligibilities
    用户是否有资格获得特定课程学分的记录
    - Credit provides
    该模型代表一个可以为课程授予学分的机构。
    - Credit requests
    来自特定信贷提供者的信用请求。当用户发起信用请求时，将创建CreditRequest记录。
    每个CreditRequest都分配了一个唯一的标识符，以便我们可以在请求时找到它
    由提供商批准。CreditRequest记录存储要发送的参数在提出请求时。如果用户重新发出请求
    （可能是因为用户没有在信用提供者的网站上填写表格），请求记录将被更新，但UUID将保持不变。
    - Credit requirement statuses
    每个信用需求的状态
    1， satisfied 验证后满足
    2， failed  验证后不满足
    3，declined 还没有验证
    - Credit requirements
    代表一个信用要求
    
DARK_LANG

    - Dark lang configs
    发布的语言配置
    
    
DJANGO OAUTH TOOLKIT

    - Access tokens
    - Applications
    - Grants
    - Refresh tokens
django OAuth 工具包
OAuth2 需要用到这个包
同步数据库生成的表。


DJANGO_COMMENT_COMMON

    - Forums configs
    配置与cs_comments_service论坛后端的连接
    

Django_NOTIFY

    - Notifications
    - settins
    - Subscriptions
    - Types
django-notify 模块

DJANGO_OPENID_AUTH


    - https://github.com/edx/django-openid-auth/tree/master/django_openid_auth

DJCELERY

    pip install DJCELERY
    
    celery 的使用
    
    
EDX_OAUTH2_PROVIDER：

    - Trusted clients

https://github.com/edx/edx-oauth2-provider

edX平台的OAuth2提供程序。

edx_oauth2_provider是一个Django应用程序，用于edx平台中的身份验证和授权。身份验证机制与OpenID Connect规范保持一致，支持其一些基本功能。


EDX_PROCTORING

open edx 平台的考试监考子系统



EDXVAL

    edx-val是一个django应用程序，可以创建和检索视频和字幕的元数据。创建视频条目时，可以将它们分配给预设配置文件，例如“high_quality”或“mobile_only”。在请求视频时，客户端不需要知道要检索的配置文件，而只需要知道该视频的edx_video_id。由于返回了该特定视频的所有不同配置文件，因此客户端可以决定他们想要使用哪些配置文件。
    
EMBARGO

    - ip filters
    - Restricted courses
    
    
ip filters 表

    Register specific IP addresses to explicitly block or unblock

 
Restricted courses    

    受到限制的课程    

ENTERPRISE

ENTERPRISE CONSENT

ENTERPRISE DEGREED INTEGRATION

ENTERPRISE SAP SUCCESSFACTORS INTEGRATION

ENTERPRISE XAPI INTEGRATION


ENTITLEMENTS

    - Course entitlement policys
    Represents the Entitlement's policy for expiration, refunds, and regaining a used certificate
    - Course entitlement support details 
    支持与权利的交互记录表
    - Course entitlements
    Represents a Student's Entitlement to a Course Run for a given Course
		
EXTERNAL_AUTH
	- External auth maps
	外部身份验证model
	
MICROSITE_CONFIGURATION
	 - Microsite histories
	 这是微型网站的档案表模型,这样我们就能保持历史的变化。请注意,关键字段不再是独一无二的
	 - Microsite organization mappings
	 microsite  
	 - Microsite templates
	 Mapping of Organization to which Microsite it belongs 
	 A HTML template that a microsite can use
	 - Microsites
	 微型网站的信息存储，实现最大的灵活性,大多数字段存储在里面一个json。
	 
MILESTONES
 edx   的一个Django APP 
 github : https://github.com/edx/edx-milestones
 
ORGANIZATIONS 
 edx 管理组织的Django APP
 
REDIRECTS

SCHEDULES:
 /edx-platform/openedx/core/djangoapps/schedules/models.py

SELF_PACED
openedx.core.djangoapps.self_paced
Enable Self-Paced Courses in the Learning Management System

SITE_CONFIGURATION
	-  Site configuration historys	 	
	-  Site configurations
站点配置：
您可以使用站点配置覆盖站点名称，徽标图像，favicon等。
站点配置历史记录

SITES
配置主题

STATIC_REPLACE
 配置静态资源CDN 加速的
 - Asset base url configs	
 - Asset excluded extensions configs


STUDENT
	- Course access roles	
	Maps users to org, courses, and roles. Used by student.roles.CourseRole and OrgRole.
	To establish a user as having a specific role over all courses in the org, create an entry
	without a course_id.
	
	- Course enrollment alloweds	
	 Table of users (specified by email address strings) who are allowed to enroll in a specified course.
    The user may or may not (yet) exist.  Enrollment by users listed in this table is allowed
    even if the enrollment time window is past.  Once an enrollment from this list effectively happens,
    the object is marked with the student who enrolled, to prevent students from changing e-mails and
    enrolling many accounts through the same e-mail
		
	- Dashboard configurations	
	  Dashboard Configuration settings
		
	- Linked in add to profile configurations	
	LinkedIn Add to Profile Configuration
	This configuration enables the "Add to Profile" LinkedIn
    button on the student dashboard.  The button appears when
    users have a certificate available; when clicked,
    users are sent to the LinkedIn site with a pre-filled
    form allowing them to add the certificate to their
    LinkedIn profile.
		
	- Pending name changes	
	This model keeps track of pending requested changes to a user's email address
	
	- Registration cookie configurations	
	  Configuration for registration cookies
		
	- Registrations	
	Allows us to wait for e-mail before user is registered. A
	registration profile is created when the user creates an
	account, but that account is inactive. Once the user clicks
	on the activation key, it becomes active
	
	- User attributes	
	Record additional metadata about a user, stored as key/value pairs of text.
	- User test groups


STUDENT IDENTITY VERIFICATION
		- Manual verifications
		Each ManualVerification represents a user's verification that bypasses the need for
				any other verification

		- Software secure photo verifications
		Model to verify identity using a service provided by Software Secure. Much
		of the logic is inherited from `PhotoVerification`, but this class encrypts the photos

		- Sso verifications
		Each SSOVerification represents a Student's attempt to establish their identity
		by signing in with SSO. ID verification through SSO bypasses the need forphoto verification
		
STUDENT SURVEYS
- Surver forms
Model to define a Survey Form that contains the HTML form data
that is presented to the end user. A SurveyForm is not tied to
a particular run of a course, to allow for sharing of Surveys
across courses


SUBMISSIONS
- Score Summaries	
- Scores	
- Student items	
- Submissions	
用于创建提交和分数的API。
github : https://github.com/edx/edx-submissions

TAGGING
- Available tag values	
this model represents available values for tags 
- Tag categories
this model represents tag categories 	

THEMING
- Site themes	
主站的主题存储 

TRACK
- Tracking logs
日志追踪	

USER TASKS
- User task artifacts	
- User task statuses
django-user-tasks是一个可重用的Django应用程序，用于管理用户触发的异步任务。它为每个此类任务提供状态页面，如果任务当前正在执行，则包括有意义的进度指示器，并在任务完成后提供任何适当的文本和/或输出链接。
github :  https://github.com/edx/django-user-tasks


USER_API
	- Retirement states	
	- User Retirement Reporting Statuses	
	- User Retirement Requests	
	- User Retirement Statuses	 	
用户的Api model


VERIFIED_TRACK_CONTENT
		- Migrate verified track cohorts settings	
		Configuration for the swap_from_auto_track_cohorts management command. 
		- Verified track cohorted courses	
		Tracks which courses have verified track auto-cohorting enabled

VIDEO_CONFIG
	- Course hls playback enabled flags
	为特定课程启用HLS播放。 全局功能必须启用此功能才能生效。
	- Course video transcript enabled flags
	为特定课程启用视频脚本。 全局功能必须启用此功能才能生效。
	启用此功能后，第三方脚本集成功能将可用于
	将提供特定课程和S3视频脚本（目前作为后备）。
	- Hls playback enabled flags
	在整个平台上启用HLS播放。
	当此功能标志设置为true时，单个课程
	还必须为此功能启用HLS播放
	生效
	- Migration enqueued courses
	临时模型，用于保留已将队列迁移到S3的队列ID。	
	- Transcript migration settings
	Transcript Migration管理命令的参数
	- Updated course videoss
	临时模型，用于保存已加入更新视频缩略图的课程视频。	
	- Video thumbnail settings
	视频缩略图管理命令的参数	
	- Video transcript enabled flags
	在整个平台上启用视频转录。
	当此功能标志设置为true时，单个课程
	还必须为此功能启用Video Transcript 生效。
	启用此功能后，第三方脚本集成功能将全部可用
	将提供课程或一些特定课程和S3视频成绩单（目前作为后备）

VIDEO_PIPELINE
- Course video uploads enabled by defaults
为特定课程启用默认的视屏上传，启动此功能后 它的全球特性才生效
- Video pipeline integrations
管理用于连接到edx-video-pipeline服务并使用其API的配置
- Video uploads enabled by defaults
启用视频上传启用平台上的默认功能

WAFFLE
- Flags	
- Samples	
- Switches
github :https://github.com/django-waffle/django-waffle
文档：https://waffle.readthedocs.io/en/stable/about/why-waffle.html
功能标志是持续集成和部署应用程序的关键工具。Waffle是管理Django应用程序中的功能标志的几种选择之一。

WAFFLE_UTILS
- Waffle flag course overrides	
- WIKI
- Article revisions	
- Articles	
- URL paths	

WORKFLOW
- Assessment workflows	

XBLOCK CONFIGURATION
- Course edit lti fields enabled flags	
- Studio configs	

XBLOCK_DJANGO
- X block configurations	
- X block studio configuration flags	
- X block studio configurations	

    
    
## 四、相关脚本
## 五、发布相关
## 六、常见问题
## 七、引用参考
**https://edx.readthedocs.io/projects/edx-partner-course-staff/en/latest**

edx git 仓库

https://github.com/edx/edx-celeryutils

Django-oauth-toolkit

##  studio功能
Studio中创建全新课程，也可以重新运行现有课程。
也可以通过导出和导入XML文件，来
备份课程和编辑课程。

### 创建课程：
    
#### 选择创建新课程

important：创建课程后，组织，课程编号，课程运行后不能修改。

####  课程标题
- 使用标题大写和正常间距和标点符号。
- 将课程名称限制为70个字符。许多最有效的课程标题有50个或更少的字符。

#### 更改课程标题

要更改课程标题在Studio和LMS中的显示方式，请按以下步骤操作。

在Studio中打开课程。
在“ 设置”菜单上，选择“ 高级设置”。
在“ 课程显示名称”字段中，输入所需的标题。
选择保存。
在Studio和LMS中，课程标题将更改为您在“ 课程显示名称”字段中指定的值。您课程的网址不会更改。

#### 课程编号
- 课程编号最多可包含10个字符。
- 字符可以是字母，数字或句点。
- 如果课程由多个模块组成，则课程编号可以包含.1x或.2x等结尾。

#### 更改课程编号
要更改课程编号在Studio和LMS中的显示方式，请按照以下步骤操作。

在Studio中打开课程。
在“ 设置”菜单上，选择“ 高级设置”。
在“ 课程编号显示字符串”字段中，输入所需的编号。
选择保存。
在Studio和LMS中，您的课程编号将更改为您在“ 课程编号显示字符串”字段中指定的值。您课程的网址不会更改。

#### 注意：
（如果您的课程是有效的，EdX不建议您这样做）


#### 设置课程开始时间和结束时间

studio settings

Schedule & Details

Course Schedule section

select save changes

#### 如何设置一个宣传开始时间
您可以宣传课程的开课日期与您在“课程表和详细信息”页面中设置的课程开始日期不同。如果确切的开始日期不确定，您可能希望这样做。

您可以输入特定日期或说明。例如，您可以将开始日期宣传为“2016年10月15日”或“随时，自定进度”。

要在Studio中设置广告的开始日期，请按照下列步骤操作。
1, On the Settings menu, select Advanced Settings.
2,Locate the Course Advertised Start Date field. The default value is null.

3, Enter the start date that you want learners to see for your course in MM/DD/YYYY format.

4, A date value entered in MM/DD/YYYY format appears to learners in DD Mon YYYY format. For example, 10/15/2016 appears as 15 Oct 2016.

5, Add quotation marks (" ") before and after the start date value. An example follows.

6, "Anytime, self-paced"
Select Save Changes.

A message lets you know whether your changes were saved successfully.


#### 在Studio中为您的课程设置起搏
在使用此功能设置自定进度课程之前，必须使用Open edX Django管理面板启用它。请按照以下步骤操作，或与Open edX站点管理员联系以获取帮助。

登录您的Open edX Django Admin面板。
在Self_Paced部分中，找到自定进度配置，然后选择添加。
选中“ 启用并启用课程主页改进” 复选框。
选择保存。
要为课程设置调步，请按以下步骤操作。

注意

课程开始日期过后，您无法更改课程节奏。

在设置菜单中，选择计划与细则。
向下滚动到“ 课程起搏”部分。
在“ 课程起搏”下，选择“ 讲师 - 起搏”或“ 自我节奏”。
选择保存更改。


#### 定先决条件课程和考试

-先修课程:

要将一门课程定义为另一门课程的先决条件，你必须是当前课程和前提课程的课程创建者
 
 需要配置cms /common 下 'ENABLE_PREREQUISITE_COURSES': True
 studio --> schedule & details --> requirements --> Prerequisite course


-先修考试:

  在studio --> schedule & details --> extrance exams 勾选 
  在outline 里面设置入学考试。

#### 构建课程内容
##### 课程构建块
  创建课程内容
- 课程大纲是所有课程内容的容器。大纲包含一个或多个部分。
- 课程部分位于课程的顶层，通常代表一段时间。部分包含一个或多个子部分。
- 课程小节是一节的一部分，通常代表一个主题或其他组织原则。子部分包含一个或多个单元。
- 课程单元是课程中的课程，学习者将其视为单页。单元包含一个或多个组件。
- 课程组件是包含实际课程内容的单元内的对象

一旦了解了edX课程的结构，您就可以开始组织内容并将其输入Studio。
您可以在课程大纲中创建部分，子部分和单元。
对于评分小节，您还可以 设置分配类型和截止日期。
您可以在单元页面中创建组件。
此外，您可以通过在大纲和发布单元上设置发布日期来控制内容可见性。

##### 课程内容对学生可见设置：
- 课程开始日期
 课程没设置开始日期。学习者只是看到该课程尚未开始。
- section 和 subsection 的 发行日期
 发布日期： 可以配置部分和子部分的发布日期。注：讲师节奏的课程才有发布日期和时间，自学课程是没有发布日期和时间的。
- 子部分先决条件 
  在设置菜中，选择高级设置，设置 Enable Subsection Prerequisites = True
- 隐藏基于日期的字部分
可以根据日期使子部分内容不可见，你可能希望在某个日期之后是考试问题无法使用。
基于 讲师指导的课程，此选项使用小节的截止日期
基于 自学课程，此选项使用课程的结束日期
以这种方式隐藏的子部分在课程导航中仍然可见，并在计算成绩时包括在内。但是，学生在截止日期或课程结束日期之后无法再访问该小节的内容
To hide a subsection based on date, follow these steps.
Select the Configure icon in the subsection box.
The subsection settings dialog box opens.
On the Visibility tab, locate Subsection Visibility, and then select the appropriate option.
In instructor-led courses, select Hide content after due date.
In self-paced courses, select Hide content after course end date.

	
##### 设置问题可见性

默认情况下，当学习者提交问题答案时，他们会立即收到问题的结果：他们是否正确回答了问题，以及他们的分数。但是，您可能希望在运行考试时暂时隐藏学习者的问题结果，或者在管理调查时永久隐藏结果。您可以使用“ 评估结果可见性”设置来执行此操作。

注意

“ 评估结果可见性”设置是一个子部分设置。您无法更改个别问题的可见性。“ 评估结果可见性”子部分设置会覆盖各个问题的“ 显示答案”设置。隐藏结果时，问题的答案不可见。

“ 评估结果可见性”设置可与以下常见问题类型一起使用。

复选框问题
下拉问题
多项选择问题
数字输入问题
文字输入问题
“ 评估结果可见性”设置可与以下高级问题类型一起使用。

注释问题
电路原理图构建器问题
自定义JavaScript显示和评分
自定义Python评估输入
图像映射输入问题
数学表达式输入问题
在LaTeX中写的问题
自适应提示问题
分子结构
要更改子部分的结果可见性，请按照下列步骤操作。

在子部分框中选择“ 配置”图标。

将打开“ 设置”对话框。

选择“ 可见性”选项卡，然后找到“ 评估结果可见性”。

选择一个可用选项。

始终显示结果：这是默认设置。当学习者和工作人员提交答案时，问题结果和分段分数立即可见。

从不显示结果：分段分数是可见的，但问题结果从未对学习者或课程人员可见。

小节到期时显示结果：对于学习者，直到小组截止日期（针对讲师节奏课程）或课程结束日期（针对自学课程）已经过去，结果才会显示。对于课程人员，除非工作人员正在预览或查看作为学习者的课程，否则结果始终可见 。

注意
如果该小节没有截止日期，或者课程没有结束日期，则结果始终可见。

#### 使课程内容可搜索 
使课程内容可搜索
学员可以使用“ 课程”页面顶部的“ 搜索”框搜索HTML组件和视频脚本中的课程文本。
在学员可以搜索课程之前，Studio必须为内容编制索引。Studio在发布内容时会自动为所有新课程内容编制索引。
如有必要，您可以随时手动重新索引课程中的所有内容。通常，如果学员看到意外的搜索结果，您只需手动重新编制课程内容索引。重新索引你的课程内容，选择重新编制内容在顶部课程大纲页。重新索引通常需要不到30秒。

#### 修改课程内容
重新编辑课程内容后，需要发布才能使得学生能够看到修改后的变化。

#### 开发组件
组件是包含实际课程内容的单元的一部分。一个单元可以包含一个或多个组件。
默认情况下，studio包含4种基本类型的组件供您添加课程。
- 讨论组件 讨论组件提供课程正文中的讨论空间，学习者可以在讨论空间中和同伴探讨有关课程的想法。
- HTML组件 在课程中天剑文本，图像和某些类型的学习工具，HTML组件中的内容格式为HTML。
- 问题组件  添加不同类型的练习和问题。
- 视频组件  包含课程中的视频。

注明：Open edX课程由称为XBlocks的单元组成。任何人都可以编写新的XBlock，允许教育工作者和技术人员扩展他们课程的组件集。edX平台还包含几个XModule，它们是XBlocks的前身。EdX正在努力将现有的XModule重写为XBlocks，并从我们的代码库中删除XModule。

除了XBlock之外，还有几种方法可以扩展课程行为：

LMS是LTI工具消费者。课程作者可以嵌入LTI工具，将其他学习工具集成到Open edX课程中。
问题可以使用嵌入式Python代码来呈现问题或评估学习者的响应。教师编写的Python代码在名为CodeJail的安全环境中执行。
可以使用JS Input集成JavaScript组件。
可以使用OLX（开放式学习XML）导出和导入课程，这是一种基于XML的课程格式。

xblock 梳理： http://pms.elitemc.cn/index.php?m=doc&f=view&docID=243
如何在问题里面嵌套代码来呈现。在创建的问题里面

x1 = random.randint(0, 100)
x2 = random.randint(0, 100)
y = x1+x2



#### 学习者看到的内容
学习者视图显示课程中的内容，可以在选择不同身份看到不同的内容。

#### 创建特定于群组的课程内容
- 启动同类群组， 创建不同群组的学习者不同的课程体验
启用和配置群组功能 
在lms中，选择 Instructor  选择 Cohorts 
选择启用 Cohorts
- 添加同类群组
 添加同类群组
 添加一个名字给同类群组
 指定是否自动或者手动将学员分配到此同类群组里面
 可以选择特定的内容组关联
- 创建特定的内容组
在studio里面settings 里面选择 group configurations 里面添加内容组
- 设置单元组件的访问权限， 在单元Access Settings 配置里面设置 阻止访问 选择群组。


## 题库整理
 

## I版本新的变化

###  Studio通过LMS登录

现在登录到Studio是通过将用户重定向到LMS登录，然后重定向回Studio来完成的。站点操作员可以使用新的DISABLE_STUDIO_SSO_OVER_LMS功能标志禁用此功能。

注意： 通过Studio中的更改以使用LMS进行登录身份验证，LMS和Studio必须通过Cookie兼容的域提供服务。如果Studio域名是LMS域名的子域，则EDXAPP_SESSION_COOKIE_DOMAIN Ansible变量（转换为SESSION_COOKIE_DOMAINlms.env.json）必须设置为“。”。 在登录工作后，必须将Studio域添加到 EDXAPP_LOGIN_REDIRECT_WHITELISTAnsible变量（lms.env.json中的变量LOGIN_REDIRECT_WHITELIST），以便从LMS重定向到Studio。

## 参考资料

> - [edx-proctoring](https://github.com/edx/edx-proctoring)
> - [edxval](https://github.com/edx/edx-val)
> - [enterprise](http://open-edx-enterprise-service-documentation.readthedocs.io/en/latest/)
> - [配置open edx 开启功能](https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/configuration/)
> - [django_user_tasks](https://django-user-tasks.readthedocs.io/en/latest/)
