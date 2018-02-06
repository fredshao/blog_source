---
title: Discourse配置阿里云企业邮箱发邮件
date: 2017-11-20 12:25:36
tags: 服务器配置
---

修改 Containers/app.yml

```yaml
## TODO: List of comma delimited emails that will be made admin and developer
  ## on initial signup example 'user1@example.com,user2@example.com'
  DISCOURSE_DEVELOPER_EMAILS: 'admin@yuming.com'

  ## TODO: The SMTP mail server used to validate new accounts and send notifications
  DISCOURSE_SMTP_ADDRESS: smtp.mxhichina.com
  DISCOURSE_SMTP_PORT: 80
  DISCOURSE_SMTP_USER_NAME: admin@yuming.com
  DISCOURSE_SMTP_PASSWORD: aabbccdd(企业邮箱登陆密码)
  DISCOURSE_SMTP_AUTHENTICATION: login
  DISCOURSE_SMTP_OPENSSL_VERIFY_MODE: none
  DISCOURSE_SMTP_ENABLE_START_TLS: true
```

注意阿里企业邮箱端口必须为80，
DISCOURSE_DEVELOPER_EMAILS与网站管理员保持一致
邮箱登陆密码不要使用#字符

1. 修改完后重建容器：

   ./launcher rebuild app

2. 后台更换notification email，耐心等会就可以用了

   {% asset_img unnamed.jpg %}

