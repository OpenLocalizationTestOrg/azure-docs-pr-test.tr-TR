---
title: Azure AD SSPR'yi parola geri yazma ile | Microsoft Docs
description: "Azure AD ile Azure AD Connect toowriteback parolaları tooon içi dizini"
services: active-directory
keywords: "Active directory parola yönetimi, Azure AD parola yönetimi self servis parola sıfırlama"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>Parola geri yazma genel bakış

Parola geri yazma, Azure AD tooconfigure toowrite parolaları tooyou şirket içi Active Directory yedekleme sağlar. Yukarı hello gerek tooset kaldırır ve karmaşık şirket içi Self Servis parola sıfırlama çözümünü yönetmek ve nerede olurlarsa olsunlar bulut tabanlı kolay bir yol şirket içi parolalarını için kullanıcılar tooreset sağlar.. Parola geri yazma özelliğini bir bileşenidir [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) , etkinleştirilebilir ve Premium geçerli aboneler tarafından kullanılan [Azure Active Directory sürümleri](active-directory-editions.md).

Parola geri yazma özellikleri aşağıdaki hello sağlar

* **Sıfır gecikme geri bildirim** -parola geri yazma eşzamanlı bir işlem değil. Kullanıcılarınızın kendi parola ilkesine uygun değil veya erişilemiyor toobe sıfırlama veya herhangi bir nedenle değişti hemen bildirilir.
* **AD FS veya diğer Federasyon teknolojileri kullanan kullanıcılar parolalarını sıfırlama destekler** -hello birleştirilmiş kullanıcı hesapları Azure AD kiracınıza eşitlenir sürece parola geri yazma ile mümkün toomanage oldukları kendi şirket içi AD Merhaba bulut parolalardan.
* **Kullanarak kullanıcıların parolalarını sıfırlama destekler [parola karması eşitlemesi](./connect/active-directory-aadconnectsync-implement-password-synchronization.md) ** - hello parola sıfırlama hizmeti algıladığında, eşitlenen kullanıcı hesabı için parola karma eşitlemesi etkinleştirildiğinde, biz hem bu hesabın sıfırlama Şirket içi ve parola aynı anda bulut.
* **Hello parolaları değiştirme destekler erişim paneli ve Office 365** - federe olduğunda veya parola süresi dolmuş ya da süresi dolmuş olmayan parolalarını kullanıcıların gelen toochange eşitlenen, biz Bu parolalar geri tooyour yerel AD ortam yazma.
* **Bir yönetici onlardan sıfırladığınızda parola geri yazmayı destekler hello Azure portal** - yönetici hello bir kullanıcının parolasını sıfırlar her [Azure portal](https://portal.azure.com), kullanıcının Federasyon ya da eşitlenmiş bir parola hello ayarlar Parola hello Yöneticisi, yerel AD üzerinde de seçer. Bu hello Office Yönetici portalı şu anda desteklenmiyor.
* **Şirket içi zorlar AD parola ilkeleri** - bir kullanıcı kendi parolasını sıfırlandıktan sonra biz şirket içi karşıladığından emin olun toothat dizin gerçekleştirmeden önce AD ilkesi. Bu geçmiş, karmaşıklık, yaş, parola filtreleri ve yerel AD içinde tanımlanan diğer parola kısıtlamaları içerir.
* **Tüm gelen güvenlik duvarı kurallarını gerektirmeyen** -parola geri yazma, tooopen gelen bağlantı noktalarının duvarınızda bu özellik toowork sahip olmadığını anlamı temel alınan bir iletişim kanalı olarak Azure Service Bus geçişini kullanır.
* **Şirket içi Active Directory'de korunan grupları içinde mevcut kullanıcı hesapları için desteklenmiyor** - korumalı grupları hakkında daha fazla bilgi için bkz: [korumalı hesapları ve grupları Active Directory'de](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>Parola geri yazma nasıl çalışır?

Federe veya parola karma eşitlendiğinde kullanıcı tooreset gelir veya hello aşağıdakiler gerçekleşir parolalarını hello bulutta değiştirin:

1. Biz, toosee parola hello kullanıcı türüne sahip kontrol edin.
    * Biz görürseniz hello parola şirket içinde yönetilir
        * Biz hello geri yazma hizmetin çalışır durumda, çalışan, biz devam hello kullanıcı izin kontrol edin ve
        * Merhaba geri yazma hizmet yukarı değilse, biz hello kullanıcı parolalarını şimdi sıfırlanamaz bildirin
2. Ardından, hello kullanıcı hello uygun kimlik doğrulama geçitleri geçirir ve hello sıfırlama parola ekran ulaştığında.
3. Merhaba kullanıcı yeni bir parola seçer ve bunu doğrular.
4. Gönderme tıklatıldığında, biz hello düz metin parolası hello geri yazma Kurulum işlemi sırasında oluşturulmuş simetrik anahtarla şifreler.
5. Merhaba parola şifreleme sonrasında biz (biz de için hello geri yazma Kurulum işlemi sırasında ayarladığınız) bir HTTPS kanal tooyour Kiracı özgü service bus geçişi üzerinden gönderilen bir yükü dahil edin. Bu geçiş, yalnızca şirket içi yüklemenizi bilir rastgele oluşturulmuş bir parola tarafından korunuyor.
6. Selamlama iletisine hizmet veri yolu ulaştığında, hello parola sıfırlama endpoint otomatik olarak uyanır ve bekleyen sıfırlama isteği olduğunu görür.
7. Merhaba hizmeti ardından hello kullanıcıdan hello bulut bağlayıcı özniteliğini kullanarak söz konusu arar. Bu arama toosucceed için:

    * Merhaba AD bağlayıcı alanı Hello kullanıcı nesnesi mevcut olmalıdır
    * Merhaba kullanıcı nesnesi bağlı toohello karşılık gelen MV nesnesi olmalıdır
    * Merhaba kullanıcı nesnesi bağlı toohello karşılık gelen AAD bağlayıcı nesnesi olmalıdır.
    * Merhaba AD Bağlayıcısı nesne tooMV bağlantısından hello eşitleme kuralına sahip olmalıdır `Microsoft.InfromADUserAccountEnabled.xxx` hello bağlantıyı. <br> <br>
    Hello çağrısı hello buluttan geldiğinde, hello eşitleme altyapısı kullanır cloudAnchor özniteliği toolook hello AAD bağlayıcı alanı nesne yukarı Merhaba, hello bağlantı geri toohello MV nesnesi izler ve hello bağlantı geri toohello AD nesne izler. Aynı kullanıcı, hello eşitleme altyapısı kullanır üzerinde hello hello için birden çok AD nesnelerini (Çoklu orman) olabilir çünkü `Microsoft.InfromADUserAccountEnabled.xxx` bağlantı toopick hello bir düzeltin.

    > [!Note]
    > Bu mantığı sonucu olarak Azure AD Connect mümkün toocommunicate hello PDC öykünücüsü parola geri yazma toowork için sahip olması gerekir. Tooenable bu işlemi el ile gerekiyorsa, Azure AD Connect toohello PDC öykünücüsü hello üzerinde sağ tıklayarak bağlanabileceğiniz **özellikleri** hello Active Directory eşitleme bağlayıcısının, ardından seçerek **yapılandırın dizin bölümlerini**. Merhaba, buradan Ara **etki alanı denetleyicisi bağlantı ayarları** bölümünde ve başlıklı hello kutuyu **yalnızca tercih edilen etki alanı denetleyicilerinin kullandığı**. DC, PDC öykünücüsü değil Hello tercih edilen olsa bile, Azure AD Connect parola geri yazma için tooconnect toohello PDC deneyecek.

8. Merhaba kullanıcı hesabı bulunduktan sonra biz tooreset hello parola doğrudan hello uygun AD ormanında deneyin.
9. Merhaba parola ayarlama işlemi başarılı olursa, biz hello kullanıcı parolalarını değiştirildi söyleyin.
    > [!NOTE]
    > Merhaba kullanıcının parolasını eşitlenmiş tooAzure AD olduğunda hello durumda Parola Eşitleme'yi kullanılarak hello şirket içi parola ilkesi hello bulut parola ilkesi zayıf bir fırsat yok. Bu durumda, biz yine ne olursa olsun hello şirket içi İlkesi olduğu ve bunun yerine parola karma eşitlemesi toosynchronize hello parola karmasını izin uygulayın. Bu parola eşitleme ya da Federasyon tooprovide kullanıyorsanız, şirket içi İlkesi hello bulutta bağımsız uygulandığını sağlar çoklu oturum açma.

10. Hello parola işlemi başarısız ayarlarsanız, biz hello hata toohello kullanıcı dönün ve yeniden deneyin olanak sağlayacak.
    * Merhaba işlemi hello aşağıdaki nedeniyle başarısız olabilir
        * Aşağı Hello hizmeti
        * Bunlar Seçili hello parola kuruluş ilkeleri karşılamayan
        * Merhaba kullanıcı hello yerel AD bulamadık

    İleti pek çok durumda ve yapabileceklerini hello kullanıcıya bildir belirli bir sahip olduğumuz tooresolve hello sorun.

## <a name="configuring-password-writeback"></a>Parola geri yazma özelliğini yapılandırma

Merhaba otomatik güncelleştirme özelliğini kullanmanızı öneririz [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) toouse parola geri yazma istiyorsanız.

DirSync ve Azure AD eşitleme olan artık parola geri yazma hello makale etkinleştirme desteklenen anlamına gelir [yükseltme DirSync ve Azure AD eşitleme](connect/active-directory-aadconnect-dirsync-deprecated.md) geçişinizin ile daha fazla bilgi toohelp sahiptir.

Merhaba adımları zaten yapılandırdığınız Azure AD Connect hello kullanarak, ortamınızda varsayın [Express](./connect/active-directory-aadconnect-get-started-express.md) veya [özel](./connect/active-directory-aadconnect-get-started-custom.md) ayarlar.

1. tooconfigure ve etkinleştir parola geri yazma tooyour Azure AD Connect sunucusunun oturum ve hello başlatın **Azure AD Connect** Yapılandırma Sihirbazı.
2. Merhaba Hoş Geldiniz ekranında tıklatın **yapılandırma**.
3. Merhaba üzerinde ek görevleri tıklatın ekran **eşitleme seçeneklerini özelleştirme** ve ardından **sonraki**.
4. Merhaba Bağlan tooAzure AD ekranında bir genel yönetici kimlik bilgileri girin ve seçin **sonraki**.
5. Merhaba dizinler ve etki alanı bağlanmak ve OU filtreleme seçtiğiniz **sonraki**.
6. Merhaba isteğe bağlı özellikler ekranında hello sonraki çok onay kutusunu**parola geri yazma** tıklatıp **sonraki**.
   ![Azure AD CONNECT'te parola geri yazma etkinleştir][Writeback]
7. Merhaba hazır tooconfigure ekranında tıklatın **yapılandırma** ve hello işlem toocomplete için bekleyin.
8. Yapılandırma gördüğünüzde tam tıklayabilirsiniz **çıkış**

## <a name="licensing-requirements-for-password-writeback"></a>Parola geri yazma için lisans gereksinimleri

Lisans, bkz: ilgili bilgi hello konu [lisansları parola geri yazma için gereken](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) veya hello aşağıdaki siteleri

* [Azure Active Directory fiyatlandırma site](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Güvenli üretken Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Şirket içi parola geri yazma için desteklenen kimlik doğrulama modu

Parola geri yazma için şu kullanıcı parolası türlerini hello çalışır:

* **Yalnızca bulut kullanıcıları**: parola geri yazma şirket içi parola olduğundan bu durumda, uygulanmaz
* **Kullanıcıları parola eşitlenmiş**: desteklenen parola geri yazma
* **Federe kullanıcılar**: desteklenen parola geri yazma
* **Doğrudan kimlik doğrulama kullanıcıların**: desteklenen parola geri yazma

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Parola geri yazma için desteklenen kullanıcı ve yönetim işlemleri

Parolalar, tüm hello durumlarda aşağıdaki geri yazılır:

* **Desteklenen son kullanıcı işlemleri**
  * Tüm son kullanıcı Self Servis gönüllü değiştirme parola işlemi
  * Tüm son kullanıcı Self Servis zorla parola değiştirme işlemi (örneğin, parola sona erme)
  * Tüm son kullanıcı Self Servis parola sıfırlama hello kaynaklanan [parola sıfırlama portalı](https://passwordreset.microsoftonline.com)
* **Desteklenen yöneticisi işlemleri**
  * Tüm yönetici Self Servis gönüllü değiştirme parola işlemi
  * Tüm yönetici Self Servis zorla parola değiştirme işlemi (örneğin, parola sona erme)
  * Tüm yönetici Self Servis parola sıfırlama hello kaynaklanan [parola sıfırlama portalı](https://passwordreset.microsoftonline.com)
  * Hello sıfırlama herhangi bir yönetici tarafından başlatılan son kullanıcı parola [Klasik Azure portalı](https://manage.windowsazure.com)
  * Hello sıfırlama herhangi bir yönetici tarafından başlatılan son kullanıcı parola [Azure portalı](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Parola geri yazma için desteklenmeyen kullanıcı ve yönetim işlemleri

Parolalar **değil** durumlarda aşağıdaki hello hiçbirinde başa yazılı:

* **Desteklenmeyen son kullanıcı işlemleri**
  * PowerShell v1, v2 veya hello Azure AD Graph API kullanarak kendi parolasını sıfırlama herhangi bir son kullanıcı
* **Desteklenmeyen yöneticisi işlemleri**
  * Hello sıfırlama herhangi bir yönetici tarafından başlatılan son kullanıcı parola [Office Yönetim Portalı](https://portal.office.com)
  * Tüm son kullanıcı yönetici tarafından başlatılan parola PowerShell v1, v2 veya hello Azure AD grafik API'si aracılığıyla sıfırlama

Bu sınırlamalara tooremove çalışıyoruz, ancak biz biz henüz paylaşabilirsiniz belirli bir zaman çizelgesi yok.

## <a name="password-writeback-security-model"></a>Parola geri yazma güvenlik modeli

Parola geri yazma yüksek güvenlikli bir hizmettir.  bilgilerinizi korumalı tooensure, aşağıda açıklanan 4 katmanlı güvenlik modeli sağlar.

* **Kiracı özgü service bus geçişi**
  * Merhaba hizmetini kurma ayarladığınızda, biz Microsoft hiçbir zaman erişimi rastgele oluşturulmuş güçlü bir parola tarafından korunan bir kiracıya özgü hizmet veri yolu geçişi ayarlayın.
* **Kilitli ve şifreleme açısından güçlü bir parola şifreleme anahtarı**
  * Merhaba service bus geçişi oluşturulduktan sonra hello kablo üzerinden geldiğinde tooencrypt hello parola kullanırız güçlü bir simetrik anahtar oluşturuyoruz. Bu anahtar yalnızca deposundaki şirketinizin gizli yoğun kilitlenir ve denetlenen hello dizinde herhangi bir parola gibi hello bulutta yaşar.
* **Endüstri Standart TLS**
  1. Bir parola sıfırlama veya değiştirme işlemi hello bulutta oluşur, hello düz metin parola alın ve, ortak anahtarla şifreleyebilirsiniz.
  2. Biz sonra Microsoft'un SSL sertifikaları tooyour service bus geçişini kullanarak şifrelenmiş bir kanal üzerinden gönderilen bir HTTPS iletisi yerleştirin.
  3. Selamlama iletisine Service Bus, şirket içi aracınızı ayarlama uyku modundan çıkar ulaşan ve kimlik doğrulaması sonra önceden oluşturulan güçlü bir parola hello tooService veri yolu kullanarak.
  4. Şirket içi aracı hello şifreli ileti seçer, biz üretilen hello özel anahtarı kullanarak şifresini çözer.
  5. Şirket içi Aracısı tooset hello parola hello AD DS SetPassword API'si aracılığıyla daha sonra çalışır.
     * Bize tooenforce sağlayan bu adımdır AD şirket içi parola ilkesi (karmaşıklık, yaş, geçmiş, filtreleri, vb.) hello bulutta.
* **İleti sona erme** 
  * Şirket içi hizmetiniz çalışmadığı için hizmet veri yolundaki selamlama iletisine bulunur, zaman aşımına uğrayacaktır ve birkaç dakika tooincrease güvenlik sonra daha kaldırılması.

### <a name="password-writeback-encryption-details"></a>Parola geri yazma şifreleme ayrıntıları

parola sıfırlama isteği, şirket içi ortamına, tooensure maksimum hizmet güvenilirlik ve güvenlik gelmeden önce kullanıcı onu gönderdikten sonra geçtiği hello şifreleme adımları aşağıda açıklanmıştır.

* **1. adım - parola şifreleme 2048 bit RSA anahtarı ile** - kullanıcı geri tooon içi ilk hello gönderilen parola kendisini yazılan parola toobe 2048 bit RSA anahtarıyla şifrelenir gönderdikten sonra.
* **2. adım - paket düzeyi şifreleme AES-GCM ile** - sonra hello tüm paket (parola + gerekli meta veriler), AES-GCM kullanılarak şifrelenir. Bu doğrudan erişim toohello temel ServiceBus kanalı kimseyle görüntüleme/oynama hello içeriğiyle engeller.
* **Adım 3 - tüm iletişimin TLS / SSL** -ServiceBus ile tüm hello iletişim SSL/TLS kanalda olur. Bu, yetkisiz 3 taraflardan hello içeriği güvenliğini sağlar.
* **Otomatik anahtar geçişi altı ayda** - otomatik olarak her 6 ayda veya parola geri yazma özelliğini devre dışı / Azure AD Connect üzerinde yeniden etkinleştirilmiş her zaman biz geçişi Bu anahtarları tooensure maksimum hizmeti güvenlik ve güvenilirlik.

### <a name="password-writeback-bandwidth-usage"></a>Parola geri yazma bant genişliği kullanımı

Parola geri yazma isteklerini toohello şirket içi aracı yalnızca aşağıdaki durumlarda hello altında geri gönderdiği düşük bant genişlikli bir hizmettir:

1. Etkinleştirme veya Azure AD Connect aracılığı hello özelliği devre dışı bırakırken gönderilen iki iletileri.
2. Merhaba çalıştığı sürece her beş dakikada bir hizmet sinyalinin olarak tek bir ileti gönderilir.
3. İki ileti gönderilen her zaman yeni bir parola gönderildi
    * Bir istek tooperform hello işlemi olarak ilk ileti
    * Hello hello işleminin sonucunu içerir ve aşağıdaki koşullar hello gönderilen ikinci ileti:
        * Her bir kullanıcı Self Servis parola sıfırlama sırasında yeni bir parola gönderilir.
        * Her bir kullanıcı parolasını değiştirme işlemi sırasında yeni bir parola gönderilir.
        * Her bir kullanıcı yönetici tarafından başlatılan parola (yalnızca hello Azure Yönetim Portalı) sıfırlama sırasında yeni bir parola gönderilir.

#### <a name="message-size-and-bandwidth-considerations"></a>İleti boyutu ve bant genişliği konuları

Hello boyutu her yukarıda açıklanan selamlama iletisine genellikle aşırı yükü altında bile altında 1 kb, birkaç saniye başına kilobittir bant genişliğinin hello parola geri yazma hizmetin kendisini kullanma. Her ileti yalnızca bir parola güncelleştirme işlemi tarafından gerekli olduğunda gerçek zamanlı olarak gönderilir, ve hello ileti boyutu kadar küçük olmadığından, hello bant genişliği kullanımını hello geri yazma özelliği etkin çok küçük toohave olduğundan gerçek ölçülebilir bir etkisi.

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Azure AD CONNECT'te parola geri yazma etkinleştir"
