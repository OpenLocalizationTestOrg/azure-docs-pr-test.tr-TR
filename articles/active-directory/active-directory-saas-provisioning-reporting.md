---
title: "Azure Active Directory otomatik kullanıcı hesabında tooSaaS uygulamalar sağlama raporlama | Microsoft Docs"
description: "Toocheck hello nasıl otomatik olarak bir kullanıcı hesabının işleri sağlama durumu ve nasıl öğrenin tootroubleshoot hello bireysel kullanıcıları sağlama."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>Öğretici: otomatik olarak bir kullanıcı hesabı sağlama raporlama


Azure Active Directory içeren bir [hizmet sağlama kullanıcı hesabı](active-directory-saas-app-provisioning.md) yardımcı hello XML'deki sağlama SaaS uygulamaları ve diğer sistemler uçtan uca kimlik yaşam döngüsü hello amacı için kullanıcı hesapları sağlama otomatikleştirme yönetimi. Azure AD destekleyen tüm hello uygulamaları ve hello hello "Öne çıkan" bölüm içinde sistemleri için bağlayıcıları sağlama önceden tümleştirilmiş kullanıcı [Azure AD uygulama galerisinde](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).

Yukarı ve nasıl ayarlandıktan sonra toocheck hello durumunu, sağlama nasıl işler bu makalede tek tek kullanıcılar ve gruplar hello tootroubleshoot sağlama.

## <a name="overview"></a>Genel Bakış

Sağlama bağlayıcılar öncelikle ayarlanır ve hello kullanılarak yapılandırılan [Azure Yönetim Portalı](https://portal.azure.com), aşağıdaki hello tarafından [belgelerine sağlanan](active-directory-saas-tutorial-list.md) burada kullanıcı hesabı sağlama Merhaba uygulaması için İstenen. Yapılandırılmış ve çalışan sonra bir uygulama için işleri sağlama iki yöntemden birini kullanarak bildirilebilir:

* **Azure Yönetim Portalı** -bu makalede, öncelikle hello rapor bilgilerini alma açıklanır [Azure Yönetim Portalı](https://portal.azure.com), hem bir özet raporu sağlama hem de ayrıntılı sağlama sağlar belirli bir uygulama için günlükleri denetleyin.

* **API denetim** -Azure Active Directory denetim günlükleri hello programlı alınmasını ayrıntılı sağlama etkinleştirir API denetim de sağlar. Bkz: [Azure Active Directory denetim API Başvurusu](active-directory-reporting-api-audit-reference.md) belgeleri belirli toousing için bu API. Bu makalede nasıl toouse hello API özellikle kapsamaz olsa da, hello Denetim günlüğüne olayları sağlama hello türleri ayrıntı.

### <a name="definitions"></a>Tanımlar

Bu makalede aşağıda tanımlanan koşullarını izleyen hello kullanır:

* **Kaynak sistem** -Azure AD sağlama hizmeti hello kullanıcıların hello deposu eşitler. Azure Active Directory hello kaynak sistem hello çoğunluğu için bağlayıcıları sağlama önceden tümleştirilmiştir, ancak kopyalanamayan bazı özel durumlar (örnek: Workday gelen eşitleme).

* **Hedef sistem** -Azure AD sağlama hizmeti hello kullanıcıların hello deposu eşitler için. Bu genellikle bir SaaS uygulaması olur (örnek: Salesforce, ServiceNow, Google Apps, iş için Dropbox), ancak bazı durumlarda Active Directory gibi şirket içi sistem olabilir (örnek: Workday gelen eşitleme tooActive Directory).


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>Raporları hello Azure Yönetim Portalı'ndan sağlama alma

Rapor bilgilerini belirli bir uygulamada sağlama tooget hello başlatma tarafından başlangıç [Azure Yönetim Portalı](https://portal.azure.com) ve toohello Kurumsal uygulama için sağlama yapılandırılmış tarama. Örneğin, kullanıcılar tooLinkedIn yükseltme sağlıyorsanız, hello Gezinti yolu toohello uygulama ayrıntıları verilmiştir:

**Azure Active Directory > Kurumsal uygulamalar > tüm uygulamaları > LinkedIn Yükselt**

Buradan, hello sağlama özet raporu hem hello sağlama denetim günlüklerini erişebilir, her ikisi de aşağıda açıklanmıştır.


### <a name="provisioning-summary-report"></a>Sağlama özet raporu

Özet raporu sağlama hello hello görülebilir **sağlama** uygulama sekmesinde için. Merhaba eşitleme ayrıntıları bölümü altında bulunan **ayarları**ve aşağıdaki bilgilerle hello sağlar:

* Merhaba sayısı toplam kullanıcı ve / grupları, eşitlenmemiş ve şu anda kapsamında hello hedef sistem hello kaynak sistemi arasında sağlama.

* Merhaba son zaman hello eşitleme çalıştırıldı. Eşitlemeler genellikle 20-40 tam eşitleme tamamlandıktan sonra dakikada oluşur.

* Desteklemediğini ilk tam Eşitleme tamamlandı.

* Sağlama işlemi hello Karantinadaki yerleştirilmiş olup olmadığına ve hangi hello hello karantina durumu örneğin (tooinvalid yönetici kimlik bilgileri nedeniyle hedef sistemiyle hatası toocommunicate) nedeni

Özet raporu sağlama hello hello ilk yer admins görünüm toocheck hello sağlama işi işletimsel durumunu hello üzerinde olmalıdır.

 ![Özet raporu](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>Sağlama denetim günlükleri
Hizmet sağlama hello tarafından gerçekleştirilen tüm etkinlikler hello görüntülenebilir hello Azure AD denetim günlüklerine kaydedilir **denetim günlüklerini** hello sekmesinde **hesap sağlama** kategorisi. Günlüğe kaydedilen etkinlik olay türleri şunlardır:

* **Olayları alma** -hello Azure AD sağlama hizmet alır. kaynak sistem ya da hedef sistem tek bir kullanıcı veya grup hakkında bilgi her zaman bir "alma" olayı kaydedilir. Eşitleme sırasında kullanıcıların hello kaynak sistemden ilk olarak, "olayları Al"olarak kaydedilen hello sonuçlarıyla alınır. Merhaba, aynı zamanda "olayları Al"olarak kaydedilen hello sonuçlarıyla varsa eşleşen alınan hello kullanıcıların kimliklerini hello hedef sistem toocheck karşı sonra seçmeleri istenir. Bu olaylar, tüm eşlenen kullanıcı öznitelikleri ve hello olay hello aynı anda hello Azure AD sağlama hizmeti tarafından karşılaşılan değerlerine kaydeder. 

* **Eşitleme kuralı olayları** - bu olayları hello özniteliği eşleme kurallarını hello sonuçlarını rapor ve kullanıcı verilerini içe ve hello hedef ve kaynak sistemlerden hesaplanan sonra herhangi bir kapsam filtreleri, yapılandırılmış. Örneğin, bir kullanıcı bir kaynak sistemde toobe sağlama kapsamında kabul edilir ve kabul toonot yoksa hello hedef sistemde sonra kullanıcı hello bu olay kayıtlarını hello hedef sistemde sağlanacak. 

* **Olay Ver** -hello Azure AD sağlama hizmeti, bir kullanıcı hesabı veya grup nesnesi tooa hedef sistem Yazar her zaman "export" olay kaydedilir. Bu olaylar, tüm kullanıcı özniteliklerini ve değerlerini tarafından hello hello olay hello aynı anda Azure AD sağlama hizmeti yazılmış kaydedin. Varsa bir hata hello kullanıcı hesabını veya grubunu nesne toohello hedef sistem yazılırken, burada görüntülenir.

* **İşlem emanet olayları** -işlem escrows gerçekleşmesini hello olduğunda hizmet sağlama bir işlem çalışırken bir hatayla karşılaşırsa ve zaman bir geri alma aralıkta tooretry hello işlemi başlar. Bir "emanet" olay sağlama işlemi devre dışı bırakılan her zaman kaydedilir.

Tek bir kullanıcı için sağlama olayları bakıldığında hello olayları normalde bu sırada oluşur:

1. Alma olayı: kullanıcı hello kaynak sistemden alınır.

2. Alma olayı: hedef sistemidir sorgulanan toocheck alınan hello kullanıcı hello varlığı.

3. Eşitleme kuralı olayı: kullanıcı verilerini hedef ve kaynak sistemlerden eşleme kurallarını ve varsa, hangi eylemin gerçekleştirileceğini filtreleri toodetermine kapsamı yapılandırılmış hello özniteliğiyle karşılaştırılmalıdır değerlendirilir.

4. Olayı ver: hello eşitleme kuralını olay eylem olması gerektiğini dikte varsa (örneğin ekleme, güncelleştirme, silme), hello eylemin hello sonuçlarını dışarı aktarma olayda kaydedilir sonra gerçekleştirilen.

![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>Belirli bir kullanıcı için olayları sağlama yukarı aranıyor

Hello en yaygın kullanım için denetim günlüklerini sağlama hello bireysel bir kullanıcı hesabı durumunu sağlama toocheck hello geçerlidir. toolook hello son sağlama olayları belirli bir kullanıcı için:

1. Toohello Git **denetim günlüklerini** bölümü.

2. Merhaba gelen **kategori** menüsünde, select **hesap sağlama**.

3. Merhaba, **tarih aralığı** menüsü, toosearch, istediğiniz select hello tarih aralığı

4. Merhaba, **arama** çubuğu, hello kullanıcının toosearch için hello kullanıcı Kimliğini girin. ID değeri Hello biçimi ne olursa olsun, hello özniteliği eşleme yapılandırması (örn. userPrincipalName veya çalışan kimlik numarası) birincil eşleşen Kimliğinde hello olarak seçilen eşleşmesi gerekir. Merhaba kimliği değer gerekli hello hedeflere sütununda görünür.

5. Toosearch ENTER tuşuna basın. Merhaba olayları sağlama en son ilk döndürülür.

6. Olayları döndürülürse, hello etkinlik türleri ve olup bunlar başarılı veya başarısız unutmayın. Ardından hiç sonuç döndürmedi, hello kullanıcı yok veya henüz bir tam eşitleme henüz tamamlanmadı, sağlama işlemi hello tarafından algılanmadı demektir.

7. Olayları tek tek alınan, değerlendirilen ya da hello olay bir parçası olarak yazılan tüm kullanıcı özellikler de dahil olmak üzere, genişletilmiş tooview Ayrıntılar'ı tıklatın.


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>Denetim günlüklerini sağlama hello görüntülemek için ipuçları

Hello Azure portal'ın en iyi okunabilirlik için hello seçin **sütunları** düğmesini tıklatın ve bu sütunları seçin:

* **Tarih** -başlangıç tarihi hello olayın gerçekleştiği gösterir.
* **Hedeflere** -hello konular hello olay hello uygulama adı ve kullanıcı Kimliğini gösterir.
* **Etkinlik** -daha önce açıklandığı gibi hello etkinlik türü.
* **Durum** - hello olay veya başarılı olup olmadığını.
* **Durum Açıklaması** -olay sağlama hello ne Özet.


## <a name="troubleshooting"></a>Sorun giderme

Özet raporu ve denetim günlüklerini sağlama hello sorunları sağlama çeşitli kullanıcı hesabı sorun giderme admins yardımcı olacak önemli bir rol oynar.

Senaryo tabanlı nasıl hakkında yönergeler için tootroubleshoot otomatik kullanıcı hazırlama, bkz: [yapılandırma ve kullanıcılar tooan uygulama sağlama sorunları](active-directory-application-provisioning-content-map.md).


## <a name="additional-resources"></a>Ek Kaynaklar

* [Kullanıcı hesabı Kurumsal uygulamaları için sağlama yönetme](active-directory-enterprise-apps-manage-provisioning.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)
