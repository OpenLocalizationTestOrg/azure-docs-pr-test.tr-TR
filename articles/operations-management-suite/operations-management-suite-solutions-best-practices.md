---
title: "aaaOMSManagement çözüm en iyi uygulamalar | Microsoft Docs"
description: 
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>Operations Management Suite (OMS) (Önizleme) yönetim çözümleri oluşturmak için en iyi uygulamalar
> [!NOTE]
> Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir. Aşağıda açıklanan herhangi bir şema konu toochange ' dir.  

Bu makale için en iyi yöntemler sağlar [bir yönetim çözümü dosyası oluşturma](operations-management-suite-solutions-solution-file.md) Operations Management Suite (OMS).  Diğer en iyi yöntemleri tanımlandığı gibi bu bilgileri güncelleştirilir.

## <a name="data-sources"></a>Veri kaynakları
- Veri kaynakları olabilir [Resource Manager şablonu ile yapılandırılmış](../log-analytics/log-analytics-template-workspace-configuration.md), ancak bir çözüm dosyasında eklenmemelidir.  Merhaba neden veri kaynaklarını yapılandırma şu anda çözümünüzü hello kullanıcının çalışma alanında mevcut yapılandırmanın üzerine anlamına ıdempotent olmamasıdır.<br><br>Örneğin, çözümünüzü hello uygulama olay günlüğü uyarı ve hata olayları gerektirebilir.  Bu veri kaynağı olarak çözümünüzde belirtirseniz, hello kullanıcı bunu kendi çalışma alanında yapılandırılmış olsaydı bilgi olayları kaldırma riski oluşur.  Tüm olayları dahil edilmişse, hello kullanıcının çalışma alanındaki aşırı bilgi Olay toplama.

- Ardından, çözümünüzün hello standart veri kaynaklarından biri verilerden gerektiriyorsa, bu bir önkoşul olarak tanımlamalısınız.  Durum belgelerinde o hello müşteri hello veri kaynağı, kendi yapılandırmanız gerekir.  
- Eklemek bir [veri akışı doğrulaması](../log-analytics/log-analytics-view-designer-tiles.md) tooany görünümleri çözüm tooinstruct hello kullanıcınız veri kaynakları için gerekli verileri toobe yapılandırılmış bu gereksinimi toobe ileti toplanır.  Bu ileti hello görünüm hello parçasına görüntülenir gerekli verileri bulunamadı.


## <a name="runbooks"></a>Runbook'lar
- Ekleme bir [Otomasyonu zamanlaması](../automation/automation-schedules.md) her runbook'un çözümünüzdeki bir zamanlamaya göre toorun gerekiyor.
- Merhaba dahil [IngestionAPI Modülü](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) veri toohello günlük analizi havuzu yazma runbook'lar tarafından kullanılan, çözüm toobe içinde.  Merhaba çözümü çok yapılandırmak[başvuru](operations-management-suite-solutions-solution-file.md#solution-resource) böylece hello çözüm kaldırılırsa, BT'nin bu kaynak.  Bu, birden çok çözümleri tooshare hello modülü sağlar.
- Kullanım [Otomasyon değişkenleri](../automation/automation-schedules.md) tooprovide değerleri toohello çözüm kullanıcılar daha sonra toochange isteyebilirsiniz.  Merhaba çözüm yapılandırılmış toocontain hello değişkeni olsa bile, değeri hala değiştirilebilir.

## <a name="views"></a>Görünümler
- Tüm çözümleri hello Kullanıcı Portalı'nda görüntülenen tek bir görünüm içermesi gerekir.  Merhaba görünümü birden çok içerebilir [görselleştirme bölümleri](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate farklı verilerini ayarlar.
- Eklemek bir [veri akışı doğrulaması](../log-analytics/log-analytics-view-designer-tiles.md) tooany görünümleri çözüm tooinstruct hello kullanıcınız veri kaynakları için gerekli verileri toobe yapılandırılmış bu gereksinimi toobe ileti toplanır.
- Merhaba çözümü çok yapılandırmak[içeren](operations-management-suite-solutions-solution-file.md#solution-resource) hello çözüm kaldırılırsa kaldırılmadan böylece hello görünümü.

## <a name="alerts"></a>Uyarılar
- Merhaba çözüm yüklediğinizde hello kullanıcı bunları tanımlayabilirsiniz şekilde hello alıcılar listesi hello çözüm dosyasına bir parametre olarak tanımlayın.
- Merhaba çözümü çok yapılandırmak[başvuru](operations-management-suite-solutions-solution-file.md#solution-resource) uyarı kuralları bu kullanıcının kendi yapılandırmasını değiştirebilirsiniz.  Merhaba alıcı listesini değiştirerek, hello hello uyarı eşiğinin değiştirilmesi veya hello uyarı kuralı devre dışı bırakma gibi toomake değişiklikler istedikleri. 


## <a name="next-steps"></a>Sonraki adımlar
* Hello basic işleminde size kılavuzluk [tasarlama ve bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md).
* Nasıl çok öğrenin[bir çözüm dosyası oluşturma](operations-management-suite-solutions-solution-file.md).
* [Kaydedilmiş aramaları ve Uyarıları Ekle](operations-management-suite-solutions-resources-searches-alerts.md) tooyour yönetim çözümü.
* [Görünümler ekleme](operations-management-suite-solutions-resources-views.md) tooyour yönetim çözümü.
* [Otomasyon runbook'ları ve diğer kaynakları eklemek](operations-management-suite-solutions-resources-automation.md) tooyour yönetim çözümü.

