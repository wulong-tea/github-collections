
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
