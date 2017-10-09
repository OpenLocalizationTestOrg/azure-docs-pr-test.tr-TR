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
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Self Servis parola sıfırlama Azure AD derin Dalış

SSPR nasıl çalışır? Bu seçenek hello arabiriminde anlamı nedir? Azure AD Self Servis parola hakkında daha fazla toofind okuma devam sıfırlayın.

## <a name="how-does-hello-password-reset-portal-work"></a>Merhaba parola portalı iş nasıl sıfırlama

Bir kullanıcı toohello parola sıfırlama portalı gittiğinde, bir iş akışı toodetermine başlayacağı zamana:

   * Nasıl hello sayfa yerelleştirilmiş?
   * Merhaba kullanıcı hesabı geçerli mi?
   * Hangi kuruluş hello kullanıcının ait?
   * Merhaba kullanıcının parolasını yönetildiği?
   * Merhaba kullanıcı lisanslı toouse hello özellik mi var?


Merhaba adımlar aşağıda toolearn hello parola sıfırlama sayfasına arkasındaki hello mantığı hakkında okuyun.

1. Merhaba, hesap bağlantısı erişilemiyor veya doğrudan çok girdiği kullanıcı tıklama[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Temel hello tarayıcı yerel hello üzerinde deneyimi hello uygun dilde işlenir. Merhaba parola sıfırlama deneyimi içine yerelleştirilmiş Office 365 desteklediği dillerini hello.
3. Kullanıcı bir kullanıcı kimliği girer ve bir güvenlik kodu geçirir.
4. Azure AD doğrular hello kullanıcı mümkün toouse olup olmadığını hello aşağıdakileri yaparak bu özellik:
   * Bu özellik etkinleştirildiğinde ve bir Azure AD lisansı atanmış hello kullanıcının sahip denetler.
     * Merhaba kullanıcının bu özellik etkinleştirildiğinde veya atanmış bir lisans yok hello kullanıcı varsa, bunların yönetici tooreset toocontact sorulan parolalarını.
   * Merhaba kullanıcı hesaplarında Yönetici İlkesi uygun olarak tanımlanan hello sağ sınama veri sahip olmadığını denetler.
     * Merhaba zorluklar hello Yönetici İlkesi tarafından etkinleştirilmiş en az biri için tanımlanan hello uygun verileri hello kullanıcının sahip sağlamış sonra ilkesi yalnızca bir sınama gerektiriyorsa.
       * Merhaba kullanıcı yapılandırılmamış sonra hello kullanıcı tavsiye edilir toocontact kendi yönetici tooreset ise parolalarını.
     * Hello İlkesi iki zorluk gerektiriyorsa, sonra en az iki hello Yönetici İlkesi tarafından etkinleştirilen hello zorluklar için tanımlanan hello uygun verileri hello kullanıcının sahip güvence altına.
       * Merhaba kullanıcı yapılandırılmamış sonra size kullanıcı hello kendi yönetici tooreset tavsiye edilir toocontact olan parolalarını.
   * Merhaba kullanıcının parolasını (Federe veya parola karması eşitlenen) şirket içinde yönetilen olup olmadığını denetler.
     * Geri yazma dağıtılır ve hello kullanıcının parolasını şirket içinde yönetilir, hello kullanıcı tooproceed tooauthenticate izin verilir ve parolalarını sıfırlayın.
     * Geri yazma dağıtılmadığı ve hello kullanıcının parolasını şirket içinde yönetilir durumunda hello kullanıcı kendi yönetici tooreset toocontact sorulan parolalarını.
5. Bu hello kullanıcının belirlenirse toosuccessfully parolalarını sıfırlama sonra hello kullanıcı hello sıfırlama işlemi yönlendirilir.

## <a name="authentication-methods"></a>Kimlik doğrulama yöntemleri

Self Servis parola sıfırlama (SSPR) etkinleştirilirse, aşağıdaki seçenekleri kimlik doğrulama yöntemleri için şu hello en az birini seçmeniz gerekir. Böylece, kullanıcılarınızın daha fazla esnekliğe sahip en az iki kimlik doğrulama yöntemi seçme öneririz.

* E-posta
* Cep telefonu
* Ofis telefonu
* Güvenlik Soruları

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>Hangi alanların hello dizininde kimlik doğrulama verileri için kullanılır

* Ofis telefonu tooOffice telefon karşılık gelir.
    * Bu alanda kendilerini bir yönetici tarafından tanımlanmalıdır oluşturulamıyor tooset kullanıcılardır
* Cep telefonu tooeither (herkese görünür) kimlik doğrulama telefon veya cep telefonu (herkese görünür) karşılık gelen
    * Hello hizmet için kimlik doğrulama telefon ilk görünür, ardından tooMobile telefon geri döner yoksa
* Alternatif e-posta adresi tooeither kimlik doğrulama e-posta (herkese görünür) veya alternatif e-posta karşılık gelen
    * Merhaba hizmet kimlik doğrulama e-posta için önce arar ve ardından geri tooAlternate e-posta başarısız

Varsayılan olarak, ofis telefonu ve cep telefonu hello bulut öznitelikleri tooyour bulut directory kimlik doğrulama verileri için şirket içi dizininizden eşitlenmiş.

Kullanıcılar parolalarını o hello yönetici hello kimlik doğrulama yöntemlerini mevcut verileri varsa etkinleştirilmiş yalnızca sıfırlama ve gerektirir.

Kullanıcılar, cep telefonu numarası toobe hello dizinde görünür istiyor musunuz ancak toouse gibi parola sıfırlama için hala, yöneticiler değil doldurmak onu hello dizininde ve hello kullanıcı ardından doldurmak kendi **kimlik doğrulama telefon**  özniteliği hello aracılığıyla [parola sıfırlama kayıt portalı](http://aka.ms/ssprsetup). Yöneticiler hello kullanıcının profili için bu bilgiyi görebilir, ancak başka bir yerde yayınlanmadı. Azure yönetici hesabı kimlik doğrulaması telefon numarasını kaydederse, hello cep telefonu alanına doldurulur ve görülebilir.

### <a name="number-of-authentication-methods-required"></a>Gereken kimlik doğrulama yöntemleri sayısı

Bu seçenek hello en az bir kullanıcı tooreset gitmek gerekir hello kullanılabilir kimlik doğrulama yöntemleri sayısını belirler veya kilidini açma parolasını ve tooeither 1 veya 2 ayarlayabilirsiniz.

Hello Yöneticisi tarafından etkinleştirilirse kullanıcılar daha fazla kimlik doğrulama yöntemleri toosupply seçebilirsiniz.

Bir kullanıcıya kayıtlı gerekli en düşük hello yöntemleri yoksa toorequest bir yönetici tooreset yönlendiren bir hata sayfası gördükleri parolalarını.

### <a name="how-secure-are-my-security-questions"></a>My güvenlik soruları ne kadar güvenli mi

Güvenlik soruları kullanırsanız, bazı kişiler hello yanıtlar tooanother kullanıcıların sorularını bildiğiniz beri bunlar diğer yöntemlerinden daha az güvenli olabilir olarak bunları kullanımda başka bir yöntemle öneririz.

> [!NOTE] 
> Güvenlik soruları özel olarak ve güvenli bir şekilde hello dizininde bir kullanıcı nesnesi üzerinde depolanır ve kullanıcılar tarafından kayıt sırasında yalnızca yanıtlanması. Bir yönetici tooread bir yolu yoktur veya kullanıcı değiştirme soru veya yanıt.
>

### <a name="security-question-localization"></a>Güvenlik sorusu yerelleştirme

İzleyen tüm önceden tanımlanmış soruları hello kullanıcının tarayıcı bölgesel ayarına göre Office 365 dilleri hello kümesini içine yerelleştirilmiştir.

* İlk eşiniz/partneriniz ile hangi şehirde tanıştınız?
* Anneniz ile babanız hangi şehirde tanıştı?
* Size en yakın kardeşiniz hangi şehirde yaşıyor?
* Babanız hangi şehirde doğdu?
* İlk işiniz hangi şehirdeydi?
* Anneniz hangi şehirde doğdu?
* 2000 yılına girdiğimiz yılbaşında hangi şehirdeydiniz?
* Merhaba Soyadı yüksek içinde en sevdiğiniz öğretmenin nedir * Okul?
* Merhaba, uyguladığınız üniversitenin adı nedir kaydetmedi toobut katılın?
* İlk düğününüzü gerçekleştirdiğiniz yerin hello hello adı nedir?
* Babanızın ikinci adı nedir?
* En sevdiğiniz yemek nedir?
* Anneannenizin adı ve soyadı nedir?
* Annenizin ikinci adı nedir?
* En büyük kardeşinizin Doğum günü ay ve yıl nedir? (örn. Kasım 1985)
* En büyük kardeşinizin ikinci adı nedir?
* Dedenizin adı ve soyadı nedir?
* En küçük kardeşinizin ikinci adı nedir?
* Altıncı sınıfta hangi okula gidiyordunuz?
* Ne hello ilk oldu ve çocukken en iyi arkadaşınızın adı en son?
* Ne hello ilk oldu ve ilk partnerinizin adı en son?
* Merhaba, ilkokulda en sevdiğiniz öğretmenin Soyadı neydi?
* Merhaba marka ve model ilk arabanızın veya motosikletinizin neydi?
* Merhaba gittiğiniz hello ilk okulun adı neydi?
* Merhaba, Doğduğunuz hello Hastanenin adı neydi?
* Merhaba Sokak, ilk evin, hello adı neydi?
* Merhaba çocukluk kahramanınızın adı neydi?
* Merhaba en sevdiğiniz peluş hayvanın adı neydi?
* Merhaba ilk Evcil hayvanınızın adı neydi?
* Çocukken lakabınız neydi?
* Lisedeyken en sevdiğiniz spor hangisiydi?
* İlk işiniz neydi?
* Ne olan hello çocukken kullandığınız telefon numaranızın son dört rakamı?
* Küçükken olduğunda, Büyüyünce ne toobe istiyordunuz?
* Merhaba tanıştığınız En ünlü kişi kim?

### <a name="custom-security-questions"></a>Özel güvenlik soruları

Özel güvenlik soruları farklı yerel ayarlar için yerelleştirilmiş değil. Tüm özel soruları hello görüntülenen bunlar girilir hello yönetici kullanıcı arabiriminde hello kullanıcının tarayıcı yerel farklı olsa bile aynı dildir. Yerelleştirilmiş soruları gerekiyorsa, lütfen önceden tanımlanmış hello soruları kullanın.

bir özel Güvenlik sorusu Hello en fazla 200 karakter olabilir.

### <a name="security-question-requirements"></a>Güvenlik sorusu gereksinimleri

* En az yanıt karakter sınırı 3 karakterdir
* En büyük yanıt karakter sınırı 40 karakterdir
* Kullanıcılar aynı birden fazla kez soru hello yanıt vermeyebilir
* Kullanıcıların hello değil sağlayabilir aynı yanıt bir soru daha toomore
* Herhangi bir karakter kümesi kullanılan toodefine sorular ve yanıtlar Unicode karakterler dahil olabilir
* tanımlı soruları Hello sayısı büyüktür veya soruları gerekli tooregister toohello sayısı eşit

## <a name="registration"></a>Kayıt

### <a name="require-users-tooregister-when-signing-in"></a>Oturum açarken kullanıcıların tooregister gerektirir

Bu seçeneğin etkinleştirilmesi tooapplications izleyin olanlar gibi Azure AD toosign kullanarak oturum açtıysanız toocomplete hello parola sıfırlama kaydı parolasını etkin bir kullanıcı sıfırlama gerektirir:

* Office 365
* Azure portalına
* Erişim Paneli
* Federasyon uygulamalarına
* Azure AD kullanarak özel uygulamalar

Bu özellik devre dışı bırakma hala izni verdiği kullanıcılar toomanually kayıt kişi bilgileri ziyaret ederek [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) veya hello tıklatarak **parola sıfırlama için kaydetme** hello altındaki bağlantı Merhaba erişim panelinde profili sekmesi.

> [!NOTE]
> Kullanıcılar hello parola sıfırlama kayıt portalı İptal'i tıklatarak veya hello pencereyi sayabilirsiniz ancak kayıt tamamlanana kadar kullanıcılar oturum açma her zaman istenir.
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>Sayısı kullanıcılar önce gün sorulan tooreconfirm kendi kimlik doğrulama bilgileri

Bu seçenek hello ayarlama ve kimlik doğrulama bilgilerini reconfirming arasındaki süreyi belirler ve yalnızca hello etkinleştirirseniz, kullanılabilir **oturum açarken kullanıcıların tooregister gerektiren** seçeneği.

Geçerli değerler: 0-730 kullanıcılar tooreconfirm kendi kimlik doğrulama bilgileri hiçbir zaman isteyin anlamına 0 gün

## <a name="notifications"></a>Bildirimler

### <a name="notify-users-on-password-resets"></a>Parola sıfırlamayı kullanıcılara bildir

Bu seçeneği tooyes ayarlarsanız, parola sıfırlama hello kullanıcı parolalarını hello SSPR portal tootheir birincil değiştirildi ve Azure AD içinde dosyada alternatif e-posta adresleri bildiren bir e-posta alır. Hiç kimse bu sıfırlanmasını bildirilir olay.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Tüm Yöneticiler diğer yöneticilerin kullanıcıların parolalarını sıfırladığınızda bildir

Bu seçenek tooyes, ardından ayarlanırsa **tüm yöneticiler** dosya bir e-posta tootheir birincil e-posta adresi başka bir yönetici SSPR kullanarak parolalarını değiştiğini bildiren Azure AD'de alırsınız.

Örnek: Bir ortamda dört Yöneticiler vardır. Yönetici "A" SSPR kullanarak kendi parolasını sıfırlar. Yöneticiler B, C ve D bunları bunun uyarı bir e-posta alır.

## <a name="on-premises-integration"></a>Şirket içi tümleştirme

Yükledikten, yapılandırılmış ve Azure AD Connect etkin değilse, şirket içi tümleştirmeler için ek seçenekler gerekir.

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>Tooyour şirket içi dizine parolaları geri Yaz

Parola geri yazma bu dizin için etkin denetler ve geri yazma açıksa hello hello şirket içi geri yazma hizmetinin durumunu gösterir. Bu, Azure AD Connect'i yeniden yapılandırma olmadan tootemporarily devre dışı bırak hello parola geri yazma istiyorsanız kullanışlıdır.

* Merhaba anahtar kümesi tooyes geri yazma, Federasyon ve etkinleştirilir ve parola karma eşitlenen kullanıcılar mümkün tooreset olacaktır parolalarını olur.
* Merhaba anahtar kümesi toono geri yazma ve devre dışı, Federasyon ve parola karma eşitlenen kullanıcılar mümkün tooreset olmayacaktır parolalarını olur.

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>Kullanıcıların parolalarını sıfırlamadan toounlock hesaplarına izin ver

Merhaba parola sıfırlama portalı ziyaret eden kullanıcılar kendi şirket içi Active Directory parolalarını sıfırlama olmadan hesapları verilen hello seçeneği toounlock olmalıdır olup olmadığını belirler. Varsayılan olarak, Azure AD her zaman hesapları parola sıfırlama gerçekleştirirken kilidini, bu ayar, tooseparate sağlar bu iki işlem. 

* Varsa çok "Evet", kullanıcıların parolalarını verilen hello seçeneği tooreset olması ve hello parola sıfırlamadan hello hesabı ya da toounlock kilidini ayarlayın.
* Kullanıcılar yalnızca mümkün tooperform sonra çok "Hayır", ayarlamak birleşik parola sıfırlama ve hesap işlemi kilidini durumunda.

## <a name="network-requirements"></a>Ağ gereksinimleri

### <a name="firewall-rules"></a>Güvenlik duvarı kuralları

[Microsoft Office URL'leri ve IP adreslerinin listesi](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Azure AD Connect'i sürüm 1.1.443.0 ve yukarıdaki, giden HTTPS erişim toohello aşağıdakilere sahip olmanız gerekir
* passwordreset.microsoftonline.com
* servicebus.Windows.NET

Daha ayrıntılı erişim için Microsoft Azure veri merkezi IP her Çarşamba güncelleştirilen ve etkili hello aşağıdaki put aralıkları hello güncelleştirilmiş listesini bulabilirsiniz Pazartesi [burada](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Boşta kalma zaman aşımları

Hello Azure AD Connect aracı, düzenli aralıklarla ping/ayarlandığında Canlı tutmalar tooServiceBus uç noktaları tooensure hello bağlantıları canlı kalması gönderir. Merhaba aracı çok fazla bağlantı sonlandırıldı algılaması gerekir, bu otomatik olarak hello ping toohello uç noktasının artacaktır. Hello en düşük 'aralıklarla ping' düşme toois 1 ping 60 saniyede ancak biz kesinlikle proxy/güvenlik duvarları en az 2-3 dakika boyunca boşta bağlantıları toopersist izin öneriyoruz. * Eski sürümleri için dört dakika veya daha fazla öneririz.

## <a name="active-directory-permissions"></a>Active Directory izinleri

Merhaba hello Azure AD Connect yardımcı programı belirtilen hesabın parola sıfırlama, parola değiştirme, lockoutTime yazma izinlerini ve her iki hello kök nesne üzerinde hakları genişletilmiş pwdLastSet yazma izinlerini olmalıdır **her etki alanı** o ormandaki **veya** hello kullanıcı OU'lar SSPR kapsamına toobe istiyor.

Emin değilseniz, yukarıdaki hangi hesabı hello hello Azure Active Directory Connect yapılandırma kullanıcı arabirimini açın ve hello görünümü geçerli yapılandırma seçeneğini ifade eder. Merhaba hesabı "Eşitlenmiş dizinleri" altında listelenen tooadd izin toois gerekir

Bu izinlerin ayarlanması her orman toomanage parolalar için kullanıcı hesapları adına hello MA hizmet hesabının bu orman içindeki sağlar. **Geri yazma doğru yapılandırılmış toobe görünse bile, tooassign bu izinleri daha sonra yayımlarsanız, kullanıcılar toomanage hello buluttan şirket içi parolalarını çalışırken hatalarla.**

> [!NOTE]
> Tooan saat veya daha fazla bilgi için bu izinleri tooreplicate tooall nesneleri dizininizde ele geçirebilir.
>

Parola geri yazma toooccur için uygun izinleri hello tooset

1. Active Directory Kullanıcıları ve bilgisayarları hello uygun etki alanı yönetim izinlerine sahip bir hesap ile açın
2. Merhaba Görünüm menüsünden Gelişmiş Özellikler açık olduğundan emin olun
3. Merhaba sol panelinde hello hello etki alanının kökünü temsil eder hello nesnesine sağ tıklayın ve Özellikler'i seçin
    * Merhaba Güvenlik sekmesini tıklatın
    * Ardından Gelişmiş'i tıklatın.
4. Merhaba izinleri sekmesinden Ekle
5. İzinler (Azure AD Connect Kurulum'u) çok uygulanıyor hello hesabı seç
6. Merhaba uygulanacağı toodrop aşağı kutusu alt kullanıcı nesneleri seçin
7. İzinler altında hello aşağıdaki hello kutularını kontrol edin
    * Süresi dolmasın parola
    * Parola Sıfırlama
    * Parolayı Değiştir
    * LockoutTime yazma
    * PwdLastSet yazma
8. Tooapply Uygula/Tamam'ı tıklatın ve tüm açık iletişim kutularını kapatın.

## <a name="how-does-password-reset-work-for-b2b-users"></a>Parola iş B2B kullanıcıları için nasıl sıfırlama?
Parola sıfırlama ve değişiklik tüm B2B yapılandırmaları ile tam olarak desteklenir.  Aşağıda parola sıfırlama tarafından desteklenen hello üç açık B2B durumlarda okuyun.

1. **Kullanıcıların mevcut Azure AD kiracısı ile partner org'dan** - hello kuruluş ile ortaklık mevcut bir Azure AD kiracısı biz **Kiracı içinde ne olursa olsun parola sıfırlama ilkelerinin etkinleştirildiğinden dikkate**. Parola toowork sıfırlama, O365 müşteriler için ek ücret ödemeden olan iş ortağı kuruluş yalnızca gereksinimlerini toomake Azure AD SSPR'yi etkinleştirildiğinden emin hello ve izleyerek etkinleştirilebilir hello adımları bizim [parola yönetimi ile çalışmaya başlama ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) Kılavuzu.
2. **Kaydolan kullanarak kullanıcıların [Self Servis kaydolma](active-directory-self-service-signup.md)**  - hello kuruluş ile ortaklık hello kullandıysanız [Self Servis kaydolma](active-directory-self-service-signup.md) özelliği tooget Kiracı içine biz izin bunları ile Sıfırla Merhaba eposta kayıtlı.
3. **B2B kullanıcılar** -hello kullanarak yeni oluşturulan tüm yeni B2B kullanıcılar [Azure AD B2B yetenekleri](active-directory-b2b-what-is-azure-ad-b2b.md) mümkün tooreset parolalarını hello davet işlemi sırasında kayıtlı hello e-posta ile de olur.

tootest bu iş ortağı kullanıcılar biriyle gidin, toohttp://passwordreset.microsoftonline.com. Bir alternatif e-posta veya tanımlanan kimlik doğrulama e-posta sahip oldukları sürece, parola beklendiği gibi çalıştığını sıfırlayın.

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin

