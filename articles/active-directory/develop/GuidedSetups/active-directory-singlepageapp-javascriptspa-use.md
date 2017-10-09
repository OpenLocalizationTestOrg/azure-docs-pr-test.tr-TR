---
title: "aaaAzure AD v2 JS SPA destekli Kurulumu - kullanım | Microsoft Docs"
description: "JavaScript SPA uygulamaları Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="fd61b-103">Merhaba Microsoft kimlik doğrulama kitaplığı (MSAL) toosign bileşenini hello kullanıcı kullanın</span><span class="sxs-lookup"><span data-stu-id="fd61b-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="fd61b-104">Adlı bir dosya oluşturun `app.js`.</span><span class="sxs-lookup"><span data-stu-id="fd61b-104">Create a file named `app.js`.</span></span> <span data-ttu-id="fd61b-105">Visual Studio, select hello proje (Proje kök klasöründe) kullanıyorsanız, sağ tıklatın ve seçin: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="fd61b-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="fd61b-106">Aşağıdaki kodu tooyour hello eklemek `app.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="fd61b-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="fd61b-107">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="fd61b-107">More Information</span></span>

<span data-ttu-id="fd61b-108">Bir kullanıcı hello tıklattıktan sonra *'Microsoft Graph API çağrısı'* hello ilk kez düğmesi `callGraphApi` yöntem çağrılarını `loginRedirect` toosign hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="fd61b-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="fd61b-109">Bu yöntem hello kullanıcı toohello yeniden yönlendirme sonucu *Microsoft Azure Active Directory v2 endpoint* tooprompt ve hello kullanıcının kimlik bilgilerini doğrulama.</span><span class="sxs-lookup"><span data-stu-id="fd61b-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="fd61b-110">Bir başarılı oturum açma sonucu olarak, hello kullanıcının yeniden yönlendirilen geri toohello özgün olduğu *index.html* sayfası ve bir belirteç alındığında, tarafından işlenen `msal.js` ve hello belirtecinde yer alan hello bilgileri önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="fd61b-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="fd61b-111">Bu belirteç hello adlandırılıyor *kimliği belirteci* ve hello kullanıcı görünen adı gibi hello kullanıcı hakkındaki temel bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="fd61b-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="fd61b-112">Toouse düşünüyorsanız toomake bu belirteç belirteci Merhaba, arka uç sunucu tooguarantee tarafından doğrulandığından emin gereken herhangi bir amaçla bu belirteç tarafından sağlanan herhangi bir veri tooa geçerli kullanıcı, uygulamanız için verilmiş.</span><span class="sxs-lookup"><span data-stu-id="fd61b-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="fd61b-113">Merhaba bu kılavuzu tarafından oluşturulan SPA yapmaz doğrudan hello kimliği belirteci kullanın-bunun yerine, çağıran `acquireTokenSilent` ve/veya `acquireTokenRedirect` tooacquire bir *erişim belirteci* tooquery hello Microsoft Graph API kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fd61b-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="fd61b-114">Merhaba kimliği belirteci doğrular bir örnek gerekiyorsa, bir göz atalım [bu](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 örnek") örnek uygulama github'da – hello örnek kullanır bir ASP.NET Web API belirteci doğrulama için.</span><span class="sxs-lookup"><span data-stu-id="fd61b-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="fd61b-115">Kullanıcı etkileşimli olarak belirteci alma</span><span class="sxs-lookup"><span data-stu-id="fd61b-115">Getting a user token interactively</span></span>

<span data-ttu-id="fd61b-116">Oturum açma Hello sonra ilk, hello istiyor musunuz toorequest ihtiyaç duydukları her zaman kullanıcılar tooreauthenticate belirteci tooaccess bir kaynak – böylece isteyin *acquireTokenSilent* olmalıdır hello zaman tooacquire belirteçleri çoğu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fd61b-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="fd61b-117">Durumlar vardır ancak kullanıcıların Azure Active Directory v2 noktayla – etkileşim tooforce gereken bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fd61b-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="fd61b-118">Merhaba parolanızın süresi dolduğu için kullanıcıların kimlik bilgilerini tooreenter gerekebilir</span><span class="sxs-lookup"><span data-stu-id="fd61b-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="fd61b-119">Uygulamanız için kullanıcı gereksinimlerini tooconsent hello erişim tooa kaynak isteme</span><span class="sxs-lookup"><span data-stu-id="fd61b-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="fd61b-120">İki faktörlü kimlik doğrulama gereklidir</span><span class="sxs-lookup"><span data-stu-id="fd61b-120">Two factor authentication is required</span></span>

<span data-ttu-id="fd61b-121">Arama hello *acquireTokenRedirect(scope)* neden kullanıcılar toohello Azure Active Directory v2 endpoint yönlendirerek (veya *acquireTokenPopup(scope)* bir açılır pencere sonucuna) burada kullanıcıların gerekir onaylayarak ya da kullanıcıların kimlik bilgilerini hello izin toohello vermiş toointeract ile kaynak ya da Tamamlanıyor hello iki faktörlü kimlik doğrulaması gerekli.</span><span class="sxs-lookup"><span data-stu-id="fd61b-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="fd61b-122">Bir kullanıcı sessizce belirteci alma</span><span class="sxs-lookup"><span data-stu-id="fd61b-122">Getting a user token silently</span></span>
<span data-ttu-id="fd61b-123">Merhaba ` acquireTokenSilent` yöntemi belirteci satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler.</span><span class="sxs-lookup"><span data-stu-id="fd61b-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="fd61b-124">Sonra `loginRedirect` (veya `loginPopup`) hello için ilk kez yürütüldüğünde `acquireTokenSilent` hello yaygın olarak kullanılan yöntemi tooobtain kullanılan belirteçleri tooaccess sonraki çağrılar için-kaynaklar çağrıları toorequest korumalı veya belirteçleri yenileme sessiz bir şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="fd61b-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="fd61b-125">`acquireTokenSilent`, örneğin, hello kullanıcının parolasını bazı durumlarda – başarısız sona erdi.</span><span class="sxs-lookup"><span data-stu-id="fd61b-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="fd61b-126">Uygulamanız bu özel durumun iki yolla işleyebilir:</span><span class="sxs-lookup"><span data-stu-id="fd61b-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="fd61b-127">Çok çağırmaya`acquireTokenRedirect` hemen hangi sonuçlarındaki isteyen kullanıcı toosign hello.</span><span class="sxs-lookup"><span data-stu-id="fd61b-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="fd61b-128">Bu desen çevrimiçi uygulamalarında yaygın olarak kullanılan hello uygulama kullanılabilir toohello kullanıcı kimliği doğrulanmamış içerik olduğu.</span><span class="sxs-lookup"><span data-stu-id="fd61b-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="fd61b-129">Merhaba örnek destekli bu kurulum tarafından oluşturulan bu deseni kullanır.</span><span class="sxs-lookup"><span data-stu-id="fd61b-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="fd61b-130">Uygulamalar ayrıca bir etkileşimli oturum açma hello kullanıcı hello doğru zamanı toosign seçebilir ya da hello başvurusunda gerekli olan bir görsel gösterimi toohello kullanıcı olun `acquireTokenSilent` daha sonra.</span><span class="sxs-lookup"><span data-stu-id="fd61b-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="fd61b-131">Bunun yaygın olarak kullanılan hello kullanıcı kesintiye olmadan hello uygulama diğer işlevlerini kullanabilirsiniz - örneğin, kimliği doğrulanmamış içerik hello uygulamada kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="fd61b-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="fd61b-132">Bu durumda, hello kullanıcı ne zaman toosign tooaccess korumalı hello kaynak istedikleri veya toorefresh hello süresi geçmiş bilgilere karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd61b-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="fd61b-133">Yalnızca aldığınız hello belirteci kullanarak hello Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="fd61b-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="fd61b-134">Aşağıdaki kodu tooyour hello eklemek `app.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="fd61b-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in hello page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in hello page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="fd61b-135">Karşı korumalı bir API REST çağrısı yapma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="fd61b-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="fd61b-136">Bu kılavuz tarafından oluşturulan hello örnek uygulamasında hello `callWebApiWithToken()` yöntemdir kullanılan toomake bir HTTP `GET` belirteci ve ardından dönüş hello içerik toohello çağıran gerektirir korunan bir kaynağa karşı istek.</span><span class="sxs-lookup"><span data-stu-id="fd61b-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="fd61b-137">Bu yöntem hello edinilen belirteci hello ekler *HTTP Authorization Üstbilgisi*.</span><span class="sxs-lookup"><span data-stu-id="fd61b-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="fd61b-138">Merhaba Microsoft Graph API bu kılavuzu tarafından oluşturulan hello örnek uygulama için hello kaynaktır *bana* endpoint – hello kullanıcının profil bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fd61b-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="fd61b-139">Merhaba kullanıcı çıkışı yöntemi toosign Ekle</span><span class="sxs-lookup"><span data-stu-id="fd61b-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="fd61b-140">Aşağıdaki kodu tooyour hello eklemek `app.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="fd61b-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
