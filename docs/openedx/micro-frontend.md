---
title: Open edX 微前端进度
date: 2019-08-20 16:13:09
tags:
categories:
 - openedx
---

### 1. Openedx 2019年会前端进展与规划

https://openedx2019.sched.com/event/Ktnn/state-of-open-edx-front-end

- 重构200个页面

- 从风险低的页面开始: profile(已经完成), account, order history

- 有25-75 micro-frontends(可复用的组件25+, 如edx/frontend-auth)

- 重构范围，包括学生，老师接触到的页面

- 第一个micro-frontend在J版本发布

- 优点：开发效率提高，更少资源加载，API接口，速度快可扩展。更好的体验，加载时间更短，渐进式加载，更多功能

- 前端技术： es2015, webpack, babel, react, redux, bootstrap, Jest, Enzyme, cypress

- 核心npm包

【授权登录】npm module (@edx/frontend-auth); JSON Web Token-based; built on axios

【翻译】npm module(@edx/frontend-i18n); react-intl实现多语言; english defaults; message descriptions for translators

【数据分析】npm module(@edx/frontend-logging); Analytics; error logging; performance logging







### 2. 官方组件仓库

#### 2.1 edx/fronend-auth

使用axios.interceptors确保在发出API请求前，用户的浏览器中存在有效的token(JWT)。 如果不存在有效的token，它将尝试用refresh token(如果存在)来获取一个新的token。 如果refresh token不存在或无效，则用户将被注销并重定向到您选择的页面。

import { getAuthenticatedAPIClient } from '@edx/frontend-auth';
const apiClient = getAuthenticatedAPIClient({
appBaseUrl: process.env.BASE_URL,
loginUrl: process.env.LOGIN_URL,
logoutUrl: process.env.LOGOUT_URL,
refreshAccessTokenEndpoint: process.env.REFRESH_ACCESS_TOKEN_ENDPOINT,
accessTokenCookieName: process.env.ACCESS_TOKEN_COOKIE_NAME,
});


提供了一个PrivateRoute组件，你可以使用这个组件，自定义你的登录验证流程。

<ConnectedRouter history={history}>
<Switch>
<Route exact path="/unauthenticated" component={UnauthenticatedComponent} />
<PrivateRoute
path="/authenticated"
component={AuthenticatedComponent}
authenticatedAPIClient={apiClient}
redirect={process.env.BASE_URL}  // This should be the base URL of your app.
/>
</Switch>
</ConnectedRouter>


edx/frontend-auth还提供了Redux actions and a reducer， 来登录后的profile信息注入你的react-app store里。






#### 2.2 edx/frontend-i18n

因为没有了模板渲染的概念，edx-react-app使用rect-intl完成多语言翻译工作。首先需要了解[rect-intl](https://github.com/formatjs/react-intl/wiki)。 edx/frontend-i18n在react-intl上封装了一层，使得可以根据key为openedx-language-preference的cookie, 显示不同语言。



core functionality: 

configure, getPrimaryLanguageSubtag, isRtl, handleRtl, localeSortFunction

getLocale     // 获取当前语言

getMessages   // 获取中英文语句的json



react-intl function:

intlShape, FormattedMessage, defineMessages, IntlProvider, injectIntl



Actions:

setLocale



获取当前语言，获取包含所有中英文语句的object。

import { getLocale, getMessages } from '@edx/frontend-i18n';
<IntlProvider locale={getLocale()} messages={getMessages()}>
</IntlProvider>






#### 2.3 edx/front-end-cookie-cutter-application

edx micro-fronend脚手架，当需要新建项目时，clone这个项目并初始化，我们会得到固定的目录结构，打包流程，然后就可以直接开发业务代码。

# set up the openedx devstack
git clone https://github.com/edx/frontend-cookie-cutter-application.git
cd frontend-cookie-cutter
# Connection with the openedx platform authentication
# this will build and start the frontend-cookie-cutter web application in a docker container
make up-detached
make logs


*通用项目目录*

├── config # Directory for webpack configurations
├── public # Entry point for the single-page application - frontend-cookie-cutter has a single index.html file
├── src
    ├── components # Directory for presentational React components
    ├── containers # Directory for container React components
├── data
    ├──actions # Directory for Redux action creators
    ├──constants
    ├──reducers # Directory for Redux reducers
├── .babelrc
├── .dockerignore
├── .eslintignore
├── .eslintrc.js
├── .gitignore
├── npmignore
├── .travis.yml
├── docker-compose.yml
├── Dockerfile
├── LICENSE
├── Makefile
├── package-lock.json
├── package.json






#### 2.4 gradebook

i版本上已完成。成绩本对应的API在文件 https://github.com/edx/edx-platform/blob/master/lms/djangoapps/grades/api/v1/gradebook_views.py，API将学员的成绩信息用统一的接口返回。

```

Request

GET /api/grades/v1/gradebook/{course_id}/                       - Get gradebook entries for all users in course

GET /api/grades/v1/gradebook/{course_id}/?username={username}   - Get grades for specific user in course

GET /api/grades/v1/gradebook/{course_id}/?username_contains={username_contains}

GET /api/grades/v1/gradebook/{course_id}/?cohort_id={cohort_id}

GET /api/grades/v1/gradebook/{course_id}/?enrollment_mode={enrollment_mode}



Response

* course_id

* email

* user_id

* username

* full_name

* passed: 课程有没有及格

* percent: 成绩排名

* letter_grade: 成绩 (e.g. 'A' 'B' 'C' for 6.002x) or None

* progress_page_url: 用户progress页的链接

* section_breakdown: 课程各个模块的得分详情

```







#### 2.5 共用UI组件

frontend-component-footer

frontend-component-site-header





#### 2.6 frontend-app-account 账号设置页

功能不可用，持续更新中(143commits)











#### 2.7 frontend-app-profile 用户资料页

功能已完成，但还在一直更新。





#### 2.8 frontend-app-learner-portal 课程面板

UI完成，未对接接口，数据为静态数据。









#### 2.9 journals-frontend

【journals-frontend】

一个专门对接https://github.com/edx/journals的前端app。启动报错。

journals-frontend is a single page application written in React/Redux to be used with the Journals Service backend.It communciates with Journals Service via Rest API's, and authenticates through the edx LMS.



journals-frontend main features include:

- Marketing Pages: About and Index pages to display and highlight information about your collection of Journals

- Journal Content Viewing: rendering of Journal pages with html, images, inline pdf's and videos

- Table of Contents: navigable heirarchical content overview

- Full-text search: search and filtering of journal content





#### 2.10 publisher-frontend

作用不详，只有三个页面，持续更新中













#### 2.11 frontend-app-ecommerce

ecommerce相关页面，订单信息，购物车。持续更新中


<Switch>
    <Route path="/orders" component={ConnectedOrderHistoryPage} />
    <Route path="/wip-payments" component={ConnectedPaymentsPage} />
    <Route path="/notfound" component={NotFoundPage} />
    <Route path="*" component={NotFoundPage} />
</Switch>




#### 2.12 fronend-app-program-manager

什么都没有，只是建了个仓库











### 参考资料

- [State of open edx front end](https://openedx2019.sched.com/event/Ktnn/state-of-open-edx-front-end)

- [Appsembelr react-lms](https://github.com/appsembler/react-lms)

- [create-edx-react-app](https://openedx2019.sched.com/event/L6bV/building-open-edx-frontend-applications-with-create-edx-react-app-part-1)

