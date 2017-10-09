---
title: "aaaAzure günlük analizi sorgu dili kopya sayfası | Microsoft Docs"
description: "Bu makale, zaten hello eski diline alışık değilseniz, toohello yeni sorgu dili için günlük analizi geçiş hakkında Yardım sağlar."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>TooAzure günlük analizi yeni sorgu dili geçiş

> [!NOTE]
> Yükseltme sırasında çalışma alanınızda yeni günlük analizi sorgu dili ve alma hello hakkında daha fazla hello yordamı tooupgrade okuyabilir, [Azure günlük analizi çalışma alanı toonew günlük arama](log-analytics-log-search-upgrade.md).

Bu makale, zaten hello eski diline alışık değilseniz, toohello yeni sorgu dili için günlük analizi geçiş hakkında Yardım sağlar.

## <a name="language-converter"></a>Dil dönüştürücü

Merhaba eski günlük analizi sorgu dili ile aşinaysanız hello toocreate hello hello yeni dil aynı sorguda kolay toouse hello çalışma alanınızı dönüştürüldüğünde hello günlük arama Portalı'nda yüklü dil Dönüştürücüsü yoludur.  Merhaba dönüştürücü ile eski sorgu hello üst metin kutusuna yazarak ve ardından olarak basit **dönüştürme**.  Merhaba arama düğmesini toorun hello sorgusu veya Kopyala'yı tıklatın ve toouse yapıştırın başka bir yere.

![Dil dönüştürücü](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Kopya kağıdı

Merhaba aşağıdaki tablo genel sorgular çeşitli arasında bir karşılaştırma tooequivalent komutlar Azure günlük analizi hello yeni ve eski sorgu dili arasında sağlar.

| Açıklama | Eski | Yeni |
|:--|:--|:--|
| Tüm tabloları arama      | error | "error" (büyük/küçük harfe duyarlı değildir) arama |
| Tablodan veri seçin | Tür olay = |  Olay |
|                        | Tür = olay &#124; Kaynak, olay günlüğüne olay kimliği seçin | Olay &#124; Kaynak, olay günlüğüne, EventID proje |
|                        | Tür = olay &#124; en iyi 100 | Olay &#124; 100 alın |
| Dize karşılaştırması      | Tür olay Computer=srv01.contoso.com =   | Olay &#124; Burada bilgisayar "srv01.contoso.com" == |
|                        | Tür olay Computer=contains("contoso") = | Olay &#124; Burada "contoso" (büyük/küçük harfe duyarlı değildir) bilgisayar içeriyor<br>Olay &#124; Burada bilgisayar contains_cs "Contoso" (büyük küçük harf duyarlı) |
|                        | Tür = olay bilgisayarı RegEx = ("@contoso@")  | Olay &#124; Bilgisayar regex eşleştiği ". *contoso*" |
| Tarih karşılaştırması        | Tür olay TimeGenerated = > şimdi 1DAYS | Olay &#124; Burada TimeGenerated > ago(1d) |
|                        | Tür olay TimeGenerated = > 2017-05-01 TimeGenerated < 2017-05-31 | Olay &#124; Burada TimeGenerated (datetime(2017-05-01).. arasında DateTime(2017-05-31)) |
| Boolean karşılaştırması     | Tür sinyal IsGatewayInstalled = = false  | Sinyal | Burada IsGatewayInstalled == false |
| Sırala                   | Tür = olay &#124; Sıralama bilgisayarı asc, olay günlüğüne desc, EventLevelName asc | Olay \| Bilgisayar asc, olay günlüğüne desc, EventLevelName asc göre sıralama |
| Farklı               | Tür = olay &#124; Yinelenenleri kaldırma bilgisayar \| Bilgisayar seçin | Olay &#124; Bilgisayar, olay günlüğüne özetler |
| Sütunları Genişlet         | Türü Perf CounterName = = "% işlemci zamanı" &#124; GENİŞLETME if(map(CounterValue,0,50,0,1),"HIGH","LOW") kullanımı olarak | Perf &#124; CounterName burada "% işlemci zamanı" == \| Kullanımı genişletmek olur = (> 50, "Yüksek", "Düşük" CounterValue) |
| Toplama            | Tür = olay &#124; Bilgisayar bazında sayı olarak ölçü Count() işlevi | Olay &#124; Count özetlemek bilgisayar tarafından count() = |
|                                | Türü Perf ObjectName = işlemci CounterName = = "% işlemci zamanı" &#124; Ölçü avg(CounterValue) bilgisayar aralığı 5 dakika | Perf &#124; Burada ObjectName "İşlemci" ve CounterName == "% işlemci zamanı" &#124; == Bilgisayar, bin (TimeGenerated, 5 dk.) tarafından AVG(CounterValue) özetler |
| Sınır toplama | Tür = olay &#124; Bilgisayar & #124 tarafından ölçü count(); İlk 10 | Olay &#124; AggregatedValue özetlemek bilgisayar &#124; tarafından count() = Sınırı 10 |
| birleşim                  | Tür olay veya türü = Syslog = | UNION olay, Syslog |
| Birleştir                   | Tür = NetworkMonitoring &#124; İç AgentIP katılma (tür = sinyal) ComputerIP | NetworkMonitoring &#124; Birleştirme türü iç = (türünü arama "Sinyal" ==) $left üzerinde. AgentIP $right.ComputerIP == |



## <a name="next-steps"></a>Sonraki adımlar
- Kullanıma bir [sorgu yazmakla ilgili öğretici](https://go.microsoft.com/fwlink/?linkid=856078) hello yeni sorgu dilini kullanma.
- Toohello başvuran [sorgu dili başvurusu](https://go.microsoft.com/fwlink/?linkid=856079) tüm komutu, işleçler ve işlevleri hello yeni sorgu dili için hakkında ayrıntılar için.  
