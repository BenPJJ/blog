# SPA（单页应用）理解

## 1. 什么是SPA

SPA（single page application）仅在Web 页面**初始化**时加载相应的*HTML、JavaScript、CSS*。

一旦页面加载完成，SPA **不会**因为用户的操作而进行*页面的重新加载或跳转*；取而代之的是*利用路由机制实现HMLT 内容的变换，UI 与用户的交互*，避免页面的重新加载。

**优点**

1. 具有桌面应用的即时性、网站的可移植性和可访问性
2. 用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染
3. 基于上面一点，SPA 相对对服务器压力小
4. 良好的前后端分离，分工更明确

**缺点**

1. 首次渲染速度相对较慢
   - 为实现页面Web 应用功能及显示效果，需要在加载页面的时候将JavaScript、CSS 统一加载，部分页面按需加载；
2. 前进后退路由管理
   - 由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理；
3. 不利于搜索引擎的抓取
   - 由于所有的内容都在一个页面中动态替换显示，所以在SEO 上其有着天然的弱势。
4. SEO 难度较大：由于所有的内容都在一个页面中动态替换显示，所以在SEO 上其有着天然的弱势

## 2. SPA vs MPA(多页面)

MPA（multipage page application），每个页面都是一个主页面，都是独立的；

当我们在访问另一个页面的时候，都需要重新加载html、css、js文件，公共文件则根据需求按需加载

|                 | 单页面应用（SPA）         | 多页面应（MPA）                     |
| --------------- | ------------------------- | ----------------------------------- |
| 组成            | 一个主页面和多个页面片段  | 多个主页面                          |
| 刷新方式        | 局部刷新                  | 整个刷新                            |
| url模式         | 哈希模式                  | 历史模式                            |
| SEO搜索引擎优化 | 难实现，可使用SSR方式改善 | 容易实现                            |
| 数据传递        | 容易                      | 通过url、cookie、localStorage等传递 |
| 页面切换        | 速度快，用户体验良好      | 切换加载资源，速度慢，用户体验差    |
| 维护成本        | 相对容易                  | 相对复杂                            |

