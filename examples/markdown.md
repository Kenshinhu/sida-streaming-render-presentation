<!-- .slide: data-background="#000000" -->
# 浏览器内核、前端发展与渲染概述



## 渲染引擎浏览器主流内核
- Blink (Google Chrome, Microsoft Edge)   
- WebKit (Safari)
- Gecko (Firefox)
- Trident (旧版 Internet Explorer)
- EdgeHTML (旧版 Microsoft Edge)



## 前端开发简史
<!-- .slide: data-background="#000000" -->
- 1990年代: 静态HTML页面
- 2000年代初: CSS的广泛应用，动态网页技术（如Flash）兴起
- 2005年左右: AJAX技术推动Web 2.0时代
- 2010年代: 响应式设计，单页应用（SPA）兴起
- 2015年后: 现代前端框架（React, Vue, Angular）普及
- 现在: 渐进式Web应用（PWA），WebAssembly等新技术



## 什么是浏览器渲染
<!-- .slide: data-background="#000000" -->
- 定义: 将HTML、CSS和JavaScript转换为用户可以交互的网页的过程


- 关键步骤:
  1. 解析HTML和CSS
  2. 构建DOM和CSSOM
  3. 创建渲染树
  4. 布局计算
  5. 绘制页面



## 浏览器渲染的类型


## 传统渲染 
### (SSR - Server-Side Rendering)
   - 服务器生成完整的HTML
   - 优点: 首次加载快，SEO友好
   - 缺点: 页面刷新慢，服务器负载高



## 客户端渲染 
### (CSR - Client-Side Rendering)
   - 浏览器执行JS来生成内容
   - 优点: 交互性强，后续加载快
   - 缺点: 首次加载慢，SEO挑战


## 客户端渲染 
### (CSR - Client-Side Rendering)
   - 浏览器执行JS来生成内容
   - 优点: 交互性强，后续加载快
   - 缺点: 首次加载慢，SEO挑战


## 混合渲染
### (Hybrid Rendering)
 - 性能优化：为不同类型的内容选择最合适的渲染方式。
 - 灵活性：可以根据具体需求调整渲染策略。
 - SEO友好：确保关键内容可以被搜索引擎爬虫正确索引。
 - 用户体验：提供快速的初始加载和流畅的交互体验。
 - 可扩展性：能够处理各种复杂的应用场



## 现代渲染优化技术


- 渐进式渲染
- 懒加载
- 代码分割
- 预渲染
- 流式服务器渲染 (Streaming Server-Side Rendering)