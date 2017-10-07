---
title: "Azure Güvenlik Merkezi'nde aaaResolve endpoint protection durumu uyarıları | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** çözmek Endpoint Protection durumu uyarıları **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde uç nokta koruma durumu uyarıları Çözümle
Azure Güvenlik Merkezi, algılanan endpoint protection durumu uyarıları gidermek önerir.  Güvenlik Merkezi, endpoint protection hatalarını ve kaç tane hataları hangi sanal makineleri (VM'ler) sahip toosee sağlar.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar. Bu, adım adım ilerleyen bir kılavuz değildir.
> 
> 

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **öneriler dikey**seçin **gidermek Endpoint Protection durumu uyarıları**.
   ![Endpoint Protection sistem durumu uyarılarını çözümleme][1]
2. Bu hello dikey pencere açılır **Endpoint Protection hata** listelerinin VM'ler hataları ve hello sayısı için her bir VM. Bir VM hello listeden seçin.
   ![Uç nokta koruma hatası][2]
3. A **hataları listesi** hello hatalarının listesini görüntüleyen VM, seçilen için dikey pencere açılır. Bir hata hello listesi toolearn daha fazla seçin. Bu, seçilen hello hata hakkında bilgi içeren bir dikey pencere açılır.
   ![Hataları listesi][3]
   ![hatası olayı][4]

## <a name="see-also"></a>Ayrıca bkz.
Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md)--öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md)--nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md)--öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/)--hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
