概要
---
Docker上でVue.jsの開発環境構築〜デモアプリ作成まで。

今更ながらVue.js触ったこと無かったので、個人学習用。

Dockerfile、docker-compose.ymlを用意
---

Dockerfile
***
```

FROM node:14.4.0-alpine

WORKDIR /usr/src/app

RUN apk update && \
    npm install -g npm @vue/cli
    
```

docker-compose.yml
***
```
version: '3'

services:
    vue:
        container_name: vue
        build: ./docker
        ports:
            - 9050:9050
        privileged: true
        volumes:
            - ./server:/usr/src/app
        tty: true
        stdin_open: true
        command: /bin/sh

```

docker構築、起動
---
```
$ docker-compose up -d
```

コンテナに入る
---
```
$ docker-compose exec vue sh
```

vueプロジェクト作成
---
```
vue create project_name
```
何回か選択項目があるが、

`preset`は`default`

`package manager`は`NPM`

を選択

ポートの設定を変更
---
Vueのプロジェクトディレクトリに`vue.config.js`を作成

portを`9050`に変更。
```
module.exports = {
	devServer: {
		port: 9050,
		host: '0.0.0.0',
		disableHostCheck: true,
	},
};
```

開発サーバー起動
---
```
# npm run serve
```
`http://localhost:9050/`にアクセスしてページが表示されればOK
