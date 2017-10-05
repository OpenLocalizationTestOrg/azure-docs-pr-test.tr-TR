---
title: "Azure Güvenlik Merkezi güvenlik açıkları OS düzeltme | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** düzeltmek OS güvenlik açıkları **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>İşletim sistemi güvenlik açıkları Azure Güvenlik Merkezi'nde Düzelt
Azure Güvenlik Merkezi günlük VM saldırı karşısında daha savunmasız hale getirebilecek ve bu güvenlik açıklarına değinen yapılandırma değişiklikleri önerir yapılandırmalar için sanal makine (VM) işletim sistemi (OS) çözümler. Güvenlik Merkezi, VM işletim sistemi yapılandırması önerilen yapılandırma kuralları eşleşmediğinde güvenlik açıkları gidermek önerir.

> [!NOTE]
> İzlenmekte olan belirli yapılandırmalar hakkında daha fazla bilgi için bkz: [önerilen yapılandırma kuralları listesi](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-the-recommendation"></a>Öneriyi uygulamayı

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.  Bu belge hakkında adım adım kılavuz değildir.
>
>

1. İçinde **önerileri** dikey penceresinde, select **düzeltmek OS güvenlik açıkları**.
   ![İşletim sistemi güvenlik açıklarını düzeltin][1]

    **Düzeltmek OS güvenlik açıkları** dikey penceresi açılır ve Vm'lerinizi önerilen yapılandırma kuralları eşleşmeyen işletim sistemi yapılandırmalarını ile listeler.  Her bir VM dikey tanımlar:

   * **BAŞARISIZ kuralları** --VM işletim sistemi yapılandırmasını başarısız kuralları sayısı.
   * **En son tarama zamanı** --Güvenlik Merkezi VM işletim sistemi yapılandırmasını son tarama saati ve tarihi.
   * **Durum** --güvenlik açığı geçerli durumu:

     * Açık: Güvenlik açığı henüz ele alınmadı
     * Devam ediyor: Güvenlik açığı uygulanmakta olan, sizin tarafınızdan herhangi bir eylem gerekli
     * Çözüm: Bu güvenlik açığı zaten giderilmiş (sorun çözüldükten sonra girdi gri renkte görüntülenir)
   * **Önem DERECESİ** --tüm güvenlik açıkları bir güvenlik açığının ele alınması gerekiyor ancak hemen ilgilenilmesi gerekmiyor anlamı bir düşük önem derecesi için ayarlanır.

2. Bir VM'yi seçin. Bu VM için bir dikey pencere açar ve başarısız olan kuralları görüntüler.
   ![Başarısız olan yapılandırma kuralları][2]

3. Bir kural seçin. Bu örnekte seçin **parola, karmaşıklık gereksinimlerini karşılamalıdır**. Başarısız kuralı ve etkisi açıklayan bir dikey pencere açılır. Ayrıntıları gözden geçirin ve işletim sistemi yapılandırmalarının nasıl uygulanacağını göz önünde bulundurun.
  ![Başarısız kuralı için açıklama][3]

  Güvenlik Merkezi, yapılandırma kuralları için benzersiz tanımlayıcı atamak için Common Configuration Enumeration (CCE) kullanır. Aşağıdaki bilgiler bu dikey pencerede sağlanır:

  - ADI--Kural adı
  - Önem DERECESİ--Kritik, önemli ya da uyarı CCE önem derecesi değeri
  - CCIED--CCE kuralı için benzersiz bir tanımlayıcı
  - AÇIKLAMASI--Kural açıklaması
  - Güvenlik AÇIĞI - Açıklama güvenlik açığı veya kural uygulanmamış durumunda riski
  - ETKİSİ--kuralı uygulandığında iş etkisi
  - BEKLENEN değer--Güvenlik Merkezi kural karşı VM OS yapılandırmanızı inceler, beklenen değer
  - Kural işlemi--VM OS yapılandırmanızın kural karşı Çözümleme sırasında Güvenlik Merkezi tarafından kullanılan kuralı işlemi
  - Gerçek değer--VM OS yapılandırmanızı kural karşı analizini sonra değer döndürdü.
  - Değerlendirme sonucu –-analiz sonucu: geçirmek, başarısız

## <a name="see-also"></a>Ayrıca bkz.
Bu makalede "Düzelt işletim sistemi güvenlik açıkları." Güvenlik Merkezi öneriyi uygulamayı nasıl oluşturulacağını gösterir Yapılandırma kuralları gözden geçirebilirsiniz [burada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Güvenlik Merkezi, yapılandırma kuralları için benzersiz tanımlayıcı atamak için CCE (ortak yapılandırma sıralaması) kullanır. Ziyaret [CCE](https://nvd.nist.gov/cce/index.cfm) daha fazla bilgi için site.

Güvenlik Merkezi hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [Azure Güvenlik Merkezi'nde desteklenen platformlar](security-center-os-coverage.md) -desteklenen Windows ve Linux VM'ler listesini sağlar.
* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri yapılandırmayı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) -önerilerin Azure kaynaklarınızı korumanıza nasıl yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) -Azure kaynaklarınızın sistem durumunu izlemek öğrenin.
* [Yönetme ve Azure Güvenlik Merkezi'nde güvenlik uyarılarını yanıtlama](security-center-managing-and-responding-alerts.md) -yönetme ve güvenlik uyarılarını yanıtlama hakkında bilgi edinin.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) -iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) -Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
