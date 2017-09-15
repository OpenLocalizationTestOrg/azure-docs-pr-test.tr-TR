### <span data-ttu-id="44479-101"><a name="server-auth"></a>Nasıl yapılır: Bir sağlayıcı ile (Sunucu Akışı) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="44479-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="44479-102">Mobile Apps hizmetinin uygulamanızdaki kimlik doğrulama işlemini yönetmesi için kimlik sağlayıcınıza uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44479-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="44479-103">Ardından, Azure App Service'te sağlayıcınız tarafından verilen uygulama kimliği ile parolasını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="44479-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span></span>
<span data-ttu-id="44479-104">Daha fazla bilgi için [Uygulamanıza kimlik doğrulaması ekleme](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md) öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="44479-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="44479-105">Kimlik sağlayıcınızı kaydettikten sonra sağlayıcınızın adıyla `.login()` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="44479-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span></span> <span data-ttu-id="44479-106">Örneğin, Facebook ile oturum açmak için aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="44479-106">For example, to login with Facebook use the following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="44479-107">'aad', 'facebook', 'google', 'microsoftaccount' ve 'twitter', sağlayıcı için geçerli değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="44479-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="44479-108">Google Kimlik Doğrulaması şu anda Sunucu Akışı ile çalışmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="44479-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="44479-109">Google kimlik doğrulamasını yapmak için bir [istemci akışı yöntemi](#client-auth) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="44479-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="44479-110">Bu durumda, OAuth 2.0 kimlik doğrulama akışını Azure App Service yönetir.</span><span class="sxs-lookup"><span data-stu-id="44479-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="44479-111">Seçili sağlayıcının oturum açma sayfasını gösterir ve kimlik sağlayıcı ile oturum başarıyla açıldıktan sonra bir App Service kimlik doğrulama belirteci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="44479-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span></span> <span data-ttu-id="44479-112">Oturum açma işlevi tamamlandığında, hem kullanıcı kimliğini hem de App Service kimlik doğrulama belirtecini sırasıyla userId ve authenticationToken alanlarında ortaya çıkaran bir JSON nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="44479-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="44479-113">Bu belirteç önbelleğe alınabilir süresi sona erene kadar yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="44479-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="44479-114"><a name="client-auth"></a>Nasıl yapılır: Bir sağlayıcı ile (İstemci Akışı) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="44479-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="44479-115">Uygulamanız kimlik sağlayıcısı ile bağımsız olarak da iletişim kurabilir ve sonra döndürülen belirteci kimlik doğrulaması için App Service’e döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="44479-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span></span> <span data-ttu-id="44479-116">Bu istemci akışı, kullanıcılar için çoklu oturum açma deneyimi sağlamanıza veya kimlik sağlayıcısından ek kullanıcı verileri almanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="44479-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="44479-117">Sosyal Kimlik Doğrulaması temel örneği</span><span class="sxs-lookup"><span data-stu-id="44479-117">Social Authentication basic example</span></span>

<span data-ttu-id="44479-118">Bu örnekte kimlik doğrulaması için Facebook istemci SDK’sı kullanılır:</span><span class="sxs-lookup"><span data-stu-id="44479-118">This example uses Facebook client SDK for authentication:</span></span>

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
<span data-ttu-id="44479-119">Bu örnek, ilgili sağlayıcı SDK’sı tarafından sağlanan belirtecin belirteç değişkenine depolandığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="44479-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="44479-120">Microsoft Hesabı örneği</span><span class="sxs-lookup"><span data-stu-id="44479-120">Microsoft Account example</span></span>

<span data-ttu-id="44479-121">Aşağıdaki örnekte Microsoft Hesabı kullanarak Windows Mağazası için çoklu oturum açmayı destekleyen Live SDK’sı kullanılır:</span><span class="sxs-lookup"><span data-stu-id="44479-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

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

<span data-ttu-id="44479-122">Bu örnek, Live Connect’ten, oturum açma işlevi çağrılarak App Service hizmetinize sunulan bir belirteç alır.</span><span class="sxs-lookup"><span data-stu-id="44479-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span></span>

###<span data-ttu-id="44479-123"><a name="auth-getinfo"></a>Nasıl yapılır: Kimliği doğrulanmış kullanıcı hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="44479-123"><a name="auth-getinfo"></a>How to: Obtain information about the authenticated user</span></span>

<span data-ttu-id="44479-124">Kimlik doğrulama bilgileri, herhangi bir AJAX kitaplığı ile HTTP çağrısı kullanılarak `/.auth/me` uç noktasından alınabilir.</span><span class="sxs-lookup"><span data-stu-id="44479-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="44479-125">`X-ZUMO-AUTH` üst bilgisini kimlik doğrulama belirtecinize ayarlandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="44479-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span></span>  <span data-ttu-id="44479-126">Kimlik doğrulama belirteci `client.currentUser.mobileServiceAuthenticationToken` içine depolanır.</span><span class="sxs-lookup"><span data-stu-id="44479-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="44479-127">Örneğin, fetch API’sini kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="44479-127">For example, to use the fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

<span data-ttu-id="44479-128">Fetch, [bir npm paketi](https://www.npmjs.com/package/whatwg-fetch) olarak mevcuttur veya [CDNJS](https://cdnjs.com/libraries/fetch)’den tarayıcı ile indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="44479-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="44479-129">Bilgileri getirmek için jQuery veya başka bir AJAX API’si de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44479-129">You could also use jQuery or another AJAX API to fetch the information.</span></span>  <span data-ttu-id="44479-130">Veriler bir JSON nesnesi olarak alınır.</span><span class="sxs-lookup"><span data-stu-id="44479-130">Data is received as a JSON object.</span></span>
