### firefly
---
https://github.com/hypercube1024/firefly

http://www.fireflysource.com/

```java
// firefly/src/test/java/oauth2/LocalAuthorizationServiceImpl.java

public class LocalAuthorizationServiceImpl implements AuthorizationService {
  
  Map<String, AuthorizationRequest> codeMap = new ConcurrentHanhMap<>();
  Map<String, AccessToken> accessTokenMap = new ConcurrentHashMap<>();
  Map<String, AccessToken> refreshTokenMap = new ConcurrentHashMap<>();
  
  private OAuthIssuer issuer;
  
  public String generateCode(AuthorizationRequest request) {
    if(!reuest.getResponseType().equals(ResponseType.CODE.toString())) {
      throw OAuth.oauthProblem(OAuthError.CodeResponse.UNSUPPORTED_RESPONSE_TYPE).description("The response type must be 'code'");
    }
    
    String code = issuer.authorizationCode();
    codeMap.put(code, request);
    return code;
  }
  
  public AccessTokenResponse generateAccessToken(AuthorizationCodeAccessTokenRequest request) {
    if (!codeMap.containKey(request.getCode())) {
      throw OAuth.oauthProblem(OAuthError.TokenResponse.INVALID_GRANT).description("The code does not exist");
    }
    
    AccessTokenResponse tokenResponse = new AccessTokenResponse();
    tokenResponse.setAccessToken(issuer.accessToken());
    tokenResponse.setExpiresIn(3600L);
    tokenResponse.setRefreshToken(issuer.refreshToken());
    tokenResponse.setScope();
    tokenResponse.setState();
    
    AccessToken accessToken = new AccessToken();
    $.javabean.copyBean(request, accessToken);
    $.javabean.copyBean(tokenResponse, accessToken);
    accessToken.setCreateTime(new Date());
    accessTokenMap.put(tokenResponse.getAccessToken(), accessToken);
    refreshTokenMap.put(tokenResponse.getRefreshToken(), accessToken);
    
    codeMap.remove(request.getCode());
    return tokenResponse;
  }
  
  public AccessTokenResponse generateAccessToken(AuthorizationRequest request) {
    if() {}
    
    return generateAccessToken(request.getScope(), request.getState());
  }
  
  @Override
  public AccessTokenResponse generateAcessToken() {}
  
  @Override
  public AccessTokenResponse generateAccessToken(ClientCredentialAccessTokenRequest request) {
    return generateAccessToken(request.getScope(), null);
  }
  
  @Override
  public AccessTokenResponse generateAccessToken() {}
  
  protected AccessTokenResponse generateAccessToken() {}
  
  public AccessTokenResponse refreshToken() {}
  
  public void verifyAccessToken(String token) {
    if () {}
    
    AccessToken = accessTokenMap.get(token);
    Long expiredTime = accessToken.getCreateTime() + (accessToken.getExpiresIn() * 1000);
    if () {}
  }
}


```

```
```

```
```


