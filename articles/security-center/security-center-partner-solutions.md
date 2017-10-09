---
title: "Azure Güvenlik Merkezi'nde aaaManaging iş ortağı çözümleri | Microsoft Docs"
description: "Bu belge, Azure Güvenlik Merkezi, Azure aboneliğinizle tümleşik iş ortağı Çözümlerinizin bir bakışta hello sistem durumunu izleyiciyi nasıl sağlar açıklanmaktadır."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme
Bu belge nasıl toomonitor hello Azure Güvenlik Merkezi'nde iş ortağı çözümlerinizin sistem durumunu size yol göstermektedir.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar. Bu belge hakkında adım adım kılavuz değildir.
>
>

## <a name="monitoring-partner-solutions"></a>İş ortağı çözümlerini izleme
Merhaba **iş ortağı çözümleri** döşeme hello üzerinde **Güvenlik Merkezi** adresindeki Azure aboneliğinizle tümleşik iş ortağı Çözümlerinizin bir bakışta hello sistem durumunu izleme dikey sağlar.

![İş ortağı çözümleri kutucuğu][1]

Merhaba **iş ortağı çözümleri** kutucuğu aboneliğinizle tümleşik iş ortağı çözümleri hello sayısını görüntüler. Tümleşik çözüm yoksa, hello döşeme hello sıfır görüntüler.

tooview hello iş ortağı çözümlerinizin sistem durumu:

1. Select hello **iş ortağı çözümleri** döşeme. Merhaba **iş ortağı çözümleri** tooSecurity Center bağlı iş ortağı çözümlerinizin listesini görüntüleyen dikey penceresi açılır.

   ![İş ortağı çözümleri][3]

   iş ortağı çözümü Hello durumu aşağıdakilerden biri olabilir:

   * Korumalı (yeşil) - sistem durumuyla ilgili bir sorun yok.
   * Sağlıksız (kırmızı) - sistem durumunda hemen ilgilenilmesi gereken bir sorun var.
   * Durdurulan Raporlama (turuncu) - hello çözüm, sistem durumunu raporlamayı durdurdu.
   * Bilinmeyen koruma durumu (turuncu) - hello çözüm hello durumunu yeni bir kaynak toohello varolan çözüm ekleme işlemi başarısız tooa nedeniyle şu anda bilinmiyor.
   * (Gri) - bildirmemiş hello çözüm değil bildirdi herhangi bir şey henüz yakın zamanda bağlanmış ve hala çözümün durumu bildirilmeyebilir.

2. İş ortağı çözümü seçin. Bu örnekte, select hello sağlar **Qualys** çözümü.  Merhaba durumunu hello iş ortağı çözümü ve hello çözümün ilişkili kaynakları gösteren dikey pencere açılır. Seçin **çözüm konsolunu** tooopen hello iş ortağı Yönetimi deneyimini Bu çözüm için.

   ![İş ortağı çözümü ayrıntısı][4]
3. Toohello dönün **Qualys** dikey penceresinde ve select **bağlantı VM**. Merhaba **bağlantı uygulamaları** dikey pencere açılır. Burada kaynakları toohello iş ortağı çözümüne bağlayabilirsiniz.

   ![Bağlantı kaynakları toopartner çözümü][5]

## <a name="next-steps"></a>Sonraki adımlar
Bu belgede, sunulan toohello olan **iş ortağı çözümleri** döşeme Güvenlik Merkezi'nde. Güvenlik Merkezi hakkında daha fazla toolearn makaleler hello bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) — hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
