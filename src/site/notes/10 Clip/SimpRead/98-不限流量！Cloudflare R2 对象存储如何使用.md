---
{"title":"[转载]不限流量！Cloudflare R2 对象存储如何使用","tags":["simpread","clipping"],"dg-publish":true,"permalink":"/10-clip/simp-read/98-cloudflare-r2/","dgPassFrontmatter":true}
---



- 🗒️**File Info**
- 📋转载日期: 2024-05-08 21:04:49
- 🔗原文链接: [不限流量！Cloudflare R2 对象存储如何使用](https://juejin.cn/post/7331584783611281444)
- 📑原文标题: 不限流量！Cloudflare R2 对象存储如何使用
- 🤵作者: juejin.cn
- 🏡源站: juejin.cn
- 📃简介: 对象存储相信很多人都有所耳闻，例如腾讯云 COS、阿里云 OSS、七牛云 KODO 等。那么，为什么我们还要使用 Cloudflare R2 呢？答案在于它拥有独特的优势：不限访问流量。


>本文由 [10k](https://tenthousand.cn) 使用 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址: [不限流量！Cloudflare R2 对象存储如何使用](https://juejin.cn/post/7331584783611281444)
对象存储相信很多人都有所耳闻，例如腾讯云 COS、阿里云 OSS、七牛云 KODO 等。那么，为什么我们还要使用 Cloudflare R2 呢？答案在于它拥有独特的优势：不限访问流量。

对于对象存储来说，流量费用是一项不小的支出。Cloudflare 直接免除流量费用，堪称慈善大佛。不过，我们也不要过度薅羊毛。前几天，某网友在 X 上发布帖子，称自己因为一个月消耗了 1PB 流量，差点被封号。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/44a5016321844a159e3402d10f0b01be~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1170&h=2507&s=283568&e=jpg&b=131313)

一个月 1PB 流量，1.43 亿请求数，平均每天 50TB 流量。1PB 什么概念？来看看 1PB 流量在阿里云要多少大洋。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5d0ce5a80606410da4dcf3893a510ee8~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1672&h=1146&s=169851&e=png&b=fefefe)

差不多到 43W，太恐怖了！慈善公司也不能这么玩呀。后面作者作出解释，是由于某知名成人社区用来当官方图床了，咳，看来类似网站的需求量很大嘛。

上面提到了流量费也仅仅是 CDN 的费用，实际其他对象存储服务还会有 CDN 回源的流量费和存储容量费，按 1PB 来算也是一笔巨款。那么，Cloudflare R2 是怎么收费的？来看看下图：

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4e2419e405864f5ebe8ba8dd083f4d53~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1396&h=412&s=65976&e=png&b=1d1f20)

Cloudflare R2 主要靠存储容量收费，10G 以内是免费的，对于写写博客做个图床完全是够用的。就算是收费也不贵，100G 差不多也就 10 大洋多点。A 类操作和 B 类操作是指一些读写操作，应该没有多少网站能超过这个数。总的来说，的确够实惠。

那要怎么使用呢？首先你得有个 Cloudflare 账号，怎么注册就不说了，相信不会有什么难度。直接来看看创建一个存储桶：

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7a6f4a81d3514e56b2219b18cd087e5a~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=2056&h=996&s=162670&e=png&b=fefefe)

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ba4222adc3cf40a0badddd4738ba826b~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1732&h=1442&s=219384&e=png&b=fefefe)

1.  登录后，切换到 R2 页面；
2.  点击创建存储桶；
3.  填写一个名称，然后创建就完成了。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3a9f313629fd4855bea36f8b7ff1e8b0~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=2212&h=1232&s=148536&e=png&b=fefefe)

默认情况下，没有配置域名是不可用链接访问资源的，可以在设置里面启用 r2.dev 访问。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e757282bb29241919a91ec5323694f85~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=2224&h=1158&s=208937&e=png&b=ffffff)

然后在对象文件详情里面就能看到访问链接了。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/85ff8300b492435fb56a886ea8b1b855~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=2192&h=1070&s=105114&e=png&b=ffffff)

如果你有自己的域名，并且由 Cloudflare 管理，还可以使用自定义域名。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e4321656acc24e309cd53d8a2a7d584a~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=2226&h=1370&s=188281&e=png&b=fffefe)

作为程序员，当然要考虑怎么用代码实现上传、读取、删除等操作。官方提供了 2 种操作方式，包括 Workers API 和 S3 SDK。

## Workers API

Cloudflare Workers 是一个服务器托管的执行环境，可以在全球分布的 Cloudflare 数据中心中运行 JavaScript 代码。

### 创建项目

运行下面的指令创建项目，按照提示操作即可。

```
npm create cloudflare@latest


```

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1137c67606df4801a6be346f77b1c7f7~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1460&h=932&s=177780&e=png&b=1f1f1f)

### 配置

新建项目下面已经包含配置模板，只要配置帐户 ID 和存储桶名称即可。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/caba435f87bc44cdb483e370a26a4009~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1464&h=750&s=186477&e=png&b=1e1e1e)

账户 ID 可以在页面右上角找到。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1e6a0c6f4dfd4525bf39a88ea1af5eab~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=2878&h=1376&s=330917&e=png&b=fefefe)

### 代码编写

```
export default {
  async fetch(request: Request, env: Env) {
    const url = new URL(request.url)
    const key = url.pathname.slice(1)

    switch (request.method) {
      case 'PUT':
        await env.MY_BUCKET.put(key, request.body)
        return new Response(`Put ${key} successfully!`)
      // 省略其他操作
    }
  },
}


```

代码编写完成之后，使用`npm run deploy`部署。部署成功，通过域名加文件名称作路径即可上传。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f1e15c54dd0f469c982ee6956f212de4~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1926&h=1072&s=134677&e=png&b=fcfcfc)

## S3

R2 实现了 AWS S3 API，也就是可以直接使用 AWS S3 对象存储服务的 SDK。通过 S3 API 可以直接调用操作，在调用之前先要创建 API 令牌。

在账户 ID 下面找到_管理 R2 API 令牌_，进入创建 API 令牌。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3366c0ce6be04213aed0230b2c48c409~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=2222&h=1490&s=213598&e=png&b=ffffff)

创建完成之后，保留下这些参数。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3f5a38bbf2fa47c8bed2cfc2a3ffb802~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=2240&h=1352&s=175759&e=png&b=fdfdfd)

然后可以使用 Nodejs 进行调用上传。

```
import { S3Client, PutObjectCommand } from '@aws-sdk/client-s3'

const S3 = new S3Client({
  region: 'auto',
  endpoint: `https://${ACCOUNT_ID}.r2.cloudflarestorage.com`,
  credentials: {
    accessKeyId: ACCESS_KEY_ID,
    secretAccessKey: SECRET_ACCESS_KEY,
  },
})

const input = {
  Body: 'file content',
  Bucket: 'web',
  Key: '1.png',
}

const command = new PutObjectCommand(input)
const response = await S3.send(command)


```

上传调用也很简单。这里就不详细介绍每个要点，有需要的可以自行查阅文档。