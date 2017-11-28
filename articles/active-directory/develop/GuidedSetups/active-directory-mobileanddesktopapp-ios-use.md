---
title: "Azure AD v2 iOS Başlarken - kullanım | Microsoft Docs"
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
ms.openlocfilehash: 2ac1117a31a101705539a1f75520ce8de43809a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="f73fd-103">Microsoft Graph API için bir belirteç almak üzere Microsoft kimlik doğrulama kitaplığı (MSAL) kullanın</span><span class="sxs-lookup"><span data-stu-id="f73fd-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="f73fd-104">Açık `ViewController.swift` ve kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="f73fd-104">Open `ViewController.swift` and replace the code with:</span></span>

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

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
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
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
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
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
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
### <a name="more-information"></a><span data-ttu-id="f73fd-105">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="f73fd-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="f73fd-106">Kullanıcı etkileşimli olarak belirteci alma</span><span class="sxs-lookup"><span data-stu-id="f73fd-106">Getting a user token interactively</span></span>
<span data-ttu-id="f73fd-107">Çağırma `acquireToken` yöntemi, oturum açmak için kullanıcıdan bir tarayıcı penceresi sonuçlanıyor.</span><span class="sxs-lookup"><span data-stu-id="f73fd-107">Calling the `acquireToken` method results in a browser window prompting the user to sign in.</span></span> <span data-ttu-id="f73fd-108">Uygulamalar genellikle gerektirir etkileşimli olarak korunan bir kaynağa erişmek için ihtiyaç duydukları ilk kez oturum açmak bir kullanıcı ya da (örneğin kullanıcının parolasının süresi) belirteci başarısız edinmeye sessiz bir işlem.</span><span class="sxs-lookup"><span data-stu-id="f73fd-108">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="f73fd-109">Bir kullanıcı sessizce belirteci alma</span><span class="sxs-lookup"><span data-stu-id="f73fd-109">Getting a user token silently</span></span>
<span data-ttu-id="f73fd-110">`acquireTokenSilent` Yöntemi belirteci satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler.</span><span class="sxs-lookup"><span data-stu-id="f73fd-110">The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="f73fd-111">Sonra `acquireToken` ilk kez yürütüldüğünde `acquireTokenSilent` veya belirteçleri yenileme isteği için çağrıları sessizce gerçekleştirilmediğinden sonraki çağrılar için-korumalı kaynaklara erişmek için kullanılan belirteçleri elde etmek için yaygın olarak kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="f73fd-111">After `acquireToken` is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>

<span data-ttu-id="f73fd-112">Sonuç olarak, `acquireTokenSilent` başarısız olur – örneğin kullanıcı oturumunuz veya başka bir aygıtta parolalarını değişti.</span><span class="sxs-lookup"><span data-stu-id="f73fd-112">Eventually, `acquireTokenSilent` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="f73fd-113">MSAL algıladığında, etkileşimli bir eylem gerektirmeyen tarafından sorunu çözmek için harekete bir `MSALErrorCode.interactionRequired` özel durum.</span><span class="sxs-lookup"><span data-stu-id="f73fd-113">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="f73fd-114">Uygulamanız bu özel durumun iki yolla işleyebilir:</span><span class="sxs-lookup"><span data-stu-id="f73fd-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="f73fd-115">Karşı çağırmaya `acquireToken` hemen hangi sonuçları oturum açmak için kullanıcıdan içinde.</span><span class="sxs-lookup"><span data-stu-id="f73fd-115">Make a call against `acquireToken` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="f73fd-116">Bu deseni genelde çevrimiçi uygulamalarda kullanılır söz konusu olduğunda çevrimdışı içerik uygulamada kullanıcı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f73fd-116">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="f73fd-117">Bu desen destekli bu kurulum tarafından oluşturulan örnek uygulama kullanır: uygulama yürütme eylemi ilk zamanında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f73fd-117">The sample application generated by this guided setup uses this pattern: you can see it in action the first time you execute the application.</span></span> <span data-ttu-id="f73fd-118">Hiçbir kullanıcı, uygulamayı her zamankinden kullanıldığından `applicationContext.users().first` bir null değer içerir ve bir ` MSALErrorCode.interactionRequired ` özel durum.</span><span class="sxs-lookup"><span data-stu-id="f73fd-118">Because no user ever used the application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="f73fd-119">Ardından örnek kodda çağırarak özel durumu işler `acquireToken` oturum açmak için kullanıcıdan içinde sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="f73fd-119">The code in the sample then handles the exception by calling `acquireToken` resulting in prompting the user to sign in.</span></span>

2.  <span data-ttu-id="f73fd-120">Uygulamalar bir etkileşimli oturum açma kullanıcı oturum açmak için doğru zamanı seçebilir ya da uygulama deneyebilirsiniz gerekli olan kullanıcı için görsel bir gösterge de yapabilirsiniz `acquireTokenSilent` daha sonra.</span><span class="sxs-lookup"><span data-stu-id="f73fd-120">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="f73fd-121">Bu genellikle kullanılan kullanıcı kesintiye olmadan diğer uygulamanın işlevselliğini kullanabilir - Örneğin, çevrimdışı içeriği uygulamada kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="f73fd-121">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="f73fd-122">Bu durumda, kullanıcı ne zaman korumalı kaynağa erişmek için ya da eski bilgileri yenilemek için oturum açmak istedikleri veya uygulamanızın denemeye karar verebilirsiniz karar verebilir `acquireTokenSilent` ağ zaman geri geçici olarak kullanılamıyor kaldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="f73fd-122">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="f73fd-123">Yalnızca edinilen belirteçle kullanarak Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="f73fd-123">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="f73fd-124">Aşağıda yeni bir yöntem ekleyin `ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="f73fd-124">Add the new method below to `ViewController.swift`.</span></span> <span data-ttu-id="f73fd-125">Bu yöntem yapmak için kullanılan bir `GET` Microsoft grafik API'sini kullanarak karşı istek bir *HTTP Authorization Üstbilgisi*:</span><span class="sxs-lookup"><span data-stu-id="f73fd-125">This method is used to make a `GET` request against the Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="f73fd-126">Karşı korumalı bir API REST çağrısı yapma</span><span class="sxs-lookup"><span data-stu-id="f73fd-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="f73fd-127">Bu örnek uygulamasında `getContentWithToken()` yöntemi bir HTTP yapmak için kullanılan `GET` isteği için bir belirteç gerekiyor korunan bir kaynağa karşı ve ardından içeriği çağırana dönün.</span><span class="sxs-lookup"><span data-stu-id="f73fd-127">In this sample application, the `getContentWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="f73fd-128">Bu yöntem alınan belirteç ekler *HTTP Authorization Üstbilgisi*.</span><span class="sxs-lookup"><span data-stu-id="f73fd-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="f73fd-129">Bu örnek için Microsoft Graph API kaynaktır *bana* endpoint – kullanıcı profili bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f73fd-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="f73fd-130">Oturum kapatma ayarlama</span><span class="sxs-lookup"><span data-stu-id="f73fd-130">Set up sign-out</span></span>

<span data-ttu-id="f73fd-131">Aşağıdaki yöntemi ekleyin `ViewController.swift` kullanıcı imzalamak için:</span><span class="sxs-lookup"><span data-stu-id="f73fd-131">Add the following method to `ViewController.swift` to sign out the user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="f73fd-132">Oturum kapatma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f73fd-132">More info on sign-out</span></span>

<span data-ttu-id="f73fd-133">`signoutButton` Yöntemi kaldırır kullanıcı MSAL kullanıcı önbellekten – bu etkili bir şekilde etkileşimli olarak yapılırsa bir belirteç almak için gelecekteki bir isteği yalnızca başarılı şekilde geçerli kullanıcının unuttunuz MSAL söyler.</span><span class="sxs-lookup"><span data-stu-id="f73fd-133">The `signoutButton` method removes the user from the MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>

<span data-ttu-id="f73fd-134">Bu örnek uygulamasında tek bir kullanıcı desteklese de MSAL nerede birden fazla hesap aynı zamanda oturum açmadan – bir e-posta uygulamasının bir kullanıcı birden fazla hesap sahip olduğu örneğidir senaryolarını destekler.</span><span class="sxs-lookup"><span data-stu-id="f73fd-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-the-callback"></a><span data-ttu-id="f73fd-135">Kaydı geri çağırma</span><span class="sxs-lookup"><span data-stu-id="f73fd-135">Register the callback</span></span>

<span data-ttu-id="f73fd-136">Kullanıcının kimliğini doğrular sonra tarayıcı kullanıcı yeniden uygulamaya yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="f73fd-136">Once the user authenticates, the browser redirects the user back to the application.</span></span> <span data-ttu-id="f73fd-137">Bu geri çağırma kaydetmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f73fd-137">Follow the steps below to register this callback:</span></span>

1.  <span data-ttu-id="f73fd-138">Açık `AppDelegate.swift` ve MSAL içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="f73fd-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="f73fd-139">Aşağıdaki yöntemi ekleyin, <code>AppDelegate</code> geri çağırmaları işlemek üzere sınıfı:</span><span class="sxs-lookup"><span data-stu-id="f73fd-139">Add the following method to your <code>AppDelegate</code> class to handle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

