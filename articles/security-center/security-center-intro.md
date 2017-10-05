---
title: "Azure Güvenlik Merkezi'ne giriş | Microsoft Docs"
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
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a>Azure Güvenlik Merkezi'ne Giriş
Azure Güvenlik Merkezi, önemli işlevleri ve nasıl çalıştığı hakkında bilgi edinin.

> [!NOTE]
> Haziran 2017'nin ilk günlerinden itibaren Güvenlik Merkezi, veri toplamak ve depolamak için Microsoft Monitoring Agent'ı kullanacak. Daha fazla bilgi edinmek için [Azure Güvenlik Merkezi Platform Geçişi](security-center-platform-migration.md) makalesine bakın. Bu makaledeki bilgiler, Microsoft Monitoring Agent'a geçiş sonrasındaki Güvenlik Merkezi işlevselliğine yöneliktir.
>
>

## <a name="what-is-azure-security-center"></a>Azure Güvenlik Merkezi nedir?
 Güvenlik Merkezi, artırılmış görünürlük aracılığıyla tehditleri engellemenize, algılamanıza ve yanıtlamanıza, ayrıca Azure kaynaklarınızın güvenliğini denetlemenize yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

## <a name="key-capabilities"></a>Temel işlevler
 Güvenlik Merkezi, Azure'da yerleşik olan kullanımı kolay ve etkili tehdit önleme, saptama ve yanıtlama işlevlerini sunar. Temel işlevler şunlardır:

| Aşama | Özellik |
| --- | --- |
| Önleme |Azure kaynaklarınızın güvenlik durumunu izler |
| Önleme | Azure aboneliklerinize şirketinizin güvenlik gereksinimlerine, uygulama türlerini bu kullanın ve verilerinizin duyarlılığına göre ilkeleri tanımlar |
| Önleme | Gerekli denetimleri uygulama işlemi boyunca hizmet sahiplerine rehberlik etmek için ilke temelli güvenlik önerilerini kullanır |
| Önleme | Microsoft ve ortaklarından güvenlik hizmetlerini ve gereçlerini hızlı bir şekilde dağıtır |
| Algılama |Azure kaynaklarınızdan, ağdan ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden güvenlik verilerini otomatik olarak çözümleyip toplar |
| Algılama | Microsoft ürünleri'ten ve Hizmetleri, Microsoft dijital Suçlar birimi (DCU), Microsoft Güvenlik Yanıt Merkezi (MSRC) ve dış akışların kullandığı genel tehdit |
| Algılama | Machine learning ve davranış analizi dahil olmak üzere gelişmiş analizler uygular |
| Yanıtlama |Öncelikli güvenlik olayları/uyarıları sağlar |
| Yanıtlama | Saldırının kaynağı ve etkilenen kaynakları hakkında öngörüler sunar |
| Yanıtlama | Geçerli saldırıyı durdurmaya ve gelecekteki saldırıları önlenmeye yönelik yöntemler önerir |

## <a name="introductory-walkthrough"></a>Tanıtıcı kılavuz

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır. Bu belge hakkında adım adım kılavuz değildir.
>
>

 Güvenlik Merkezi'ne [Azure portalından](https://azure.microsoft.com/features/azure-portal/) erişebilirsiniz. [Portalı oturum açma](https://portal.azure.com). Ana portal menü altında kaydırın **Güvenlik Merkezi** seçeneğini veya seçin **Güvenlik Merkezi** önceden portal panosuna sabitlediğiniz döşeme.

![Azure portalında güvenlik kutucuğu][1]

Güvenlik Merkezi'nde güvenlik ilkelerini ayarlayabilir, güvenlik yapılandırmalarını izleyebilir ve güvenlik uyarıları görüntüleyebilirsiniz.

### <a name="security-policies"></a>Güvenlik ilkeleri
Şirketinizin güvenlik gereksinimlerine göre Azure aboneliklerinize için ilkeleri tanımlayabilirsiniz. Bunları kullanmakta olduğunuz uygulama türlerine veya her bir abonelikteki verilerin duyarlılığına göre de uyarlayabilirsiniz. Örneğin, geliştirme veya test etme için kullanılan kaynaklar, üretim uygulamaları için kullanılanlardan farklı güvenlik gereksinimlerine sahip olabilir. Benzer şekilde, PII gibi düzenlenen veriler içeren uygulamalar, daha yüksek bir güvenlik düzeyi gerektirebilir.

> [!NOTE]
> Güvenlik ilkesini değiştirmek için bir güvenlik yöneticisi veya aboneliğin sahibi veya katkıda olması gerekir. Rolleri hakkında daha fazla bilgi edinin ve Güvenlik Merkezi, Eylemler izin görmek için [Azure Güvenlik Merkezi'nde izinleri](security-center-permissions.md).
>
>

**Güvenlik Merkezi** dikey penceresinde, aboneliklerinizin ve kaynak gruplarınızın bir listesi için **İlke** kutucuğunu seçin.   

![Güvenlik Merkezi dikey penceresi][2]

Üzerinde **Güvenlik İlkesi** dikey penceresinde ilke ayrıntılarını görüntülemek için abonelik seçin.

**Veri toplama** bir güvenlik ilkesi için veri toplama sağlar. Etkinleştirildiğinde şunlar sağlanır:

* Sanal makineler (VM'ler), günlük tüm tarama güvenlik izleme ve öneriler için desteklenir.
* Analiz ve tehdit algılama için güvenlik olaylarının toplanması.

> [!NOTE]
> Veri toplama abonelik düzeyinde yapılandırılır.
>
>

Seçin **önleme İlkesi** açmak için **önleme İlkesi** dikey. **İçin önerileri göster** izlemek istiyorsanız ve görmek istediğiniz önerileri Abonelikteki kaynakların güvenlik gereksinimlerine bağlı olan güvenlik denetimleri seçtiğiniz sağlar.

### <a name="security-recommendations"></a>Güvenlik önerileri
 Güvenlik Merkezi, olası güvenlik açıklarını tanımlamak için Azure kaynaklarınızın güvenlik durumunu inceler. Gerekli denetimlerin yapılandırılması işlemi boyunca bir öneri listesi size rehberlik eder. Örneklere şunlar dahildir:

* Kötü amaçlı yazılımı tanımlama ve kaldırmada yardım etmesi için kötü amaçlı yazılımdan koruma yazılımı hazırlama
* Ağ güvenlik gruplarını ve kurallarını trafiği denetlemek VM'ler için yapılandırma
* Web uygulamalarınızı hedefleyen saldırılara karşı korumaya yardımcı olmak için web uygulaması güvenlik duvarı hazırlama
* Eksik sistem güncelleştirmelerini dağıtma
* Önerilen taban çizgileriyle eşleşmeyen işletim sistemi yapılandırmalarını ele alma

Öneriler listesi için **Öneriler**'e tıklayın. Ek bilgileri görüntülemek veya sorunu çözmek amacıyla eyleme geçmek için önerilere tıklayın.

![Azure Güvenlik Merkezi'nde güvenlik önerileri][5]

### <a name="security-state-of-azure-resources"></a>Azure kaynakların güvenlik durumu
**Önleme** VM'ler, web uygulamaları ve diğer kaynaklar dahil, bölümü kaynak türüne göre ortamın genel güvenlik duruşunu gösterir.   

Altında bir kaynak türü seçin **önleme** tanımlanan olası güvenlik açıkları listesi dahil olmak üzere daha fazla bilgi görüntülemek için. (**İşlem** aşağıdaki örnekte seçilir.)

![Kaynak durumu kutucuğu][6]

### <a name="security-alerts"></a>Güvenlik uyarıları
 Güvenlik Merkezi, Azure kaynaklarınızdan, ağdan ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden günlük verilerini otomatik olarak toplar, çözümler ve tümleştirir. Tehditler algılandığında bir güvenlik uyarısı oluşturulur. Örneklere şunların algılanması dahildir:

* Bilinen kötü amaçlı IP adresleri ile iletişim kuran tehlikeye atılmış VM'ler
* Windows hata raporlama kullanılarak algılanan gelişmiş kötü amaçlı yazılım
* Sanal makineleri karşı deneme yanılma saldırıları
* Tümleşik kötü amaçlı yazılımdan koruma programlarından ve güvenlik duvarlarından güvenlik uyarıları

**Güvenlik uyarıları** kutucuğuna tıkladığınızda öncelikli uyarıların bir listesi görüntülenir.

![Güvenlik uyarıları][7]

Bir uyarının seçilmesi, saldırı hakkında daha fazla bilgi ve sorunun nasıl çözüleceği hakkında öneriler gösterir.

![Güvenlik uyarısı ayrıntıları][8]

### <a name="partner-solutions"></a>İş ortağı çözümleri
**İş ortağı çözümleri** kutucuğu, Azure aboneliğinizle tümleşik iş ortağı çözümlerinizin güvenlik durumunu bir bakışta izlemenizi sağlar. Güvenlik Merkezi, çözümlerden gelen uyarıları görüntüler.

**İş ortağı çözümleri** kutucuğunu seçin. Tüm bağlı iş ortağı çözümlerinin listesini görüntüleyen bir dikey pencere açılır.

![İş ortağı çözümleri][9]

## <a name="get-started"></a>başlarken
Güvenlik Merkezi ile çalışmaya başlamak için Microsoft Azure aboneliği gerekir. Güvenlik Merkezi, Azure aboneliğiniz ile etkinleştirilir. Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.

 Güvenlik Merkezi'ne [Azure portalından](https://azure.microsoft.com/features/azure-portal/) erişebilirsiniz. Daha fazla bilgi edinmek için bkz. [portal belgeleri](https://azure.microsoft.com/documentation/services/azure-portal/).

[Azure Güvenlik Merkezi'ni kullanmaya başlama](security-center-get-started.md), Güvenlik Merkezi'nin güvenlik izleme ve ilke yönetimi bileşenlerinde size hızla rehberlik sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Bu belgede Güvenlik Merkezi, temel işlevleri ve nasıl kullanmaya başlayacağınız size tanıtıldı. Daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri yapılandırmayı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) - Azure kaynaklarınızın sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.
* [Yönetme ve Azure Güvenlik Merkezi'nde güvenlik uyarılarını yanıtlama](security-center-managing-and-responding-alerts.md) — yönetme ve güvenlik uyarılarını yanıtlama hakkında bilgi edinin.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.
- [Azure Güvenlik Merkezi veri güvenliği](security-center-data-security.md) -verilerin yönetilmesi ve diğer Güvenlik Merkezi'nde korunması nasıl öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) — en son Azure güvenlik haberlerini ve bilgilerini edinin.

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
