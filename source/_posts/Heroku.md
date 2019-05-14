---
title: Deploy to Heroku
date: 2019-05-14 15:29:10
tags:
  - Heroku
categories:
  - Deploy
---

step1: 前往 [Heroku](https://dashboard.heroku.com/)
step2: Sign in 然後 create an app， app 名稱即為網址內容
step3: 回到專案資料夾，安裝 hexo-deployer-git

```
$ npm install hexo-deployer-git --save
```

step4: 安裝完成到配置檔案 → \_config.yml 設定 deploy 內容

```
deploy:
  type: heroku
  repo: <repository url>
  // <repository url> 去 heroku 的 app setting 中， 找到 Heroku Git URL
```

step5: 要安裝 heroku cli 來登入 heroku

```
$ npm install -g heroku
$ heroku login
```

step6: 再來 deploy 即可

```
$ hexo deploy
```

---

Deploy Error

Error Message:
The 'heroku/nodejs' buildpack is set on this application, but was remote: ! unable to detect a Node.js codebase.

參考 [buildpacks](https://devcenter.heroku.com/articles/buildpacks#detection-failure)
將 buildpacks clear 後再 deploy 即可
