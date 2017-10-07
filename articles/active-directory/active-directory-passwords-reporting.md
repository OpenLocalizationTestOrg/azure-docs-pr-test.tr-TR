---
title: 'Raporlama: Azure AD SSPR''yi | Microsoft Docs'
description: "Azure AD Self Servis parola üzerinde raporlama olayları Sıfırla"
services: active-directory
keywords: 
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
ms.openlocfilehash: af65b9be1e00c2819431694a5b0064b97b9e1867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Azure AD parola yönetimi için raporlama seçenekleri

Birçok kuruluş tooknow nasıl istediğinizi veya SSPR gerçekten kullanılıp kullanılmadığını dağıtım sonrasında. Azure AD ve uygun şekilde lisanslanır ise toocreate özel sorgular izin raporları kullanarak tooanswer sorular Yardım raporlama özellikleri canned sağlar.

Merhaba aşağıdaki soruları hello [Azure portalı] mevcut raporlar yanıtlanabilir (https://portal.azure.com/).

> [!NOTE]
> Olmalıdır [genel yönetici](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) ve bu verileri toobe kuruluşunuz adına toplanan raporlama sekmesini veya denetim ziyaret hello tarafından en az bir kez oturum için katılımı gerekir. Bunun yapılması kadar veri kuruluşunuz için toplanmaz

* Kaç kişinin parola sıfırlama için kayıtlı?
* Parola sıfırlama için kayıtlı olan kim?
* Verileri kaydetme kişiler nelerdir?
* Kaç kişinin son yedi gün hello parolalarını sıfırlama?
* Hello en yaygın yöntemleri kullanıcıları veya yöneticileri tooreset parolalarını kullanmak ne var mı?
* Ne ortak olan kullanıcıları veya yöneticileri yüz toouse parola sıfırlama çalışırken verir?
* Hangi yöneticileri kendi parolalarını sık sıfırlama?
* Parola sıfırlama ile geçmeden tüm şüpheli etkinlik mi?

## <a name="how-tooview-password-management-reports-in-hello-azure-portal"></a>Hello Azure portalına nasıl tooview parola yönetimi raporları

Hello Azure portal deneyimi, bir geliştirilmiş yolu tooview parola sıfırlama ve parola sıfırlama kayıt etkinlik vardır.  Toofind hello parola sıfırlama ve parola sıfırlama kayıt olayları Hello adımları izleyin:

1. Çok gidin[**portal.azure.com**](https://portal.azure.com)
2. Merhaba tıklatın **daha fazla hizmet** hello ana Azure portal sol taraftaki gezinti menüsünde
3. Arama **Azure Active Directory** hello hizmetlerin listesi ve seçin
4. Tıklatın **kullanıcıları ve grupları** hello Azure Active Directory Gezinti menüsünde
5. Merhaba tıklatın **denetim günlüklerini** hello kullanıcıları ve grupları Gezinti menüsünde Gezinti öğesi. Bu, tüm hello denetim olaylarının dizininizdeki tüm hello kullanıcılara karşı gerçekleştiğini gösterir. Bu görünüm toosee tüm hello parola ilgili olayların de filtre uygulayabilirsiniz.
6. toofilter ilgili olaylar bu görünüm tooonly hello parola sıfırlama, hello tıklatın **filtre** hello dikey penceresinde hello üstündeki düğmesi.
7. Merhaba gelen **filtre** menüsü, select hello **kategori** açılan listesinde ve toohello değiştirmek **Self Servis parola yönetimi** kategori türü.
8. İsteğe bağlı olarak daha fazla filtre hello listesi hello özel seçerek **etkinlik** ilgilendiğiniz

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Azure AD raporları ve olayları API tooretrieve parola yönetimi olayları nasıl hello

Hello Azure AD raporları ve olayları API destekleyen tüm hello bilgileri parola sıfırlama ve parola sıfırlama kayıt raporlara dahil alınıyor. Bu API'yi kullanarak tek tek parola sıfırlama indirebilirsiniz ve tercih ettiğiniz teknolojisi raporlama hello ile tümleştirme için kayıt olayları parola sıfırlama.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Tooget hello raporlama API'si ile çalışmaya nasıl

tooaccess bu verileri toowrite küçük bir uygulama gerekiyor veya tooretrieve komut dosyası, sunucularımızda. [Tooget Azure AD raporlama API'si ile Merhaba çalışmaya nasıl bilgi](active-directory-reporting-api-getting-started.md).

Bir çalışan betik olduktan sonra sonraki senaryolarınızı toomeet alabilirsiniz tooexamine hello parola sıfırlama ve kayıt olayları isteyeceksiniz.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): olayları parola sıfırlama için kullanılabilen hello sütunları listeler
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): kayıt olayları parola sıfırlama için kullanılabilen hello sütunları listeler

### <a name="reporting-api-data-retrieval-limitations"></a>Raporlama API veri alma sınırlamaları

Şu anda Azure AD raporları hello ve çok alır yukarı olayları API**75,000 olayları tek tek** Merhaba, [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) ve [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) türleri , hello kapsayıcı **son 30 gün**.

Tooretrieve gerekir veya bu pencereyi aşan veri depolamak, dış bir veritabanında kalıcı yapma ve neden hello API tooquery hello farkları kullanarak öneririz. Bizim önerimiz, kuruluşunuzda SSPR kullanarak başlattığınızda, harici olarak kalır ve tootrack hello farkları bu noktadan İleri devam bu veri alma toobegin ' dir.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>PowerShell ile hızlı bir şekilde kayıt olayları nasıl toodownload parola sıfırlama

Ayrıca toousing Merhaba Azure AD raporları ve olayları API doğrudan, dizininizde PowerShell komut dosyası toorecent kayıt olayları aşağıda hello de kullanabilirsiniz. Bu son kaydettirildi toosee istemeniz durumunda faydalı olur veya beklediğiniz gibi parolanızı sunum sıfırlama tooensure oluştuğunu gibi gerekir.

* [Azure AD SSPR'yi kayıt etkinlik PowerShell Betiği](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Azure Portalı'nda rapor sütunlarını açıklaması

Merhaba aşağıdaki listede ayrıntılı hello rapor sütunların her biri açıklanmaktadır:

* **Kullanıcı** – bir parola deneyen hello kullanıcı sıfırlama kayıt işlemi.
* **Rol** – hello dizininde hello kullanıcı hello rolü.
* **Tarih ve saat** – hello tarih ve saat hello denemesinin.
* **Veri kayıtlı** – kayıt sırasında parola hangi kimlik doğrulama verileri hello kullanıcı tarafından sağlanan sıfırlayın.

### <a name="description-of-report-values-in-azure-portal"></a>Azure Portalı'nda rapor değerlerinin açıklaması

Merhaba aşağıdaki tabloda her sütun için izin verilen hello farklı değerler açıklanmaktadır:

| Sütun | İzin verilen değerler ve anlamları |
| --- | --- |
| Kayıtlı veri |**Alternatif e-posta** – kullanıcı kullanılan alternatif e-posta veya kimlik doğrulama e-posta tooauthenticate<p><p>**Ofis telefonu**– kullanıcı kullanılan office telefon tooauthenticate<p>**Cep telefonu** -kullanıcı kullanılan cep telefonu veya kimlik doğrulama telefon tooauthenticate<p>**Güvenlik soruları** – kullanılan kullanıcı güvenlik sorularını tooauthenticate<p>**Herhangi bir bileşimini hello (örneğin, alternatif e-posta + cep telefonu) yukarıdaki** – 2 kapısı İlkesi belirtilir ve hangi iki yöntem kullanılan kullanıcı tooauthentication hello gösterir oluşur parolasını sıfırlama isteği. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Görünüm parola sıfırlama etkinliği hello Klasik portalında

Bu rapor, tüm parola sıfırlama, kuruluşunuzda oluşmuş denemeleri gösterir.

* **En büyük zaman aralığı**: 30 gün
* **En fazla sayıda satırı**: 75.000
* **İndirilebilir**: Evet, CSV dosyası aracılığıyla

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Azure Klasik Portalı'nda rapor sütunlarını açıklaması

Merhaba aşağıdaki listede ayrıntılı hello rapor sütunların her biri açıklanmaktadır:

1. **Kullanıcı** – bir parola deneyen hello kullanıcı sıfırlama işlemi (Merhaba kullanıcı tooreset parola geldiğinde sağlanan hello kullanıcı kimliği temel alan).
2. **Rol** – hello dizininde hello kullanıcı hello rolü.
3. **Tarih ve saat** – hello tarih ve saat hello denemesinin.
4. **Yöntemleri kullanılan** – kullanılan kullanıcı kimlik doğrulama yöntemleri hello bu sıfırlama işlemi için.
5. **Sonuç** – hello sonucu hello parola sıfırlama işlemi.
6. **Ayrıntılar** – neden hello parola sıfırlama ayrıntılarını hello olduğu hello değerinde sonuçlandı.  Ayrıca tooresolve beklenmeyen bir hata alabilir herhangi azaltma adımlarını içerir.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Azure Klasik Portalı'nda rapor değerlerinin açıklaması

Merhaba aşağıdaki tabloda her sütun için izin verilen hello farklı değerler açıklanmaktadır:

| Sütun | İzin verilen değerler ve anlamları |
| --- | --- |
| Kullanılan yöntemler |**Alternatif e-posta** – kullanıcı kullanılan alternatif e-posta veya kimlik doğrulama e-posta tooauthenticate<p>**Ofis telefonu** – kullanıcı kullanılan office telefon tooauthenticate<p>**Cep telefonu** – kullanıcı kullanılan cep telefonu veya kimlik doğrulama telefon tooauthenticate<p>**Güvenlik soruları** – kullanılan kullanıcı güvenlik sorularını tooauthenticate<p>**Herhangi bir bileşimini hello (örneğin, alternatif e-posta + cep telefonu) yukarıdaki** – 2 kapısı İlkesi belirtilir ve hangi iki yöntem kullanılan kullanıcı tooauthentication hello gösterir oluşur parolasını sıfırlama isteği. |
| Sonuç |**Terk** – kullanıcı parola sıfırlama başladı, ancak yarı yarıya aracılığıyla tamamlamadan durdu<p>**Engellenen** – kullanıcının hesap idi önlenmiş toouse parola sıfırlama tooattempting toouse hello parola sıfırlama sayfasına veya bir 24 saatlik sürede çok sayıda ağ geçidi tek bir parola sıfırlama<p>**İptal** – kullanıcı parola sıfırlama başladı, ancak hello iptal düğmesi toocancel hello oturum parçası şekilde ile tıklattınız <p>**Yönetici ile bağlantı kurulamadı** – kullanıcı kendisinin çözümlenemedi kendi oturumu sırasında bir sorun var, hello kullanıcı sonlandırma yerine hello "yöneticinize başvurun" bağlantıyı tıklattığında şekilde akış hello parola sıfırlama<p>**Başarısız** – kullanıcı değildi mümkün tooreset büyük olasılıkla bir parola olduğundan hello kullanıcı olmayan yapılandırılmış toouse hello özelliği (örneğin, hiçbir lisans, eksik kimlik bilgileri, parola yönetilen şirket içi ancak geri yazma kapalıdır).<p>**Başarılı** – parola sıfırlama başarılı oldu. |
| Ayrıntılar |Aşağıdaki tabloya bakın |

### <a name="allowed-values-for-details-column"></a>İzin verilen değerler Ayrıntılar sütunu için

Sonuç türleri hello parola kullanarak Etkinlik Raporu sıfırladığınızda bekleyebilir hello listesi aşağıdadır:

| Ayrıntılar | Sonuç türü |
| --- | --- |
| Merhaba e-posta doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Merhaba mobil SMS doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Merhaba mobil sesli arama doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Merhaba office sesli arama doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Merhaba güvenlik soruları seçeneği tamamladıktan sonra terk kullanıcı |terk |
| Kullanıcı Kimliğini girdikten sonra terk kullanıcı |terk |
| Merhaba e-posta doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Merhaba mobil SMS doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Merhaba mobil sesli arama doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Merhaba office sesli arama doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Merhaba güvenlik soruları seçeneği başlattıktan sonra terk kullanıcı |terk |
| Yeni bir parola seçmeden önce terk kullanıcı |terk |
| Yeni bir parola seçerken terk kullanıcı |terk |
| Kullanıcı çok fazla geçersiz SMS doğrulama kodları girilen ve 24 saat engellendi |Engellendi |
| Kullanıcı, cep telefonu sesli doğrulama birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı office telefon sesli doğrulama birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı çok fazla kez tooanswer güvenlik soruları denedi ve 24 saat engellendi |Engellendi |
| Kullanıcı tooverify bir telefon numarası birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı gerekli hello kimlik doğrulama yöntemleri gönderilmeden önce iptal etti |İptal edildi |
| Yeni bir parola göndermeden önce kullanıcı iptal etti |İptal edildi |
| Kullanıcı bir yönetici hello e-posta doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici hello mobil SMS doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici hello mobil sesli arama doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici hello office sesli arama doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici hello Güvenlik sorusu doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Parola sıfırlama bu kullanıcı için etkin değil. Etkinleştir parola sıfırlama altında Merhaba yapılandırma sekmesi tooresolve bu |Başarısız oldu |
| Kullanıcı bir lisans yok. Bu lisans toohello kullanıcı tooresolve ekleyebilirsiniz. |Başarısız oldu |
| Kullanıcı bir aygıttan tooreset etkin tanımlama bilgileri çalıştı. |Başarısız oldu |
| Kullanıcı hesabı tanımlanan yetersiz kimlik doğrulama yöntemlerine sahiptir. Bu kimlik doğrulama bilgileri tooresolve Ekle |Başarısız oldu |
| Kullanıcının, yönetilen şirket içi paroladır. Bu parola geri yazma tooresolve etkinleştirebilirsiniz |Başarısız oldu |
| Şirket içi parola sıfırlama hizmetinizi erişemedi. Eşitleme makinenizin olay günlüğünü denetleyin |Başarısız oldu |
| Merhaba kullanıcının şirket içi parolanızı sıfırlarken bir sorun oluştu. Eşitleme makinenizin olay günlüğünü denetleyin |Başarısız oldu |
| Bu kullanıcı hello parola sıfırlama kullanıcılar grubunun bir üyesi değil. Bu kullanıcı toothat Grup tooresolve bu ekleyin. |Başarısız oldu |
| Parola sıfırlama tamamen bu Kiracı için devre dışı bırakıldı. Bkz: [burada](http://aka.ms/ssprtroubleshoot) tooresolve bu. |Başarısız oldu |
| Kullanıcı parolası başarıyla sıfırlandı |Başarılı oldu |

## <a name="self-service-password-management-activity-types"></a>Self Servis parola yönetimi etkinlik türleri

şu etkinlik türlerini hello görünür hello **Self Servis parola yönetimi** denetim olay kategorisi.  Aşağıdaki her bir açıklama.

* [**Self Servis parola sıfırlama engellenen** ](#activity-type-blocked-from-self-service-password-reset) -bir kullanıcı bir parola tooreset çalıştı gösterir belirli bir ağ geçidi kullanın veya bir telefon numarası 24 saat içindeki toplam 5'ten fazla kez doğrulayın.
* [**Parola (Self Servis) değiştirme** ](#activity-type-change-password-self-service) -kullanıcı bir gönüllü gerçekleştirilen veya zorunlu gösterir (son tooexpiry) parola değiştirme.
* [**Parola sıfırlama (yönetici tarafından)** ](#activity-type-reset-password-by-admin) -parola sıfırlama hello Azure Portalı'ndan bir kullanıcı adına bir yönetici gerçekleştirilen gösterir.
* [**Parola sıfırlama (Self Servis)** ](#activity-type-reset-password-self-service) -kullanıcı başarıyla hello parolalarını sıfırlama gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com).
* [**Self Servis parola sıfırlama akış etkinliği ilerleme** ](#activity-type-self-serve-password-reset-flow-activity-progress) -sıfırlama işlemi hello parola parçası olarak bir kullanıcı geçer aracılığıyla (belirli bir parola geçirme kimlik doğrulama geçidi sıfırlama gibi) her belirli adım gösterir.
* [**Kullanıcı hesabının (Self Servis) kilidini** ](#activity-type-unlock-user-account-self-service) -kullanıcı kilidi başarıyla açıldı Active Directory hesabı parolalarını hello sıfırlamadan gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com) kullanma Merhaba AD hesabının kilidi açma sıfırlama özelliği.
* [**Kullanıcı Self Servis parola sıfırlama için kayıtlı** ](#activity-type-user-registered-for-self-service-password-reset) -bir kullanıcı tüm gerekli hello bilgi toobe mümkün tooreset kayıtlı belirtir parolalarını hello uygun olarak, şu anda Kiracı parolası sıfırlama İlkesi belirtilmiş.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Etkinlik türü: Self Servis parola sıfırlama engellendi

liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – belirtir bir kullanıcı bir parola tooreset çalıştı, belirli bir ağ geçidi kullanın veya bir telefon numarası 24 saat içindeki toplam 5'ten fazla kez doğrulayın.
* **Etkinlik aktör** -ek gerçekleştirmesini kısıtlanan hello kullanıcı sıfırlama işlemleri. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -ek gerçekleştirmesini kısıtlanan hello kullanıcı sıfırlama işlemleri. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı kısıtlanan gösteren herhangi bir ek sıfırlar gerçekleştirmeyi ek kimlik doğrulama yöntemleri deneyin veya herhangi bir ek telefon numaraları hello için sonraki 24 saat doğrula.
* **Etkinlik durumu hata nedeni** - geçerli değil

### <a name="activity-type-change-password-self-service"></a>Etkinlik türü: parola değiştirme (Self Servis)

liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – bir kullanıcı bir gönüllü gerçekleştirilen veya zorunlu gösterir (son tooexpiry) parola değiştirme.
* **Etkinlik aktör** -parolalarını değiştiren hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parolalarını değiştiren hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı parolasını başarıyla değiştirildiğini gösterir
  * _Hata_ -bir kullanıcı parolasını toochange başarısız gösterir. Tıklatmak hello satır toosee hello verir **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.
* **Etkinlik durumu hata nedeni** - 
  * _FuzzyPolicyViolationInvalidPassword_ -hello kullanıcı seçilen çok sık kullanılan veya özellikle zayıf toobe bulma tooMicrosoft'ın yasaklanan parola algılama özellikleri otomatik olarak yasaklanan bir parola.

### <a name="activity-type-reset-password-by-admin"></a>Etkinlik türü: (yönetici tarafından) parola sıfırlama

liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – yönetici gerçekleştirilen parola hello Azure Portalı'ndan bir kullanıcı adına sıfırlama gösterir.
* **Etkinlik aktör** -hello parola başka bir son kullanıcı veya yönetici adına sıfırlama gerçekleştiren hello Yöneticisi. Ya da bir genel yönetici, parola yönetici, kullanıcı veya Yardım Masası yönetici olması gerekir.
* **Etkinlik hedef** -hello kullanıcı parolasını sıfırlandı. Bir son kullanıcı veya farklı bir yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir yönetici kullanıcının parolası başarıyla sıfırlandı gösterir
  * _Hata_ -bir yönetici bir kullanıcının parolasını toochange başarısız gösterir. Tıklatmak hello satır toosee hello verir **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.

### <a name="activity-type-reset-password-self-service"></a>Etkinlik türü: parola sıfırlama (Self Servis)

liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı başarıyla hello parolalarını sıfırlama gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com).
* **Etkinlik aktör** -parolalarını sıfırlama hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parolalarını sıfırlama hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı, kendi parola başarıyla sıfırlandı gösterir
  * _Hata_ -bir kullanıcı kendi parolasını tooreset başarısız gösterir. Tıklatmak hello satır toosee hello verir **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.
* **Etkinlik durumu hata nedeni** -
  * _FuzzyPolicyViolationInvalidPassword_ -hello Yöneticisi seçili çok sık kullanılan veya özellikle zayıf toobe bulma tooMicrosoft'ın yasaklanan parola algılama özellikleri otomatik olarak yasaklanan bir parola.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Etkinlik türü: kendi kendine parola sıfırlama akış etkinliği ilerleme hizmet

liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı geçer aracılığıyla (belirli bir parola geçirme kimlik doğrulama geçidi sıfırlama gibi) sıfırlama işlemi hello parola parçası olarak her belirli adım gösterir.
* **Etkinlik aktör** -hello parola parçası gerçekleştiren hello kullanıcı sıfırlama akış. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -hello parola parçası gerçekleştiren hello kullanıcı sıfırlama akış. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı belirli bir adıma hello parola sıfırlama akışının başarıyla tamamlandı gösterir.
  * _Hata_ -belirli bir adıma hello parola sıfırlama başarısız akış gösterir. Tıklatmak hello satır toosee hello verir **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.
* **Etkinlik durumu nedeniyle izin verilen**
  * İçin aşağıdaki tabloya bakın [tüm sıfırlama etkinliği durumu nedeniyle izin verilen](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Etkinlik türü: kullanıcı hesabı (Self Servis) kilidini aç

liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcının kilidi başarıyla açıldı Active Directory hesabı parolalarını hello sıfırlamadan gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com) hello AD hesabı kullanarak kilidini Sıfırla özelliği.
* **Etkinlik aktör** -hesaplarında, parola sıfırlama olmadan kilidi hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -hesaplarında, parola sıfırlama olmadan kilidi hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı, kendi hesabını başarıyla kilidi gösterir
  * _Hata_ -kullanıcı hesaplarında toounlock başarısız gösterir. Tıklatmak hello satır toosee hello verir **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Etkinlik türü: kullanıcı Self Servis parola sıfırlama için kayıtlı

liste aşağıdaki hello bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı tüm gerekli hello bilgi toobe mümkün tooreset kayıtlı belirtir parolalarını hello uygun olarak, şu anda Kiracı parolası sıfırlama İlkesi belirtilmiş. 
* **Etkinlik aktör** -parola sıfırlama için kaydolan hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parola sıfırlama için kaydolan hello kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -parola sıfırlama hello geçerli ilkesiyle uygun şekilde başarıyla kayıtlı bir kullanıcı gösterir. 
  * _Hata_ -parola sıfırlama için başarısız kullanıcı tooregister gösterir. Tıklatmak hello satır toosee hello verir **etkinlik durum nedeni** kategori toolearn neden hello başarısızlığından hakkında daha fazla bilgi. Not - Bu gelmez bir kullanıcı oluşturulamıyor tooreset kendi hello kayıt işlemi tamamlanmadı yalnızca paroladır. (Doğrulanmazsa, bir telefon numarası gibi), doğru kendi hesabındaki doğrulanmamış verileri ise bunlar bu telefon numarası doğrulanmadı olsa bile, yine tooreset kullanabileceklerini parolalarını. Daha fazla bilgi için bkz: [kullanıcı kayıtları ne olur?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Sonraki adımlar

bağlantılar aşağıdaki hello parola sıfırlama ve Azure AD kullanma ile ilgili ek bilgiler sağlar

* [Kısayol toouser yönetim denetim günlüklerini](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) - tooyour kiracının kullanıcı yönetimi denetim doğrudan günlükleri gidin
* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri** ](active-directory-passwords-data.md) - gereklidir hello verileri anlamak ve nasıl kullanıldığı için parola yönetimi
* [**Sunum** ](active-directory-passwords-best-practices.md) -planlama ve burada bulunan hello kılavuzu kullanarak SSPR tooyour kullanıcılara dağıtma
* [**Özelleştirme** ](active-directory-passwords-customize.md) -hello görünümüne hello SSPR deneyimi, şirketiniz için özelleştirebilirsiniz.
* [**Teknik derinlemesine** ](active-directory-passwords-how-it-works.md) -hello perdenin toounderstand nasıl çalıştığını gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? -Her zaman tooask istediğinizi tooquestions yanıtlar
* [**Sorun giderme** ](active-directory-passwords-troubleshoot.md) -nasıl biz SSPR ile bkz tooresolve ortak sorunları öğrenin
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
