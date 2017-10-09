### <span data-ttu-id="df4f0-101"><a name="server-auth"></a>Nasıl yapılır: Bir sağlayıcı ile (Sunucu Akışı) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="df4f0-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="df4f0-102">Merhaba kimlik doğrulama işlemi, uygulamanızda toohave mobil uygulamaları yönetme, kimlik sağlayıcınız ile uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="df4f0-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="df4f0-103">Sonra Azure App Service'te tooconfigure hello uygulama Kimliğini ve parolasını sağlayıcınız tarafından sağlanan yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="df4f0-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="df4f0-104">Merhaba öğretici daha fazla bilgi için bkz [Ekle kimlik doğrulama tooyour uygulama](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="df4f0-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="df4f0-105">Kimlik sağlayıcınızı kaydettiğinizde, hello çağrı `.login()` sağlayıcınızın hello adla yöntemi.</span><span class="sxs-lookup"><span data-stu-id="df4f0-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="df4f0-106">Örneğin, Facebook ile toologin koddan hello kullan:</span><span class="sxs-lookup"><span data-stu-id="df4f0-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="df4f0-107">Merhaba geçerli hello sağlayıcısı için 'aad', 'facebook', 'google', 'microsoftaccount' ve 'twitter' değerleridir.</span><span class="sxs-lookup"><span data-stu-id="df4f0-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="df4f0-108">Google Kimlik Doğrulaması şu anda Sunucu Akışı ile çalışmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="df4f0-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="df4f0-109">tooauthenticate Google ile kullanmalıdır bir [istemci akışı yöntemi](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="df4f0-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="df4f0-110">Bu durumda, Azure App Service hello OAuth 2.0 kimlik doğrulaması akışı yönetir.</span><span class="sxs-lookup"><span data-stu-id="df4f0-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="df4f0-111">Merhaba seçili sağlayıcı hello oturum açma sayfasını görüntüler ve hello kimlik sağlayıcısı ile başarılı oturum açma işleminden sonra bir uygulama hizmeti kimlik doğrulama belirteci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="df4f0-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="df4f0-112">Merhaba oturum açma işlevini tamamlandığında, hello kullanıcı kimliği ve uygulama hizmeti sunan bir JSON nesnesi kimlik doğrulama belirteci hello UserID ve authenticationToken alanları sırasıyla verir.</span><span class="sxs-lookup"><span data-stu-id="df4f0-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="df4f0-113">Bu belirteç önbelleğe alınabilir süresi sona erene kadar yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="df4f0-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="df4f0-114"><a name="client-auth"></a>Nasıl yapılır: Bir sağlayıcı ile (İstemci Akışı) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="df4f0-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="df4f0-115">Uygulamanızı bağımsız olarak da hello kimlik sağlayıcısı başvurun ve kimlik doğrulaması için belirteç tooyour uygulama hizmeti hello döndürülen sağlayın.</span><span class="sxs-lookup"><span data-stu-id="df4f0-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="df4f0-116">Bu istemci akışı tooprovide bir tek oturum açma deneyimi için kullanıcılar veya hello kimlik sağlayıcısı tooretrieve ek kullanıcı verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="df4f0-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="df4f0-117">Sosyal Kimlik Doğrulaması temel örneği</span><span class="sxs-lookup"><span data-stu-id="df4f0-117">Social Authentication basic example</span></span>

<span data-ttu-id="df4f0-118">Bu örnekte kimlik doğrulaması için Facebook istemci SDK’sı kullanılır:</span><span class="sxs-lookup"><span data-stu-id="df4f0-118">This example uses Facebook client SDK for authentication:</span></span>

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
<span data-ttu-id="df4f0-119">Bu örnek Hello ilgili sağlayıcı tarafından SDK hello belirteci değişkende depolanır sağlanan hello belirtecini varsayar.</span><span class="sxs-lookup"><span data-stu-id="df4f0-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="df4f0-120">Microsoft Hesabı örneği</span><span class="sxs-lookup"><span data-stu-id="df4f0-120">Microsoft Account example</span></span>

<span data-ttu-id="df4f0-121">örnek kullanımları aşağıdaki hello Microsoft Account kullanarak çoklu oturum açma için Windows mağazası uygulamaları destekler Live SDK hello:</span><span class="sxs-lookup"><span data-stu-id="df4f0-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

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

<span data-ttu-id="df4f0-122">Bu örnek bir belirteç Canlı Connect'ten hello oturum açma işlevini çağırarak sağlanan tooyour uygulama hizmeti olduğu alır.</span><span class="sxs-lookup"><span data-stu-id="df4f0-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="df4f0-123"><a name="auth-getinfo"></a>Nasıl yapılır: hello kimliği doğrulanmış kullanıcı hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="df4f0-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="df4f0-124">Merhaba kimlik doğrulama bilgilerini hello alınabilir `/.auth/me` bir HTTP kullanarak uç noktasını herhangi bir AJAX kitaplığı ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="df4f0-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="df4f0-125">Merhaba ayarladığınız olun `X-ZUMO-AUTH` üstbilgi tooyour kimlik doğrulama belirteci.</span><span class="sxs-lookup"><span data-stu-id="df4f0-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="df4f0-126">Merhaba kimlik doğrulama belirteci depolanan `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="df4f0-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="df4f0-127">Örneğin, toouse hello fetch API:</span><span class="sxs-lookup"><span data-stu-id="df4f0-127">For example, toouse hello fetch API:</span></span>

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

<span data-ttu-id="df4f0-128">Fetch, [bir npm paketi](https://www.npmjs.com/package/whatwg-fetch) olarak mevcuttur veya [CDNJS](https://cdnjs.com/libraries/fetch)’den tarayıcı ile indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="df4f0-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="df4f0-129">JQuery veya başka bir AJAX API toofetch hello bilgileri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df4f0-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="df4f0-130">Veriler bir JSON nesnesi olarak alınır.</span><span class="sxs-lookup"><span data-stu-id="df4f0-130">Data is received as a JSON object.</span></span>
