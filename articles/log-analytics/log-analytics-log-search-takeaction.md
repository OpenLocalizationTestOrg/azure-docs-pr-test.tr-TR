---
title: "aaaUser başlatılan Azure Otomasyonu Runbook eylemini günlük analizi | Microsoft Docs"
description: "Bu makalede nasıl toorun günlük analizi Otomasyon runbook'tan arama sonucu isteğe bağlı açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Günlük analizi günlük arama sonucu Otomasyon Runbook'tan eylemiyle alın

Azure günlük analizi'da bir günlük Arama sonuçlarından şimdi seçebileceğiniz **ele eylem** toorun bir Otomasyon runbook'u.  Merhaba runbook kullanılabilir tooremediate hello sorunu veya sorun giderme bilgileri toplama gibi diğer bazı işlemler yapması, bir e-posta göndermek veya bir hizmet isteği oluşturun. 

## <a name="components-and-features-used"></a>Kullanılan bileşenler ve özellikler
* [Azure Otomasyon hesabı](../automation/automation-offering-get-started.md)
* [Günlük analizi çalışma alanı](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>Günlük arama tooinitiate runbook'tan

bir olayı ve Başlat günlük arama sonuçlarınızı runbook'tan tootake eylem, bir günlük arama oluşturarak başlayın ve hello sonuçlarından bir runbook isteğe bağlı çağırabilirsiniz.  Merhaba günlük arama özelliğini hello Azure'nın bu elde edilebilir veya [OMS portalı](../log-analytics/log-analytics-log-searches.md).  Bu örnekte, hello Azure portalı, bu özelliğin temel Tanıtımı ile gelen bir günlük arama yapın.

1. Merhaba Hub menüsünde Hello Azure portal, **daha fazla hizmet** seçip **günlük analizi**.  
2. Merhaba günlük analizi dikey penceresinde, günlük analizi çalışma alanınız seçip hello çalışma dikey penceresinde **günlük arama**.  
3. Merhaba günlük arama dikey penceresinde, günlük arama yapın.  
4. Merhaba günlük Arama sonuçlarından hello elips toohello sol bir hello alanlarının ve hello açılan, select tıklatın **ele eylem**.<br><br> ![Arama sonuçlarından gerçekleştirmesi eylemi seçin](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. Merhaba Al eylem dikey penceresinden seçin **bir Runbook'a**ve hello **bir runbook'u çalıştırmak** dikey runbook toorun seçebilirsiniz.  Herhangi bir runbook hello bağlantılı toohello günlük analizi çalışma alanı olan Otomasyon hesabı seçebilirsiniz.  Merhaba aşağıdakileri göz önünde bulundurun:

    * Runbook'ları etiketlere göre düzenlenir
    * Runbook giriş parametresi değerleri doğrudan hello alanlardan hello arama sonucunun seçilebilir.  Aşağı açılan listesi tüm hello kullanılabilir alanlardan hello sonuç tooselect görüntüleme görünür.  
    * Toorun hello runbook seçebileceğiniz bir [karma runbook çalışanı](../automation/automation-hybrid-runbook-worker.md) bu makinenin bir üye olarak yalnızca içeren karşılık gelen bir karma Runbook çalışanı grubunu varsa hello sorun var. hello makinede yüklü.  Merhaba karma çalışanı grubu Hello adını hello hello günlük arama sonucunda hello bilgisayar adını eşleşirse, hello Grup otomatik olarak seçilir.    

6. Tıklattıktan sonra **çalıştırmak**, tooallow hello runbook iş dikey penceresi, tooreview hello hello işinin durumu.   

Yapılandırılmış toobe olan bir runbook seçerseniz [adlı günlük analizi uyarıdan](../automation/automation-invoke-runbook-from-omsla-alert.md), adlı bir giriş parametresi var. **WebhookData** diğer bir deyişle **nesne** türü.  Merhaba giriş parametre zorunluysa, runbook etkinlikleri başvurur belirli öğeler hakkında toofilter sağlayan bir nesne türü, hello JSON biçimli dize dönüştürebilir şekilde toopass hello arama sonuçları toohello runbook gerekir.  Seçerek bunu **arama sonucu (nesne)** hello aşağı açılan listeden.<br><br> ![Runbook parametresi için Web kancası veri nesnesi seçin](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Sonraki adımlar

* Gözden geçirme hello [günlük analizi oturum Arama başvurusu](log-analytics-search-reference.md) tooview tüm hello arama alanları ve modelleri günlük analizi içinde kullanılabilir.
* nasıl tooinvoke bir Otomasyon runbook'u otomatik olarak gözden toolearn [bir OMS günlük analizi uyarıdan bir Azure Otomasyonu runbook çağırma](../automation/automation-invoke-runbook-from-omsla-alert.md).  
