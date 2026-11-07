# JustAuth 后端骨架（用于真实登录）

本目录提供一个最小可用的 Spring Boot + JustAuth 后端示例，支持微信、抖音、Google、X (Twitter) 登录。

## 依赖

在 `pom.xml` 中加入：

```xml
<dependency>
    <groupId>me.zhyd.oauth</groupId>
    <artifactId>JustAuth</artifactId>
    <version>1.16.7</version>
</dependency>
<dependency>
    <groupId>com.xkcoding</groupId>
    <artifactId>justauth-spring-boot-starter</artifactId>
    <version>1.4.0</version>
</dependency>
```

## application.yml 配置示例

```yaml
justauth:
  enabled: true
  type:
    WECHAT_OPEN:
      client-id: 你的微信开放平台AppID
      client-secret: 你的微信开放平台AppSecret
      redirect-uri: https://你的域名/oauth/WECHAT_OPEN/callback
    DOUYIN:
      client-id: 你的抖音AppKey
      client-secret: 你的抖音AppSecret
      redirect-uri: https://你的域名/oauth/DOUYIN/callback
    GOOGLE:
      client-id: 你的Google Client ID
      client-secret: 你的Google Client Secret
      redirect-uri: https://你的域名/oauth/GOOGLE/callback
    TWITTER:
      client-id: 你的X/Twitter Client ID
      client-secret: 你的X/Twitter Client Secret
      redirect-uri: https://你的域名/oauth/TWITTER/callback
  cache:
    type: default
```

## 最小 Controller

```java
@RestController
@RequestMapping("/oauth")
@RequiredArgsConstructor
public class OAuthController {
    private final AuthRequestFactory factory;

    @GetMapping("/login/{type}")
    public void login(@PathVariable String type, HttpServletResponse response) throws IOException {
        AuthRequest authRequest = factory.get(type);
        response.sendRedirect(authRequest.authorize(AuthStateUtils.createState()));
    }

    @RequestMapping("/{type}/callback")
    public AuthResponse callback(@PathVariable String type, AuthCallback callback) {
        AuthRequest authRequest = factory.get(type);
        return authRequest.login(callback);
    }
}
```

## 前端对接

前端登录按钮跳转到：

```
https://你的后端域名/oauth/login/WECHAT_OPEN
https://你的后端域名/oauth/login/DOUYIN
https://你的后端域名/oauth/login/GOOGLE
https://你的后端域名/oauth/login/TWITTER
```

回调成功后，后端返回用户信息，前端即可保存并显示。

更多细节参考：
- https://github.com/justauth/JustAuth
- https://github.com/justauth/justauth-spring-boot-starter-demo
