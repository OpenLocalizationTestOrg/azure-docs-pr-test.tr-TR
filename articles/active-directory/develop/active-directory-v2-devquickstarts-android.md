---
title: "aaaAzure Active Directory v2.0 Android uygulaması | Microsoft Docs"
description: "Nasıl toobuild kişisel Microsoft hesabı ve iş veya Okul hesapları hem çağrıları kullanıcılar oturum açtığında bir Android uygulaması hello grafik API'si üçüncü taraf kitaplıklar kullanılarak."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Grafik API'si hello v2.0 uç kullanarak bir üçüncü taraf kitaplık kullanılarak oturum açma tooan Android uygulaması ekleyin
Merhaba Microsoft kimlik platformu OAuth2 ve Openıd Connect gibi açık standartlar kullanır. Geliştiricilerin hizmetlerimizle ile toointegrate istedikleri herhangi bir kitaplığı kullanabilirsiniz. toohelp geliştiricilerin platformumuzu diğer kitaplıklarla birlikte kullanmak, biz bu bir toodemonstrate gibi birkaç izlenecek nasıl yazdıktan tooconfigure üçüncü taraf kitaplıklar tooconnect toohello Microsoft kimlik platformu. Uygulayan çoğu kitaplık [hello RFC6749 OAuth2 belirtimi](https://tools.ietf.org/html/rfc6749) toohello Microsoft kimlik platformu bağlanabilir.

Bu izlenecek yol oluşturur hello uygulamasıyla kullanıcılar tootheir kuruluşta oturum ve ardından kendileri için kuruluşlarında hello grafik API'sini kullanarak arama.

Yeni tooOAuth2 veya Openıd Connect değilseniz, bu örnek yapılandırmanın çoğunu algılama tooyou oluşturamazsınız. Okumanızı öneririz [2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı](active-directory-v2-protocols-oauth-code.md) arka planı için.

> [!NOTE]
> Merhaba OAuth2 veya Openıd Connect standartları, koşullu erişim ve Intune ilke yönetimi gibi bir ifadeye sahip bazı özellikleri, bizim açık kaynak Microsoft Azure kimlik kitaplıkları, toouse gerektirir.
> 
> 

Merhaba v2.0 uç tüm Azure Active Directory senaryolarını ve özelliklerini desteklemez.

> [!NOTE]
> Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

## <a name="download-hello-code-from-github"></a>Github'dan Hello kodu indirme
Bu öğretici için kod Hello korunduğu [github'da](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).  yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) veya kopya hello çatıyı:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

Hello örnek ayrıca indirebilirsiniz ve hemen başlayın:

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>Bir uygulamayı kaydetme
Merhaba yeni bir uygulama oluşturma [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya ayrıntılı adımları hello izleyin [nasıl tooregister hello v2.0 uç noktası ile uygulama](active-directory-v2-app-registration.md).  Emin olun:

* Kopya hello **uygulama kimliği** , olduğundan atanan tooyour uygulama yakında gerekir.
* Merhaba eklemek **mobil** uygulamanız için platform.

> Not: hello uygulama kayıt portalı sağlayan bir **yeniden yönlendirme URI'si** değeri. Ancak, bu örnekte hello varsayılan değerini kullanmalısınız `https://login.microsoftonline.com/common/oauth2/nativeclient`.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Merhaba NXOAuth2 üçüncü taraf kitaplığını indirin ve çalışma alanı oluşturma
Bu kılavuzda hello github'dan Google Openıd Connect kodunu hello üzerinde dayalı bir OAuth2 kitaplığı olan OIDCAndroidLib kullanır. Merhaba yerel uygulama profilini uygular ve hello hello kullanıcı yetkilendirme uç noktasını destekler. Bunlar hello Microsoft identity platformu ile toointegrate gerekir tüm hello noktalardır.

Merhaba OIDCAndroidLib depodaki tooyour bilgisayara kopyalayın.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Android Studio ortamınızı ayarlama
1. Yeni bir Android Studio projesi oluşturun ve Başlangıç Sihirbazı'nda hello Varsayılanları kabul edin.
   
    ![Android Studio'da yeni proje oluşturma](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Hedef Android cihazları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Bir etkinlik toomobile Ekle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset klonlanmış hello depodaki toohello proje konumu proje modüllerinizi taşıyın. Ayrıca hello projesi oluşturun ve toohello proje konumu doğrudan kopyalama.
   
    ![Proje modülleri](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Merhaba proje modülleri ayarları hello bağlam menüsünü kullanarak veya hello Ctrl + Alt + Maj + S kısayolu kullanarak açın.
   
    ![Proje modülleri ayarları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Merhaba proje kapsayıcı ayarları yalnızca istediğinden hello varsayılan uygulama modülünü Kaldır.
   
    ![Merhaba varsayılan uygulama modülü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Modülleri hello kopyalanan depodaki toohello geçerli projeden alın.
   
    ![İçeri aktarma gradle proje](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![yeni modül sayfa oluştur](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Hello için bu adımları yineleyin `oidlib-sample` modülü.
7. Merhaba Hello oidclib bağımlılıkları denetleyin `oidlib-sample` modülü.
   
    ![Merhaba oidlib örnek modül oidclib bağımlılıkları](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. Tıklatın **Tamam** ve gradle eşitleme için bekleyin.
   
    Settings.gradle gibi görünmelidir:
   
    ![Settings.gradle ekran görüntüsü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Merhaba örnek uygulama toomake emin yapı düzgün çalışmasını hello örneği.
   
    Mümkün toouse bu Azure Active Directory ile henüz olmayacaktır. Biz tooconfigure bazı uç noktaları ilk gerekir. Merhaba örnek uygulaması özelleştirme başlamadan önce bir Android Studio sorunları yok tooensure budur.
10. Derleme ve çalıştırma `oidlib-sample` Android Studio'da hello hedefi olarak.
    
    ![Oidlib örnek yapı ilerlemesi](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Merhaba silme `app ` Android Studio güvenliği silmez çünkü hello projeden hello modülü kaldırıldığında bırakıldı dizini.
    
    ![Merhaba uygulama dizini içeren dosya yapısı](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. Açık hello **yapılandırmalarını Düzenle** hello projeden hello modülü kaldırıldığında, ayrıca sol menü tooremove çalıştırmak hello yapılandırma.
    
    ![Düzen yapılandırmaları menüsü](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![uygulama yapılandırmasını çalıştırın](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Merhaba örneğinin Hello uç noktalarını yapılandırma
Merhaba sahip olduğunuza `oidlib-sample` başarıyla çalışırken, bazı uç noktaları tooget Azure Active Directory ile bu çalışma düzenleyelim.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>Merhaba oidc_clientconf.xml dosyasını düzenleyerek istemcinizi yapılandırmak
1. OAuth2 akışları yalnızca tooget bir belirteç kullanarak ve hello grafik API'sini çağırmak için hello istemci toodo OAuth2 yalnızca ayarlayın. OIDC bir sonraki örnekte gelecektir.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Merhaba kayıt Portalı'ndan alınan istemci Kimliğiniz yapılandırın.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. Aşağıda, yeniden yönlendirme URI'si hello biri ile yapılandırın.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. Grafik API'si sipariş tooaccess hello, kapsamı yapılandırın.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

Merhaba `User.Read` değeri `oidc_scopes` , tooread hello temel profil hello imzalı kullanıcı sağlar.
Tüm hello kullanılabilir kapsamların hakkında daha fazla bilgiyi [Microsoft Graph izin kapsamları](https://graph.microsoft.io/docs/authorization/permission_scopes).

İlgili açıklamalar istiyorsanız `openid` veya `offline_access` kapsamlarda Openıd Connect, bkz: [2.0 protokolleri - OAuth 2.0 yetkilendirme kodu akışı](active-directory-v2-protocols-oauth-code.md).

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Merhaba oidc_endpoints.xml dosyasını düzenleyerek, istemci uç noktalarını yapılandırma
* Açık hello `oidc_endpoints.xml` dosya ve hello aşağıdaki değişiklikler yapın:
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

OAuth2, protokol olarak kullanıyorsanız, bu uç noktaları asla değiştirmeniz gerekir.

> [!NOTE]
> Merhaba uç noktaları için `userInfoEndpoint` ve `revocationEndpoint` şu anda Azure Active Directory tarafından desteklenmemektedir. Bunlar hello varsayılan example.com değerle bırakırsanız, hello örnek kullanılabilir olmadıklarını :-) uyarılmak
> 
> 

## <a name="configure-a-graph-api-call"></a>Bir grafik API çağrısı yapılandırın
* Açık hello `HomeActivity.java` dosya ve hello aşağıdaki değişiklikler yapın:
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

Burada basit bir grafik API çağrısı bizim bilgileri döndürür.

Toodo gereken tüm hello değişiklik izinlerdir. Merhaba çalıştırmak `oidlib-sample` uygulama ve tıklatın **oturum**.

Başarıyla kimlik doğruladınız sonra hello seçin **korumalı kaynak isteği** tootest, çağrı toohello grafik API'si düğmesine tıklayın.

## <a name="get-security-updates-for-our-product"></a>Ürünümüz için güvenlik güncelleştirmelerini alma
Güvenlik olayları hakkında tooget bildirimler hello ziyaret ederek öneririz [güvenlik TechCenter](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.

