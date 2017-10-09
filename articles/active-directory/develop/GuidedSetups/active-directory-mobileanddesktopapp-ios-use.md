---
title: "aaaAzure AD v2 iOS Başlarken - kullanım | Microsoft Docs"
description: "İOS (Swift) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="65169-103">Merhaba Microsoft Graph API Hello Microsoft kimlik doğrulama kitaplığı (MSAL) tooget bir belirteci kullanın</span><span class="sxs-lookup"><span data-stu-id="65169-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="65169-104">Açık `ViewController.swift` ve hello kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="65169-104">Open `ViewController.swift` and replace hello code with:</span></span>

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="65169-105">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="65169-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="65169-106">Kullanıcı etkileşimli olarak belirteci alma</span><span class="sxs-lookup"><span data-stu-id="65169-106">Getting a user token interactively</span></span>
<span data-ttu-id="65169-107">Arama hello `acquireToken` yöntemi sonuçlarındaki isteyen bir tarayıcı penceresinde hello kullanıcı toosign.</span><span class="sxs-lookup"><span data-stu-id="65169-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="65169-108">Uygulamalar genellikle zorunlu kullanıcı toosign etkileşimli olarak hello içinde tooaccess ihtiyaç duydukları ilk kez korunan bir kaynağa veya Sessiz işlemi tooacquire bir belirteç başarısız oluyor (örneğin hello kullanıcının parolasının süresi).</span><span class="sxs-lookup"><span data-stu-id="65169-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="65169-109">Bir kullanıcı sessizce belirteci alma</span><span class="sxs-lookup"><span data-stu-id="65169-109">Getting a user token silently</span></span>
<span data-ttu-id="65169-110">Merhaba `acquireTokenSilent` yöntemi belirteci satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler.</span><span class="sxs-lookup"><span data-stu-id="65169-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="65169-111">Sonra `acquireToken` hello için ilk kez yürütüldüğünde `acquireTokenSilent` hello yaygın olarak kullanılan yöntemi tooobtain kullanılan belirteçleri tooaccess sonraki çağrılar için-kaynaklar çağrıları toorequest korumalı veya belirteçleri yenileme sessiz bir şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="65169-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="65169-112">Sonuç olarak, `acquireTokenSilent` başarısız olur – örneğin hello kullanıcı oturumunuz veya başka bir aygıtta parolalarını değişti.</span><span class="sxs-lookup"><span data-stu-id="65169-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="65169-113">MSAL hello sorun çözümlenir etkileşimli bir eylem kılarak, harekete algıladığında bir `MSALErrorCode.interactionRequired` özel durum.</span><span class="sxs-lookup"><span data-stu-id="65169-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="65169-114">Uygulamanız bu özel durumun iki yolla işleyebilir:</span><span class="sxs-lookup"><span data-stu-id="65169-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="65169-115">Karşı çağırmaya `acquireToken` hemen hangi sonuçlarındaki isteyen kullanıcı toosign hello.</span><span class="sxs-lookup"><span data-stu-id="65169-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="65169-116">Bu deseni genelde çevrimiçi uygulamalarda kullanılır söz konusu olduğunda çevrimdışı içerik hello uygulamada hello kullanıcı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="65169-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="65169-117">Merhaba örnek uygulama destekli bu kurulum tarafından oluşturulan bu deseni kullanır: Merhaba uygulaması yürütme ilk kez eylemin hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65169-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="65169-118">Hiçbir kullanıcının herhangi bir zamanda Merhaba uygulaması kullanıldığından `applicationContext.users().first` bir null değer içerir ve bir ` MSALErrorCode.interactionRequired ` özel durum.</span><span class="sxs-lookup"><span data-stu-id="65169-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="65169-119">çağırarak özel durum işleyici hello sonra hello örnek kodda Hello `acquireToken` hello kullanıcı toosign isteyen sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="65169-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="65169-120">Uygulamalar ayrıca bir etkileşimli oturum açma hello kullanıcı hello doğru zamanı toosign seçebilir ya da hello başvurusunda gerekli olan bir görsel gösterimi toohello kullanıcı olun `acquireTokenSilent` daha sonra.</span><span class="sxs-lookup"><span data-stu-id="65169-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="65169-121">Bu genellikle kullanılan hello kullanıcı kesintiye olmadan hello uygulama diğer işlevlerini kullanabilirsiniz - örneğin, çevrimdışı içeriği hello uygulamada kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="65169-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="65169-122">Bu durumda, hello kullanıcı ne zaman toosign tooaccess korumalı hello kaynak istedikleri toorefresh hello eski bilgi veya uygulamanızın tooretry karar verebilirsiniz karar verebilir `acquireTokenSilent` ağ zaman geri geçici olarak kullanılamıyor kaldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="65169-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="65169-123">Yalnızca aldığınız hello belirteci kullanarak hello Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="65169-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="65169-124">Merhaba yeni yöntemi aşağıdaki çok eklemek`ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="65169-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="65169-125">Bu yöntem kullanılan toomake olan bir `GET` hello Microsoft grafik API'sini kullanarak karşı istek bir *HTTP Authorization Üstbilgisi*:</span><span class="sxs-lookup"><span data-stu-id="65169-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="65169-126">Karşı korumalı bir API REST çağrısı yapma</span><span class="sxs-lookup"><span data-stu-id="65169-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="65169-127">Bu örnek uygulamasında hello `getContentWithToken()` yöntemdir kullanılan toomake bir HTTP `GET` belirteci ve ardından dönüş hello içerik toohello çağıran gerektirir korunan bir kaynağa karşı istek.</span><span class="sxs-lookup"><span data-stu-id="65169-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="65169-128">Bu yöntem hello edinilen belirteci hello ekler *HTTP Authorization Üstbilgisi*.</span><span class="sxs-lookup"><span data-stu-id="65169-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="65169-129">Merhaba Microsoft Graph API Bu örnek için hello kaynaktır *bana* endpoint – hello kullanıcının profil bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="65169-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="65169-130">Oturum kapatma ayarlama</span><span class="sxs-lookup"><span data-stu-id="65169-130">Set up sign-out</span></span>

<span data-ttu-id="65169-131">Yöntem çok aşağıdaki hello eklemek`ViewController.swift` toosign hello kullanıcı çıkışı:</span><span class="sxs-lookup"><span data-stu-id="65169-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="65169-132">Oturum kapatma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="65169-132">More info on sign-out</span></span>

<span data-ttu-id="65169-133">Merhaba `signoutButton` toobe etkileşimli yapılırsa, gelecekteki isteği tooacquire bir belirteç yalnızca başarılı şekilde yöntemi kaldırır hello kullanıcı MSAL kullanıcı önbellek – hello bu etkili bir şekilde MSAL tooforget hello geçerli kullanıcı söyler.</span><span class="sxs-lookup"><span data-stu-id="65169-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="65169-134">Tek bir kullanıcı bu örnekte Merhaba uygulaması desteklemesine rağmen MSAL burada birden çok hesabı imzalanmasını hello senaryolarını destekler. aynı anda – örneğidir bir e-posta uygulamasının bir kullanıcı birden fazla hesap sahip olduğu.</span><span class="sxs-lookup"><span data-stu-id="65169-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="65169-135">Merhaba geri aramayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="65169-135">Register hello callback</span></span>

<span data-ttu-id="65169-136">Merhaba kullanıcının kimliğini doğrular sonra hello tarayıcı hello kullanıcı geri toohello uygulaması yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="65169-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="65169-137">Bu geri çağırma tooregister Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="65169-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="65169-138">Açık `AppDelegate.swift` ve MSAL içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="65169-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="65169-139">Yöntem tooyour aşağıdaki hello eklemek <code>AppDelegate</code> sınıf toohandle geri aramalar:</span><span class="sxs-lookup"><span data-stu-id="65169-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

