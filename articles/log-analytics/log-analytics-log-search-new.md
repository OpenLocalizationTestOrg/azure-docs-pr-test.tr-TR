---
title: "Günlük analizi OMS aramalarda aaaLog | Microsoft Docs"
description: "Günlük analizi tüm veriler bir günlük arama tooretrieve gerektirir.  Bu makalede aramaları günlük analizi kullanılan nasıl yeni bir günlük açıklar ve bir oluşturmadan önce toounderstand gereken kavramlar sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Günlük analizi günlük aramalarda anlama

> [!NOTE]
> Bu makalede Azure günlük analizi hello yeni sorgu dili kullanarak günlük aramalarda açıklanmaktadır.  Merhaba yeni dil hakkında daha fazla bilgi ve çalışma alanı hello yordamı tooupgrade almak [Azure günlük analizi çalışma alanı toonew günlük aramanızı yükseltme](log-analytics-log-search-upgrade.md).  
>
> Çalışma alanınızı yükseltilmiş toohello yeni sorgu dili bırakılmamışsa, çok başvurmalıdır[Bul günlük aramaları günlük analizi kullanarak verileri](log-analytics-log-searches.md).

Günlük analizi tüm veriler bir günlük arama tooretrieve gerektirir.  Merhaba Portalı'nda verileri analiz etme olup olmadığını bir uyarı kuralı toobe yapılandırma bildirim bir belirli bir koşula veya hello günlük analizi API kullanarak alınırken verileri istediğiniz bir günlük arama toospecify hello verilerini kullanır.  Bu makalede, günlük aramaları günlük analizi nasıl kullanıldığını açıklar ve bir oluşturmadan önce anlamanız gereken kavramlar sağlar. Merhaba bkz [sonraki adımlar](#next-steps) bölüm oluşturma ve günlük aramaları düzenleme hakkında bilgi ve başvurular hello sorgu dili.

## <a name="where-log-searches-are-used"></a>Günlük aramaları kullanıldığı

Günlük analizi günlük aramaları kullanacağını hello farklı şekilde hello şunları içerir:

- **Portalları.** Etkileşimli veri analizi hello deposundaki hello ile gerçekleştirebileceğiniz [günlük arama portal](log-analytics-log-search-log-search-portal.md) veya hello [Advanced Analytics portalı](https://go.microsoft.com/fwlink/?linkid=856587).  Bu tooedit sağlar, sorgu ve biçimleri ve görselleştirmeleri çeşitli hello sonuçlarını çözümleyin.  Oluşturduğunuz sorguların çoğu hello portalları birinde başlar ve beklendiği gibi çalıştığını doğrulamak sonra sonra kopyalanır.
- **Uyarı kuralları.** [Uyarı kuralları](log-analytics-alerts.md) proaktif olarak çalışma alanınızdaki verilerden sorunları belirlemek.  Her uyarı kuralı düzenli aralıklarla otomatik olarak çalışacak bir günlük arama temel alır.  bir uyarı oluşturuluyorsa hello sonuçlar incelenen toodetermine olur.
- **Görünümler.**  Kullanıcı panolarla dahil veri toobe görselleştirmeleri oluşturabilirsiniz [Görünüm Tasarımcısı](log-analytics-view-designer.md).  Günlük aramaları sağlayan tarafından kullanılan hello veri [kutucukları](log-analytics-view-designer-tiles.md) ve [görselleştirme bölümleri](log-analytics-view-designer-parts.md) her görünümünde.  Aşağı görselleştirme parçalarını hello günlük arama portal tooperform çözümlemeler hello verileri ayrıntılarına geçebilir.
- **Dışarı aktarın.**  Merhaba günlük analizi çalışma alanı tooExcel veri aktardığınızda veya [Power BI](log-analytics-powerbi.md), bir günlük arama toodefine hello veri tooexport oluşturun.
- **PowerShell.** Bir komut satırı veya kullanan bir Azure Otomasyonu runbook'u bir PowerShell betiğini çalıştırabilirsiniz [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) günlük analizi tooretrieve verileri.  Bu cmdlet, bir sorgu toodetermine hello veri tooretrieve gerektiriyor.
- **Günlük analizi API.**  Merhaba [günlük analizi oturum arama API](log-analytics-log-search-api.md) herhangi bir REST API istemcisi tooretrieve veri hello çalışma alanından izin verir.  Merhaba API isteği günlük analizi toodetermine hello veri tooretrieve karşı çalıştırmak bir sorgu içerir.

![Günlük aramalar](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Günlük analizi veri nasıl düzenlenir
Bir sorgu oluşturma sırasında hangi tabloları aradığınız hello verilere sahip belirleyerek başlayın. Her [veri kaynağı](log-analytics-data-sources.md) ve [çözüm](../operations-management-suite/operations-management-suite-solutions.md) hello günlük analizi çalışma alanındaki özel tablolardaki verileri depolar.  Her veri kaynağı ve çözüm için belgeleri oluşturduğu hello veri türü hello adını ve açıklamasını her özelliklerini içerir.     Birçok sorgular yalnızca tek bir tablodan veri gerektirir, ancak diğer çok çeşitli seçenekler tooinclude verileri birden çok tablodan kullanabilir.

![Tablolar](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Sorgu yazma
Günlük analizi aramalarda günlük Hello özünde olan [kapsamlı sorgu dili](https://docs.loganalytics.io/) olanak tanıyan almak ve verilerini çeşitli şekillerde hello depodan çözümleme.  Bu aynı sorgu dili için kullanılan [Application Insights](../application-insights/app-insights-analytics.md).  Toowrite bir sorgu kritik toocreating günlük günlük analizi aramalarda nasıl yapıldığını öğrenme.  Temel sorguları genellikle başlayacaksınız ve gereksinimlerinizi daha karmaşık hale geldikçe sonra ilerleme toouse daha işlevleri Gelişmiş.

bir sorguyu temel yapısını Hello işleçleri dikey çizgi karakteriyle ayrılmış bir dizi arkasından bir kaynak tablo olduğu `|`.  Birden çok işleçleri toorefine hello veri zincir ve gelişmiş işlevleri gerçekleştirebilirsiniz.

Örneğin, size toofind hello üst on bilgisayarlarla hello çoğu hata olayları hello geçen gün istediğinizi varsayın.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

Veya bir sinyal hello son günü sahip olmasanız toofind bilgisayarların istediğiniz olabilir.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

Ne dersiniz hello işlemci kullanımı son haftadan her bir bilgisayar ile çizgi grafiği?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

Merhaba, birlikte çalıştığınız verilerin hello türü ne olursa olsun bu hızlı örneklerinden hello sorgu yapısını benzer olduğunu görebilirsiniz.  Bunu burada hello elde edilen bir komut verilerden hello ardışık düzen toohello sonraki komutu üzerinden gönderilir ayrı adımlara ayırabilirsiniz.

Merhaba öğreticiler ve dil başvurusu dahil olmak üzere hello Azure günlük analizi sorgu dili hakkında tam belgelerine bakın [Azure günlük analizi sorgu dili belgelerini](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba hakkında bilgi edinin [toocreate kullanın ve günlük aramaları düzenleme portalı](log-analytics-log-search-portals.md).
- Kullanıma bir [sorgu yazmakla ilgili öğretici](https://go.microsoft.com/fwlink/?linkid=856078) hello yeni sorgu dilini kullanma.
