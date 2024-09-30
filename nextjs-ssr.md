# 流式服务器渲染 (SSSR)


### Next.js 

   Next.js 是一个用于构建 React 应用的流行框架，由 Vercel 公司开发和维护。

   它提供了一套强大的工具和功能，使得构建高性能、可扩展的 Web 应用变得更加简单和高效。


### 
   ![Vercel](https://cdn.intuji.com/2022/06/Logo_Vercel-1.jpg)


   Vercel 是一家领先的云平台公司，专注于为开发者提供现代 web 应用的构建、部署和扩展服务。


### 
![](https://rauchg.com/images/rauchg-3d4cecf.jpg)
   <font size="4">由阿根廷裔程序员 Guillermo Rauch（吉列尔莫·劳赫） 于 2015 年创立，最初名为 ZEIT。Rauch 是一位著名的开源贡献者，曾创建多个影响深远的项目，如实时应用框架 Socket.io 和 MongoDB ODM Mongoose。
   他还是 Next.js 的创始人，这个 React 框架彻底改变了前端开发方式。
   在Rauch领导下，Vercel 不仅推动了 JAMstack 架构的普及，还通过其平台和开源项目显著提升了 web 开发的效率和性能。</font>


### Next.js 的工作原理
   建立在 React 之上并提供了额外的结构和优化:

   - 页面概念：每个 JavaScript 文件成为一个路由。
   - 构建时优化：预渲染页面，生成优化的静态资源。
   - 运行时优化：按需加载代码，实现快速导航。
   - 服务器端逻辑：支持在服务器端执行数据获取和处理。


### Next.js 流式服务器渲染 (Streaming Server-Side Rendering)

流式服务器渲染是 Next.js 13 引入的一项创新技术，它改变了传统的服务器端渲染 (SSR) 方式。这种技术允许服务器以流的形式逐步发送页面内容到客户端，而不是等待所有内容准备就绪后一次性发送。


### 
   ![](https://nextjs.org/_next/image?url=%2Flearn%2Fdark%2Fserver-rendering-with-streaming.png&w=3840&q=75)
   一种数据传输技术，允许您将路由分解为更小的“块”，并在准备就绪时将它们逐步从服务器流式传输到客户端。


###
   ![](https://nextjs.org/_next/image?url=%2Flearn%2Fdark%2Fserver-rendering-with-streaming-chart.png&w=3840&q=75)
   通过流式服务器渲染，您可以防止缓慢的数据请求阻塞整个页面。这允许用户查看页面的部分内容并与之交互，而无需等待所有数据加载后再向用户显示任何 UI。


### 流式 SSR 的工作原理详解

1. 初始请求处理:
   - 服务器接收到请求后,立即开始生成页面的静态部分。
   - 同时,启动异步数据获取过程。

2. 流式传输:
   - 服务器使用 `renderToPipeableStream` API 创建一个可流式传输的 React 树。
   - 页面的 HTML 骨架和静态内容首先被发送到客户端。


3. 数据填充:
   - 随着异步数据的获取完成,服务器生成相应的 HTML 片段。
   - 这些片段通过同一个 HTTP 连接流式传输到客户端。

4. 客户端处理:
   - 浏览器逐步接收和渲染这些 HTML 片段。
   - React 在客户端进行 hydration,使页面变得可交互。


5. 完成加载:
   - 所有内容加载完成后,页面完全可交互。


## 性能指标解析

### TTFB (Time to First Byte) 首字节时间
- 定义: 从浏览器发起请求到接收服务器响应的第一个字节所需的时间
- 重要性: 反映服务器响应速度和网络状况
- SSSR影响: 显著缩短,因为服务器可以立即开始发送初始HTML


### FCP (First Contentful Paint) 首次内容绘制
- 定义: 页面开始加载到页面内容的任何部分在屏幕上完成渲染的时间
- 重要性: 表示用户何时能看到页面上的实际内容
- SSSR影响: 大幅提前,用户更快看到有意义的内容


### TTI (Time to Interactive) 可交互时间
- 定义: 页面从开始加载到能够快速、可靠地响应用户输入所需的时间
- 重要性: 反映页面何时真正可用
- SSSR影响: 虽然完全可交互时间可能相似,但用户可以更早部分交互


## 性能对比: SSR vs SSSR

| 指标 | 传统 SSR | 流式 SSR |
|------|---------|----------|
| TTFB | 较慢 (等待所有数据) | 更快 (立即开始传输) |
| FCP  | 较慢 | 更快 (内容逐步显示) |
| TTI  | 较慢 | 逐步变得可交互 |
| 内存使用 | 较高 | 较低 |
| 服务器负载 | 较高 | 较低 |


### 实际案例性能提升
在一个包含复杂数据的电商网站首页上,使用流式 SSR 后:
- TTFB 改善了 40%
- FCP 提前了 2 秒
- 整体加载时间减少了 30%


### SSSR 性能优势
- 更快的初始加载: 用户更快看到页面内容
- 改善的用户体验: 页面内容逐步显示,体验更流畅
- 更好的服务器性能: 减少内存使用,提高并发处理能力
- 保持 SEO 优势: 仍然是服务器端渲染,有利于搜索引擎优化


## 传统 SSR vs 流式 SSR

### 传统 SSR
服务器需要等待所有数据获取和页面渲染完成。
整个页面作为一个完整的 HTML 文档一次性发送。
可能导致较长的首字节时间 (TTFB)。


###  流式 SSR

服务器立即开始发送页面的静态部分。
动态内容在准备好后逐步流式传输。
显著减少 TTFB，提高用户感知的加载速度。


## 流式 SSR 的优势

- 更快的初始加载：用户可以更快地看到页面的初始内容。
- 改善的用户体验：页面内容逐步显示，提供更流畅的体验。
- 更好的服务器性能：减少服务器内存使用，提高并发处理能力。
- 保持 SEO 优势：仍然是服务器端渲染，保持了 SEO 的优势。


## 在Nextjs 中 实现流式 SSR


   一般使用方法
   - Next.js 利用 React 18 的 Suspense 和 lazy 特性实现流式 SSR：
   ```
   import { Suspense } from 'react';
   import Loading from './Loading';

   const DynamicComponent = lazy(() => import('./DynamicComponent'));

   function Page() {
   return (
      <div>
         <h1>My Page</h1>
         <Suspense fallback={<Loading />}>
         <DynamicComponent />
         </Suspense>
      </div>
   );
   }
   ```


###
   组件使用
   - Next.js 13 引入了 loading.js 文件，可以为整个路由段提供加载 UI：

   ```
   // app/dashboard/loading.js
      export default function Loading() {
      return <p>Loading dashboard...</p>
      }
   ```


###
   流式数据获取
   ```
   import { Suspense } from 'react';
   import { use } from 'react';

   function Profile() {
   const data = use(fetchProfileData());
   return <h1>{data.name}</h1>;
   }

   export default function Page() {
   return (
      <Suspense fallback={<p>Loading profile...</p>}>
         <Profile />
      </Suspense>
   );
   }
   ```


## 性能对比: SSR vs SSSR

| 指标 | 传统 SSR | 流式 SSR |
|------|---------|----------|
| TTFB (Time to First Byte) | 较慢 (等待所有数据) | 更快 (立即开始传输) |
| FCP (First Contentful Paint) | 较慢 | 更快 |
| TTI (Time to Interactive) | 较慢 | 逐步变得可交互 |
| 内存使用 | 较高 | 较低 |
| 服务器负载 | 较高 | 较低 |

实际案例: 在一个包含复杂数据的电商网站首页上,使用流式 SSR 后:
- TTFB 改善了 40%
- FCP 提前了 2 秒
- 整体加载时间减少了 30%



###
   Code Smarter, Not Harder.
   ![](https://mirror-boss.oss-cn-shenzhen.aliyuncs.com/image/w700d1q75cms.jpg)



###
   Repository
   [https://github.com/Kenshinhu/sida-streaming-render-presentation](https://github.com/Kenshinhu/sida-streaming-render-presentation)



###
   谢谢大家的聆听，有任何问题欢迎大家提问
