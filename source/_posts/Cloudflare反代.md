---
abbrlink: c6a56fac
categories:
- - 博客
date: '2023-03-11 16:48:25'
description: 我们的站点通常会使用一些CDN来进行加速，例如jsDelivr, UNPKG等，但是它们在境内的加速效果都不是很理想，本篇阐述如何用Cloudflare反代它们以达到提速效果。
plugins:
- indent
tags:
- Cloudflare
title: Cloudflare反代
updated: Sat, 11 Mar 2023 08:48:26 GMT
---
## 前言

我们的站点通常会使用一些CDN来进行加速，例如 [jsDelivr](https://www.jsdelivr.com), [UNPKG](https://unpkg.com) 等，但是它们在境内的加速效果都不是很理想。

## 解决方法

Cloudflare在全球速度都是相对较快的，所以这里选择使用Cloudflare进行反代以上的CDN服务以解决它们在境内速度慢的问题。

> 注：如若没有 [Cloudflare](https://www.cloudflare.com) 账号，要先去注册一个，并与 [GitHub](https://github.com) 连接。

## 源码

**index.html**

```html
<script language="javascript" type="text/javascript">
	window.location.href = 'https://cdn.wndbac.cn';
</script>
```

**_worker.js**

```js
export default {
    async fetch(request, env) {
      let url = new URL(request.url);
      if (url.pathname.startsWith('/')) {
        url.hostname="cdn.jsdelivr.net"; // 需要反代的域名
        let new_request=new Request(url,request);
        return fetch(new_request);
      }
      // 否则，提供静态资产。
      return env.ASSETS.fetch(request);
    }
  };
```

> 注：index.html文件其实即为一个重定向，请将 https://cdn.wndbac.cn 替换为自己的域名或后面Cloudflare分配的域名。

将以上代码导入Cloudflare，然后绑定自己的域名（可无），最后就大功告成了。

反代的 **cdn.jsdelivr.net** 可能用自己的域名或者Cloudflare分配给你的域名会自动跳转到原被反代域名上，此为正常现象（jsDelivr的问题）。

使用：

```
npm: https://yourdomain/npm/package@version/file
GitHub: https://yourdomain/gh/user/repo@version/file
WordPress: https://yourdomain/wp/plugins/project/tags/version/file
```

更多可访问 [jsDelivr](https://www.jsdelivr.com) 官网查看：

{% gallery %}
![jsDelivr](https://cdn.wndbac.cn/gh/wndbac/Static/blog_img/2023/3/image_f05b6c26e4dd9599882c8c06ccb2d0bb.png)
{% endgallery %}

只需将 **cdn.jsdelivr.net** 替换为你部署反代服务的域名即可。

> 同理：反代其它网站也可以使用上述代码，但若别人开启了禁止反代等保护措施，即无效。
