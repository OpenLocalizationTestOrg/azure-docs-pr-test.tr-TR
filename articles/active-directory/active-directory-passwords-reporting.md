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
ms.openlocfilehash: ba7b36e654aa0bf3b74d42a2b0ae96ae2a9b6241
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Azure AD parola yönetimi için raporlama seçenekleri

Birçok kuruluş bilmek istediğiniz dağıtım sonrası nasıl veya SSPR gerçekten kullanılıyorsa. Azure AD tamamlanmış raporları ve size uygun şekilde lisanslanır varsa, kullanarak soruları yanıtlamak için yardımcı raporlama özellikleri sağlar olanak tanır özel sorgular oluşturabilirsiniz.

[Azure portalı] mevcut raporlar aşağıdaki soruları yanıtlanabilir (https://portal.azure.com/).

> [!NOTE]
> Olmalıdır [genel yönetici](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) ve bu veriler kuruluşunuz adına raporlama sekme veya denetim günlüklerini en az bir kez ziyaret ederek toplanması katılımı gerekir. Bunun yapılması kadar veri kuruluşunuz için toplanmaz

* Kaç kişinin parola sıfırlama için kayıtlı?
* Parola sıfırlama için kayıtlı olan kim?
* Verileri kaydetme kişiler nelerdir?
* Kaç kişinin son yedi gün içinde parolalarını sıfırlama?
* En yaygın yöntemleri kullanıcıları veya yöneticileri parolalarını sıfırlamak için kullanın ne var mı?
* Sık karşılaşılan sorunları kullanıcıları veya yöneticileri yüz parola sıfırlama kullanmaya çalışırken nelerdir?
* Hangi yöneticileri kendi parolalarını sık sıfırlama?
* Parola sıfırlama ile geçmeden tüm şüpheli etkinlik mi?

## <a name="how-to-view-password-management-reports-in-the-azure-portal"></a>Azure portalında parola yönetimi raporları görüntüleme

Azure portal deneyimi, size parola sıfırlama görüntülemek için geliştirilmiş bir yolu yoktur ve parola sıfırlama kaydı etkinliği.  Parola ve parola sıfırlama kayıt olayları sıfırlama bulmak için aşağıdaki adımları izleyin:

1. Gidin [ **portal.azure.com**](https://portal.azure.com)
2. Tıklatın **daha fazla hizmet** ana Azure portal sol taraftaki gezinti menüsünde
3. Arama **Azure Active Directory** Hizmetler listesinde ve seçin
4. Tıklatın **kullanıcıları ve grupları** Azure Active Directory Gezinti menüsünde
5. Tıklatın **denetim günlüklerini** kullanıcıları ve grupları Gezinti menüsünde Gezinti öğesi. Bu, tüm dizininizdeki tüm kullanıcılara karşı gerçekleşen denetim olayları gösterir. Bu görünüm tüm parola ile ilgili olayları de görmek için filtre uygulayabilirsiniz.
6. İlgili olaylar parola sıfırlama yalnızca bu görünüme filtre uygulamak için **filtre** dikey pencerenin üstündeki düğmesi.
7. Gelen **filtre** menüsünde, select **kategori** açılan listesinde ve şekilde değiştirin **Self Servis parola yönetimi** kategori türü.
8. İsteğe bağlı olarak daha fazla filtre belirli seçerek listeyi **etkinlik** ilgilendiğiniz

## <a name="how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api"></a>Parola yönetimi olayları Azure AD raporları ve olayları API alma

Azure AD raporları ve olayları API destekler parola sıfırlama ve parola sıfırlama kayıt raporlara dahil tüm bilgileri alınıyor. Bu API'yi kullanarak tek tek parola sıfırlama indirebilirsiniz ve tercih ettiğiniz raporlama teknolojisi ile tümleştirme için kayıt olayları parola sıfırlama.

### <a name="how-to-get-started-with-the-reporting-api"></a>Nasıl raporlama API'si ile çalışmaya başlama

Bu verilere erişmek için bir küçük uygulama veya bizim sunuculardan verileri almak için komut dosyası yazmanız gerekir. [Azure AD raporlama API'si ile çalışmaya başlama öğrenin](active-directory-reporting-api-getting-started.md).

Bir çalışan betik olduktan sonra sonraki senaryolarınızı karşılayacak şekilde alabilirsiniz parola sıfırlama ve kayıt olayları inceleyin istersiniz.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): olayları parola sıfırlama için kullanılabilen sütunları listeler
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): kayıt olayları parola sıfırlama için kullanılabilen sütunları listeler

### <a name="reporting-api-data-retrieval-limitations"></a>Raporlama API veri alma sınırlamaları

Şu anda Azure AD raporları ve olayları API alır kadar **75,000 olayları tek tek** , [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) ve [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) türleri kapsayıcı **son 30 gün**.

Almak veya bu pencereyi aşan veri depolamak gerekiyorsa, dış bir veritabanında kalıcı yapma ve neden farkları sorgulamak için API kullanarak öneririz. Bizim önerimiz, kuruluşunuzda SSPR kullanmaya başladığınızda, bu veri alma başlamak, harici olarak kalır ve bu noktadan itibaren farkları izlemek devam etmek için ' dir.

## <a name="how-to-download-password-reset-registration-events-quickly-with-powershell"></a>Parola sıfırlama kayıt olayları hızla PowerShell ile karşıdan yükleme

Azure AD raporları ve olayları API kullanarak doğrudan ek olarak, ayrıca kullanabilirsiniz PowerShell Betiği dizininizde yeni kayıt olayları aşağıda. Kim son kayıtlı olan veya beklediğiniz gibi parola sıfırlama sunum oluştuğunu sağlamak istediğiniz görmek istediğiniz durumlarda kullanışlıdır.

* [Azure AD SSPR'yi kayıt etkinlik PowerShell Betiği](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Azure Portalı'nda rapor sütunlarını açıklaması

Aşağıdaki listede ayrıntılı raporu sütunların her biri açıklanmaktadır:

* **Kullanıcı** – bir parola deneyen kullanıcıya kayıt işlemi sıfırlayın.
* **Rol** – dizindeki kullanıcı rolü.
* **Tarih ve saat** – tarih ve saat girişimi.
* **Veri kayıtlı** – hangi kimlik doğrulama verileri kullanıcı sağlanan sırasında parola sıfırlama kaydı.

### <a name="description-of-report-values-in-azure-portal"></a>Azure Portalı'nda rapor değerlerinin açıklaması

Aşağıdaki tabloda her sütun için izin verilen farklı değerler açıklanmaktadır:

| Sütun | İzin verilen değerler ve anlamları |
| --- | --- |
| Kayıtlı veri |**Alternatif e-posta** – kullanıcı kimlik doğrulaması için alternatif e-posta veya kimlik doğrulama e-posta kullanılır<p><p>**Ofis telefonu**– kimlik doğrulaması için kullanılan kullanıcı ofis telefonu<p>**Cep telefonu** -kullanıcı kullanılan cep telefonu veya kimlik doğrulaması için kimlik doğrulama telefon<p>**Güvenlik soruları** – kullanıcı kimlik doğrulaması için güvenlik soruları kullanılır<p>**Yukarıdaki (örneğin, alternatif e-posta + cep telefonu) herhangi bir bileşimini** – 2 kapısı İlkesi belirtilir ve kullanılan kullanıcı hangi iki yöntemi gösterilir oluşur kimlik doğrulama parolasını sıfırlama isteği. |

## <a name="view-password-reset-activity-in-the-classic-portal"></a>Görünüm parola sıfırlama etkinliği Klasik portalda

Bu rapor, tüm parola sıfırlama, kuruluşunuzda oluşmuş denemeleri gösterir.

* **En büyük zaman aralığı**: 30 gün
* **En fazla sayıda satırı**: 75.000
* **İndirilebilir**: Evet, CSV dosyası aracılığıyla

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Azure Klasik Portalı'nda rapor sütunlarını açıklaması

Aşağıdaki listede ayrıntılı raporu sütunların her biri açıklanmaktadır:

1. **Kullanıcı** – bir parola denemesi kullanıcının (kullanıcı parola sıfırlama geldiğinde sağlanan kullanıcı kimliği temel alan) işlemi Sıfırla.
2. **Rol** – dizindeki kullanıcı rolü.
3. **Tarih ve saat** – tarih ve saat girişimi.
4. **Yöntemleri kullanılan** – kullanıcının bu için kullanılan kimlik doğrulama yöntemleri sıfırlama işlemi.
5. **Sonuç** – işlemi sonuç parola sıfırlama.
6. **Ayrıntılar** – neden parola sıfırlama ayrıntılarını olduğu değerle sonuçlandı.  Ayrıca beklenmeyen bir hata çözümlemek için sürebilir herhangi azaltma adımlarını içerir.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Azure Klasik Portalı'nda rapor değerlerinin açıklaması

Aşağıdaki tabloda her sütun için izin verilen farklı değerler açıklanmaktadır:

| Sütun | İzin verilen değerler ve anlamları |
| --- | --- |
| Kullanılan yöntemler |**Alternatif e-posta** – kullanıcı kimlik doğrulaması için alternatif e-posta veya kimlik doğrulama e-posta kullanılır<p>**Ofis telefonu** – kimlik doğrulaması için kullanılan kullanıcı ofis telefonu<p>**Cep telefonu** – kullanıcı kullanılan cep telefonu veya kimlik doğrulaması için kimlik doğrulama telefon<p>**Güvenlik soruları** – kullanıcı kimlik doğrulaması için güvenlik soruları kullanılır<p>**Yukarıdaki (örneğin, alternatif e-posta + cep telefonu) herhangi bir bileşimini** – 2 kapısı İlkesi belirtilir ve kullanılan kullanıcı hangi iki yöntemi gösterilir oluşur kimlik doğrulama parolasını sıfırlama isteği. |
| Sonuç |**Terk** – kullanıcı parola sıfırlama başladı, ancak yarı yarıya aracılığıyla tamamlamadan durdu<p>**Engellenen** – kullanıcı hesabının engelledi parola sıfırlama sayfası kullanmak için parola sıfırlama çalışırken nedeniyle kullanmanızı veya bir 24 saatlik sürede çok sayıda ağ geçidi tek bir parola sıfırlama<p>**İptal** – kullanıcı parola sıfırlama başladı, ancak parçası şekilde ile oturum iptal etmek için İptal düğmesine tıklandığında <p>**Yönetici ile bağlantı kurulamadı** – kullanıcı kendisinin çözümlenemedi kendi oturumu sırasında bir sorun var, kullanıcı tamamlama yerine "yöneticinize başvurun" bağlantısına tıkladığınız için akış parola sıfırlama<p>**Başarısız** – kullanıcı, kullanıcı (örneğin, hiçbir lisans, eksik kimlik bilgileri, parola yönetilen şirket içi ancak geri yazma kapalıdır) özelliğini kullanmak için yapılandırılmadığı için büyük olasılıkla bir parola sıfırlama mümkün değildi.<p>**Başarılı** – parola sıfırlama başarılı oldu. |
| Ayrıntılar |Aşağıdaki tabloya bakın |

### <a name="allowed-values-for-details-column"></a>İzin verilen değerler Ayrıntılar sütunu için

Parola kullanarak Etkinlik Raporu sıfırladığınızda bekleyebilir sonuç türleri listesi aşağıdadır:

| Ayrıntılar | Sonuç türü |
| --- | --- |
| Kullanıcı e-posta doğrulama seçeneğini tamamladıktan sonra terk |terk |
| Kullanıcı mobil SMS doğrulama seçeneğini tamamladıktan sonra terk |terk |
| Kullanıcı mobil sesli arama doğrulama seçeneğini tamamladıktan sonra terk |terk |
| Office sesli arama doğrulama seçeneğini tamamladıktan sonra terk kullanıcı |terk |
| Kullanıcı seçeneği sorular güvenlik tamamladıktan sonra bırakıldı |terk |
| Kullanıcı Kimliğini girdikten sonra terk kullanıcı |terk |
| Kullanıcı e-posta doğrulama seçeneğini başlattıktan sonra terk |terk |
| Kullanıcı mobil SMS doğrulama seçeneğini başlattıktan sonra terk |terk |
| Kullanıcı mobil sesli arama doğrulama seçeneğini başlattıktan sonra terk |terk |
| Office sesli arama doğrulama seçeneğini başlattıktan sonra terk kullanıcı |terk |
| Kullanıcı güvenlik başlangıç seçeneği sorular sonra bırakıldı |terk |
| Yeni bir parola seçmeden önce terk kullanıcı |terk |
| Yeni bir parola seçerken terk kullanıcı |terk |
| Kullanıcı çok fazla geçersiz SMS doğrulama kodları girilen ve 24 saat engellendi |Engellendi |
| Kullanıcı, cep telefonu sesli doğrulama birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı office telefon sesli doğrulama birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı güvenlik sorularını birden çok kez denediniz ve 24 saat engellendi |Engellendi |
| Kullanıcı bir telefon numarası çok fazla kez doğrulamaya çalıştı ve 24 saat engellendi |Engellendi |
| Gerekli kimlik doğrulama yöntemlerini geçirmeden önce kullanıcı iptal etti |İptal edildi |
| Yeni bir parola göndermeden önce kullanıcı iptal etti |İptal edildi |
| Kullanıcı bir yönetici e-posta doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı mobil SMS doğrulama seçeneğini denendikten sonra bir yönetici ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı mobil sesli arama doğrulama seçeneğini denendikten sonra bir yönetici ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı bir yönetici office sesli arama doğrulama seçeneğini denendikten sonra ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Kullanıcı Güvenlik sorusu doğrulama seçeneğini denendikten sonra bir yönetici ile bağlantı kurulamadı |Bağlantı kuruldu yönetici |
| Parola sıfırlama bu kullanıcı için etkin değil. Parola sıfırlama bu sorunu çözmek için Yapılandır sekmesi altında etkinleştir |Başarısız oldu |
| Kullanıcı bir lisans yok. Bu sorunu çözmek için kullanıcıya bir lisans ekleyebilirsiniz. |Başarısız oldu |
| Kullanıcı tanımlama bilgilerinin etkin bir aygıttan sıfırlamaya |Başarısız oldu |
| Kullanıcı hesabı tanımlanan yetersiz kimlik doğrulama yöntemlerine sahiptir. Bu sorunu çözmek için kimlik bilgisi ekleyin |Başarısız oldu |
| Kullanıcının, yönetilen şirket içi paroladır. Bu sorunu gidermek parola geri yazma özelliğini etkinleştirme |Başarısız oldu |
| Şirket içi parola sıfırlama hizmetinizi erişemedi. Eşitleme makinenizin olay günlüğünü denetleyin |Başarısız oldu |
| Kullanıcının sıfırlama parola içi ederken bir sorun oluştu. Eşitleme makinenizin olay günlüğünü denetleyin |Başarısız oldu |
| Bu kullanıcının parola sıfırlama kullanıcılar grubunun bir üyesi değil. Bu kullanıcıyı bu sorunu çözmek için bu gruba ekleyin. |Başarısız oldu |
| Parola sıfırlama tamamen bu Kiracı için devre dışı bırakıldı. Bkz: [burada](http://aka.ms/ssprtroubleshoot) bu sorunu gidermek için. |Başarısız oldu |
| Kullanıcı parolası başarıyla sıfırlandı |Başarılı oldu |

## <a name="self-service-password-management-activity-types"></a>Self Servis parola yönetimi etkinlik türleri

Aşağıdaki etkinlik türlerini görünür **Self Servis parola yönetimi** denetim olay kategorisi.  Aşağıdaki her bir açıklama.

* [**Self Servis parola sıfırlama engellenen** ](#activity-type-blocked-from-self-service-password-reset) -parola sıfırlama, belirli bir ağ geçidi kullanın veya bir telefon numarası 24 saat içindeki toplam 5'ten fazla kez doğrulamak bir kullanıcı çalıştı gösterir.
* [**Parola (Self Servis) değiştirme** ](#activity-type-change-password-self-service) -bir kullanıcı bir gönüllü gerçekleştirilen ya da (Bitiş nedeniyle) zorunlu parola değiştirme.
* [**Parola sıfırlama (yönetici tarafından)** ](#activity-type-reset-password-by-admin) -parola sıfırlama Azure portalından bir kullanıcı adına bir yönetici gerçekleştirilen gösterir.
* [**Parola sıfırlama (Self Servis)** ](#activity-type-reset-password-self-service) -kullanıcı parolalarını sıfırlama başarıyla gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com).
* [**Self Servis parola sıfırlama akış etkinliği ilerleme** ](#activity-type-self-serve-password-reset-flow-activity-progress) -sıfırlama işlemi parola parçası olarak bir kullanıcı geçer aracılığıyla (belirli bir parola geçirme kimlik doğrulama geçidi sıfırlama gibi) her belirli adım gösterir.
* [**Kullanıcı hesabının (Self Servis) kilidini** ](#activity-type-unlock-user-account-self-service) -kullanıcı kilidi başarıyla açıldı Active Directory hesabı parolalarını sıfırlamadan gösterir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com) AD kullanma Hesap kilidi açma sıfırlama özelliği.
* [**Kullanıcı Self Servis parola sıfırlama için kayıtlı** ](#activity-type-user-registered-for-self-service-password-reset) -bir kullanıcı parolasını şu anda belirtilen Kiracı parolası sıfırlama ilkesini uygun olarak sıfırlamayı kullanabilmek için gerekli tüm bilgileri kayıtlı belirtir.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Etkinlik türü: Self Servis parola sıfırlama engellendi

Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı denedi belirtir bir parola sıfırlama, belirli bir ağ geçidi kullanın veya bir telefon numarası 24 saat içindeki toplam 5'ten fazla kez doğrulayın.
* **Etkinlik aktör** -ek gerçekleştirmesini kısıtlanan kullanıcı sıfırlama işlemlerinin. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -ek gerçekleştirmesini kısıtlanan kullanıcı sıfırlama işlemlerinin. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı kısıtlanan gösteren herhangi bir ek sıfırlar gerçekleştirmeyi, ek kimlik doğrulama yöntemleri deneyin veya sonraki 24 saat için hiçbir ek telefon numaralarını doğrulayın.
* **Etkinlik durumu hata nedeni** - geçerli değil

### <a name="activity-type-change-password-self-service"></a>Etkinlik türü: parola değiştirme (Self Servis)

Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – bir kullanıcı bir gönüllü gerçekleştirilen ya da (Bitiş nedeniyle) zorunlu parola değiştirme.
* **Etkinlik aktör** -parolalarını değiştiren kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parolalarını değiştiren kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı parolasını başarıyla değiştirildiğini gösterir
  * _Hata_ -kullanıcı başarısız parolalarını değiştirmek gösterir. Satır tıklatarak verir görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.
* **Etkinlik durumu hata nedeni** - 
  * _FuzzyPolicyViolationInvalidPassword_ -kullanıcı bir parola çok genel veya özellikle zayıf bulmakta Microsoft'un yasaklanan parola algılama özellikleri nedeniyle otomatik olarak yasaklanan seçilen.

### <a name="activity-type-reset-password-by-admin"></a>Etkinlik türü: (yönetici tarafından) parola sıfırlama

Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – yönetici gerçekleştirilen parola Azure portalından bir kullanıcı adına sıfırlama gösterir.
* **Etkinlik aktör** -parola sıfırlama başka bir son kullanıcı veya yönetici adına gerçekleştiren yönetici. Ya da bir genel yönetici, parola yönetici, kullanıcı veya Yardım Masası yönetici olması gerekir.
* **Etkinlik hedef** -kullanıcının parolasını sıfırlandı. Bir son kullanıcı veya farklı bir yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir yönetici kullanıcının parolası başarıyla sıfırlandı gösterir
  * _Hata_ -yönetici başarısız bir kullanıcının parolasını değiştirmek gösterir. Satır tıklatarak verir görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.

### <a name="activity-type-reset-password-self-service"></a>Etkinlik türü: parola sıfırlama (Self Servis)

Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı parolalarını sıfırlama başarıyla belirtir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com).
* **Etkinlik aktör** -parolalarını sıfırlama kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parolalarını sıfırlama kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı, kendi parola başarıyla sıfırlandı gösterir
  * _Hata_ -kullanıcı başarısız kendi parolasını sıfırlamak gösterir. Satır tıklatarak verir görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.
* **Etkinlik durumu hata nedeni** -
  * _FuzzyPolicyViolationInvalidPassword_ -çok genel veya özellikle zayıf bulmakta Microsoft'un yasaklanan parola algılama özellikleri nedeniyle otomatik olarak yasaklanan bir parola yönetici seçili.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Etkinlik türü: kendi kendine parola sıfırlama akış etkinliği ilerleme hizmet

Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcı geçer aracılığıyla (belirli bir parola geçirme kimlik doğrulama geçidi sıfırlama gibi) sıfırlama işlemi parola parçası olarak her belirli adım gösterir.
* **Etkinlik aktör** -parola parçası gerçekleştiren kullanıcı Akış sıfırlayın. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parola parçası gerçekleştiren kullanıcı Akış sıfırlayın. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -kullanıcı parolası sıfırlama akışının belirli bir adıma başarıyla tamamlandı gösterir.
  * _Hata_ -belirli bir adıma parola sıfırlama başarısız akış gösterir. Satır tıklatarak verir görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.
* **Etkinlik durumu nedeniyle izin verilen**
  * İçin aşağıdaki tabloya bakın [tüm sıfırlama etkinliği durumu nedeniyle izin verilen](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Etkinlik türü: kullanıcı hesabı (Self Servis) kilidini aç

Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcının kilidi başarıyla açıldı Active Directory hesabı parolalarını sıfırlamadan belirtir [Azure AD parola sıfırlama portalı](https://passwordreset.microsoftonline.com) AD hesabı kullanarak kilidi Sıfırla özelliği.
* **Etkinlik aktör** -hesaplarında, parola sıfırlama olmadan kilidi kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -hesaplarında, parola sıfırlama olmadan kilidi kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -bir kullanıcı, kendi hesabını başarıyla kilidi gösterir
  * _Hata_ -kullanıcı hesaplarının kilidini başaramadı gösterir. Satır tıklatarak verir görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Etkinlik türü: kullanıcı Self Servis parola sıfırlama için kayıtlı

Aşağıdaki listede bu etkinliği ayrıntılı açıklanmıştır:

* **Etkinlik açıklama** – kullanıcının parolasını şu anda belirtilen Kiracı parolası sıfırlama ilkesini uygun olarak sıfırlamayı kullanabilmek için gerekli tüm bilgileri kayıtlı belirtir. 
* **Etkinlik aktör** -parola sıfırlama için kayıtlı olan kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **Etkinlik hedef** -parola sıfırlama için kayıtlı olan kullanıcı. Bir son kullanıcı veya yönetici olabilir.
* **İzin verilen aktivitesi durumları**
  * _Başarı_ -parola sıfırlama geçerli ilkesiyle uygun şekilde başarıyla kayıtlı bir kullanıcı gösterir. 
  * _Hata_ -kullanıcı başarısız parola sıfırlama için kaydedilecek gösterir. Satır tıklatarak verir görmek **etkinlik durum nedeni** neden oluştuğuna hakkında daha fazla bilgi için kategori. Not - Bu gelmez bir kullanıcı, oluşturamıyor kendi parolasını sıfırlamak için henüz kayıt işlemi tamamlanmadı. (Doğrulanmazsa, bir telefon numarası gibi), doğru kendi hesabındaki doğrulanmamış verileri ise bunlar bu telefon numarası doğrulanmadı olsa da, bunlar, parolasını sıfırlamak için kullanmaya devam edebilirsiniz. Daha fazla bilgi için bkz: [kullanıcı kayıtları ne olur?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Sonraki adımlar

Aşağıdaki bağlantılar, Azure AD kullanarak parola sıfırlama ile ilgili ek bilgiler sağlar

* [Kullanıcı Yönetimi denetim günlüklerini kısayolu](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) - gidin, kiracının kullanıcı yönetimi doğrudan denetim günlükleri
* [**Hızlı Başlangıç**](active-directory-passwords-getting-started.md) - Azure AD self servis parola yönetimi ile çalışmaya hazırlanın 
* [**Lisanslama**](active-directory-passwords-licensing.md) - Azure AD Lisanslarınızı yapılandırın
* [**Veri**](active-directory-passwords-data.md) - Gerekli olan verileri ve parola yönetimi için nasıl kullanıldığını anlayın
* [**Kullanıma Sunma** ](active-directory-passwords-best-practices.md) - Buradaki yönergelerle SSPR’ı planlayın ve kullanıcılarınıza dağıtın
* [**Özelleştirme**](active-directory-passwords-customize.md) - SSPR deneyiminin görünümünü şirketiniz için özelleştirin.
* [**Teknik Ayrıntı**](active-directory-passwords-how-it-works.md) - Nasıl çalıştığını anlamak için perde arkasına gidin
* [**Sık Sorulan Sorular**](active-directory-passwords-faq.md) - Nasıl? Neden? Ne? Nerede? Kim? Ne zaman? - Her zaman sormak istediğiniz soruların yanıtları
* [**Sorun giderme**](active-directory-passwords-troubleshoot.md) - SSPR ile yaygın olarak karşılaştığımız sorunların çözümü hakkında bilgi alın
* [**İlke**](active-directory-passwords-policy.md) - Azure AD parola ilkelerini anlayın ve ayarlayın
