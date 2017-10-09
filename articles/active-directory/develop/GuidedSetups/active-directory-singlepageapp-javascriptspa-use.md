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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Merhaba Microsoft kimlik doğrulama kitaplığı (MSAL) toosign bileşenini hello kullanıcı kullanın

1.  Adlı bir dosya oluşturun `app.js`. Visual Studio, select hello proje (Proje kök klasöründe) kullanıyorsanız, sağ tıklatın ve seçin: `Add`  >  `New Item`  >  `JavaScript File`:
2.  Aşağıdaki kodu tooyour hello eklemek `app.js` dosyası:

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
### <a name="more-information"></a>Daha Fazla Bilgi

Bir kullanıcı hello tıklattıktan sonra *'Microsoft Graph API çağrısı'* hello ilk kez düğmesi `callGraphApi` yöntem çağrılarını `loginRedirect` toosign hello kullanıcı. Bu yöntem hello kullanıcı toohello yeniden yönlendirme sonucu *Microsoft Azure Active Directory v2 endpoint* tooprompt ve hello kullanıcının kimlik bilgilerini doğrulama. Bir başarılı oturum açma sonucu olarak, hello kullanıcının yeniden yönlendirilen geri toohello özgün olduğu *index.html* sayfası ve bir belirteç alındığında, tarafından işlenen `msal.js` ve hello belirtecinde yer alan hello bilgileri önbelleğe alınır. Bu belirteç hello adlandırılıyor *kimliği belirteci* ve hello kullanıcı görünen adı gibi hello kullanıcı hakkındaki temel bilgileri içerir. Toouse düşünüyorsanız toomake bu belirteç belirteci Merhaba, arka uç sunucu tooguarantee tarafından doğrulandığından emin gereken herhangi bir amaçla bu belirteç tarafından sağlanan herhangi bir veri tooa geçerli kullanıcı, uygulamanız için verilmiş.

Merhaba bu kılavuzu tarafından oluşturulan SPA yapmaz doğrudan hello kimliği belirteci kullanın-bunun yerine, çağıran `acquireTokenSilent` ve/veya `acquireTokenRedirect` tooacquire bir *erişim belirteci* tooquery hello Microsoft Graph API kullanılır. Merhaba kimliği belirteci doğrular bir örnek gerekiyorsa, bir göz atalım [bu](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 örnek") örnek uygulama github'da – hello örnek kullanır bir ASP.NET Web API belirteci doğrulama için.

#### <a name="getting-a-user-token-interactively"></a>Kullanıcı etkileşimli olarak belirteci alma

Oturum açma Hello sonra ilk, hello istiyor musunuz toorequest ihtiyaç duydukları her zaman kullanıcılar tooreauthenticate belirteci tooaccess bir kaynak – böylece isteyin *acquireTokenSilent* olmalıdır hello zaman tooacquire belirteçleri çoğu kullanılır. Durumlar vardır ancak kullanıcıların Azure Active Directory v2 noktayla – etkileşim tooforce gereken bazı örnekler şunlardır:
-   Merhaba parolanızın süresi dolduğu için kullanıcıların kimlik bilgilerini tooreenter gerekebilir
-   Uygulamanız için kullanıcı gereksinimlerini tooconsent hello erişim tooa kaynak isteme
-   İki faktörlü kimlik doğrulama gereklidir

Arama hello *acquireTokenRedirect(scope)* neden kullanıcılar toohello Azure Active Directory v2 endpoint yönlendirerek (veya *acquireTokenPopup(scope)* bir açılır pencere sonucuna) burada kullanıcıların gerekir onaylayarak ya da kullanıcıların kimlik bilgilerini hello izin toohello vermiş toointeract ile kaynak ya da Tamamlanıyor hello iki faktörlü kimlik doğrulaması gerekli.

#### <a name="getting-a-user-token-silently"></a>Bir kullanıcı sessizce belirteci alma
Merhaba ` acquireTokenSilent` yöntemi belirteci satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler. Sonra `loginRedirect` (veya `loginPopup`) hello için ilk kez yürütüldüğünde `acquireTokenSilent` hello yaygın olarak kullanılan yöntemi tooobtain kullanılan belirteçleri tooaccess sonraki çağrılar için-kaynaklar çağrıları toorequest korumalı veya belirteçleri yenileme sessiz bir şekilde yapılır.
`acquireTokenSilent`, örneğin, hello kullanıcının parolasını bazı durumlarda – başarısız sona erdi. Uygulamanız bu özel durumun iki yolla işleyebilir:

1.  Çok çağırmaya`acquireTokenRedirect` hemen hangi sonuçlarındaki isteyen kullanıcı toosign hello. Bu desen çevrimiçi uygulamalarında yaygın olarak kullanılan hello uygulama kullanılabilir toohello kullanıcı kimliği doğrulanmamış içerik olduğu. Merhaba örnek destekli bu kurulum tarafından oluşturulan bu deseni kullanır.

2. Uygulamalar ayrıca bir etkileşimli oturum açma hello kullanıcı hello doğru zamanı toosign seçebilir ya da hello başvurusunda gerekli olan bir görsel gösterimi toohello kullanıcı olun `acquireTokenSilent` daha sonra. Bunun yaygın olarak kullanılan hello kullanıcı kesintiye olmadan hello uygulama diğer işlevlerini kullanabilirsiniz - örneğin, kimliği doğrulanmamış içerik hello uygulamada kullanılabilir olduğunda. Bu durumda, hello kullanıcı ne zaman toosign tooaccess korumalı hello kaynak istedikleri veya toorefresh hello süresi geçmiş bilgilere karar verebilirsiniz.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Yalnızca aldığınız hello belirteci kullanarak hello Microsoft Graph API çağrısı

Aşağıdaki kodu tooyour hello eklemek `app.js` dosyası:

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Karşı korumalı bir API REST çağrısı yapma hakkında daha fazla bilgi

Bu kılavuz tarafından oluşturulan hello örnek uygulamasında hello `callWebApiWithToken()` yöntemdir kullanılan toomake bir HTTP `GET` belirteci ve ardından dönüş hello içerik toohello çağıran gerektirir korunan bir kaynağa karşı istek. Bu yöntem hello edinilen belirteci hello ekler *HTTP Authorization Üstbilgisi*. Merhaba Microsoft Graph API bu kılavuzu tarafından oluşturulan hello örnek uygulama için hello kaynaktır *bana* endpoint – hello kullanıcının profil bilgilerini görüntüler.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Merhaba kullanıcı çıkışı yöntemi toosign Ekle

Aşağıdaki kodu tooyour hello eklemek `app.js` dosyası:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
