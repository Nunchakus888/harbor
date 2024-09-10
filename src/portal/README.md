![Harbor UI](https://raw.githubusercontent.com/goharbor/website/master/docs/img/readme/harbor_logo.png)

Harbor UI
============
This is the project based on Clarity and Angular to build Harbor UI.

### Nginx routing configuration

> nginx会分流静态资源和API请求，分别请求对应的nginx转发path节点
> so，客户端需要根据nginx配置的转发path节点来请求对应的资源以及API
> 例如：/ 会被nginx转发到 `/cluster-center/edge/harbor`
> 所以，客户端需要请求 `/cluster-center/edge/harbor/` 来获取资源
> API请求也是同理

* 前端静态资源请求路径：`/cluster-center/dynamic/xxx/` 配置如：下 https://stackoverflow.com/questions/48347430/dynamic-location-of-assets-in-angular

```
<base href="./" />

ng build --aot --base-href ./

```

* 路由配置增加 路由prefix

```

{ provide: APP_BASE_HREF, useValue: basePath },

basePath = location.pathname;

```

* Api请求增加 prefix, todo..



Start
============
1. npm install (should trigger 'npm postinstall')
2. npm run postinstall  (if not triggered, manually run this step)
3. copy "proxy.config.mjs.temp" file to "proxy.config.mjs"                 
   `cp proxy.config.mjs.temp proxy.config.mjs`
4. Modify "proxy.config.mjs" to specify a Harbor server. And you can specify the agent if you work behind a corporate proxy
5. npm run start
6. open your browser on https://localhost:4200

