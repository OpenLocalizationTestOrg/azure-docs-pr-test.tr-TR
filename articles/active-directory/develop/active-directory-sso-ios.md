---
title: "aaaHow tooenable uygulamalar arası SSO'nun ADAL kullanarak iOS | Microsoft Docs"
description: "Nasıl toouse hello özelliklerini uygulamalarınızı boyunca çoklu oturum açma ADAL SDK tooenable hello. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a>Nasıl tooenable uygulamalar arası SSO'nun ADAL kullanarak iOS
Böylece kullanıcılar yalnızca tooenter kimlik bilgilerini bir kez gerekir ve bu kimlik bilgilerini otomatik olarak iş uygulamalarda çoklu oturum açma (SSO) sağlayarak müşteriler tarafından şimdi beklenir. ekranda bir telefon araması veya ilerideki kodu gibi ek bir etmen (2FA) kez birlikte küçük, genellikle kullanıcı adı ve parola girme hello zorluk hızlı memnuniyetsizliği kullanıcı sonuçlarında var. toodo bu ürün için birden fazla kez

Ayrıca, Microsoft Accounts veya Office365 iş hesabından gibi diğer uygulamaları kullanabilir bir kimlik platformu uygularsanız, müşterilerin kimlik bilgileri bu toobe kullanılabilir toouse tüm uygulamalar arasında Hayır, hello satıcı önemli bekler.

Merhaba, Microsoft Identity SDK ile birlikte Microsoft Identity platform tüm bu sabit sizin ve SSO ya da kendi paketi uygulamaların veya olarak içinde müşterilerinizle özelliği toodelight hello verir çalışır bizim Aracısı yetenek ve Doğrulayıcı Merhaba tüm aygıt üzerinden uygulamaları.

Bu kılavuz size nasıl söyleyecektir tooconfigure bizim SDK, uygulama tooprovide içinde bu avantajı tooyour müşteriler.

Bu kılavuz için geçerlidir:

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Azure Active Directory Koşullu Erişim

Merhaba belge önceki varsayar nasıl çok bildiğiniz[sağlamak hello eski portalı uygulamalarında Azure Active Directory için](active-directory-how-to-integrate.md) ve uygulamanızı hello ile tümleşik [Microsoft Identity iOS SDK'sı](https://github.com/AzureAD/azure-activedirectory-library-for-objc).

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Microsoft kimlik platformu hello SSO kavramlar
### <a name="microsoft-identity-brokers"></a>Microsoft Identity aracıları
Microsoft hello kimlik bilgilerini farklı satıcılardan uygulamalar arasında köprü oluşturma için izin uygulamaları mobil her platform için sağlar ve nerede tek güvenli bir yerde gerektiren özel Gelişmiş özellikleri sağlar toovalidate kimlik bilgileri. Bunlar diyoruz **aracıların**. İOS ve Android cihazlarda bu aracıların müşteriler bağımsız olarak yüklemek veya toohello aygıt bazılarını veya tümünü hello cihaz için kendi çalışan yöneten bir şirket tarafından gönderilen indirilebilir uygulamaları aracılığıyla sağlanır. Bu aracıları yönetme güvenlik yalnızca bazı uygulamalar veya ne BT yöneticileri işlemleriniz dayalı hello tüm cihaz desteği. Windows, bu işlev toohello işletim sistemi, teknik olarak Web kimlik doğrulama Aracısı hello bilinen yerleşik bir hesabı seçicide tarafından sağlanır.

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
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
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
 
 Merhaba gerek tooensure hello bir uygulama çağrısı hello Aracısı destekli Aracısı oturum açma bilgilerini sağladığımız önemli toohello güvenlik kimliğidir. İOS ne Android kötü amaçlı uygulamalar ve "yasal uygulamanın tanımlayıcı aldatıcı" Merhaba yasal uygulaması için amacı hello belirteçleri almak için yalnızca belirli bir uygulama için geçerli olan benzersiz tanımlayıcıları zorlar. Biz her zaman zamanında hello doğru uygulama ile iletişim kuran tooensure, biz hello Geliştirici tooprovide özel redirectURI kendi uygulama Microsoft ile kaydedilirken isteyin. **Geliştiricilerin bu yeniden yönlendirme URI'si nasıl oluşturabilir aşağıda ayrıntılı olarak ele alınmıştır.** Bu özel redirectURI ve toobe benzersiz toohello uygulama hello Apple App Store tarafından güvence altına hello hello uygulama paket Kimliğini içerir. Bir uygulama çağrıları hello Aracısı hello iOS hello Aracısı sorduğunda işletim sistemi tooprovide ile Merhaba hello Aracısı adlı bir paket kimliği. Merhaba Aracısı bu paket kimliği tooMicrosoft hello çağrısı tooour kimlik sistemi sağlar. Merhaba hello uygulama paket Kimliğini paket kimliği kayıt sırasında toous hello geliştirici tarafından sağlanan hello eşleşmiyorsa hello kaynak hello uygulama istenirken için size erişim toohello belirteçleri reddeder. Bu denetim yalnızca hello geliştirici tarafından kayıtlı hello uygulama belirteçlerini almasını sağlar.

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
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
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
Merhaba ADAL iOS SDK'sı burada kullandığımız için:

* Aracı olmayan Yardımlı SSO Uygulama paketiniz için Aç
* Aracısı destekli SSO desteği Aç

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Aracı olmayan için SSO üzerinde kapatma SSO Destekli
Uygulamalar arasında aracı olmayan Yardımlı SSO için hello Microsoft Identity SDK'ları yönetmek SSO hello karmaşıklığını çoğunu sizin için. Bu, hello Önbelleği'nde hello doğru kullanıcı bulma ve bakımını yapma, tooquery için oturum açan kullanıcıların listesini içerir.

Aşağıdaki toodo hello ihtiyacınız sahip uygulamalar arasında SSO tooenable:

1. Tüm, uygulamaların kullanıcı hello aynı istemci Kimliğini veya uygulama kimliği emin olun
2. Tüm aynı imzalama sertifikası Apple'dan anahtarlıklar paylaştırabilirsiniz, uygulama paylaşımı hello olun
3. İstek Merhaba, uygulamaların her biri için aynı Anahtarlık yetkilerini.
4. Hello Microsoft Identity SDK'ları hakkında paylaşılan hello Anahtarlık toouse istediğiniz bize bildirin.

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>Merhaba aynı istemci kimliği kullanarak / tüm uygulamaların paketiniz uygulamalarda hello için uygulama kimliği
Bu tooshare belirteçleri, uygulamalar arasında izin verildiğini sırayla hello Microsoft Identity platform tooknow için uygulamalarınızın her birinde aynı istemci Kimliğini veya uygulama kimliği tooshare hello gerekir Bu ilk uygulamanızı hello Portalı'nda kayıtlı yükleyen tooyou sağlanan hello benzersiz tanımlayıcısıdır.

Farklı uygulamaları nasıl kullanacağını merak ediyor toohello onu kullanıyorsa, Microsoft Identity hizmet hello aynı uygulama kimliği Merhaba cevaptır ile Merhaba **yeniden yönlendirme URI'ler**. Her uygulamanın birden çok yeniden yönlendirme hello hazırlama Portalı'nda kayıtlı URI'ler olabilir. Her uygulama paketiniz içinde farklı bir yeniden yönlendirme URI'sine sahip olur. Bu sistem, bir örnek aşağıda verilmiştir:

App1 yeniden yönlendirme URİ'si:`x-msauth-mytestiosapp://com.myapp.mytestapp`

App2 yeniden yönlendirme URİ'si:`x-msauth-mytestiosapp://com.myapp.mytestapp2`

App3 yeniden yönlendirme URİ'si:`x-msauth-mytestiosapp://com.myapp.mytestapp3`

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

#### <a name="create-keychain-sharing-between-applications"></a>Uygulamalar arasında paylaşma Anahtarlık oluşturma
Anahtarlık paylaşımının etkinleştirilmesi hello bu belgenin kapsamı dışındadır ve Apple'nın kendi belgede ele alınan [yetenekleri ekleme](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html). Önemli olarak adlandırılan, Anahtarlık toobe istediğinize karar verin ve tüm uygulamalar için bu özelliği eklemek olmasıdır.

Varsa doğru ayarladığınıza yetkilendirmeler yetkili proje dizininde bir dosyasına görmelisiniz `entitlements.plist` hello şuna benzeyen bir şey içeren:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

Her uygulamalarınız etkinleştirdiği hello Anahtarlık yetkilendirme varsa, ve hazır toouse SSO sonra hello Microsoft Identity SDK hakkında Anahtarlık ayarında aşağıdaki hello kullanarak söyleyin, `ADAuthenticationSettings` ayarı aşağıdaki hello ile:

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> Uygulamalar arasında bir Anahtarlık paylaştığınızda herhangi bir uygulama kullanıcıların silin veya tüm hello belirteçleri, uygulamanızda da kötüsü silin. Merhaba belirteçleri toodo arka plan çalışması üzerinde kullanan uygulamalar varsa, özellikle felaket niteliğinde budur. Bir Anahtarlık paylaşımı kaldırma işlemleri hello Microsoft Identity SDK'ları aracılığıyla içindeki tüm çok dikkatli olmalıdır anlamına gelir.
> 
> 

İşte bu kadar! Microsoft Identity SDK Hello şimdi tüm uygulamalar için kimlik bilgileri paylaşacaktır. Merhaba kullanıcı listesinde de uygulama örnekleri arasında paylaşılır.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>SSO destekli aracısı için SSO üzerinde kapatma
Merhaba hello cihazda yüklü Aracısı olduğu bir uygulama toouse yeteneği **varsayılan olarak devre dışı**. İçinde uygulamanızın toouse sipariş hello Aracısı ile bazı ek yapılandırma adımları ve bazı kodu tooyour uygulama eklemeniz gerekir.

Merhaba adımları toofollow şunlardır:

1. Uygulama kodun çağrısı toohello MS SDK Aracısı modunda etkinleştirin.
2. Yeni yeniden yönlendirme URI'si oluşturmak ve bu tooboth hello uygulama ve uygulama kaydınızı sağlayın.
3. URL şeması kaydediliyor.
4. iOS9 desteği: izni tooyour info.plist dosyası ekleyin.

#### <a name="step-1-enable-broker-mode-in-your-application"></a>1. adım: uygulamanızı Aracısı modunda etkinleştirme
hello "context" ya da kimlik doğrulama nesnenizin ilk kurulum oluşturduğunuzda, uygulama toouse hello Aracısı hello özelliği açıktır. Kimlik bilgileri türü kodunuzda ayarlayarak bunu yapabilirsiniz:

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
Merhaba `AD_CREDENTIALS_AUTO` ayarı hello Microsoft Identity SDK tootry toocall toohello Aracısı çıkışı izin `AD_CREDENTIALS_EMBEDDED` hello Microsoft Identity SDK toohello Aracısı çağırma engeller.

#### <a name="step-2-registering-a-url-scheme"></a>2. adım: bir URL şemasını kaydetme
Merhaba Microsoft Identity platformu URL'leri tooinvoke hello aracısı ve ardından dönüş denetim geri tooyour uygulaması kullanır. toofinish bir URL şemasını ihtiyacınız o gidiş dönüş bu hello Microsoft Platformu hakkında bilirsiniz Identity uygulamanız için kayıtlı. Bu ek olarak tooany daha önce kaydettirdiğiniz uygulamanızla diğer uygulama düzenleri olabilir.

> [!WARNING]
> URL şeması oldukça benzersiz toominimize hello hello kullanarak başka bir uygulama olasılığını hello yapmadan öneririz aynı URL şeması. Apple hello uygulama Mağazası'nda kayıtlı URL şemalarını hello benzersizliğini uygulamaz.
> 
> 

Aşağıda, bu proje yapılandırmanızda görünme bir örnektir. Ayrıca bu Xcode'da de yapabilirsiniz:

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a>Adım 3: yeni yeniden yönlendirme URI'si URL şeması ile oluşturma
Her zaman hello kimlik bilgisi toohello doğru uygulama belirteçleri döndürürüz, sipariş tooensure içinde toomake geri tooyour uygulaması, iOS işletim sistemi hello şekilde doğrulayabilirsiniz diyoruz emin gerekir. Merhaba iOS işletim sistemi raporları toohello Microsoft Aracısı uygulamaları, çağırma hello uygulama paket Kimliğini hello. Standart dışı bir uygulama tarafından sahte olamaz. Bu nedenle, biz bu hello belirteçleri toohello doğru uygulama döndürüldüğünü bizim Aracısı uygulama tooensure URI'sini hello birlikte yararlanın. Tooestablish biz bizim Geliştirici Portalı'nda tek tek bir yeniden yönlendirme URI'si bu benzersiz yeniden yönlendirme URI'si hem de uygulama ve kümesi gerektirir.

Yeniden yönlendirme URI'si hello uygun biçiminde olmalıdır:

`<app-scheme>://<your.bundle.id>`

örn: *x msauth mytestiosapp://com.myapp.mytestapp*

Bu yeniden yönlendirme URI'si uygulama kaydınızı hello kullanarak belirtilen toobe gereken [Azure portal](https://portal.azure.com/). Azure AD uygulama kaydı hakkında daha fazla bilgi için bkz: [Azure Active Directory ile tümleştirme](active-directory-how-to-integrate.md).

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a>Adım 3a: yeniden yönlendirme URI'si, uygulama ve Geliştirici Portalı toosupport sertifika tabanlı kimlik doğrulaması ekleme
toosupport sertifikası tabanlı kimlik doğrulaması ikinci "msauth" gerekiyor, uygulama ve hello kayıtlı toobe [Azure portal](https://portal.azure.com/) tooadd istiyorsanız toohandle sertifika kimlik doğrulamasını destekleyen uygulamanızda.

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

örn: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a>4. adım: iOS9: bir yapılandırma parametresi tooyour uygulama Ekle
ADAL kullanan – canOpenURL: hello Aracısı hello cihazda yüklü değilse toocheck. İOS 9 Apple ne uygulama düzenleri sorgulayabilir aşağı kilitli. Tooadd "msauth" toohello LSApplicationQueriesSchemes bölümünü gerekir, `info.plist file`.

<key>LSApplicationQueriesSchemes</key>

<array><string>msauth</string>
</array>

### <a name="youve-configured-sso"></a>SSO yapılandırdıktan!
Şimdi hello Microsoft Identity SDK otomatik olarak hem kimlik bilgileri, uygulamalar arasında paylaşmak ve cihazlarının varsa hello Aracısı çağırma.

