---
title: "Azure Active Directory B2C: özel ilkelerini kullanmaya başlama | Microsoft Docs"
description: "Tooget Azure Active Directory B2C özel ilkeleri ile çalışmaya nasıl"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C: özel ilkelerini kullanmaya başlama

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu makalede hello adımları tamamladıktan sonra özel ilkeniz "yerel hesabı" destekleyecek kaydolma veya oturum açma aracılığıyla bir e-posta adresi ve parola. Ayrıca, kimlik sağlayıcıları (örneğin, Facebook veya Azure Active Directory) eklemek için ortamınızın hazırlar. Diğer okumayı önce bu adımları kullanan Azure Active Directory (Azure AD) B2C kimlik deneyimi Framework Merhaba toocomplete öneririz.

## <a name="prerequisites"></a>Ön koşullar

Devam etmeden önce tüm kullanıcıların, uygulamaları, ilkeleri ve daha fazla bilgi için bir kapsayıcıdır bir Azure AD B2C kiracısı olduğundan emin olun. Zaten yoksa, çok ihtiyacınız[bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md). Biz kesinlikle tüm geliştiriciler toocomplete hello Azure AD B2C yerleşik ilke izlenecek teşvik eder ve devam etmeden önce yerleşik ilkeleriyle uygulamalarını yapılandırın. Küçük değişiklik toohello ilkesi adı tooinvoke hello özel bir ilke yaptıktan sonra uygulamalarınızın her iki tür ilke ile çalışır.

>[!NOTE]
>tooaccess özel ilkesi düzenleme, geçerli bir Azure abonelik bağlantılı tooyour Kiracı gerekir. Siz yapmadıysanız [Azure AD B2C Kiracı tooan Azure aboneliğine bağlı](active-directory-b2c-how-to-enable-billing.md) veya Azure aboneliğiniz devre dışı bırakılmış, hello kimlik deneyimi Framework düğmesi kullanılamaz.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>Özel ilkeleri tarafından kullanım için imzalama ve şifreleme anahtarları tooyour B2C Kiracı Ekle

1. Açık hello **kimlik deneyimi Framework** dikey penceresinde, Azure AD B2C Kiracı ayarlarınızı.
2. Seçin **İlkesi anahtarları** tooview hello anahtarları kiracınızda kullanılabilir.
3. Henüz yoksa B2C_1A_TokenSigningKeyContainer oluşturun:<br>
    a. **Add (Ekle)** seçeneğini belirleyin. <br>
    b. Seçin **oluşturmak**.<br>
    c. İçin **adı**, kullanmak `TokenSigningKeyContainer`. <br> 
    Merhaba önek `B2C_1A_` otomatik olarak eklenebilir.<br>
    d. İçin **anahtar türü**, kullanın **RSA**.<br>
    e. İçin **tarihleri**, hello varsayılanları kullanın. <br>
    f. İçin **anahtar kullanımı**, kullanın **imza**.<br>
    g. **Oluştur**’u seçin.<br>
4. Henüz yoksa B2C_1A_TokenEncryptionKeyContainer oluşturun:<br>
 a. **Add (Ekle)** seçeneğini belirleyin.<br>
 b. Seçin **oluşturmak**.<br>
 c. İçin **adı**, kullanmak `TokenEncryptionKeyContainer`. <br>
   Merhaba önek `B2C_1A`_ eklenmesi otomatik olarak.<br>
 d. İçin **anahtar türü**, kullanın **RSA**.<br>
 e. İçin **tarihleri**, hello varsayılanları kullanın.<br>
 f. İçin **anahtar kullanımı**, kullanın **şifreleme**.<br>
 g. **Oluştur**’u seçin.<br>
5. B2C_1A_FacebookSecret oluşturun. <br>
Facebook uygulama gizli anahtarı zaten varsa, bu, bir ilke anahtar tooyour Kiracı olarak başına ekleyin. Aksi takdirde, böylece ilkelerinizi geçemediğinden bir yer tutucu değerle hello anahtarı oluşturmanız gerekir.<br>
 a. **Add (Ekle)** seçeneğini belirleyin.<br>
 b. İçin **seçenekleri**, kullanın **el ile**.<br>
 c. İçin **adı**, kullanmak `FacebookSecret`. <br>
 Merhaba önek `B2C_1A_` otomatik olarak eklenebilir.<br>
 d. Merhaba, **gizli** kutusuna, developers.facebook.com, FacebookSecret girin veya `0` yer tutucu olarak. *Bu, Facebook uygulama kimliği değil.* <br>
 e. İçin **anahtar kullanımı**, kullanın **imza**. <br>
 f. Seçin **oluşturma** ve oluşturma onaylayın.

## <a name="register-identity-experience-framework-applications"></a>Kimlik deneyimi Framework uygulamalarını kaydetme

Azure AD B2C hello altyapısı toosign tarafından kullanılır ve kullanıcılar oturum tooregister iki ek uygulamalar gerektirir.

>[!NOTE]
>Bu etkinleştirme yerel hesap kullanarak oturum açın, iki uygulama oluşturmanız gerekir: IdentityExperienceFramework (bir web uygulaması) ve ProxyIdentityExperienceFramework (yerel bir uygulama) ile temsilci hello IdentityExperienceFramework uygulama izni. Yerel hesap yalnızca kiracınızda yok. Kullanıcılarınızı benzersiz e-posta adresi/parola bileşimi tooaccess ile Kiracı kayıtlı uygulamalarınız için kaydolun.

### <a name="create-hello-identityexperienceframework-application"></a>Merhaba IdentityExperienceFramework uygulaması oluşturma

1. Merhaba, [Azure portal](https://portal.azure.com), geçiş hello [Azure AD B2C kiracınızın bağlamında](active-directory-b2c-navigate-to-b2c-context.md).
2. Açık hello **Azure Active Directory** dikey (değil hello **Azure AD B2C** dikey penceresinde). Tooselect gerekebilecek **daha Hizmetleri** toofind onu.
3. Seçin **uygulama kayıtlar**.
4. Seçin **yeni uygulama kaydı**.
   * İçin **adı**, kullanmak `IdentityExperienceFramework`.
   * İçin **uygulama türü**, kullanın **Web app/API**.
   * İçin **oturum açma URL'si**, kullanın `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, burada `yourtenant` , Azure AD B2C Kiracı etki alanı adıdır.
5. **Oluştur**’u seçin.
6. Bir kez oluşturulduktan sonra yeni oluşturulan hello uygulamayı seçin **IdentityExperienceFramework**.<br>
   * Seçin **özellikleri**.<br>
   * Merhaba uygulama kimliği kopyalayın ve daha sonra kullanmak üzere kaydedin.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Merhaba ProxyIdentityExperienceFramework uygulaması oluşturma

1. Seçin **uygulama kayıtlar**.
1. Seçin **yeni uygulama kaydı**.
   * İçin **adı**, kullanmak `ProxyIdentityExperienceFramework`.
   * İçin **uygulama türü**, kullanın **yerel**.
   * İçin **yeniden yönlendirme URI'si**, kullanın `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, burada `yourtenant` , Azure AD B2C kiracısı.
1. **Oluştur**’u seçin.
1. Oluşturulduktan sonra hello uygulama seçeneğini **ProxyIdentityExperienceFramework**.<br>
   * Seçin **özellikleri**. <br>
   * Merhaba uygulama kimliği kopyalayın ve daha sonra kullanmak üzere kaydedin.
1. Seçin **gerekli izinleri**.
1. **Add (Ekle)** seçeneğini belirleyin.
1. Seçin **bir API seçin**.
1. Merhaba adı IdentityExperienceFramework arayın. Seçin **IdentityExperienceFramework** hello sonuçları ve ardından **seçin**.
1. Merhaba onay kutusunu işaretleyin sonraki çok**erişim IdentityExperienceFramework**ve ardından **seçin**.
1. Seçin **Bitti**.
1. Seçin **izinler**ve ardından seçerek onaylayın **Evet**.

## <a name="download-starter-pack-and-modify-policies"></a>Başlatıcı paketini karşıdan yüklemek ve ilkelerini değiştirme

Özel ilkeler, karşıya toobe tooyour Azure AD B2C Kiracı gereken XML dosyaları kümesidir. Başlangıç paketleri tooget sağladığımız, hızlı bir şekilde geçiyor. Kullanıcı Yolculuklar açıklanan tooachieve hello senaryoları gereken ve teknik profilleri en az sayıda hello listesi aşağıdaki hello her başlatıcı paketinde içerir:
 * LocalAccounts. Yalnızca yerel hesaplar Hello kullanımını etkinleştirir.
 * SocialAccounts. Yalnızca sosyal (ya da Federasyon) hesapları Hello kullanımını etkinleştirir.
 * **SocialAndLocalAccounts**. Bu dosya hello kılavuz için kullanırız.
 * SocialAndLocalAccountsWithMFA. Sosyal, yerel ve çok faktörlü kimlik doğrulama seçeneklerini buraya dahil edilir.

Her bir başlangıç paketi içerir:

* Merhaba [temel dosyanın](active-directory-b2c-overview-custom.md#policy-files) hello ilkesi. Birkaç değişikliklerin gerekli toohello temel olduğu.
* Merhaba [uzantısının](active-directory-b2c-overview-custom.md#policy-files) hello ilkesi.  Burada çoğu yapılandırma değişikliklerinin yapılması bu dosyasıdır.
* [Bağlı olan taraf dosyaları](active-directory-b2c-overview-custom.md#policy-files) görev özgü dosyaları, uygulamanız tarafından çağrılır.

>[!NOTE]
>XML düzenleyicinizi doğrulama destekliyorsa, hello dosyalara hello başlangıç paketinin hello kök dizininde yer alan hello TrustFrameworkPolicy_0.3.0.0.xsd XML Şeması karşı doğrulayın. XML şema doğrulaması karşıya yüklemeden önce hataları tanımlar.

 Haydi başlayalım:

1. Github'dan active-directory-b2c-custom-policy-starterpack indirin. [Merhaba .zip dosyasını indirdikten](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) veya çalıştırın

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Merhaba SocialAndLocalAccounts klasörünü açın.  Bu klasördeki Hello temel dosyanın (TrustFrameworkBase.xml) hem yerel hem de sosyal/şirket hesapları için gereken içerik içerir. Merhaba sosyal içerik için yerel hesaplar Başlarken hazırlarken ve çalışırken hello adımlara engellemez.
3. TrustFrameworkBase.xml açın. Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.
4. Merhaba kök `TrustFrameworkPolicy` öğesi, güncelleştirme hello `TenantId` ve `PublicPolicyUri` değiştirme öznitelikleri `yourtenant.onmicrosoft.com` Azure AD B2C kiracınızın hello etki alanı adıyla:
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`Merhaba Portalı'nda bkz hello ilkesi adı ve bu ilke dosyası diğer ilke dosyaları tarafından başvuruluyor hello adıdır.

5. Merhaba dosyasını kaydedin.
6. TrustFrameworkExtensions.xml açın. Merhaba aynı iki değiştirerek değişiklik `yourtenant.onmicrosoft.com` , Azure AD B2C kiracısı ile. Aynı hello olun hello değiştirme `<TenantId>` üç değişiklikleri toplam öğesi. Merhaba dosyasını kaydedin.
7. SignUpOrSignIn.xml açın. Merhaba aynı değiştirerek değişiklik `yourtenant.onmicrosoft.com` üç yerde, Azure AD B2C kiracısı ile. Merhaba dosyasını kaydedin.
8. Açık hello parola sıfırlama ve profili dosyalarını düzenleyebilirsiniz. Merhaba aynı değiştirerek değişiklik `yourtenant.onmicrosoft.com` Azure AD B2C kiracınızda her dosya üç yerde ile. Merhaba dosyalarını kaydedin.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Merhaba uygulama kimlikleri tooyour özel ilke Ekle
Merhaba uygulama kimlikleri toohello uzantıları dosya ekleme (`TrustFrameworkExtensions.xml`):

1. Merhaba öğesi Hello uzantıları dosyasında (TrustFrameworkExtensions.xml), bulma `<TechnicalProfile Id="login-NonInteractive">`.
2. Her iki örneği yerine `IdentityExperienceFrameworkAppId` hello daha önce oluşturduğunuz kimlik deneyimi Framework uygulaması hello uygulama kimliği. Örnek aşağıda verilmiştir:

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. Her iki örneği yerine `ProxyIdentityExperienceFrameworkAppId` hello daha önce oluşturduğunuz Proxy kimlik deneyimi Framework uygulaması hello uygulama kimliği.
4. Uzantıları dosyanızı kaydedin.

## <a name="upload-hello-policies-tooyour-tenant"></a>Merhaba ilkeleri tooyour Kiracı karşıya yükle

1. Merhaba, [Azure portal](https://portal.azure.com), geçiş hello [bağlamı Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md)ve açık hello **Azure AD B2C** dikey.
2. Seçin **kimlik deneyimi Framework**.
3. Seçin **karşıya İlkesi**.

    >[!WARNING]
    >Merhaba özel ilke dosyaları sırasının hello yüklenmelidir:

1. TrustFrameworkBase.xml karşıya yükleyin.
2. TrustFrameworkExtensions.xml karşıya yükleyin.
3. SignUpOrSignin.xml karşıya yükleyin.
4. Diğer ilke dosyalarınızı karşıya yükleyin.

Bir dosyayı karşıya yüklendiğinde, hello ilkesi dosyasının hello adı ile eklenir `B2C_1A_`.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Şimdi Çalıştır kullanarak Hello özel ilkesini test

1. Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.

   >[!NOTE]
   >**Şimdi Çalıştır** en az bir uygulama toobe preregistered hello Kiracı'gerektirir. Uygulamaları kayıtlı, hello kullanarak ya da hello B2C kiracısı içinde **uygulamaları** menü seçimi Azure AD B2C veya hello kimlik deneyimi Framework tooinvoke kullanarak yerleşik ve özel ilkeleri. Uygulama başına yalnızca bir kayıt gerekiyor.<br><br>
   tooregister uygulamaları nasıl görürüm toolearn hello Azure AD B2C [başlama](active-directory-b2c-get-started.md) makale veya hello [uygulama kaydı](active-directory-b2c-app-registration.md) makalesi.  

2. B2C_1A_signup_signin açın, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello. Seçin **Şimdi Çalıştır**.

3. Bir e-posta adresi kullanarak yukarı mümkün toosign olmalıdır.

4. Merhaba elinizde tooconfirm aynı hesabı ile oturum hello doğru yapılandırma.

>[!NOTE]
>Oturum açma hatası ortak bir nedeni yanlış yapılandırılmış bir IdentityExperienceFramework uygulamadır.


## <a name="next-steps"></a>Sonraki adımlar

### <a name="add-facebook-as-an-identity-provider"></a>Facebook kimlik sağlayıcısı olarak Ekle
Facebook yukarı tooset:
1. [Bir Facebook uygulaması içinde developers.facebook.com yapılandırın](active-directory-b2c-setup-fb-app.md).
2. [Merhaba Facebook uygulaması gizli tooyour Azure AD B2C Kiracı eklemek](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).
3. Merhaba TrustFrameworkExtensions ilke dosyasında hello değerini değiştirin `client_id` hello Facebook uygulama kimliği:

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Merhaba TrustFrameworkExtensions.xml ilke dosyası tooyour Kiracı karşıya yükleyin.
5. Kullanarak test **Şimdi Çalıştır** veya hello İlkesi kayıtlı uygulamanızdan doğrudan çağırma.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Azure Active Directory kimlik sağlayıcısı olarak Ekle
Bu başlangıç kılavuzuna içinde zaten kullanılan hello temel dosyanın diğer kimlik sağlayıcılardan eklemek için gereksinim duyduğunuz hello içeriğin içerir. Merhaba oturum açma işlemleri ayarlama hakkında daha fazla bilgi için bkz [Azure Active Directory B2C: Azure AD hesapları kullanarak oturum](active-directory-b2c-setup-aad-custom.md) makalesi.

Merhaba hello kimlik deneyimi Framework kullanan özel Azure AD B2C ilkelere genel bakış için bkz: [Azure Active Directory B2C: özel ilkeler](active-directory-b2c-overview-custom.md) makalesi. 
