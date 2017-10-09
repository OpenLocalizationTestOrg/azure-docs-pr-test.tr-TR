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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Merhaba Microsoft Graph API Hello Microsoft kimlik doğrulama kitaplığı (MSAL) tooget bir belirteci kullanın

Açık `ViewController.swift` ve hello kod ile değiştirin:

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
### <a name="more-information"></a>Daha Fazla Bilgi
#### <a name="getting-a-user-token-interactively"></a>Kullanıcı etkileşimli olarak belirteci alma
Arama hello `acquireToken` yöntemi sonuçlarındaki isteyen bir tarayıcı penceresinde hello kullanıcı toosign. Uygulamalar genellikle zorunlu kullanıcı toosign etkileşimli olarak hello içinde tooaccess ihtiyaç duydukları ilk kez korunan bir kaynağa veya Sessiz işlemi tooacquire bir belirteç başarısız oluyor (örneğin hello kullanıcının parolasının süresi).

#### <a name="getting-a-user-token-silently"></a>Bir kullanıcı sessizce belirteci alma
Merhaba `acquireTokenSilent` yöntemi belirteci satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler. Sonra `acquireToken` hello için ilk kez yürütüldüğünde `acquireTokenSilent` hello yaygın olarak kullanılan yöntemi tooobtain kullanılan belirteçleri tooaccess sonraki çağrılar için-kaynaklar çağrıları toorequest korumalı veya belirteçleri yenileme sessiz bir şekilde yapılır.

Sonuç olarak, `acquireTokenSilent` başarısız olur – örneğin hello kullanıcı oturumunuz veya başka bir aygıtta parolalarını değişti. MSAL hello sorun çözümlenir etkileşimli bir eylem kılarak, harekete algıladığında bir `MSALErrorCode.interactionRequired` özel durum. Uygulamanız bu özel durumun iki yolla işleyebilir:

1.  Karşı çağırmaya `acquireToken` hemen hangi sonuçlarındaki isteyen kullanıcı toosign hello. Bu deseni genelde çevrimiçi uygulamalarda kullanılır söz konusu olduğunda çevrimdışı içerik hello uygulamada hello kullanıcı için kullanılabilir. Merhaba örnek uygulama destekli bu kurulum tarafından oluşturulan bu deseni kullanır: Merhaba uygulaması yürütme ilk kez eylemin hello görebilirsiniz. Hiçbir kullanıcının herhangi bir zamanda Merhaba uygulaması kullanıldığından `applicationContext.users().first` bir null değer içerir ve bir ` MSALErrorCode.interactionRequired ` özel durum. çağırarak özel durum işleyici hello sonra hello örnek kodda Hello `acquireToken` hello kullanıcı toosign isteyen sonuçlanır.

2.  Uygulamalar ayrıca bir etkileşimli oturum açma hello kullanıcı hello doğru zamanı toosign seçebilir ya da hello başvurusunda gerekli olan bir görsel gösterimi toohello kullanıcı olun `acquireTokenSilent` daha sonra. Bu genellikle kullanılan hello kullanıcı kesintiye olmadan hello uygulama diğer işlevlerini kullanabilirsiniz - örneğin, çevrimdışı içeriği hello uygulamada kullanılabilir olduğunda. Bu durumda, hello kullanıcı ne zaman toosign tooaccess korumalı hello kaynak istedikleri toorefresh hello eski bilgi veya uygulamanızın tooretry karar verebilirsiniz karar verebilir `acquireTokenSilent` ağ zaman geri geçici olarak kullanılamıyor kaldıktan sonra.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Yalnızca aldığınız hello belirteci kullanarak hello Microsoft Graph API çağrısı

Merhaba yeni yöntemi aşağıdaki çok eklemek`ViewController.swift`. Bu yöntem kullanılan toomake olan bir `GET` hello Microsoft grafik API'sini kullanarak karşı istek bir *HTTP Authorization Üstbilgisi*:

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
### <a name="making-a-rest-call-against-a-protected-api"></a>Karşı korumalı bir API REST çağrısı yapma

Bu örnek uygulamasında hello `getContentWithToken()` yöntemdir kullanılan toomake bir HTTP `GET` belirteci ve ardından dönüş hello içerik toohello çağıran gerektirir korunan bir kaynağa karşı istek. Bu yöntem hello edinilen belirteci hello ekler *HTTP Authorization Üstbilgisi*. Merhaba Microsoft Graph API Bu örnek için hello kaynaktır *bana* endpoint – hello kullanıcının profil bilgilerini görüntüler.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Oturum kapatma ayarlama

Yöntem çok aşağıdaki hello eklemek`ViewController.swift` toosign hello kullanıcı çıkışı:

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
### <a name="more-info-on-sign-out"></a>Oturum kapatma hakkında daha fazla bilgi

Merhaba `signoutButton` toobe etkileşimli yapılırsa, gelecekteki isteği tooacquire bir belirteç yalnızca başarılı şekilde yöntemi kaldırır hello kullanıcı MSAL kullanıcı önbellek – hello bu etkili bir şekilde MSAL tooforget hello geçerli kullanıcı söyler.

Tek bir kullanıcı bu örnekte Merhaba uygulaması desteklemesine rağmen MSAL burada birden çok hesabı imzalanmasını hello senaryolarını destekler. aynı anda – örneğidir bir e-posta uygulamasının bir kullanıcı birden fazla hesap sahip olduğu.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Merhaba geri aramayı kaydetme

Merhaba kullanıcının kimliğini doğrular sonra hello tarayıcı hello kullanıcı geri toohello uygulaması yönlendirir. Bu geri çağırma tooregister Hello adımları izleyin:

1.  Açık `AppDelegate.swift` ve MSAL içeri aktarın:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Yöntem tooyour aşağıdaki hello eklemek <code>AppDelegate</code> sınıf toohandle geri aramalar:
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

