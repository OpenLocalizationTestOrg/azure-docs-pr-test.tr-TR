---
title: "Bir iOS uygulaması - Azure AD B2C kullanarak bir belirteç alınırken | Microsoft Docs"
description: "Bu makale size nasıl gösterir toocreate Azure Active Directory B2C toomanage kullanıcı kimliklerle AppAuth kullanır ve kullanıcıların kimliklerini bir iOS uygulaması."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C: Bir iOS uygulaması kullanarak oturum açın

Merhaba Microsoft kimlik platformu OAuth2 ve Openıd Connect gibi açık standartlar kullanır. Açık bir standart protokol kullanarak, bir kitaplık toointegrate hizmetlerimizle ile seçerken daha fazla Geliştirici seçenekleri sunar. Bu kılavuzda ve diğerleri gibi tooaid geliştiriciler toohello Microsoft Identity platform bağlanan uygulamaları yazma ile sağladık. Uygulayan çoğu kitaplık [hello RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) mümkün tooconnect toohello Microsoft Identity platformu olan.

> [!WARNING]
> Microsoft, üçüncü taraf kitaplıklar için düzeltmeler ve bu kitaplıkları gözden yapılmadı sağlamaz. Bu örnek temel senaryolarda hello Azure AD B2C ile uyumluluk için test edilmiştir AppAuth adlı bir üçüncü taraf kitaplık kullanıyor. Sorunları ve özellik istekleri yönlendirilmiş toohello kitaplığın açık kaynaklı proje olması gerekir. Daha fazla bilgi için [bu makaleye](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) bakın.
>
>

Yeni tooOAuth2 veya Openıd Connect değilseniz, bu örnek yapılandırmanın çoğunu kadar algılama tooyou oluşturamazsınız. Kısaca öneririz [biz burada belgelediğimiz hello protokolüne genel bakış](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C dizini alma
Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir. Bir dizin, tüm kullanıcıların, uygulamaları, grupları ve daha fazlası için bir kapsayıcıdır. Henüz yoksa devam etmeden önce [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).

## <a name="create-an-application"></a>Uygulama oluşturma
Ardından B2C dizininizde uygulama toocreate gerekir. Hello uygulama kaydı, uygulamanız ile güvenli toocommunicate gereken bilgileri Azure AD'ye verir. bir mobil uygulama toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md). Şunları yaptığınızdan emin olun:

* Dahil bir **Native client** hello uygulamada.
* Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama. Bu GUID daha sonra gerekir.
* Ayarlanmış bir **yeniden yönlendirme URI'si** özel şema (örneğin, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect) sahip. Bu URI daha sonra gerekir.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>İlkelerinizi oluşturma
Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır. Bu uygulama bir kimlik deneyimi içerir: bir birleşik oturum açma ve kaydolma. Bu ilkeyi açıklandığı gibi oluşturmak [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Hello ilkesi oluşturduğunuzda, emin olun:

* Altında **kaydolma özniteliklerini**seçin hello özniteliği **görünen adı**.  Diğer öznitelikler de seçebilirsiniz.
* Altında **uygulama talepleri**, seçin hello talep **görünen adı** ve **kullanıcının nesne kimliği**. Diğer talepleri de seçebilirsiniz.
* Kopya hello **adı** oluşturduktan sonra her ilkenin. İlke adı önekine sahip `b2c_1_` hello İlkesi kaydettiğinizde.  Hello ilkesi adı daha sonra gerekir.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

İlkelerinizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.

## <a name="download-hello-sample-code"></a>Merhaba örnek kodu indirin
Azure AD B2C ile AppAuth kullanan bir çalışma örneği sağladık [github'da](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Merhaba kodu indirin ve çalıştırın. toouse kendi Azure AD B2C Kiracı, hello hello yönergeleri izleyin [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

Bu örnek tarafından hello hello Benioku yönergeleri izleyerek oluşturulduğu [iOS AppAuth proje Github'da](https://github.com/openid/AppAuth-iOS). Hello örnek ve hello kitaplığı nasıl çalıştığı hakkında daha fazla ayrıntı için github'da AppAuth Benioku hello başvuru.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Uygulama toouse Azure AD B2C AppAuth ile değiştirme

> [!NOTE]
> AppAuth destekleyen iOS 7 ve üstü.  Ancak, Google, SFSafariViewController toosupport sosyal oturum gereklidir iOS 9 veya üstü gerektirir.
>

### <a name="configuration"></a>Yapılandırma

Merhaba yetkilendirme uç noktası ve belirteç uç noktası URI belirterek Azure AD B2C ile iletişim yapılandırabilirsiniz.  toogenerate bu URI bilgisinden hello gerekir:
* Kiracı kimliği (örneğin, contoso.onmicrosoft.com)
* İlke adı (örneğin, B2C\_1\_SignUpIn)

Merhaba belirteç uç noktası URI değiştirerek oluşturulabilir hello Kiracı\_kimliği ve hello İlkesi\_URL aşağıdaki hello adı:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

Merhaba yetkilendirme uç noktası URI değiştirerek oluşturulabilir hello Kiracı\_kimliği ve hello İlkesi\_URL aşağıdaki hello adı:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Aşağıdaki kod toocreate hello AuthorizationServiceConfiguration nesnenizin çalıştırın:

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Yetkilendirme

Yapılandırma veya bir yetkilendirme hizmet yapılandırmasını alma sonra bir yetkilendirme isteği oluşturulabilir. toocreate hello istek bilgisinden hello gerekir:  
* İstemci kimliği (örneğin, 00000000-0000-0000-0000-000000000000)
* Özel bir şema ile (örneğin, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect) yeniden yönlendirme URI'si

Olursa, her iki öğe kaydedildi [uygulamanızı kaydetme](#create-an-application).

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

tooset, uygulama toohandle hello yeniden yönlendirme toohello URI hello özel şema ile yukarı Info.pList dosyasında tooupdate hello 'URL şemalarını' listesi gerekir:
* Info.plist açın.
* 'Paket işletim sistemi türü kodu' gibi bir satır üzerine gelerek ve hello tıklatın \+ simgesi.
* Merhaba yeni satır 'URL türleri' olarak yeniden adlandırın.
* 'URL türleri' tooopen hello ağacının Hello ok toohello sol tıklayın.
* '0 öğe' tooopen hello ağacının Hello ok toohello sol tıklayın.
* İlk öğeyi öğesi 0 too'URL düzenleri altında yeniden adlandırmak.
* 'URL şemalarını' tooopen hello ağacının Hello ok toohello sol tıklayın.
* Merhaba 'Value' sütununda bir boş alan toohello solundaki yok 'Öğesi 0' 'Altında URL şemalarını'.  Merhaba değeri tooyour uygulamanın benzersiz düzeni ayarlayın.  Merhaba değeri içinde Redirecturl'yi hello OIDAuthorizationRequest nesnesi oluşturulurken kullanılan hello şeması eşleşmelidir.  Bizim örnek hello düzeni 'com.onmicrosoft.fabrikamb2c.exampleapp' kullandık.

Toohello başvuran [AppAuth Kılavuzu](https://openid.github.io/AppAuth-iOS/) nasıl toocomplete hello hello işleminin geri kalanında üzerinde. Tooquickly gerekiyorsa bir çalışma uygulaması ile çalışmaya başlama, kullanıma [bizim örnek](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Merhaba Hello adımları [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter kendi Azure AD B2C yapılandırma.

Her zaman açık toofeedback ve öneriler duyuyoruz! Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, hello sayfanın hello sonundaki görüşlerinize değer veriyoruz. Özellik istekleri için çok eklemediğiniz[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
