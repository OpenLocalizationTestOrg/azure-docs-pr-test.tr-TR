---
title: "aaaOperations Yönetim Paketi güvenlik ve denetim çözüm veri güvenliği | Microsoft Docs"
description: "Bu belgede verilerin Operations Management Suite Güvenlik ve Denetim Çözümünde nasıl yönetildiği ve korunduğu açıklanmaktadır."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Operations Management Suite Güvenlik ve Denetim çözümü veri güvenliği
toohelp müşteriler engellemenize, algılamanıza ve toothreats, yanıt [Operations Management Suite (OMS) güvenlik ve denetim çözümü](operations-management-suite-overview.md) içeren veri kaynaklarınızı ilgili işler ve toplar:

* Güvenlik olay günlüğü
* Windows için Olay İzleme (ETW) olayları
* AppLocker denetim olayları
* Windows Güvenlik Duvarı günlüğü
* Gelişmiş Threat Analytics olayları
* Temel değerlendirmesinin sonuçları
* Kötü amaçlı yazılımdan koruma değerlendirmesinin sonuçları
* Güncelleştirme/düzeltme eki değerlendirmesinin sonuçları
* Merhaba aracısında açıkça etkin Syslog modüllerini akışlar

Önemli taahhütlerde tooprotect hello gizlilik ve bu verilerin güvenliğini vermiyoruz. Microsoft aynılarını toostrict uyumluluk ve güvenlik yönergelerine — toooperating hizmet kodlama gelen.
Bu makalede, OMS Güvenlik ve Denetim Çözümü'nde verilerin nasıl yönetildiği ve korunduğu açıklanmaktadır.

## <a name="data-sources"></a>Veri kaynakları
OMS güvenlik ve denetim çözüm hello OMS Aracısı yüklendiği, sanal makineleri ve fiziksel bilgisayarların verilerini analiz eder. OMS Güvenlik ve Denetim Çözümü; Windows olayı, denetim günlükleri, IIS günlükleri ve syslog iletileri gibi güvenlik olayları hakkında yapılandırma bilgilerini toplayabilir. Bu verilere örnek olarak işletim sistemi türü ve sürümü, devam eden işlemler, makine adı, IP adresleri, oturum açmış kullanıcı ve kiracı kimliği verilebilir.  

## <a name="data-protection"></a>Veri koruma
**Veriler arasında ayrım yapma**: veri hello hizmet boyunca her bir bileşende baz mantıksal olarak ayrı tutulur. Tüm veriler kuruluşa göre etiketlenir. Bu etiketleme hello veri yaşam döngüsü boyunca devam ederse ve her hello hizmet katmanında uygulanır. 

**Veri erişimi**: tooprovide güvenlik önerileri ve olası güvenlik tehditlerini araştırmak, Microsoft personeli, toplanan veya hizmetleri tarafından analiz bilgiler erişebilir. Biz toohello uyması [Microsoft çevrimiçi Hizmet Koşulları'nı](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) ve [gizlilik bildirimi](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), Microsoft olmayan müşteri verilerini veya kullanacağınız bilgileri, gelen tüm tanıtım veya benzer olduğunu belirtin Ticari amaçlarla. tooprovide güvenlik önerileri ve olası güvenlik tehditlerini araştırmak, Microsoft personeli, toplanan veya hizmetleri tarafından analiz bilgiler erişebilir. Yalnızca müşteri verileri, Azure ile bu hizmetleri sağlamayla uyumlu amaçlar da dahil olmak üzere Hizmetleri gerekli tooprovide olarak kullanırız. Tüm hakları tooyour kendi verileri korur.

**Veri kullanımı**: Microsoft desenleri kullanır ve tehdit bilgileri birden çok görülen kiracılar tooenhance bizim önleme ve algılama yeteneklerini; biz açıklanan hello gizlilik taahhütlerine uygun olarak bunu bizim [gizlilik Deyimi](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

> [!NOTE]
> Veri konumu hello ilk OMS güvenlik ve denetim yapılandırma işleminin bir parçası olan hello çalışma alanı oluşturma sırasında hello OMS çalışma düzeyinde yapılandırılır.
> 
> 

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, OMS'de verilerin nasıl yönetileceğine ve korunacağına ilişkin bilgi edindiniz. OMS güvenlik ve denetim çözümü hakkında daha fazla toolearn bakın:

* [Operations Management Suite'e (OMS) genel bakış](operations-management-suite-overview.md)
* [İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](oms-security-responding-alerts.md)
* [Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme](oms-security-monitoring-resources.md)

