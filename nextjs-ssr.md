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



###
   Code Smarter, Not Harder.
   ![](https://i.ibb.co/Ld5Gw2k/w700d1q75cms.png)