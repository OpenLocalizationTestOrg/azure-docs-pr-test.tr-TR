---
title: "aaaCollect ve OMS günlük analizi, Windows olay günlüklerini analiz edin | Microsoft Docs"
description: "Windows olay günlüklerini hello günlük analizi tarafından kullanılan en yaygın veri kaynaklarının biridir.  Bu makalede nasıl hello kayıtları ayrıntılarını ve Windows olay günlüklerini tooconfigure koleksiyonunu hello OMS deposunda oluşturdukları açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Windows olay günlüğü veri kaynaklarında, günlük analizi
Windows olay günlüklerini hello en yaygın biri olan [veri kaynakları](log-analytics-data-sources.md) birçok uygulama toohello Windows olay günlüğüne yazma beri Windows aracıları kullanarak veri toplama için.  Oluşturulan özel günlükleri toplama toospecifying sistem ve uygulama gibi standart günlükleri gelen olayları toplayabilir uygulamalar tarafından toomonitor gerekir.

![Windows olayları](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Yapılandırma Windows olay günlükleri
Merhaba Windows olay günlüklerini yapılandırma [günlük analizi ayarları veri menüde](log-analytics-data-sources.md#configuring-data-sources).

Günlük analizi hello ayarlarında belirtilen hello Windows olay günlüklerini yalnızca olayları toplar.  Bir olay günlüğü hello günlüğünün hello adını yazıp'yi tıklatarak ekleyebilirsiniz  **+** .  Her bir günlükteki seçili hello önem derecelerine sahip yalnızca hello olayları toplanır.  Merhaba önem derecelerine toocollect istediğiniz hello belirli günlük için denetleyin.  Herhangi bir ek ölçütü toofilter olayları sağlayamaz.

Bir olay günlüğü hello adı yazarken, günlük analizi ortak olay günlüğü adlarının öneriler sağlar. Merhaba günlük tooadd istediğiniz hello listede görünmüyorsa, hello günlüğünün hello tam adını yazarak hala ekleyebilirsiniz. Olay Görüntüleyicisi'ni kullanarak hello günlüğünün tam adı hello bulabilirsiniz. Olay Görüntüleyicisi'nde hello açmak *özellikleri* hello dizeden günlük ve kopyalama hello hello için sayfa *tam adı* alan.

![Windows olayları yapılandırın](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Veri toplama
Günlük analizi hello olay oluşturuldu olarak seçilen bir önem derecesi izlenen bir olay günlüğünden eşleşen her olay toplar.  Merhaba Aracısı onun yerine üzerinden topladığı her olay günlüğüne kaydeder.  Hello Aracısı bir süre için çevrimdışı olursa, bu olayları hello Aracısı çevrimdışıyken oluşturulmuş olsalar bile sonra günlük analizi olayları son devre dışı kaldığı toplar.  Merhaba olay günlüğü hello Aracısı çevrimdışı durumdayken üzerine yazmaya uncollected olaylarla sarmalar varsa bu olayları toonot toplanması için olası bir yoktur.

>[!NOTE]
>Günlük analizi kaynağından SQL Server tarafından oluşturulan denetim olaylarını toplama olmayan *MSSQLSERVER* anahtar sözcükleri - içeren olay kimliği 18453 *Klasik* veya *denetim başarı* ve anahtar sözcüğü *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Windows olay kayıtlarını özellikleri
Windows olay kayıtlarını sahip bir tür **olay** ve aşağıdaki tablonun hello hello özelliklere sahiptir:

| Özellik | Açıklama |
|:--- |:--- |
| Bilgisayar |Olay hello hello bilgisayarın adını toplandığı. |
| EventCategory |Merhaba olay kategorisi. |
| EventData |Tüm olay verileri ham biçiminde. |
| Olay Kimliği |Merhaba olay sayısı. |
| eventLevel |Sayısal formunda hello olayın önem derecesi. |
| EventLevelName |Metin biçiminde hello olayın önem derecesi. |
| Olay günlüğü |Olay hello hello olay günlüğünün adı toplandığı. |
| ParameterXml |Olay parametre değerleri XML biçiminde. |
| ManagementGroupName |System Center Operations Manager aracıları hello yönetim grubu adı.  Diğer aracıları için bu değer AOI -:<workspace ID> |
| RenderedDescription |Parametre değerleri ile olay açıklaması |
| Kaynak |Merhaba olay kaynağı. |
| SourceSystem |Aracı hello olay türü toplandığı. <br> OpsManager – Windows aracı, ya da doğrudan bağlanın veya Operations Manager yönetilen <br> Linux – tüm Linux aracıları  <br> AzureStorage – Azure tanılama |
| TimeGenerated |Tarih ve saat hello olay Windows oluşturuldu. |
| Kullanıcı adı |Merhaba olay günlüğe hello hesabının kullanıcı adı. |

## <a name="log-searches-with-windows-events"></a>Windows olay günlüğü aramalar
Merhaba aşağıdaki tabloda Windows olay kayıtlarını almak günlük arama farklı örnekleri sağlar.

| Sorgu | Açıklama |
|:--- |:--- |
| Tür olay = |Tüm Windows olayları. |
| Tür olay EventLevelName = hata = |Tüm Windows olayları hata önem derecesi. |
| Tür = olay &#124; Kaynak tarafından ölçü Count() işlevi |Kaynak olayların Windows sayısı. |
| Tür olay EventLevelName = = hata &#124; Kaynak tarafından ölçü Count() işlevi |Sayısı, Windows hata olayları kaynağa göre. |


>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra.
>
>| Sorgu | Açıklama |
|:---|:---|
| Olay |Tüm Windows olayları. |
| Olay &#124; Burada EventLevelName "error" == |Tüm Windows olayları hata önem derecesi. |
| Olay &#124; Kaynak tarafından Count() özetler |Kaynak olayların Windows sayısı. |
| Olay &#124; Burada EventLevelName "error" &#124; == Kaynak tarafından Count() özetler |Sayısı, Windows hata olayları kaynağa göre. |


## <a name="next-steps"></a>Sonraki adımlar
* Günlük analizi toocollect diğer yapılandırma [veri kaynakları](log-analytics-data-sources.md) çözümleme için.
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.  
* Kullanım [özel alanlar](log-analytics-custom-fields.md) tooparse hello olay kayıtlarını tek tek alanlara.
* Yapılandırma [performans sayaçları koleksiyonunu](log-analytics-data-sources-performance-counters.md) Windows aracılardan gelen.
