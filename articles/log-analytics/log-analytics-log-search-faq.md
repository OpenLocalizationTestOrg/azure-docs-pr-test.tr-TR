---
title: "aaaLog Analytics yeni günlük arama sık sorulan sorular | Microsoft Docs"
description: "Bu makale, günlük analizi toohello yeni sorgu dili hello yükseltme ile ilgili sık sorulan sorular sağlar."
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
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Yeni günlük analizi oturum arama SSS ve bilinen sorunlar

Bu makalede sık sorulan sorular ve hello yükseltme ile ilgili bilinen sorunları içerir [günlük analizi toohello yeni sorgu dili](log-analytics-log-search-upgrade.md).  Çalışma alanınızı hello karar tooupgrade yapmadan önce bu makalenin tümünü okumanız gerekir.


## <a name="alerts"></a>Uyarılar

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>Soru: çok sayıda uyarı kuralları sahibim. Toocreate gerekiyor mu ı yükselttikten sonra yeniden hello yeni dil bunları?  
Hayır, uyarı kurallarınızı otomatik olarak dönüştürülen toohello yeni arama dili yükseltme sırasında ' dir.  


## <a name="computer-groups"></a>Bilgisayar grupları

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>Soru: hataları toouse bilgisayar grupları çalışırken alıyorum.  Kendi sözdizimi değişti mi?
Evet, çalışma alanınızı yükseltildiğinde kullanarak bilgisayar hello söz dizimi değişiklikleri gruplandırır.  Bkz: [günlük analizi bilgisayar gruplarında oturum aramaları](log-analytics-computer-groups.md) Ayrıntılar için.

### <a name="known-issue-groups-imported-from-active-directory"></a>Bilinen sorun: Active Directory'den içe gruplar
Active Directory'den içe aktarılan bir bilgisayar grubu kullanan bir sorgu şu anda oluşturulamıyor.  Geçici bir çözüm olarak bu sorun düzeltilene kadar içeri hello Active Directory grubunu kullanarak yeni bir bilgisayar grubu oluşturun ve ardından bu yeni grubun sorgunuzda kullanın.

Bir örnek sorgu toocreate içeri aktarılan bir Active Directory grubu içeren yeni bir bilgisayar grubu aşağıdaki gibidir:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Panolar

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Soru: hala panolar yükseltilen bir çalışma alanında kullanabilir miyim?
Çok eklediğiniz tüm kutucukları toouse devam edebilmeniz için**My Pano** önce çalışma alanınızı yükseltilmişse ancak bu kutucuklar düzenleyemez veya yenilerini ekleyebilirsiniz.  Toocreate devam etmek ve görünümlerle Düzenle [Görünüm Tasarımcısı](log-analytics-view-designer.md) ve ayrıca hello Azure portal panolar oluşturabilirsiniz.


## <a name="log-searches"></a>Günlük aramalar

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>Soru: t dışında yükseltilmiş çalışma Alanım aramaları kaydettiniz. I bunları toohello yeni arama dili otomatik olarak dönüştürebilir miyim?
Merhaba dil dönüştürücü hello günlük arama sayfası tooconvert aracında her birini kullanabilirsiniz.  Merhaba çalışma yükseltme yapmadan birden çok arar yöntemi tooautomatically dönüştürme yok.

### <a name="question-why-are-my-query-results-not-sorted"></a>Soru: Neden my sorgu sonuçları sıralanır değil mi?
Sonuçları varsayılan hello yeni sorgu dili olarak sıralanmış değil.  Kullanım hello [sıralama işleci](https://go.microsoft.com/fwlink/?linkid=856079) toosort sonuçlarınızı bir veya daha fazla özelliğe göre.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Bilinen sorun: bir liste arama sonuçlarında, veri içermeyen özellikler içerebilir
Günlük arama sonuçları listesinde veri içermeyen özelliklerini görüntüleyebilir.  Önceki tooupgrade, bu özellikler dahil değildir.  Bu sorun, böylece boş özellikler görüntülenmez düzeltilecektir.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Bilinen sorun: bir grafikte bir değer seçerek ayrıntılı sonuçları görüntüler değil
Önceki tooupgrade grafikte bir değer seçildiğinde seçili hello değerle eşleşen kayıtları ayrıntılı bir listesi döndürecektir.  Yükseltmeden sonra yalnızca hello tek özetlenen satır döndürülür.  Bu sorun şu anda incelenmektedir.

## <a name="log-search-api"></a>Log Arama API’si

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>Soru: t yükselttikten sonra hello günlük arama API güncelleştirilmiş olur mu?
Merhaba [günlük arama API](log-analytics-log-search-api.md) henüz yükseltilmiş toohello yeni arama dili ayarlanmadı.  Çalışma alanınızı yükselttiğinizde toouse hello eski sorgu dili bu API ile devam edin.  Bunu güncelleştirildiğinde güncelleştirilmiş belgeler günlük arama API hello için kullanılabilir hale gelir.


## <a name="portals"></a>Portallar

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>Soru: T hello yeni Advanced Analytics portalı kullanın veya gerekir hello günlük arama portal'ı kullanmaya devam?
Merhaba iki portalları karşılaştırması görebilirsiniz [oluşturma ve Azure günlük analizi günlük sorgularda düzenleme için portalları](log-analytics-log-search-portals.md).  Gereksinimleriniz için en iyi bir hello seçebilmeniz her ayrı avantajları vardır.  Merhaba Advanced Analytics portalında ortak toowrite sorguları ve Görünüm Tasarımcısı gibi diğer yerler yapıştırın.  İlgili bilgiyi okumalısınız [tooconsider sorunları](log-analytics-log-search-portals.md#advanced-analytics-portal) yaparken.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Soru: hiçbir şey Powerbı tümleşme değişiyor mu?
Evet.  Çalışma alanınızı yükseltildikten sonra günlük analizi veri tooPower BI dışarı aktarma hello işlem artık çalışmaz.  Yükseltmeden önce oluşturulan tüm var olan zamanlamalar devre dışı bırakılacaktır.  Yükseltmeden sonra aynı platform Application Insights olarak Azure günlük analizi kullanır hello ve aynı işlemi olarak tooexport günlük analizi sorguları tooPower BI hello kullandığınız [hello işlem tooexport Application Insights sorgular tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Bilinen sorun: Power BI isteği boyut sınırı
Şu anda 8 MB dışarı aktarılan tooPower BI olabilir bir günlük analizi sorgu için bir boyut sınırı yoktur.  Bu sınır yakında artırılır.


##<a name="powershell-cmdlets"></a>PowerShell cmdlet'leri

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Soru: t yükselttikten sonra hello günlük arama PowerShell cmdlet'ini güncelleştirilmiş olur mu?
Merhaba [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) henüz yükseltilmiş toohello yeni arama dili ayarlanmadı.  Çalışma alanınızı yükselttiğinizde toouse hello eski sorgu dili, bu cmdlet'i ile devam edin.  Güncelleştirilmiş belgeleri, güncelleştirildiğinde hello cmdlet'i için kullanılabilir hale gelir.


## <a name="resource-manager-templates"></a>Resource Manager şablonları

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Soru: Resource Manager şablonu ile yükseltilen bir çalışma alanı oluşturabilirim?
Evet.  2017-03-15-Önizleme API sürümünü kullanın ve içeren bir **özellikleri** şablonunuzu aşağıdaki örneğine hello olduğu gibi bölümünde.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>Çözümler

### <a name="question-will-my-solutions-continue-toowork"></a>Soru: my çözümleri toowork devam eder?
Dönüştürülen toohello yeni sorgu dili olmaları durumunda kendi performansını artırır ancak tüm çözümleri yükseltilen bir çalışma alanında toowork devam eder.  Bu bölümde açıklanan bazı varolan çözümleri ile ilgili sorunları bilinen vardır.

### <a name="known-issue-capacity-and-performance-solution"></a>Bilinen sorun: kapasite ve performans çözümü
Bazı hello hello bölümlerinde [kapasite ve performans](log-analytics-capacity.md) görünümü boş.  Bir düzeltme toothis sorunu kısa süre içinde kullanılabilir.

### <a name="known-issue-device-health-solution"></a>Bilinen sorun: cihaz sistem durumu çözümü
Merhaba [cihaz sistem durumu çözüm](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) yükseltilmiş bir çalışma alanında veri toplamaz.  Bir düzeltme toothis sorunu kısa süre içinde kullanılabilir.

### <a name="known-issue-application-insights-connector"></a>Bilinen sorun: Application Insights Bağlayıcısı
Açılardan [uygulama Öngörüler Bağlayıcısı çözüm](log-analytics-app-insights-connector.md) yükseltilmiş bir çalışma alanında şu anda desteklenmemektedir.  Bir düzeltme toothis şu anda analysis altında bir sorundur.

## <a name="upgrade-process"></a>Yükseltme işlemi

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>Soru: birkaç çalışma alanları sahibim. Merhaba, tüm çalışma alanları yükseltebilmek için aynı anda?  
Hayır.  Yükseltme tooa tek çalışma her zaman geçerlidir. Şu anda çok sayıda çalışma alanları aynı anda yükseltme yolu yoktur. Yükseltilmiş hello çalışma alanının diğer kullanıcılar da etkileneceğini unutmayın.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Soru: t yükseltirseniz, çalışma Alanım toplanan mevcut günlük verilerini değiştirilecek?  
Hayır. Merhaba günlük verileri kullanılabilir tooyour çalışma aramaları hello yükseltme tarafından etkilenmez. Kayıtlı aramalar, uyarılara ve görünümlere dönüştürülmüş toohello yeni arama dili otomatik olarak olacaktır.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Soru: çalışma Alanım yükseltmediyseniz ne olur?  
Merhaba eski günlük arama ay gelen hello kullanım dışı kalacaktır. O zamana dek yükseltilmemiş çalışma alanları otomatik olarak yükseltilir.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Soru: t tooupgrade seçmediyseniz, ancak çalışma Alanım yine de yükseltilmiş! Ne oldu?  
Bu çalışma alanı'nın başka bir yönetici hello çalışma yükselttiniz. Merhaba yeni dil genel kullanılabilirlik ulaştığında tüm çalışma alanları otomatik olarak yükseltilecek olduğunu unutmayın.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>Soru: t yanlışlıkla yükselttiniz ve şimdi toocancel ve her şeyi geri geri yükleme gerekiyor. Ne yapmalıyım?  
Sorun değil.  Geri yükleyebilmeniz için anlık görüntüsünü, yükseltme işleminden önce çalışma alanınızı oluşturuyoruz. Uyarıları veya ancak hello yükseltme kaybolacak sonra kaydettiğiniz görünümleri arar göz önünde bulundurun.  toorestore çalışma ortamınızı izleyin hello yordamı, [geri sürümüne yükseltme sonra ı gidebilirsiniz?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Görünümler

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Soru: Nasıl yeni bir görünüm Görünüm Tasarımcısı ile oluşturulur?
Önceki tooupgrade hello ana Panoda bir kutucuğu öğesinden Görünüm Tasarımcısı ile yeni bir görünüm oluşturabilirsiniz.  Çalışma alanınızı yükseltildiğinde bu kutucuğu kaldırılır.  Merhaba yeşil + düğmesini hello soldaki menüde üzerinde tıklatarak yararlı hello OMS portalında Görünüm Tasarımcısı ile yeni bir görünüm oluşturabilirsiniz.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Bilinen sorun: çizgi grafiklerde görünümleri için tüm seçeneği bir çizgi grafiğine neden değil bakın
Merhaba üzerinde tıkladığınızda *tümünü görmek* seçeneği bir çizgi grafiği bölümünü bir görünümde hello altındaki içeren bir tablo sunulur.  Önceki tooupgrade bir çizgi grafiği ile sunulan.  Bu sorun için olası bir değişiklik analiz edilir.


## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [çalışma toohello yükseltme yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md).
