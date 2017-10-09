### <a name="server-auth"></a>Nasıl yapılır: Bir sağlayıcı ile (Sunucu Akışı) kimlik doğrulaması
Merhaba kimlik doğrulama işlemi, uygulamanızda toohave mobil uygulamaları yönetme, kimlik sağlayıcınız ile uygulamanızı kaydetmeniz gerekir. Sonra Azure App Service'te tooconfigure hello uygulama Kimliğini ve parolasını sağlayıcınız tarafından sağlanan yeterlidir.
Merhaba öğretici daha fazla bilgi için bkz [Ekle kimlik doğrulama tooyour uygulama](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

Kimlik sağlayıcınızı kaydettiğinizde, hello çağrı `.login()` sağlayıcınızın hello adla yöntemi. Örneğin, Facebook ile toologin koddan hello kullan:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

Merhaba geçerli hello sağlayıcısı için 'aad', 'facebook', 'google', 'microsoftaccount' ve 'twitter' değerleridir.

> [!NOTE]
> Google Kimlik Doğrulaması şu anda Sunucu Akışı ile çalışmamaktadır.  tooauthenticate Google ile kullanmalıdır bir [istemci akışı yöntemi](#client-auth).

Bu durumda, Azure App Service hello OAuth 2.0 kimlik doğrulaması akışı yönetir.  Merhaba seçili sağlayıcı hello oturum açma sayfasını görüntüler ve hello kimlik sağlayıcısı ile başarılı oturum açma işleminden sonra bir uygulama hizmeti kimlik doğrulama belirteci oluşturur. Merhaba oturum açma işlevini tamamlandığında, hello kullanıcı kimliği ve uygulama hizmeti sunan bir JSON nesnesi kimlik doğrulama belirteci hello UserID ve authenticationToken alanları sırasıyla verir. Bu belirteç önbelleğe alınabilir süresi sona erene kadar yeniden kullanılabilir.

###<a name="client-auth"></a>Nasıl yapılır: Bir sağlayıcı ile (İstemci Akışı) kimlik doğrulaması

Uygulamanızı bağımsız olarak da hello kimlik sağlayıcısı başvurun ve kimlik doğrulaması için belirteç tooyour uygulama hizmeti hello döndürülen sağlayın. Bu istemci akışı tooprovide bir tek oturum açma deneyimi için kullanıcılar veya hello kimlik sağlayıcısı tooretrieve ek kullanıcı verileri sağlar.

#### <a name="social-authentication-basic-example"></a>Sosyal Kimlik Doğrulaması temel örneği

Bu örnekte kimlik doğrulaması için Facebook istemci SDK’sı kullanılır:

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
Bu örnek Hello ilgili sağlayıcı tarafından SDK hello belirteci değişkende depolanır sağlanan hello belirtecini varsayar.

#### <a name="microsoft-account-example"></a>Microsoft Hesabı örneği

örnek kullanımları aşağıdaki hello Microsoft Account kullanarak çoklu oturum açma için Windows mağazası uygulamaları destekler Live SDK hello:

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

Bu örnek bir belirteç Canlı Connect'ten hello oturum açma işlevini çağırarak sağlanan tooyour uygulama hizmeti olduğu alır.

###<a name="auth-getinfo"></a>Nasıl yapılır: hello kimliği doğrulanmış kullanıcı hakkında bilgi edinin

Merhaba kimlik doğrulama bilgilerini hello alınabilir `/.auth/me` bir HTTP kullanarak uç noktasını herhangi bir AJAX kitaplığı ile çağırın.  Merhaba ayarladığınız olun `X-ZUMO-AUTH` üstbilgi tooyour kimlik doğrulama belirteci.  Merhaba kimlik doğrulama belirteci depolanan `client.currentUser.mobileServiceAuthenticationToken`.  Örneğin, toouse hello fetch API:

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

Fetch, [bir npm paketi](https://www.npmjs.com/package/whatwg-fetch) olarak mevcuttur veya [CDNJS](https://cdnjs.com/libraries/fetch)’den tarayıcı ile indirilebilir. JQuery veya başka bir AJAX API toofetch hello bilgileri de kullanabilirsiniz.  Veriler bir JSON nesnesi olarak alınır.
