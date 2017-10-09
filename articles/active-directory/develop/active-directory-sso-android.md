---
title: "aaaHow tooenable uygulamalar arası SSO'nun ADAL kullanarak Android üzerinde | Microsoft Docs"
description: "Nasıl toouse hello özelliklerini uygulamalarınızı boyunca çoklu oturum açma ADAL SDK tooenable hello. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a>Nasıl tooenable uygulamalar arası SSO'nun ADAL kullanarak Android üzerinde
Böylece kullanıcılar yalnızca tooenter kimlik bilgilerini bir kez gerekir ve bu kimlik bilgilerini otomatik olarak iş uygulamalarda çoklu oturum açma (SSO) sağlayarak müşteriler tarafından şimdi beklenir. ekranda bir telefon araması veya ilerideki kodu gibi ek bir etmen (2FA) kez birlikte küçük, genellikle kullanıcı adı ve parola girme hello zorluk hızlı memnuniyetsizliği kullanıcı sonuçlarında var. toodo bu ürün için birden fazla kez

Ayrıca, Microsoft Accounts veya Office365 iş hesabından gibi diğer uygulamaları kullanabilir bir kimlik platformu uygularsanız, müşterilerin kimlik bilgileri bu toobe kullanılabilir toouse tüm uygulamalar arasında Hayır, hello satıcı önemli bekler.

Merhaba, Microsoft Identity SDK ile birlikte Microsoft Identity platform tüm bu sabit sizin ve SSO ya da kendi paketi uygulamaların veya olarak içinde müşterilerinizle özelliği toodelight hello verir çalışır bizim Aracısı yetenek ve Doğrulayıcı Merhaba tüm aygıt üzerinden uygulamaları.

Bu kılavuz size nasıl söyleyecektir tooconfigure bizim SDK, uygulama tooprovide içinde bu avantajı tooyour müşteriler.

Bu kılavuz için geçerlidir:

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Azure Active Directory Koşullu Erişim

Merhaba belge önceki varsayar nasıl çok bildiğiniz[sağlamak hello eski portalı uygulamalarında Azure Active Directory için](active-directory-how-to-integrate.md) ve uygulamanızı hello ile tümleşik [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android) .

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Microsoft kimlik platformu hello SSO kavramlar
### <a name="microsoft-identity-brokers"></a>Microsoft Identity aracıları
Microsoft hello kimlik bilgilerini farklı satıcılardan uygulamalar arasında köprü oluşturma için izin uygulamaları mobil her platform için sağlar ve nerede tek güvenli bir yerde gerektiren özel Gelişmiş özellikleri sağlar toovalidate kimlik bilgileri. Bunlar diyoruz **aracıların**. İOS ve Android bunlar müşteriler bağımsız olarak yüklemek veya toohello aygıt bazılarını veya tümünü hello cihaz için kendi çalışan yöneten bir şirket tarafından gönderilen indirilebilir uygulamaları aracılığıyla sağlanır. Bu aracıları yönetme güvenlik yalnızca bazı uygulamalar veya ne BT yöneticileri işlemleriniz dayalı hello tüm cihaz desteği. Windows, bu işlev toohello işletim sistemi, teknik olarak Web kimlik doğrulama Aracısı hello bilinen yerleşik bir hesabı seçicide tarafından sağlanır.

Hakkında daha fazla bilgi için bu aracıların ve nasıl müşterilerinizin bunları okuyun hello Microsoft Identity platform için kullanıcıların oturum açma akışını görebileceğiniz kullanırız.

### <a name="patterns-for-logging-in-on-mobile-devices"></a>Mobil cihazlarda günlüğe kaydetme için desenleri
Erişim toocredentials cihazlarda hello Microsoft Identity platformuna yönelik iki temel düzenlerden izleyin:

* Olmayan Aracısı Yardımlı oturum açmalar
* Yardımlı Oturum Aracısı

#### <a name="non-broker-assisted-logins"></a>Olmayan Aracısı Yardımlı oturum açmalar
Olmayan Aracısı Yardımlı satır içi hello uygulamayla gerçekleşir ve hello cihazda bu uygulama için hello yerel depolama kullanan oturum açma deneyimlerini oturumlardır. Bu depolama uygulamalar arasında paylaşılıyor olabilir ancak sıkı şekilde bağlı toohello uygulama ya da bu kimlik bilgilerini kullanarak uygulama paketi hello kimlik bilgileridir. Bir kullanıcı adı ve parola hello uygulamanın kendi içinde girdiğinizde, bu büyük olasılıkla birçok mobil uygulamalarda tecrübe ettiklerinize.

Bu oturumlar hello aşağıdaki faydaları vardır:

* Kullanıcı deneyimi tamamen hello uygulaması içinde zaten var.
* Kimlik bilgileri, hello tarafından imzalanmış uygulamalar arasında paylaşılabilir aynı sertifika, çoklu oturum açma deneyimini tooyour suite uygulamaların sağlama.
* Denetim Günlüğü'nde hello deneyimi geçici toohello uygulama önce ve sonra oturum açma sağlanır.

Bu oturumlar dezavantajları aşağıdaki hello vardır:

* Kullanıcı yalnızca bu Microsoft uygulamanızı yapılandırılmış Identities arasında Microsoft Identity kullanan tüm uygulamalar boyunca çoklu oturum açma deneyimi olamaz.
* Uygulamanız, koşullu erişim veya kullanımı hello Intune ürün paketi gibi daha gelişmiş iş özellikleriyle kullanılamaz.
* Uygulamanızı iş kullanıcıları için sertifika tabanlı kimlik doğrulamasını destekleyemez.

Merhaba Microsoft Identity SDK'ları, uygulamaları tooenable SSO hello paylaşılan depolama ile nasıl bir temsilini şöyledir:

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>Yardımlı Oturum Aracısı
Aracısı destekli hello Aracısı uygulama içinde oluşur ve hello depolama ve güvenlik hello Aracısı tooshare kimlik bilgilerinin hello Microsoft Identity platform uygulanan tüm uygulamalar için hello aygıtta kullanan oturum açma deneyimlerini oturumlardır. Bu, uygulamalarınız hello Aracısı toosign kullanıcılar kullandığını anlamına gelir. İOS ve Android cihazlarda bu aracıların müşteriler bağımsız olarak yüklemek veya toohello aygıt hello cihaz kendi kullanıcı yöneten bir şirket tarafından gönderilen indirilebilir uygulamaları aracılığıyla sağlanır. Merhaba Microsoft Authenticator uygulaması iOS bu tür bir uygulama örneğidir. Windows bu işlevselliği toohello işletim sistemi, teknik olarak Web kimlik doğrulama Aracısı hello bilinen yerleşik bir hesabı seçicide tarafından sağlanır.
Merhaba deneyimi platforma göre değişir ve kesintiye uğratan toousers bazen olabilir değilse doğru şekilde yönetilir. Merhaba Facebook uygulamanın yüklü olması ve başka bir uygulamadan Facebook bağlanmak kullanırsanız bu deseni ile en biliyor. Merhaba Microsoft kimlik platformu kullandığı aynı düzeni hello.

İOS için bu tooa "geçiş" animasyon Burada, uygulamanızın hello Microsoft Authenticator uygulamaları toohello arka toohello ön hello kullanıcı tooselect için gelen gönderilen toosign ile istediğiniz hangi hesabı doğurur.  

Android ve Windows hello hesabı seçicide daha az kesintiye uğratan toohello kullanıcı olan, uygulamanızın üzerinde görüntülenir.

#### <a name="how-hello-broker-gets-invoked"></a>Merhaba Aracısı nasıl çağrılır
Uyumlu bir aracı hello Microsoft Authenticator uygulaması, hello Microsoft Identity SDK'ları otomatik olarak ayarlanır gibi hello aygıtta yüklüyse, bir kullanıcı herhangi bir hesabı kullanarak toolog istedikleri belirttiğinde hello broker çağırma iş hello Merhaba Microsoft Identity platform. Bu hesap, kişisel Microsoft Account, bir iş veya Okul hesabı veya bir sağladığınız hesap ve konak B2C ve B2B Ürünlerimiz kullanarak azure'da olabilir. 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a>Biz Merhaba uygulaması nasıl emin geçerlidir
 
 Merhaba gerek tooensure hello bir uygulama çağrısı hello Aracısı destekli Aracısı oturum açma bilgilerini sağladığımız önemli toohello güvenlik kimliğidir. İOS ne Android kötü amaçlı uygulamalar ve "yasal uygulamanın tanımlayıcı aldatıcı" Merhaba yasal uygulaması için amacı hello belirteçleri almak için yalnızca belirli bir uygulama için geçerli olan benzersiz tanımlayıcıları zorlar. Biz her zaman zamanında hello doğru uygulama ile iletişim kuran tooensure, biz hello Geliştirici tooprovide özel redirectURI kendi uygulama Microsoft ile kaydedilirken isteyin. **Geliştiricilerin bu yeniden yönlendirme URI'si nasıl oluşturabilir aşağıda ayrıntılı olarak ele alınmıştır.** Bu özel redirectURI ve toobe benzersiz toohello uygulama Google Play mağazası hello tarafından güvence altına hello sertifika parmak izi hello uygulamasının içerir. Bir uygulama hello Aracısı hello Android işletim sistemi tooprovide ister hello Aracısı çağırdığında hello ile sertifika parmak izi, çağrılan hello Aracısı. Merhaba Aracısı bu sertifika parmak izi tooMicrosoft hello çağrısı tooour kimlik sistemi sağlar. Hello sertifika parmak izi Merhaba uygulaması hello sertifika parmak iziyle eşleşmiyor kayıt sırasında toous hello geliştirici tarafından sağlanan, hello kaynak hello uygulama istenirken için size erişim toohello belirteçleri reddeder. Bu denetim yalnızca hello geliştirici tarafından kayıtlı hello uygulama belirteçlerini almasını sağlar.

**Microsoft Identity SDK Hello hello Aracısı çağıran veya hello aracı olmayan Yardımlı akış kullanıyorsa, hello Geliştirici hello seçimine sahiptir.** Hello geliştirici değil toouse hello Aracısı destekli akış seçerse, ancak bunlar hello yararı SSO kimlik bilgilerini kullanarak bu hello kullanıcı kaybedersiniz hello aygıtta eklemiş olabilir ve kendi uygulama Microsoft iş özelliklerle kullanılmasını engeller Koşullu erişim, Intune yönetim özellikleri ve sertifika tabanlı kimlik doğrulaması gibi müşterilerinin sağlar.

Bu oturumlar hello aşağıdaki faydaları vardır:

* Kullanıcı, kendi hello satıcı olursa olsun tüm uygulamalar arasında SSO karşılaşır.
* Uygulamanız, koşullu erişim gibi daha gelişmiş iş özellikleri kullanın veya ürün hello Intune paketi kullanın.
* Uygulamanızı iş kullanıcıları için sertifika tabanlı kimlik doğrulamasını destekler.
* Çok daha güvenli oturum açma hello uygulama ve hello kullanıcı hello kimliği doğrulandı gibi ek güvenlik algoritmalarını ve şifreleme ile Merhaba Aracısı uygulaması tarafından karşılaşırsınız.

Bu oturumlar dezavantajları aşağıdaki hello vardır:

* Kimlik bilgileri seçilen sırada hello kullanıcı iOS uygulamanızın deneyimi dışında geçti.
* Kayıp hello özelliği toomanage hello oturum açma deneyimi müşterilerinize uygulamanızın içinde.

Nasıl hello Microsoft Identity SDK'ları hello çalışmak Aracısı uygulamaları tooenable SSO bir temsilini şöyledir:

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

Bu bilgiler ile çağrılmak mümkün toobetter olmalıdır anlamanıza ve SSO hello Microsoft Identity platform ve SDK'ları kullanarak uygulamanızdaki uygulamanıza.

## <a name="enabling-cross-app-sso-using-adal"></a>ADAL kullanarak uygulamalar arası SSO'nun etkinleştirme
Merhaba ADAL Android SDK burada kullandığımız için:

* Aracı olmayan Yardımlı SSO Uygulama paketiniz için Aç
* Aracısı destekli SSO desteği Aç

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Aracı olmayan için SSO üzerinde kapatma SSO Destekli
Uygulamalar arasında aracı olmayan Yardımlı SSO için hello Microsoft Identity SDK'ları yönetmek SSO hello karmaşıklığını çoğunu sizin için. Bu, hello Önbelleği'nde hello doğru kullanıcı bulma ve bakımını yapma, tooquery için oturum açan kullanıcıların listesini içerir.

Aşağıdaki toodo hello ihtiyacınız sahip uygulamalar arasında SSO tooenable:

1. Tüm, uygulamaların kullanıcı hello aynı istemci Kimliğini veya uygulama kimliği emin olun
2. Tüm uygulamalarınızın aynı SharedUserID ayarlamak hello emin olun.
3. Tüm depolama paylaştırabilirsiniz deposundan hello Google Play aynı imzalama sertifika, uygulama paylaşımı hello olun.

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>1. adım: Aynı istemci kimliği hello kullanarak / tüm uygulamaların paketiniz uygulamalarda hello için uygulama kimliği
Bu tooshare belirteçleri, uygulamalar arasında izin verildiğini sırayla hello Microsoft Identity platform tooknow için uygulamalarınızın her birinde aynı istemci Kimliğini veya uygulama kimliği tooshare hello gerekir Bu ilk uygulamanızı hello Portalı'nda kayıtlı yükleyen tooyou sağlanan hello benzersiz tanımlayıcısıdır.

Farklı uygulamaları nasıl kullanacağını merak ediyor toohello onu kullanıyorsa, Microsoft Identity hizmet hello aynı uygulama kimliği Merhaba cevaptır ile Merhaba **yeniden yönlendirme URI'ler**. Her uygulamanın birden çok yeniden yönlendirme hello hazırlama Portalı'nda kayıtlı URI'ler olabilir. Her uygulama paketiniz içinde farklı bir yeniden yönlendirme URI'sine sahip olur. Bu sistem, bir örnek aşağıda verilmiştir:

App1 yeniden yönlendirme URİ'si:`msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`

App2 yeniden yönlendirme URİ'si:`msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`

App3 yeniden yönlendirme URİ'si:`msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`

....

Bunlar altında yuvalanmış aynı istemci kimliği hello / uygulama kimliği ve Aranan göre hello redirect URI SDK yapılandırmanızda toous döndürür.

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*Bu yeniden yönlendirme URI biçimi hello Not aşağıda açıklanmıştır. Toosupport hello Aracısı istediğiniz sürece herhangi bir yeniden yönlendirme URI'si kullanabilir, bu durumda bunlar şunun gibi hello yukarıdaki görünmesi gerekir*

#### <a name="step-2-configuring-shared-storage-in-android"></a>2. adım: Android paylaşılan depolama ortamı yapılandırma
Ayar hello `SharedUserID` hello bu belgenin kapsamında değildir ancak hello hello Google Android belgeleri okuyarak öğrenilebilecek [bildirim](http://developer.android.com/guide/topics/manifest/manifest-element.html). Önemli olan, sharedUserID çağrılacağı ve tüm uygulamalar için kullanmak istediğinize karar ' dir.

Merhaba olduktan sonra `SharedUserID` hazır toouse SSO olduğunuz tüm uygulamalarınızda.

> [!WARNING]
> Uygulamalar arasında depolama paylaştığınızda herhangi bir uygulama bu bölge kullanıcılar silin veya tüm hello belirteçleri, uygulamanızda da kötüsü silin. Merhaba belirteçleri toodo arka plan çalışması üzerinde kullanan uygulamalar varsa, özellikle felaket niteliğinde budur. Depolama paylaşımı hello Microsoft Identity SDK'ları aracılığıyla tüm kaldırma işlemleri çok dikkatli olmalıdır anlamına gelir.
> 
> 

İşte bu kadar! Microsoft Identity SDK Hello şimdi tüm uygulamalar için kimlik bilgileri paylaşacaktır. Merhaba kullanıcı listesinde de uygulama örnekleri arasında paylaşılır.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>SSO destekli aracısı için SSO üzerinde kapatma
Merhaba hello cihazda yüklü Aracısı olduğu bir uygulama toouse yeteneği **varsayılan olarak devre dışı**. İçinde uygulamanızın toouse sipariş hello Aracısı ile bazı ek yapılandırma adımları ve bazı kodu tooyour uygulama eklemeniz gerekir.

Merhaba adımları toofollow şunlardır:

1. Uygulama kodun çağrısı toohello MS SDK Aracısı modunda etkinleştirme
2. Yeni yeniden yönlendirme URI'si oluşturmak ve bu tooboth hello uygulama ve uygulama kaydınızı sağlayın
3. Merhaba Android bildiriminde hello doğru izinleri ayarlama

#### <a name="step-1-enable-broker-mode-in-your-application"></a>1. adım: uygulamanızı Aracısı modunda etkinleştirme
hello "ayarlar" ya da kimlik doğrulama örneğinizi ilk kurulumu oluşturduğunuzda, uygulama toouse hello Aracısı hello özelliği açıktır. Kodunuzda ApplicationSettings türünüz ayarlayarak bunu yapabilirsiniz:

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a>2. adım: yeni yeniden yönlendirme URI'si URL şeması ile oluşturma
Her zaman hello kimlik bilgisi toohello doğru uygulama belirteçleri döndürürüz, sipariş tooensure içinde toomake geri tooyour uygulaması, Android işletim sistemi hello şekilde doğrulayabilirsiniz diyoruz emin gerekir. Merhaba Android işletim sistemi hello Google Play mağazasına hello hello sertifika karmasını kullanır. Standart dışı bir uygulama tarafından sahte olamaz. Bu nedenle, biz bu hello belirteçleri toohello doğru uygulama döndürüldüğünü bizim Aracısı uygulama tooensure URI'sini hello birlikte yararlanın. Tooestablish biz bizim Geliştirici Portalı'nda tek tek bir yeniden yönlendirme URI'si bu benzersiz yeniden yönlendirme URI'si hem de uygulama ve kümesi gerektirir.

Yeniden yönlendirme URI'si hello uygun biçiminde olmalıdır:

`msauth://packagename/Base64UrlencodedSignature`

örn: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*

Bu yeniden yönlendirme URI'si uygulama kaydınızı hello kullanarak belirtilen toobe gereken [Azure portal](https://portal.azure.com/). Azure AD uygulama kaydı hakkında daha fazla bilgi için bkz: [Azure Active Directory ile tümleştirme](active-directory-how-to-integrate.md).

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a>3. adım: uygulamanızda hello doğru izinleri ayarlayın
Aracısı uygulamamız Android uygulamalar arasında hello Hesapları Yöneticisi özelliği hello Android işletim sistemi toomanage kimlik bilgileri kullanır. Sipariş toouse hello Aracısı Android uygulama bildiriminizi izinleri toouse AccountManager hesapları olmalıdır. Bu ayrıntılı hello olarak ele alınmıştır [Google hesabı Manager belgeleri burada](http://developer.android.com/reference/android/accounts/AccountManager.html)

Özellikle, bu izinler şunlardır:

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a>SSO yapılandırdıktan!
Şimdi hello Microsoft Identity SDK otomatik olarak hem kimlik bilgileri, uygulamalar arasında paylaşmak ve cihazlarının varsa hello Aracısı çağırma.

