---
title: "aaaIntroduction tooAzure Güvenlik Merkezi | Microsoft Docs"
description: "Azure Güvenlik Merkezi, önemli işlevleri ve nasıl çalıştığı hakkında bilgi edinin."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>Giriş tooAzure Güvenlik Merkezi
Azure Güvenlik Merkezi, önemli işlevleri ve nasıl çalıştığı hakkında bilgi edinin.

> [!NOTE]
> İçinde erken Haziran 2017'den itibaren Güvenlik Merkezi hello Microsoft İzleme Aracısı toocollect kullanmak ve verileri depolamak. Bkz: [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md) toolearn daha fazla. Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>
>

## <a name="what-is-azure-security-center"></a>Azure Güvenlik Merkezi nedir?
 Güvenlik Merkezi engellemek, algılamanıza ve Artırılmış görünürlük aracılığıyla toothreats hello Azure kaynaklarınızın güvenliğini denetlemenize yanıtlamanıza yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

## <a name="key-capabilities"></a>Temel işlevler
 Güvenlik Merkezi, kullanımı kolay ve etkili tehdit tooAzure içinde yerleşik olan önleme, saptama ve yanıt özellikleri sağlar. Temel işlevler şunlardır:

| Aşama | Özellik |
| --- | --- |
| Önleme |İzleyiciler, ayrıca Azure kaynaklarınızın güvenlik durumunu hello |
| Önleme | Şirketinizin güvenlik gereksinimlerine, hello tür kullanın ve verilerinizin duyarlılığına hello uygulamaları, Azure aboneliklerinize için ilkeler tanımlar |
| Önleme | İlke temelli kullandığı güvenlik önerileri tooguide hizmet sahiplerini hello süreci uygulama gerekli denetimleri |
| Önleme | Microsoft ve ortaklarından güvenlik hizmetlerini ve gereçlerini hızlı bir şekilde dağıtır |
| Algılama |Azure kaynaklarını, hello ağ ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden güvenlik verilerini analiz eder ve otomatik olarak toplar |
| Algılama | Microsoft ürünleri ve Hizmetleri, Microsoft dijital Suçlar birimi (DCU), hello hello Microsoft Güvenlik Yanıt Merkezi (MSRC)'ten ve dış akışların kullandığı genel tehdit |
| Algılama | Machine learning ve davranış analizi dahil olmak üzere gelişmiş analizler uygular |
| Yanıtlama |Öncelikli güvenlik olayları/uyarıları sağlar |
| Yanıtlama | Merhaba kaynağı hello saldırı ve etkilenen kaynakları Öngörüler sunar |
| Yanıtlama | Toostop geçerli saldırıyı hello ve gelecekteki saldırıların önlenmesine yardımcı yöntemler önerir |

## <a name="introductory-walkthrough"></a>Tanıtıcı kılavuz

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar. Bu belge hakkında adım adım kılavuz değildir.
>
>

 Merhaba Güvenlik Merkezi erişim [Azure portal](https://azure.microsoft.com/features/azure-portal/). [Toohello Portalı'nda oturum](https://portal.azure.com). Merhaba ana portal menüsünün altında toohello kaydırma **Güvenlik Merkezi** seçeneği veya select hello **Güvenlik Merkezi** toohello portalı panosunun önceden sabitlenmiş döşeme.

![Azure portalında güvenlik kutucuğu][1]

Güvenlik Merkezi'nde güvenlik ilkelerini ayarlayabilir, güvenlik yapılandırmalarını izleyebilir ve güvenlik uyarıları görüntüleyebilirsiniz.

### <a name="security-policies"></a>Güvenlik ilkeleri
Tooyour şirketinizin güvenlik gereksinimlerine göre Azure aboneliklerinize ilkeleri tanımlayabilirsiniz. Ayrıca bunları kullanmakta olduğunuz uygulama toohello tür veya hello veri toohello duyarlılığını her abonelik uyarlayabilirsiniz. Örneğin, geliştirme veya test etme için kullanılan kaynaklar, üretim uygulamaları için kullanılanlardan farklı güvenlik gereksinimlerine sahip olabilir. Benzer şekilde, PII gibi düzenlenen veriler içeren uygulamalar, daha yüksek bir güvenlik düzeyi gerektirebilir.

> [!NOTE]
> toomodify bir güvenlik ilkesi Güvenlik Yöneticisi veya hello aboneliğinin sahibi veya Katılımcısı olmanız gerekir. rolleri ve Güvenlik Merkezi, izin verilen eylemleri hakkında daha fazla toolearn bkz [Azure Güvenlik Merkezi'nde izinleri](security-center-permissions.md).
>
>

Merhaba üzerinde **Güvenlik Merkezi** dikey penceresinde, select hello **İlkesi** Abonelikleriniz ve kaynak grupları listesi için.   

![Güvenlik Merkezi dikey penceresi][2]

Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde bir abonelik tooview hello ilkesi ayrıntıları'nı seçin.

**Veri toplama** bir güvenlik ilkesi için veri toplama sağlar. Etkinleştirildiğinde şunlar sağlanır:

* Sanal makineler (VM'ler), günlük tüm tarama güvenlik izleme ve öneriler için desteklenir.
* Analiz ve tehdit algılama için güvenlik olaylarının toplanması.

> [!NOTE]
> Veri toplama hello abonelik düzeyinde yapılandırılır.
>
>

Seçin **önleme İlkesi** tooopen hello **önleme İlkesi** dikey. **İçin önerileri göster** hello kaynakları hello abonelik içindeki hello güvenlik gereksinimlerine göre toosee istediğiniz toomonitor ve hello önerileri istediğiniz hello güvenlik denetimlerini seçmenize olanak sağlar.

### <a name="security-recommendations"></a>Güvenlik önerileri
 Güvenlik Merkezi, Azure kaynaklarını tooidentify olası güvenlik açıklarını hello güvenlik durumunu çözümler. Öneriler listesi gerekli denetimlerin yapılandırılması hello işleminde size rehberlik eder. Örneklere şunlar dahildir:

* Kötü amaçlı yazılımdan koruma sağlama toohelp tanımlamak ve kötü amaçlı yazılım kaldırma
* Ağ güvenlik gruplarını ve kurallarını toocontrol trafiği tooVMs yapılandırma
* Web uygulaması güvenlik duvarı toohelp, web uygulamalarınızı hedefleyen saldırılara karşı korumaya sağlama
* Eksik sistem güncelleştirmelerini dağıtma
* Önerilen taban çizgileri hello eşleşmeyen işletim sistemi yapılandırmalarını ele alma

Merhaba tıklatın **önerileri** için öneriler listesi. Her öneri tooview ek bilgiler veya tootake eylem tooresolve hello Çıkış'ı tıklatın.

![Azure Güvenlik Merkezi'nde güvenlik önerileri][5]

### <a name="security-state-of-azure-resources"></a>Azure kaynakların güvenlik durumu
Merhaba **önleme** başlangıç Panosu bölümü hello VM'ler, web uygulamaları ve diğer kaynakları da dahil olmak üzere kaynak türüne göre hello ortamın genel güvenlik duruşunu gösterir.   

Altında bir kaynak türü seçin **önleme** tooview tanımlanan olası güvenlik açıkları listesi dahil olmak üzere daha fazla bilgi. (**İşlem** hello aşağıdaki örnekte seçilir.)

![Kaynak durumu kutucuğu][6]

### <a name="security-alerts"></a>Güvenlik uyarıları
 Güvenlik Merkezi otomatik olarak toplar, analiz eder ve Azure kaynakları, hello ağ ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden günlük verilerini tümleştirir. Tehditler algılandığında bir güvenlik uyarısı oluşturulur. Örneklere şunların algılanması dahildir:

* Bilinen kötü amaçlı IP adresleri ile iletişim kuran tehlikeye atılmış VM'ler
* Windows hata raporlama kullanılarak algılanan gelişmiş kötü amaçlı yazılım
* Sanal makineleri karşı deneme yanılma saldırıları
* Tümleşik kötü amaçlı yazılımdan koruma programlarından ve güvenlik duvarlarından güvenlik uyarıları

Tıklatmak hello **güvenlik uyarıları** döşeme öncelikli uyarıların bir listesini görüntüler.

![Güvenlik uyarıları][7]

Bir uyarıyı seçtiğinizde gösterilir hello saldırı ve ilgili öneriler hakkında daha fazla bilgi tooremediate onu.

![Güvenlik uyarısı ayrıntıları][8]

### <a name="partner-solutions"></a>İş ortağı çözümleri
Merhaba **iş ortağı çözümleri** Azure aboneliğinizle tümleşik iş ortağı çözümlerinizin bakışta hello güvenlik durumunu izleme kutucuğu sağlar. Güvenlik Merkezi hello çözümlerden gelen uyarıları görüntüler.

Select hello **iş ortağı çözümleri** döşeme. Tüm bağlı iş ortağı çözümlerinin listesini görüntüleyen bir dikey pencere açılır.

![İş ortağı çözümleri][9]

## <a name="get-started"></a>başlarken
Güvenlik Merkezi ile çalışmaya tooget abonelik tooMicrosoft Azure gerekir. Güvenlik Merkezi, Azure aboneliğiniz ile etkinleştirilir. Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.

 Merhaba Güvenlik Merkezi erişim [Azure portal](https://azure.microsoft.com/features/azure-portal/). Merhaba bkz [portal belgeleri](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn daha fazla.

[Azure Güvenlik Merkezi ile çalışmaya başlama](security-center-get-started.md) hızlı bir şekilde hello güvenlik izleme ve ilke yönetimi bileşenleri Güvenlik Merkezi sırasında size kılavuzluk eder.

## <a name="next-steps"></a>Sonraki adımlar
Bu belgede, sunulan tooSecurity Merkezi, önemli işlevleri ve nasıl tooget başlatılacağını yoktu. toolearn daha kaynakları aşağıdaki hello bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
- [Azure Güvenlik Merkezi veri güvenliği](security-center-data-security.md) -verilerin yönetilmesi ve diğer Güvenlik Merkezi'nde korunması nasıl öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) — hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
