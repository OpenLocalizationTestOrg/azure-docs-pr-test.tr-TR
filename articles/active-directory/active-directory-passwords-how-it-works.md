---
title: "Derin Dalış: Azure AD SSPR'yi | Microsoft Docs"
description: "Derin Dalış Azure AD Self Servis parola sıfırlama"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 0fa05ee6a2df13845024e770a82f50ab7f75bafd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Self Servis parola sıfırlama Azure AD derin Dalış

SSPR nasıl çalışır? Bu seçenek arabiriminde anlamı nedir? Azure AD Self Servis parola hakkında daha fazla bilgi için okumaya devam sıfırlayın.

## <a name="how-does-the-password-reset-portal-work"></a>Parola portalı iş nasıl sıfırlama

Bir kullanıcı gittiğinde parola sıfırlama portalını, bir iş akışı belirlemek için başlayacağı zamana devre dışı:

   * Nasıl sayfa yerelleştirilmiş?
   * Kullanıcı hesabı geçerli mi?
   * Hangi kuruluş için kullanıcının ait?
   * Kullanıcının parolasını yönetildiği?
   * Kullanıcı bu özelliği kullanmak için lisanslanır?


Parola sıfırlama sayfası arkasındaki mantığı hakkında bilgi edinmek için aşağıdaki adımları okuyun.

1. Kullanıcı hesabı bağlantısı veya gelecek doğrudan erişemiyor [https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Deneyimi uygun dili işlenmeden tarayıcı yerel ayar temel. Office 365 desteklediği parola sıfırlama deneyimi aynı dillere yerelleştirilmiştir.
3. Kullanıcı bir kullanıcı kimliği girer ve bir güvenlik kodu geçirir.
4. Azure AD kullanıcı aşağıdakileri yaparak bu özelliği kullanabilmek için olup olmadığını doğrular:
   * Kullanıcının bu özellik etkinleştirildiğinde ve bir Azure AD lisansı atanmış olup olmadığını denetler.
     * Kullanıcının bu özellik etkinleştirildiğinde veya atanmış bir lisans yoksa, kullanıcı parolasını sıfırlamayı kendi yöneticisine başvurun istenir.
   * Kullanıcı hakkına sahip denetimleri hesaplarında Yönetici İlkesi uygun olarak tanımlanan verileri sınama.
     * İlkesi yalnızca bir sınama gerektiriyorsa, ardından bu kullanıcı için en az bir yönetici İlkesi tarafından etkinleştirilen zorluklar tanımlanan uygun veri olduğunu güvence altına.
       * Kullanıcı yapılandırılmamışsa, kullanıcı parolasını sıfırlamayı kendi yöneticisine başvurmanız önerilir.
     * İlkesi iki zorluk gerektiriyorsa, ardından bunu kullanıcının en az iki Yönetici İlkesi tarafından etkinleştirilen zorluklar için tanımlanan uygun veri olduğunu güvence altına.
       * Kullanıcı yapılandırılmamış sonra biz kullanıcıdır parolasını sıfırlamak için kendi yöneticisine başvurmanız önerilir.
   * Kullanıcının parolasını (Federe veya parola karması eşitlenen) şirket içinde yönetilen olup olmadığını denetler.
     * Daha sonra geri yazma dağıtılır ve kullanıcının parolasını şirket içinde yönetilir, kullanıcı kimliğini ve parolasını sıfırlamak için devam etmesine izin verilir.
     * Geri yazma dağıtılmadığı ve kullanıcının parolasını şirket içinde yönetilir, ardından kullanıcının parolasını sıfırlamak için kendi yöneticisine başvurun istenir.
5. Kullanıcının parolasını başarıyla sıfırlayamazsınız olduğunu belirlenirse kullanıcı sıfırlama işlemi boyunca yönlendirilir.

## <a name="authentication-methods"></a>Kimlik doğrulama yöntemleri

Self Servis parola sıfırlama (SSPR) etkinleştirilirse, en az bir kimlik doğrulama yöntemleri için aşağıdaki seçeneklerden birini seçmeniz gerekir. Böylece, kullanıcılarınızın daha fazla esnekliğe sahip en az iki kimlik doğrulama yöntemi seçme öneririz.

* E-posta
* Cep telefonu
* Ofis telefonu
* Güvenlik Soruları

### <a name="what-fields-are-used-in-the-directory-for-authentication-data"></a>Hangi alanların dizinde kimlik doğrulama verileri için kullanılır

* Ofis telefonu iş telefonu karşılık gelen
    * Kullanıcılar bu ayarlanamıyor kendilerini onu tanımlanmalıdır bir yönetici tarafından alan
* Cep telefonu kimlik doğrulama telefon (herkese görünür) veya cep telefonu (herkese görünür) karşılık gelir.
    * Hizmet için kimlik doğrulama telefon ilk görünür, ardından cep telefonuna geri döner yoksa
* Kimlik doğrulama e-posta (herkese görünür) veya alternatif e-posta için alternatif e-posta adresi karşılık gelen
    * Hizmet kimlik doğrulama e-posta için önce arar ve ardından geri alternatif e-posta başarısız

Varsayılan olarak, yalnızca bulut öznitelikleri ofis telefonu ve cep telefonu, kimlik doğrulama verileri için şirket içi dizininizden bulut dizininiz için eşitlenir.

Bunlar, yönetici etkin olduğundan ve gerektiren kimlik doğrulama yöntemlerini mevcut verileri varsa kullanıcılar yalnızca parolalarını sıfırlayabilir.

Kullanıcıların cep telefonu numaralarına dizinde görünür olmasını istiyor musunuz ancak hala parola sıfırlama için kullanmak istediğiniz yöneticileri değil doldurmak bu dizinde ve kullanıcı ardından doldurur kendi **kimlik doğrulama telefon** aracılığıyla özniteliği [parola sıfırlama kayıt portalı](http://aka.ms/ssprsetup). Yöneticiler kullanıcı profili için bu bilgiyi görebilir, ancak başka bir yerde yayınlanmadı. Azure yönetici hesabı kimlik doğrulaması telefon numarasını kaydederse, cep telefonu alana doldurulur ve görülebilir.

### <a name="number-of-authentication-methods-required"></a>Gereken kimlik doğrulama yöntemleri sayısı

Bu seçenek en az bir kullanıcı sıfırlama veya parolalarını kilidini açmak için geçtikleri gerekir ve 1 veya 2'ye ayarlanabilir kullanılabilir kimlik doğrulama yöntemleri sayısını belirler.

Kullanıcılar, yönetici tarafından etkinleştirilmişse daha fazla kimlik doğrulama yöntemleri sağlamak seçebilirsiniz.

Bir kullanıcıya kayıtlı gerekli en düşük yöntemleri yoksa, parolasını sıfırlamak için yönetici istemek için yönlendirmez bir hata sayfası görürler.

### <a name="how-secure-are-my-security-questions"></a>My güvenlik soruları ne kadar güvenli mi

Güvenlik soruları kullanırsanız, bazı kişiler başka bir kullanıcı soruların yanıtlarını bildiğiniz beri bunlar diğer yöntemlerinden daha az güvenli olabilir olarak bunları kullanımda başka bir yöntemle öneririz.

> [!NOTE] 
> Güvenlik soruları dizininde bir kullanıcı nesnesi üzerinde özel olarak ve güvenli bir şekilde depolanır ve kullanıcılar tarafından kayıt sırasında yalnızca yanıtlanması. Hiçbir şekilde okumak veya kullanıcılar değiştirmek bir yöneticinin soru veya yanıt.
>

### <a name="security-question-localization"></a>Güvenlik sorusu yerelleştirme

İzleyen tüm önceden tanımlanmış sorular kullanıcının tarayıcı bölgesel ayarına göre Office 365 diller, tamamını içine yerelleştirilmiştir.

* İlk eşiniz/partneriniz ile hangi şehirde tanıştınız?
* Anneniz ile babanız hangi şehirde tanıştı?
* Size en yakın kardeşiniz hangi şehirde yaşıyor?
* Babanız hangi şehirde doğdu?
* İlk işiniz hangi şehirdeydi?
* Anneniz hangi şehirde doğdu?
* 2000 yılına girdiğimiz yılbaşında hangi şehirdeydiniz?
* Yüksek içinde en sevdiğiniz öğretmenin soyadı nedir * Okul?
* Başvurduğunuz ancak gitmediğiniz üniversitenin adı nedir?
* İlk düğününüzü gerçekleştirdiğiniz yerin adı nedir?
* Babanızın ikinci adı nedir?
* En sevdiğiniz yemek nedir?
* Anneannenizin adı ve soyadı nedir?
* Annenizin ikinci adı nedir?
* En büyük kardeşinizin Doğum günü ay ve yıl nedir? (örn. Kasım 1985)
* En büyük kardeşinizin ikinci adı nedir?
* Dedenizin adı ve soyadı nedir?
* En küçük kardeşinizin ikinci adı nedir?
* Altıncı sınıfta hangi okula gidiyordunuz?
* Çocukken en iyi arkadaşınızın adı ve soyadı neydi?
* İlk partnerinizin adı ve soyadı neydi?
* İlkokulda en sevdiğiniz öğretmenin soyadı neydi?
* İlk arabanızın veya motosikletinizin markası ve modeli neydi?
* Gittiğiniz ilk okulun adı neydi?
* Doğduğunuz hastanenin adı neydi?
* Çocukluğunuzun geçtiği ilk evin bulunduğu sokağın adı neydi?
* Çocukluk kahramanınızın adı neydi?
* En sevdiğiniz peluş hayvanın adı neydi?
* İlk evcil hayvanınızın adı neydi?
* Çocukken lakabınız neydi?
* Lisedeyken en sevdiğiniz spor hangisiydi?
* İlk işiniz neydi?
* Çocukken kullandığınız telefon numaranızın son dört rakamı neydi?
* Küçükken büyüdüğünüzde ne olmak istiyordunuz?
* Tanıştığınız en ünlü kişi kim?

### <a name="custom-security-questions"></a>Özel güvenlik soruları

Özel güvenlik soruları farklı yerel ayarlar için yerelleştirilmiş değil. Tüm özel sorular kullanıcının tarayıcı yerel farklı olsa bile yönetici kullanıcı arabiriminde girildiği dilde görüntülenir. Yerelleştirilmiş soruları gerekiyorsa, lütfen önceden tanımlanmış soruları kullanın.

Bir özel Güvenlik sorusu uzunluğu en fazla 200 karakter olabilir.

### <a name="security-question-requirements"></a>Güvenlik sorusu gereksinimleri

* En az yanıt karakter sınırı 3 karakterdir
* En büyük yanıt karakter sınırı 40 karakterdir
* Kullanıcılar, aynı soruyu birden fazla kez yanıt vermeyebilir
* Kullanıcıların birden fazla soru aynı yanıt sağlamayabilir
* Herhangi bir karakter kümesi sorular ve yanıtlar Unicode karakterler içeren tanımlamak için kullanılabilir
* Tanımlanmış soru sayısını kaydetmek için gereken soru sayısına eşit veya daha büyük olmalıdır

## <a name="registration"></a>Kayıt

### <a name="require-users-to-register-when-signing-in"></a>Kullanıcılardan oturum açarken kaydolmalarını iste

Bu seçeneğin etkinleştirilmesi izleyen olanlar gibi oturum açmak için Azure AD kullanan uygulamalar için oturum açma, parola tamamlamak amacıyla parola sıfırlama için etkin bir kullanıcı sıfırlama kaydı gerektirir:

* Office 365
* Azure portalına
* Erişim Paneli
* Federasyon uygulamalarına
* Azure AD kullanarak özel uygulamalar

Bu özellik devre dışı bırakma hala izni verdiği kişi bilgileri ziyaret ederek el ile kaydetmek kullanıcıların [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) veya tıklatarak **parola sıfırlama için kaydetme** altında bağlantı erişim paneli sekmesinde profil.

> [!NOTE]
> Kullanıcıları parola sıfırlama kayıt Portalı'nı İptal'i tıklatarak veya pencereyi sayabilirsiniz ancak kayıt tamamlanana kadar kullanıcılar oturum açma her zaman istenir.
>

### <a name="number-of-days-before-users-are-asked-to-reconfirm-their-authentication-information"></a>Kullanıcıların kimlik doğrulaması bilgilerini yeniden onaylamasını istemeden önce geçen gün sayısı

Bu seçenek ayarlama ve kimlik doğrulama bilgilerini reconfirming arasındaki süreyi belirler ve yalnızca etkinleştirirseniz, kullanılabilir **oturum açarken kullanıcıların** seçeneği.

Geçerli değerler: 0-730 hiçbir zaman kullanıcıların kendi kimlik bilgilerini yeniden onayladıktan ister yani 0 gün

## <a name="notifications"></a>Bildirimler

### <a name="notify-users-on-password-resets"></a>Parola sıfırlamayı kullanıcılara bildir

Bu seçenek Evet olarak ayarlarsanız, parola sıfırlama kullanıcı parolalarını SSPR portal üzerinden birincil ve alternatif e-posta adreslerini dosyada Azure AD içinde değiştirildi olduğunu bildiren bir e-posta alır. Hiç kimse bu sıfırlanmasını bildirilir olay.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Tüm Yöneticiler diğer yöneticilerin kullanıcıların parolalarını sıfırladığınızda bildir

Bu seçenek Evet olarak ayarlarsanız, ardından **tüm yöneticiler** başka bir yönetici SSPR kullanarak parolalarını değiştiğini bildiren Azure AD'de dosya, birincil e-posta adresine bir e-posta alırsınız.

Örnek: Bir ortamda dört Yöneticiler vardır. Yönetici "A" SSPR kullanarak kendi parolasını sıfırlar. Yöneticiler B, C ve D bunları bunun uyarı bir e-posta alır.

## <a name="on-premises-integration"></a>Şirket içi tümleştirme

Yükledikten, yapılandırılmış ve Azure AD Connect etkin değilse, şirket içi tümleştirmeler için ek seçenekler gerekir.

### <a name="write-back-passwords-to-your-on-premises-directory"></a>Şirket içi dizininize parolaları geri Yaz

Parola geri yazma bu dizin için etkin denetler ve geri yazma açıksa, şirket içi geri yazma hizmetinin durumunu gösterir. Bu parola geri yazma'nın Azure AD Connect'i yeniden yapılandırma olmadan geçici olarak devre dışı bırakmak istiyorsanız kullanışlıdır.

* Anahtar Evet olarak ayarlarsanız, daha sonra geri yazma, Federasyon ve etkinleştirilir ve parola karma eşitlenmiş kullanıcıların parolalarını sıfırlayabilmesi mümkün olacaktır.
* Anahtarı ayarlanırsa Hayır'a, ardından geri yazma ve devre dışı, Federasyon ve parola karma eşitlenmiş kullanıcıların parolalarını sıfırlayabilmesi mümkün olmaz.

### <a name="allow-users-to-unlock-accounts-without-resetting-their-password"></a>Kullanıcıların parolalarını sıfırlamadan hesaplarının kilidini izin ver

Parola sıfırlama portalı ziyaret eden kullanıcılar, şirket içi Active Directory hesaplarını, parola sıfırlama olmadan kilidini açmak için seçeneği verilmelidir olup olmadığını belirler. Varsayılan olarak, bir parola sıfırlama gerçekleştirirken Azure AD her zaman hesapları kilitlenmeden, bu ayar, bu iki işlem ayırmanıza olanak sağlar. 

* "Evet" olarak ayarlayın, sonra kullanıcılar seçeneği parolalarını sıfırlama ve hesabın kilidini ya da parola sıfırlama olmadan kilidini açmak için sunulur durumunda.
* Yalnızca kullanıcıların açabilirler sonra "Hayır" olarak ayarlayın birleşik bir parola gerçekleştirmek için sıfırlama ve hesabın kilidini açma işlemi varsa.

## <a name="network-requirements"></a>Ağ gereksinimleri

### <a name="firewall-rules"></a>Güvenlik duvarı kuralları

[Microsoft Office URL'leri ve IP adreslerinin listesi](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Azure AD Connect'i sürüm 1.1.443.0 ve yukarıdaki, giden HTTPS aşağıdaki erişim
* passwordreset.microsoftonline.com
* servicebus.Windows.NET

Daha ayrıntılı erişim için Microsoft Azure veri merkezi IP her Çarşamba güncelleştirilen ve aşağıdaki yürürlüğe koymak aralıkları güncelleştirilmiş listesini bulabilirsiniz Pazartesi [burada](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Boşta kalma zaman aşımları

Azure AD Connect aracını ServiceBus Uç noktalara bağlantıları etkin kalmasını sağlamak için düzenli aralıklarla ping/ayarlandığında Canlı tutmalar gönderir. Aracın çok fazla bağlantının sonlandırıldığını algılaması halinde, uç noktasına ping sıklığını otomatik olarak artırır. En düşük 'aralıklarla ping' düşme 1 ping 60 saniyede, ancak biz kesinlikle proxy/güvenlik duvarları en az 2-3 dakika boyunca kalıcı hale getirmek boşta bağlantılara izin öneriyoruz. * Eski sürümleri için dört dakika veya daha fazla öneririz.

## <a name="active-directory-permissions"></a>Active Directory izinleri

Azure AD Connect yardımcı programında belirtilen hesabın parola sıfırlama, parola değiştirme, yazma izinleri üzerinde lockoutTime olmalıdır ve genişletilmiş pwdLastSet yazma izinlerini hakları üzerinde kök nesne **her etki alanı** , Orman **veya** OU'lar SSPR kapsamında olmasını istediğiniz kullanıcı.

Yukarıdaki başvurduğu hangi hesabın emin değilseniz Azure Active Directory Connect yapılandırma kullanıcı arabirimini açın ve görünüm geçerli yapılandırma seçeneğini tıklatın. Hesap listelenir "Altındaki dizinler eşitlenen" izni eklemeniz gerekir

Bu izinlerin ayarlanması MA hizmet hesabının bu orman içindeki kullanıcı hesapları adına parolaları yönetmek her bir orman için sağlar. **Bu izinleri atamazsanız geri yazma doğru yapılandırılmış gibi görünüyor olsa da sonra kullanıcılar buluttan şirket içi parolalarını yönetme girişiminde bulunduğunda hatalarla.**

> [!NOTE]
> Bu bir saat veya daha fazla bilgi için bu izinlerin dizininizdeki tüm nesnelere çoğaltmak için kadar sürebilir.
>

Parola geri yazmanın gerçekleşmesini sağlamak için gerekli izinleri ayarlamak için

1. Active Directory Kullanıcıları ve bilgisayarları uygun etki alanı yönetim izinleri olan bir hesap ile açma
2. Görünüm menüsünden Gelişmiş Özellikler açık olduğundan emin olun
3. Sol bölmede, etki alanının kökünü temsil eden nesne sağ tıklayın ve Özellikler'i seçin
    * Güvenlik sekmesini tıklatın
    * Ardından Gelişmiş'i tıklatın.
4. İzinleri sekmesinden Ekle
5. İzinler (Azure AD Connect kurulumdan) uygulanmakta olan hesabı seç
6. Açılan kutusu uygulanacağı alt kullanıcı nesneleri seçin.
7. İzinler altında aşağıdaki onay kutularını işaretleyin
    * Süresi dolmasın parola
    * Parola Sıfırlama
    * Parolayı Değiştir
    * LockoutTime yazma
    * PwdLastSet yazma
8. Uygula/Tamam aracılığıyla uygulamak ve açık iletişim kutularını çıkmak için'ı tıklatın.

## <a name="how-does-password-reset-work-for-b2b-users"></a>Parola iş B2B kullanıcıları için nasıl sıfırlama?
Parola sıfırlama ve değişiklik tüm B2B yapılandırmaları ile tam olarak desteklenir.  Aşağıda parola sıfırlama tarafından desteklenen üç açık B2B durumlarda okuyun.

1. **Kullanıcıların mevcut Azure AD kiracısı ile partner org'dan** - mevcut bir Azure AD kiracısı ile ortaklık kuruluş varsa, biz **Kiracı içinde ne olursa olsun parola sıfırlama ilkelerinin etkinleştirildiğinden dikkate**. Parola O365 müşteriler için ek ücret ödemeden olan Azure AD SSPR'yi etkinleştirildiğinden emin olmak için iş ortağı kuruluş yalnızca gereksinimlerini çalışmaya sıfırlamak ve içindeki adımları izleyerek etkinleştirilebilir bizim [parola yönetimiileçalışmayabaşlama](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords)Kılavuzu.
2. **Kaydolan kullanarak kullanıcıların [Self Servis kaydolma](active-directory-self-service-signup.md)**  - kuruluş, kullanılan ile ortaklık [Self Servis kaydolma](active-directory-self-service-signup.md) Kiracı alınacağı özellik, size bildirmek ile Sıfırla Kayıtlı e-posta.
3. **B2B kullanıcılar** -yeni kullanılarak oluşturulan tüm yeni B2B kullanıcılar [Azure AD B2B yetenekleri](active-directory-b2b-what-is-azure-ad-b2b.md) parolalarını davet işlemi sırasında kayıtlı e-posta ile mümkün olacaktır.

Bunu test etmek için bu iş ortağı kullanıcılar biriyle http://passwordreset.microsoftonline.com gidin. Bir alternatif e-posta veya tanımlanan kimlik doğrulama e-posta sahip oldukları sürece, parola beklendiği gibi çalıştığını sıfırlayın.

## <a name="next-steps"></a>Sonraki adımlar

Aşağıdaki bağlantılar, Azure AD kullanarak parola sıfırlama ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri**](active-directory-passwords-data.md) - Gerekli olan verileri ve parola yönetimi için nasıl kullanıldığını anlayın
* [**Kullanıma Sunma** ](active-directory-passwords-best-practices.md) - Buradaki yönergelerle SSPR’ı planlayın ve kullanıcılarınıza dağıtın
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın
* [**Özelleştirme**](active-directory-passwords-customize.md) - SSPR deneyiminin görünümünü şirketiniz için özelleştirin.
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? - Her zaman sormak istediğiniz soruların yanıtları
* [**Sorun giderme**](active-directory-passwords-troubleshoot.md) - SSPR ile yaygın olarak karşılaştığımız sorunların çözümü hakkında bilgi alın

