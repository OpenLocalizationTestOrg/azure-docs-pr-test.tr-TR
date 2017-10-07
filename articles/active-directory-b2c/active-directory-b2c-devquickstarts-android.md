---
title: "Azure Active Directory B2C: bir Android uygulamasını kullanarak bir belirteç alınırken | Microsoft Docs"
description: "Bu makale size nasıl gösterir toocreate, Azure Active Directory B2C toomanage kullanıcı kimliklerle AppAuth kullanır ve kullanıcıların kimliklerini bir Android uygulaması."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure AD B2C: Bir Android uygulamasını kullanarak oturum açın

Merhaba Microsoft kimlik platformu OAuth2 ve Openıd Connect gibi açık standartlar kullanır. Böylece geliştiriciler tooleverage hizmetlerimizle ile toointegrate istedikleri herhangi bir kitaplığı. platformumuzu diğer kitaplıklarla birlikte kullanarak tooaid geliştiriciler, yazılan bu bir toodemonstrate gibi birkaç izlenecek nasıl tooconfigure 3 taraf kitaplıklar tooconnect toohello Microsoft kimlik platformu. Uygulayan çoğu kitaplık [hello RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) mümkün tooconnect toohello Microsoft Identity platform olacaktır.

> [!WARNING]
> Microsoft, 3 düzeltmelerin kitaplıkları taraf ve bu kitaplıkları gözden yapılmadı sağlamaz. Bu örnek temel senaryolarda hello Azure AD B2C ile uyumluluk için test edilmiştir AppAuth adlı 3 bir taraf kitaplık kullanıyor. Sorunları ve özellik istekleri yönlendirilmiş toohello kitaplığın açık kaynaklı proje olması gerekir. Lütfen bakın [bu makalede](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) daha fazla bilgi için.  
>
>

Yeni tooOAuth2 veya Openıd Connect değilseniz bu örnek yapılandırmanın çoğunu kadar algılama tooyou oluşturamazsınız. Kısaca öneririz [biz burada belgelediğimiz hello protokolüne genel bakış](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C dizini alma

Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir. Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır. Henüz yoksa devam etmeden önce [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).

## <a name="create-an-application"></a>Uygulama oluşturma

Ardından B2C dizininizde uygulama toocreate gerekir. Bu, uygulamanız ile güvenli toocommunicate gereken bilgileri Azure AD'ye verir. bir mobil uygulama toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md). Şunları yaptığınızdan emin olun:

* Dahil bir **Native Client** hello uygulamada.
* Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama. Bu daha sonra ihtiyacınız olacak.
* Bir yerel istemcisi ayarlama **yeniden yönlendirme URI'si** (örneğin com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Buna da daha sonra ihtiyacınız olacak.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>İlkelerinizi oluşturma

Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır. Bu uygulama bir kimlik deneyimi içerir: bir birleşik oturum açma ve kaydolma. Toocreate açıklandığı gibi bu ilkeyi gereken [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Hello ilkesi oluşturduğunuzda, emin olun:

* Merhaba seçin **görünen adı** ilkenizde kaydolma özniteliği olarak.
* Merhaba seçin **görünen adı** ve **nesne kimliği** her ilkede uygulamanın talep. Diğer talepleri de seçebilirsiniz.
* Kopya hello **adı** oluşturduktan sonra her ilkenin. Merhaba önekine sahip olmalıdır `b2c_1_`.  Hello ilkesi adı daha sonra ihtiyacınız olacak.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

İlkelerinizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.

## <a name="download-hello-sample-code"></a>Merhaba örnek kodu indirin

Azure AD B2C ile AppAuth kullanan bir çalışma örneği sağladık [github'da](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Merhaba kodu indirin ve çalıştırın. Hızlı bir şekilde hello hello yönergeleri takip ederek kendi Azure AD B2C Yapılandırması'nı kullanarak kendi uygulamanızı kullanmaya [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

Merhaba örnektir tarafından sağlanan hello örnek değiştirilmesini [AppAuth](https://openid.github.io/AppAuth-Android/). Lütfen AppAuth ve özellikleri hakkında daha fazla kendi sayfa toolearn adresini ziyaret edin.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Uygulama toouse Azure AD B2C AppAuth ile değiştirme

> [!NOTE]
> AppAuth destekleyen Android API 16 (Jellybean) ve üstü. API 23 kullanmanızı öneririz ve üstü.
>

### <a name="configuration"></a>Yapılandırma

Azure AD B2C ile iletişim belirtme ya da hello bulma URI veya hello yetkilendirme uç noktası ve belirteç uç noktası URI belirterek yapılandırabilirsiniz. Her iki durumda da, aşağıdaki bilgilerle hello gerekir:

* Kiracı kimliği (ör. contoso.onmicrosoft.com)
* İlke adı (örneğin B2C\_1\_SignUpIn)

Seçtiğiniz varsa tooautomatically hello yetkilendirme ve belirteç uç noktası URI bulmak, hello keşfi URI toofetch bilgilere ihtiyacınız olacaktır. URI hello Kiracı değiştirerek oluşturulabilir hello bulma\_kimliği ve hello İlkesi\_URL aşağıdaki hello adı:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

Ardından, hello yetkilendirme ve belirteç uç noktası URI edinmeli ve hello aşağıdakini çalıştırarak bir AuthorizationServiceConfiguration nesnesi oluşturun:

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

Bulma tooobtain hello yetkilendirme ve belirteç uç noktası URI kullanmak yerine, ayrıca bunları açıkça hello Kiracı değiştirerek belirtebilirsiniz\_kimliği ve hello İlkesi\_adlarında hello URL'SİNİN aşağıdaki:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Aşağıdaki kod toocreate hello AuthorizationServiceConfiguration nesnenizin çalıştırın:

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Yetkilendirme

Yapılandırma veya bir yetkilendirme hizmet yapılandırmasını alma sonra bir yetkilendirme isteği oluşturulabilir. toocreate hello istek bilgisinden hello gerekir:

* İstemci kimliği (örneğin 00000000-0000-0000-0000-000000000000)
* Özel bir şema ile (örneğin com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect) yeniden yönlendirme URI'si

Olursa, her iki öğe kaydedildi [uygulamanızı kaydetme](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Lütfen toohello bakın [AppAuth Kılavuzu](https://openid.github.io/AppAuth-Android/) nasıl toocomplete hello hello işleminin geri kalanında üzerinde. Tooquickly gerekiyorsa bir çalışma uygulaması ile çalışmaya başlama, kullanıma [bizim örnek](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Merhaba Hello adımları [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter kendi Azure AD B2C yapılandırma.

Her zaman açık toofeedback ve öneriler duyuyoruz! Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, hello sayfanın hello sonundaki görüşlerinize değer veriyoruz. Özellik istekleri için çok eklemediğiniz[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

