---
title: "Azure Güvenlik Merkezi'nde aaaRemediate işletim sistemi güvenlik açıkları | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** düzeltmek OS güvenlik açıkları **."
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>İşletim sistemi güvenlik açıkları Azure Güvenlik Merkezi'nde Düzelt
Azure Güvenlik Merkezi çözümler günlük, sanal makine (VM) işletim sistemi (OS) yapabilir yapılandırmaları VM hello için daha savunmasız tooattack ve önerir yapılandırmasını açıklarından tooaddress değiştirir. Güvenlik Merkezi, VM işletim sistemi yapılandırması yapılandırma kuralları önerilen hello eşleşmediğinde güvenlik açıkları gidermek önerir.

> [!NOTE]
> İzlenmekte olan hello belirli yapılandırmalar hakkında daha fazla bilgi için bkz: Merhaba [önerilen yapılandırma kuralları listesi](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu belge hakkında adım adım kılavuz değildir.
>
>

1. Merhaba, **önerileri** dikey penceresinde, select **düzeltmek OS güvenlik açıkları**.
   ![İşletim sistemi güvenlik açıklarını düzeltin][1]

    Merhaba **düzeltmek OS güvenlik açıkları** dikey penceresi açılır ve yapılandırma kuralları önerilen hello eşleşmeyen işletim sistemi yapılandırmalarını ile sanal makineleri listeler.  Her bir VM hello dikey tanımlar:

   * **BAŞARISIZ kuralları** --hello VM işletim sistemi yapılandırmasını hello kuralların sayısını başarısız oldu.
   * **En son tarama zamanı** --hello tarih ve Güvenlik Merkezi hello VM'ın işletim sistemi yapılandırması son tarama zamanı.
   * **Durum** --hello hello güvenlik açığı geçerli durumu:

     * Açık: hello güvenlik açığı henüz ele alınmadı
     * Devam ediyor: hello güvenlik açığı uygulanmakta olan, sizin tarafınızdan herhangi bir eylem gerekli
     * Çözümlendi: hello güvenlik açığı zaten giderilmiş (Merhaba sorun çözüldükten sonra hello girdi gri renkte görüntülenir)
   * **Önem DERECESİ** --tüm güvenlik açıkları bir güvenlik açığının ele alınması gerekiyor ancak hemen ilgilenilmesi gerekmiyor anlamına düşük tooa önemini ayarlanır.

2. Bir VM'yi seçin. Bir dikey pencere söz konusu VM açar ve başarısız olan hello kurallarını görüntüler.
   ![Başarısız olan yapılandırma kuralları][2]

3. Bir kural seçin. Bu örnekte seçin **parola, karmaşıklık gereksinimlerini karşılamalıdır**. Açıklayan başarısız hello kuralı ve hello etkisi bir dikey pencere açılır. Merhaba ayrıntılarını gözden geçirin ve işletim sistemi yapılandırmalarının nasıl uygulanacağını göz önünde bulundurun.
  ![Merhaba başarısız kuralı için açıklama][3]

  Güvenlik Merkezi Common Configuration Enumeration (CCE) tooassign benzersiz tanımlayıcıları için yapılandırma kuralları kullanır. Aşağıdaki bilgilerle hello bu dikey pencerede sağlanır:

  - ADI--Kural adı
  - Önem DERECESİ--Kritik, önemli ya da uyarı CCE önem derecesi değeri
  - CCIED--CCE hello kuralı için benzersiz bir tanımlayıcı
  - AÇIKLAMASI--Kural açıklaması
  - Güvenlik AÇIĞI - Açıklama güvenlik açığı veya kural uygulanmamış durumunda riski
  - ETKİSİ--kuralı uygulandığında iş etkisi
  - BEKLENEN değer--Güvenlik Merkezi hello kural karşı VM OS yapılandırmanızı inceler, beklenen değer
  - Kural işlemi--VM OS yapılandırmanızın hello kural karşı Çözümleme sırasında Güvenlik Merkezi tarafından kullanılan kuralı işlemi
  - Gerçek değer--VM OS yapılandırmanızı hello kural karşı analizini sonra değer döndürdü.
  - Değerlendirme sonucu –-analiz sonucu: geçirmek, başarısız

## <a name="see-also"></a>Ayrıca bkz.
Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "Düzelt işletim sistemi güvenlik açıkları." gösterdi. Yapılandırma kuralları hello kümesi gözden geçirebilirsiniz [burada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Güvenlik Merkezi CCE (ortak yapılandırma sıralaması) tooassign benzersiz tanımlayıcıları için yapılandırma kuralları kullanır. Merhaba ziyaret [CCE](https://nvd.nist.gov/cce/index.cfm) daha fazla bilgi için site.

Güvenlik Merkezi hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın:

* [Azure Güvenlik Merkezi'nde desteklenen platformlar](security-center-os-coverage.md) -desteklenen Windows ve Linux VM'ler listesini sağlar.
* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) -önerilerin Azure kaynaklarınızı korumanıza nasıl yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) -nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) -öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) -nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) -Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
