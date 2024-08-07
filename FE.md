## UI
- [tailwind-landing-page-template](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/cruip/tailwind-landing-page-template)：免费、开源的落地页模板。该项目是基于 TailwindCSS、React 和 Next.js 构建的落地页模板，它界面美观、代码简单、设计在线，适用于快速制作公司主页、活动落地页等。
```
git clone 项目
yarn install
yarn dev
# http://localhost:3000
```

<p align="center"><img src='https://raw.githubusercontent.com/521xueweihan/img3/master/hellogithub/97/304350054.gif' style="max-width:80%; max-height=80%;"></img></p>

## Library:

- [swr](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/vercel/swr)：用于数据请求的 React Hooks 库。该项目是帮助开发者简化数据请求逻辑的 React 库，支持自动处理数据的缓存、重验证、错误重试等多种功能，比如当用户重新点击/回到页面时，自动请求接口获取最新数据。
```javascript
import useSWR from 'swr'
 
function Profile() {
  const { data, error, isLoading } = useSWR('/api/user', fetcher)
 
  if (error) return <div>failed to load</div>
  if (isLoading) return <div>loading...</div>
  return <div>hello {data.name}!</div>
}
```

- [undraw-ui](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/readpage/undraw-ui)：基于 Vue 3 的评论组件。这是一个基于 Vue 3 的 UI 组件，提供了评论、内容折叠、回复、表情等功能，以及目录、搜索等组件。来自 [@Mr.King](https://hellogithub.com/user/fUDKIpV5ohlc3qb) 的分享

<p align="center"><img src='https://raw.githubusercontent.com/521xueweihan/img4/master/hellogithub/98/479253212.png' style="max-width:80%; max-height=80%;"></img></p>

- [uppy](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/transloadit/uppy)：易于集成的 JavaScript 文件上传组件。这是一个轻量级的 JavaScript 文件上传组件，它提供了一个美观的用户界面，支持从多个源导入文件、断点续传、国际化，以及预览、编辑和多文件上传的功能。
```javascript
import React, { useEffect } from 'react'
import Uppy from '@uppy/core'
import Webcam from '@uppy/webcam'
import { Dashboard } from '@uppy/react'

const uppy = new Uppy().use(Webcam)

function Component () {
  return <Dashboard uppy={uppy} plugins={['Webcam']} />
}
```

- [Photo-Sphere-Viewer](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/mistic100/Photo-Sphere-Viewer)：用于显示 360° 球体全景的 JavaScript 库。这是一个基于 Three.js 开发的全景照片查看器，提供了友好的交互和丰富的功能。它支持多种全景图格式和功能，包括 2:1 全景图、六面体全景图、全景图分片、显示文本、视频全景等。来自 [@wanzij](https://hellogithub.com/user/QkXB6ugmwMTqteF) 的分享

<p align="center"><img src='https://raw.githubusercontent.com/521xueweihan/img3/master/hellogithub/97/33748729.png' style="max-width:80%; max-height=80%;"></img></p>

- [cmdk](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/pacocoursey/cmdk)：快速、无样式的命令菜单 React 组件。该项目可以帮助开发者轻松实现一个直观且功能丰富的命令菜单，类似于 ⌘K 快捷键唤起的交互式菜单，从而提升用户的交互体验，适用于各种 Web 应用。来自 [@Daaihang Wong](https://hellogithub.com/user/G8ft6na1FH03KEW) 的分享
```typescript
import { Command } from 'cmdk'

const CommandMenu = () => {
  return (
    <Command label="Command Menu">
      <Command.Input />
      <Command.List>
        <Command.Empty>No results found.</Command.Empty>

        <Command.Group heading="Letters">
          <Command.Item>a</Command.Item>
          <Command.Item>b</Command.Item>
          <Command.Separator />
          <Command.Item>c</Command.Item>
        </Command.Group>

        <Command.Item>Apple</Command.Item>
      </Command.List>
    </Command>
  )
}
```

<p align="center"><img src='https://raw.githubusercontent.com/521xueweihan/img3/master/hellogithub/97/514395914.png' style="max-width:80%; max-height=80%;"></img></p>

## CMS
- [strapi](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/strapi/strapi)：全球领先的开源无头 CMS。这是一款完全免费、采用 JavaScript/TypeScript 开发的无头内容管理系统。它拥有开箱即用的 API 和友好的管理面板，自带权限管理、默认安全、SEO 友好等特点。Strapi 作为目前 GitHub 上最流行的开源内容管理系统之一，已成为多家世界 500 强公司的首选 CMS。来自 [@greatYe](https://hellogithub.com/user/5YRq97xhZ1zyUme) 的分享

<p align="center"><img src='https://raw.githubusercontent.com/521xueweihan/img3/master/hellogithub/97/43441403.gif' style="max-width:80%; max-height=80%;"></img></p>

## Team
- [outline](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/outline/outline)：开源的文档和团队知识库管理工具。这是一款用 React 和 Node.js 开发的在线文档编辑和协作工具，它界面美观、功能丰富、兼容 Markdown 的特点，支持中文和 Docker 部署。此外，它还提供了 Windows、macOS、iOS 和 Android 客户端，可作为私人 wiki 或中小型公司的内部文档和知识库平台。

<p align="center"><img src='https://raw.githubusercontent.com/521xueweihan/img3/master/hellogithub/97/59435364.png' style="max-width:80%; max-height=80%;"></img></p>

- [focalboard](https://hellogithub.com/periodical/statistics/click/?target=https://github.com/mattermost/focalboard)：开源的项目管理和团队协作工具。这是一款开源、多语言、自托管的项目管理工具，兼容了 Trello 和 Notion 的特点。它支持看板、表格和日历等视图管理任务，并提供评论同步、文件共享、用户权限等功能。该工具还提供了适用于 Windows、macOS、Linux 系统的客户端。

<p align="center"><img src='https://raw.githubusercontent.com/521xueweihan/img3/master/hellogithub/96/301793434.jpg' style="max-width:80%; max-height=80%;"></img></p>
