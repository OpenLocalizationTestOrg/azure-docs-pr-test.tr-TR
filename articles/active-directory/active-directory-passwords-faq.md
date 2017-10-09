---
title: "Sık sorulan sorular: Azure AD SSPR'yi | Microsoft Docs"
description: "Azure AD Self Servis parola hakkında sık sorulan sorular Sıfırla"
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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>Parola yönetimi sık sorulan sorular

Aşağıdaki hello toopassword sıfırlama her şey ilgili sık sorulan bazı sorular olursunuz.

Azure AD hakkında genel bir sorunuz varsa ve Self Servis parola burada cevaplanıp değil, sıfırlama, istenir hello Topluluk Yardım için hello üzerinde [Azure Ad forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). Merhaba topluluk üyeleri mühendisleri, ürün yöneticileri, MVP ve arkadaşa BT uzmanları içerir.

Bu SSS, aşağıdaki bölümlerde hello ayrılır:

* [**Parola sıfırlama kaydı hakkında sorular**](#password-reset-registration)
* [**Parola sıfırlama hakkında sorular**](#password-reset)
* [**Parola değiştirme hakkında sorular**](#password-change)
* [**Parola yönetimi hakkında sorular raporları**](#password-management-reports)
* [**Parola geri yazma hakkında sorular**](#password-writeback)

## <a name="password-reset-registration"></a>Parola sıfırlama kaydı
* **S: Kullanıcılarım kendi parola sıfırlama verileri kaydedebilirsiniz?**

  > **Y:** Evet, parola sıfırlama etkinleştirilmişse ve lisansına sahip olduğunuz sürece, bunlar toohello parola sıfırlama kayıt portalı http://aka.ms/ssprsetup tooregister ', kimlik doğrulama bilgilerini gidebilirsiniz. Kullanıcılar ayrıca giderek toohello http://myapps.microsoft.com, adresinden erişim Paneli'nde tarafından hello profil sekmesini tıklatıp seçenek parola sıfırlama için kaydetme hello tıklatarak kaydedebilirsiniz.
  >
  >
* **S: parola sıfırlama verileri Kullanıcılarım adına tanımlamak?**

  > **Y:** Evet, Azure AD Connect, PowerShell hello ile yapabilirsiniz [Azure portal](https://portal.azure.com), veya hello Office Yönetim Portalı. Daha fazla bilgi için hello makalesine bakın [Azure AD Self Servis parola sıfırlama tarafından kullanılan verileri](active-directory-passwords-data.md).
  >
  >
* **S: şirket içi güvenlik soruları verileri eşitlemek?**

  > **Y:** bu bugün mümkün değildir.
  >
  >
* **S: Kullanıcılarım veri diğer kullanıcılar bu verileri göremez yolla kaydedebilirsiniz?**

  > **Y:** Evet, kullanıcılar yalnızca genel Yöneticiler ve hello kullanıcı tarafından görülebilir özel kimlik doğrulama alanlara hello kaydedilen parola sıfırlama kayıt portalı kullanarak veri kaydettiğinizde.
    >
    > [!NOTE]
    > Varsa bir **Azure yönetici hesabı** hello cep telefonu alanına da doldurulur ve görünür kendi kimlik doğrulama telefon numaranızı kaydeder.
    >
  >
  >
* **S: Kullanıcılarım parola sıfırlamayı kullanabilmek kayıtlı toobe var mı?**

  > **Y:** onların adına yeterli kimlik doğrulaması bilgilerini tanımlayın, Hayır, kullanıcıların tooregister yoktur. Merhaba uygun hello dizin alanlarında depolanan verilerin düzgün biçimlendirilmiş olduğu sürece works parolasını sıfırlayın.
  >
  >
* **S: eşitlemek veya miyim Kullanıcılarım adına ayarlanmış hello kimlik doğrulama telefon, kimlik doğrulama e-posta veya diğer kimlik doğrulama telefon alanları?**

  > **Y:** bu bugün mümkün değildir.
  >
  >
* **S: nasıl hello kayıt portalı hangi seçenekleri tooshow Kullanıcılarım biliyor?**

  > **Y:** gösterir, kullanıcılarınız için etkinleştirdiğiniz seçenekleri hello yalnızca hello parola sıfırlama kayıt portalı. Bu seçenekler, dizinin Yapılandır sekmesi kullanıcı parolası sıfırlama ilkesini bölümünü hello altında bulunur. Örneğin, bu güvenlik soruları etkinleştirmezseniz, ardından kullanıcıları bu seçenek için mümkün tooregister anlamına gelir.
  >
  >
* **Kullanıcı ne zaman kabul s: kayıtlı?**

  > **Y:** kayıtlı olduğunda SSPR için kayıtlı kullanıcı kabul en az hello **yöntemleri gerekli tooreset sayısı** hello ayarladığınız [Azure portal](https://portal.azure.com).
  >
  >
## <a name="password-reset"></a>Parola sıfırlama
* **S: ne kadar ı tooreceive bir e-posta, SMS ya da parola sıfırlama telefon çağrısında beklemesi gerektiğini?**

  > **Y:** SMS iletileri, e-posta ve telefon aramaları altında bir dakika içinde 5-20 saniye hello normal durumuyla ulaşması.
    >Bu zaman dilimi içinde hello bildirim almazsanız:
        > * Gereksiz klasörünüzü kontrol edin.
        > * Onay hello numarası veya e-posta iletişim kurulan hello bir beklediğiniz değil.
        > * Merhaba dizinindeki Hello kimlik doğrulama verileri doğru biçimlendirilmiş denetleyin.
                >     * Örnek: "+ 1 4255551234" veya "user@contoso.com"
  >
  >
* **S: hangi dilde parola sıfırlama tarafından destekleniyor mu?**

  > **Y:** hello parola sıfırlama kullanıcı Arabirimi, SMS iletileri ve sesli aramalar hello yerelleştirilmiş Office 365'te desteklenen dillerini.
  >
  >
* **S: ı my dizininde markalama kuruluş ayarladığınızda hello parola sıfırlama deneyimi hangi kısımlarının markalı alma kullanıcının yapılandırma sekmesi?**

  > **Y:** hello parola sıfırlama portalı kuruluş logonuzun gösterir ve tooconfigure hello kişi yönetici bağlantı toopoint tooa özel e-posta adresiniz veya URL sağlar. Parola sıfırlama gönderilir e-posta kuruluşunuzun logosu, renkler, adı hello hello e-posta gövdesindeki içerir ve adından özelleştirilebilir.
  >
  >
* **S: nasıl miyim eğitin Kullanıcılarım nerede hakkında toogo tooreset parolalarını?**

  > **Y:** kullanıcılar toohttps://passwordreset.microsoftonline.com doğrudan gönderebilir veya tooclick hello söyleyebilirsiniz **hesap bağlantısı erişemiyor** herhangi bir iş veya Okul oturum açma sayfasında bulunan. Ayrıca, bu bağlantılar bir yerden kolayca erişilebilir tooyour kullanıcılar yayımlayabilirsiniz.
  >
  >
* **S: bir mobil aygıttan bu sayfayı kullanın?**

  > **Y:** Evet, bu sayfayı mobil cihazlarda çalışır.
  >
  >
* **S: kullanıcıların parolalarını sıfırladığınızda kilidini açma yerel active directory hesaplarını destekler mi?**

  > **Y:** parolalarını sıfırladığınızda Evet, bir kullanıcının parolasını sıfırlar ve parola geri yazma dağıtılan Azure AD Connect'i kullanarak, bu kullanıcı hesabının kilidi otomatik olarak kaldırılır.
  >
  >
* **S: parola sıfırlama doğrudan my kullanıcının masaüstü oturum açma deneyimi nasıl tümleştirebilir miyim?**

  > **Y:** bir Azure AD Premium müşterisiyseniz, hiçbir ek ücret Microsoft Identity Manager yükleme ve bu gereksinim hello şirket içi parola sıfırlama çözüm toomeet dağıtma.
  >
  >
* **S: farklı yerel ayarlar için farklı güvenlik soruları ayarlamak?**

  > **Y:** bu bugün mümkün değildir.
  >
  >
* **S: kaç soruları biz hello güvenlik soruları kimlik doğrulaması seçeneği için yapılandırabilir miyim?**

  > **Y:** too20 özel güvenlik soruları hello içinde yukarı yapılandırabilirsiniz [Azure portal](https://portal.azure.com).
  >
  >
* **S: ne kadar süreyle güvenlik soruları olabilir mi?**

  > **Y:** güvenlik soruları 3 ila 200 karakter uzunluğunda olabilir.
  >
  >
* **S: ne kadar süreyle yanıtlar toosecurity soruları olabilir mi?**

  > **Y:** yanıtlar 3 too40 karakter uzunluğunda olabilir.
  >
  >
* **S: Yinelenen yanıtlara toosecurity sorular reddedilir?**

  > **Y:** Evet, biz yinelenen yanıtlara toosecurity sorular reddedin.
  >
  >
* **S: May bir kullanıcı kaydı hello aynı Güvenlik sorusu birden çok kez?**

  > **Y:** bir kullanıcı belirli bir sorunun kaydeder sonra Hayır, bunlar bu soruyu ikinci kez kayıt.
  >
  >
* **S: olası tooset kaydı ve sıfırlama için güvenlik soruları minimum sınırı nedir?**

  > **Y:** kaydı ve sıfırlama için başka bir sınır Evet, ayarlanabilir. 3-5 güvenlik soruları kaydı için gerekli olabilir ve 3-5 sıfırlama için gerekli olabilir.
  >
  >
* **S: nasıl bir kullanıcı birden çok soruları gerekli tooreset hello sayısının kaydedildiyse, güvenlik soruları sıfırlaması sırasında seçilir?**

  > **Y:** N güvenlik soruları seçili rastgele hello toplam soru kullanıcı sayısını dışında kayıtlı, burada N hello **sorular gerekli tooreset sayısı**. Örneğin, bir kullanıcı 5 güvenlik soruları kayıtlı var, ancak yalnızca 3'ü gerekli tooreset, hello 5 3 rastgele seçilir ve sıfırlama sırasında sunulan. Merhaba kullanıcı hello yanıtlar toohello sorular yanlış alırsa, soru tooprevent sözcüğüne hello seçimi işlemi oluşana.
  >
  >
* **S: kullanıcıları parola sıfırlama birçok kez kısa süre içinde denemelerini önlemek?**

  > **Y:** Evet, parola sıfırlama tooprotect kötüye yerleşik güvenlik özellikleri vardır. Kullanıcılar yalnızca 5 parola sıfırlama girişimlerine 24 saat kilitlenmelerini önce bir saat içinde deneyebilirsiniz. Kullanıcılar, 24 saat kilitlenmelerini önce bir saat içinde 5 kez toovalidate bir telefon numarası yalnızca deneyebilirsiniz. Kullanıcılar, 24 saat kilitlenmelerini önce 5 kez bir saat içinde tek kimlik doğrulama yöntemini yalnızca deneyebilirsiniz.
  >
  >
* **S: ne kadar süreyle hello e-posta ve SMS bir kerelik geçiş kodu geçerli misiniz?**

  > **Y:** hello oturum yaşam parola sıfırlama için olan 105 dakika. Merhaba Hello baştan işlemi parola sıfırlama, hello kullanıcı parolalarını 105 dakika tooreset sahiptir. Bu süre dolduktan sonra hello e-posta ve SMS bir kerelik geçiş kodu geçersiz.
  >
  >

## <a name="password-change"></a>Parola değiştirme
* **S: Kullanıcılarım toochange parolalarını nereye?**

  > **Y:** kullanıcıların parolalarını değişebilir gördüğünüz her yerde bunlar kendi profil resmi veya simgesi (Merhaba sağ üst köşedeki ister kendi [Office 365](https://portal.office.com) veya [erişim paneli](https://myapps.microsoft.com) karşılaştığında. Kullanıcıların parolalarını hello değişebilir [erişim paneli profili sayfasını](https://account.activedirectory.windowsazure.com/r#/profile). Kullanıcılar ayrıca olabilir parolalarının süresinin dolduğu varsa toochange parolalarını hello Azure AD oturum açma ekranı otomatik olarak istedi. Son olarak, kullanıcılar toohello gidin [Azure AD parola değişikliği Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) doğrudan toochange parolalarını istediklerinde.
  >
  >
* **S: şirket içi parolalarını sona erdiğinde Kullanıcılarım hello Office portalı bildirilebilir?**

  > **Y:** burada hello yönergeleri izleyerek ADFS kullanıyorsanız, bu bugün mümkündür: [ADFS ile parola ilkesi talep gönderme](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396). Parola karma eşitlemesi kullanıyorsanız, bu bugün mümkün değildir. Biz şirket içi parola ilkeleri eşitleme değil çünkü bu, bize mümkün değildir toopost süre sonu bildirimleri toocloud karşılaştığında. Her iki durumda da çok mümkündür[parolaları hakkında tooexpire PowerShell kullanarak kullanıcıları bildir](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).
  >
  >

## <a name="password-management-reports"></a>Parola yönetimi raporları
* **S: hello parola yönetimi raporlardaki verileri tooshow ne kadar sürer?**

  > **Y:** veri 5-10 dakika içinde hello parola yönetimi raporlarda görünmelidir. Bu tooan saat tooappear sürebilir bazı örnekler.
  >
  >
* **S: Merhaba parola yönetimi raporları filtre nasıl sağlayabilirsiniz?**

  > **Y:** hello raporun hello üstüne yakın hello sütun etiketlerinin hello küçük Büyüteç toohello aşırı sağ tıklayarak hello parola yönetimi raporları filtreleyebilirsiniz. Toodo daha zengin filtreleme istiyorsanız hello rapor tooexcel indirin ve bir PivotTable oluşturun.
  >
  >
* **S: hello sayısı en çok olay nedir depolanır hello parola yönetimi raporlarda?**

  > **Y:** too75 000 parola sıfırlama veya parola sıfırlama kayıt olayları hello parola yönetimi raporları, geri too30 günleri kapsayıcı depolanır.  Tooexpand bu çalışıyoruz tooinclude daha fazla olay numarası.
  >
  >
* **S: hello parola yönetimi raporları ne kadar geri dönün?**

  > **Y:** hello parola yönetimi raporları son 30 gün içinde hello yürütülen Göster işlem. Şu an için bu verileri tooarchive gerekiyorsa, hello raporları düzenli aralıklarla indirin ve bunları ayrı bir konuma kaydedin.
  >
  >
* **S: hello parola yönetimi raporlarda görüntülenen satır sayısının üst sınırını var mı?**

  > **Y:** bunlar gösterilir olup olmadığını Evet, en fazla 75,000 satırları hello parola yönetimi raporları, birini görünebilir UI veya yüklenen hello.
  >
  >
* **S: bir API tooaccess hello parola sıfırlama veya kayıt raporlama verileri var mı?**

  > **Y:** Evet, hello bkz belgeleri toolearn hello parola nasıl erişebileceğinizi raporlama veri akışı sıfırlayın.  [Nasıl tooaccess parola raporlama olayları program aracılığıyla sıfırlama öğrenin](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).
  >
  >

## <a name="password-writeback"></a>Parola geri yazma
* **S: parola geri yazma hello arka planda nasıl çalışır?**

  > **Y:** bkz [parola geri yazma nasıl çalıştığını](active-directory-passwords-writeback.md) , parola geri yazma ve veri hello sistemi üzerinden şirket içi ortamınıza geri akışını sağlayan bir açıklama ne gerçekleşir.
  >
  >
* **S: parola geri yazma toowork ne kadar sürer?  Parola karma eşitlemesi ile gibi bir eşitleme gecikme var mı?**

  > **Y:** parola geri yazma anlık. Parola karma eşitlemesi temelde farklı çalışır zaman uyumlu bir ardışık düzen olur. Parola geri yazma, kullanıcıların parolalarını hello başarısını hakkında gerçek zamanlı geri tooget sıfırlama veya değiştirme işlemi sağlar. başarılı bir parola geri yazma için ortalama süreyi Hello altında 500 ms ' dir.
  >
  >
* **S: şirket içi Hesabımı devre dışıysa, my bulut hesabı/erişimi nasıl etkileniyor mu?**

  > **Y:** şirket içi Kimliğinizi devre dışıysa, kimliği/erişim de devre dışı bırakılacak hello sonraki eşitleme aralıkta AAD Connect byt varsayılan aracılığıyla bulut 30 dakikada budur.
  >
  >
* **S: şirket içi Hesabımı bir şirket içi Active Directory parola ilkesi tarafından kısıtlı, SSPR hello parolayı değiştirdiğinizde, bu ilke uyma mu?**

  > **Y:** Evet, SSPR kullanır ve bağlıdır hello şirket içi tanımlanmış tüm hassas parola ilkeleri yanı sıra AD parola ilkesi tipik AD etki alanı parola ilkesi de dahil olmak üzere, hedeflenen kullanıcı verilen tooa.
  >
  >
* **S: hangi tür hesabı için parola geri yazma çalışıyor mu?**

  > **Y:** parola geri yazma federe ve parola karma eşitlenen kullanıcılar için çalışır.
  >
  >
* **S: parola geri yazma etki alanımın parola ilkelerini zorlamak mu?**

  > **Y:** Evet, parola geri yazma özelliğini parola geçerlilik süresi, geçmiş, karmaşıklık, filtreleri ve yerleştirdiğiniz parolaları bir yerde yerel etki alanınızda kısıtlama zorlar.
  >
  >
* **S: parola geri yazma güvenli mi?  I bilgisayar korsanlarının saldırısına uğrarsa olmaz nasıl mutlaka?**

  > **Y:** Evet, parola geri yazma güvenlidir. Merhaba dört güvenlik katmanları hakkında daha fazla tooread hello parola geri yazma hizmeti tarafından uygulanan, hello denetleyin [parola geri yazma güvenlik modeli](active-directory-passwords-writeback.md#password-writeback-security-model) parola geri yazma nasıl çalıştığını, bölüm.
  >
  >

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**Raporlama**](active-directory-passwords-reporting.md) - Kullanıcılarınızın SSPR işlevine erişip erişmediğini, ne zaman ve nerede eriştiğini öğrenin
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
* [**Parola Geri Yazma**](active-directory-passwords-writeback.md) - Şirket içi dizininizde parola geri yazma özelliğinin nasıl çalıştığını anlayın
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin
