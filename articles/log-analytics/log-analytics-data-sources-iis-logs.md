---
title: "aaaIIS günlüklerini günlük analizi | Microsoft Docs"
description: "Internet Information Services (IIS), günlük dosyalarında günlük analizi tarafından toplanan kullanıcı etkinliği depolar.  Bu makalede nasıl hello kayıtları ayrıntılarını ve IIS günlüklerini tooconfigure koleksiyonunu hello OMS deposunda oluşturdukları açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>IIS günlük analizi günlüğe kaydeder
Internet Information Services (IIS), günlük dosyalarında günlük analizi tarafından toplanan kullanıcı etkinliği depolar.  

![IIS günlükleri](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>IIS yapılandırma günlükleri
Günlük analizi girişleri gerekir böylece IIS tarafından oluşturulan günlük dosyalarını toplar [IIS için günlüğe kaydetmeyi yapılandırmak](https://technet.microsoft.com/library/hh831775.aspx).

Günlük analizi, yalnızca IIS günlük dosyalarına W3C biçiminde depolanan destekler ve özel alanlar veya Gelişmiş IIS günlüğü desteklemez.  
Günlük analizi Günlükleri NCSA veya IIS yerel biçiminde toplamaz.

IIS günlüklerini günlük analizi hello yapılandırma [günlük analizi ayarları veri menüde](log-analytics-data-sources.md#configuring-data-sources).  Olduğundan herhangi bir yapılandırma gerekli seçerek dışında **toplamak W3C biçimi IIS günlük dosyaları**.

IIS günlük toplama etkinleştirdiğinizde, her sunucuda hello IIS günlük aktarma ayarı yapılandırmanız gerekir öneririz.

## <a name="data-collection"></a>Veri toplama
Günlük analizi IIS günlüğü girişlerini bağlı her kaynaktan yaklaşık her 15 dakikada toplar.  Merhaba Aracısı onun yerine üzerinden topladığı her olay günlüğüne kaydeder.  Hello Aracısı çevrimdışı olursa, bu olayları hello Aracısı çevrimdışıyken oluşturulmuş olsalar bile sonra günlük analizi olayları son devre dışı kaldığı toplar.

## <a name="iis-log-record-properties"></a>IIS günlük kaydı Özellikler
IIS günlük kayıtlarını sahip bir tür **W3CIISLog** ve aşağıdaki tablonun hello hello özelliklere sahiptir:

| Özellik | Açıklama |
|:--- |:--- |
| Bilgisayar |Olay hello hello bilgisayarın adını toplandığı. |
| CIP |Merhaba istemci IP adresi. |
| csMethod |GET veya POST gibi hello istek yöntemi. |
| csReferer |Bu hello site kullanıcı toohello geçerli siteden bir bağlantıyı izlenen. |
| csUserAgent |Merhaba istemci tarayıcı türü. |
| csUserName |Merhaba adını hello Sunucu'ya kullanıcı kimliği. Anonim kullanıcılar bir tire işaretiyle gösterilir. |
| csUriStem |Hedef bir web sayfası gibi hello isteği. |
| csUriQuery |Sorgu, varsa, o hello istemci tooperform çalışıyordu. |
| ManagementGroupName |Operations Manager aracıları hello yönetim grubu adı.  Diğer aracılar için AOI - budur\<çalışma alanı kimliği\> |
| RemoteIPCountry |Ülke / bölge hello istemcinin başlangıç IP adresi. |
| RemoteIPLatitude |Enlem hello istemci IP adresi. |
| RemoteIPLongitude |Boylam hello istemci IP adresi. |
| scStatus |HTTP durum kodu. |
| scSubStatus |Alt durum hata kodu. |
| scWin32Status |Windows durum kodu. |
| SIP |Merhaba web sunucusunun IP adresi. |
| SourceSystem |OpsMgr |
| Spor |Bağlantı noktası hello sunucu hello istemcide bağlı. |
| sSiteName |Merhaba IIS site adı. |
| TimeGenerated |Tarih ve saat hello girişi günlüğe kaydedildi. |
| TimeTaken |Zaman tooprocess hello uzunluğu milisaniye cinsinden istek. |

## <a name="log-searches-with-iis-logs"></a>IIS günlükleri ile günlük aramalar
Merhaba aşağıdaki tabloda, IIS günlük kayıtlarını almak günlük sorgularının farklı örnekler verilmektedir.

| Sorgu | Açıklama |
|:--- |:--- |
| Tür W3CIISLog = |Tüm IIS günlük kaydı. |
| Tür W3CIISLog scStatus = 500 = |Tüm IIS günlük kayıtları dönüş durumu 500 ile. |
| Tür = W3CIISLog &#124; Ölçü count() CIP tarafından |Count, IIS girişleri istemci IP adresi ile oturum açın. |
| Tür W3CIISLog csHost = = "www.contoso.com" &#124; Ölçü count() csUriStem tarafından |Count, IIS URL girdilerinin hello konak www.contoso.com için oturum açın. |
| Tür = W3CIISLog &#124; Bilgisayar & #124 tarafından ölçü Sum(csBytes); üst 500000 |Her IIS bilgisayar tarafından alınan toplam bayt sayısı. |

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra.

> | Sorgu | Açıklama |
|:--- |:--- |
| W3CIISLog |Tüm IIS günlük kaydı. |
| W3CIISLog &#124; Burada scStatus 500 == |Tüm IIS günlük kayıtları dönüş durumu 500 ile. |
| W3CIISLog &#124; tarafından CIP Count() özetler |Count, IIS girişleri istemci IP adresi ile oturum açın. |
| W3CIISLog &#124; Burada csHost "www.contoso.com" &#124; == tarafından csUriStem Count() özetler |Count, IIS URL girdilerinin hello konak www.contoso.com için oturum açın. |
| W3CIISLog &#124; Bilgisayar & #124 tarafından SUM(csBytes) özetlemek; 500000 alın |Her IIS bilgisayar tarafından alınan toplam bayt sayısı. |

## <a name="next-steps"></a>Sonraki adımlar
* Günlük analizi toocollect diğer yapılandırma [veri kaynakları](log-analytics-data-sources.md) çözümleme için.
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.
* Günlük analizi tooproactively IIS günlüklerine bulunan önemli koşulları bildir uyarıları yapılandırın.
