---
title: "OMS günlük analizi veri kaynaklarında aaaConfigure | Microsoft Docs"
description: "Veri kaynakları günlük analizi toplar aracıları ve diğer kaynakları bağlı hello veri tanımlayın.  Bu makalede hello kavramını günlük analizi veri kaynaklarını nasıl kullandığını açıklar, nasıl hello ayrıntılarını açıklayan tooconfigure bunları ve hello farklı veri kaynakları özetini sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Günlük analizi veri kaynaklarında
Günlük analizi OMS çalışma alanınızdaki hello bağlı kaynaklardan veri toplar ve bunları OMS deposunda saklar.  her birinden toplanan hello veri hello yapılandırdığınız veri kaynakları tarafından tanımlanır.  Merhaba OMS deposundaki verileri bir kayıt kümesi depolanır.  Her veri kaynağı kendi özellikler kümesini sahip her türüyle belirli bir türdeki kayıtları oluşturur.

![Günlük analizi veri toplama](./media/log-analytics-data-sources/overview.png)

Veri kaynakları, aynı zamanda bağlı kaynaklardan veri toplamak ve hello OMS deposunda kayıtları oluşturmak OMS çözümleri farklıdır.  Çözümleri tooyour çalışma Çözümleri Galerisi hello eklenebilir ve genellikle hello OMS portalında ek çözümleme araçları sağlar.  

## <a name="summary-of-data-sources"></a>Veri kaynakları özeti
Günlük analizi şu anda kullanılabilir hello veri kaynakları, aşağıdaki tablonun hello listelenir.  Her ayrıntı için bu veri kaynağı sağlayarak bağlantı tooa ayrı bir makale vardır.

| Veri kaynağı | Olay türü | Açıklama |
|:--- |:--- |:--- |
| [Özel günlükler](log-analytics-data-sources-custom-logs.md) |\<Günlükadı\>_CL |Metin dosyaları günlüğü bilgilerini içeren Windows veya Linux aracıları hakkında. |
| [Windows olay günlükleri](log-analytics-data-sources-windows-events.md) |Olay |Olayları Windows bilgisayarlarda hello olay günlüğü'nden toplanır. |
| [Windows performans sayaçları](log-analytics-data-sources-performance-counters.md) |Perf |Performans sayaçları Windows bilgisayarlardan toplanan. |
| [Linux performans sayaçları](log-analytics-data-sources-performance-counters.md) |Perf |Linux bilgisayarlardan toplanan performans sayaçları. |
| [IIS günlükleri](log-analytics-data-sources-iis-logs.md) |W3CIISLog |Internet Information Services W3C biçiminde kaydeder. |
| [Syslog](log-analytics-data-sources-syslog.md) |Syslog |Syslog olayları Windows veya Linux bilgisayarlardaki. |

## <a name="configuring-data-sources"></a>Veri kaynaklarını yapılandırma
Merhaba veri kaynaklarından yapılandırma **veri** günlük analizi menüde **ayarları**.  Herhangi bir yapılandırma OMS çalışma alanınızdaki tooall bağlı kaynakları teslim edilir.  Şu anda bu yapılandırmasından tüm aracıları dışarıda bırakılamaz.

![Windows olayları yapılandırın](./media/log-analytics-data-sources/configure-events.png)

1. Merhaba Hello OMS konsolunda tıklatın **ayarları** döşeme veya hello **ayarları** Merhaba ekranında hello üstündeki düğmesi.
2. Seçin **veri**.
3. Merhaba veri kaynağı tooconfigure üzerinde'ı tıklatın.
4. Merhaba bağlantı toohello belgelerine hello tablo ayrıntı için yukarıda her veri kaynağı için kendi yapılandırmasına izleyin.

> [!NOTE]
> Bu gibi durumlarda, günlük analizi veri kaynakları şu anda hello Azure portal yapılandıramazsınız.

## <a name="data-collection"></a>Veri toplama
Veri kaynağı yapılandırmaları doğrudan bağlı tooLog Analytics birkaç dakika içinde olan tooagents teslim edilir.  Merhaba veriler hello Aracısı'ndan toplanır ve doğrudan tooLog Analytics aralıkları belirli tooeach veri kaynağında teslim belirtildi.  Bu özellikleri için her bir veri kaynağı Hello belgelerine bakın.

Bağlı yönetim grubu için aracıları System Center Operations Manager (SCOM), veri kaynağı yapılandırmaları yönetim paketleri çevrilen ve toohello yönetim grubu, varsayılan olarak 5 dakikada bir teslim.  Merhaba aracı diğer gibi hello Yönetim Paketi indirir ve belirtilen veri toplar hello. Merhaba Aracısı hello veri tooLog Analytics hello yönetim sunucusu üzerinden geçmeden göndermek veya Hello veri kaynağı hello bağlı olarak ya da hello veri toohello günlük analizi ileten tooa yönetim sunucusuna gönderilen veri olacaktır. Çok başvuran[OMS özelliklerin ve çözümlerin için veri toplama ayrıntılarına](log-analytics-add-solutions.md#data-collection-details) Ayrıntılar için.  Bu yapılandırma SCOM ve OMS bağlanma ve hello sıklığını değiştirme hakkında ayrıntılar okuyabilir, teslim [System Center Operations Manager tümleştirmesini yapılandırma](log-analytics-om-agents.md).

Merhaba Aracısı yüklenemiyor tooconnect tooLog Analytics veya Operations Manager ise, bir bağlantı kurduğunda teslim eder toocollect verileri devam eder.  Veri miktarını hello hello en büyük önbellek boyutu hello istemcisi için ulaşırsa veya hello Aracısı mümkün tooestablish 24 saat içinde bir bağlantı değilse verileri kaybolabilir.

## <a name="log-analytics-records"></a>Log Analytics kayıtları
Günlük analizi tarafından toplanan tüm veriler, hello OMS deposunda kayıt olarak depolanır.  Farklı veri kaynakları tarafından toplanan kayıtları kendi özellikler kümesini sahip olur ve tarafından tanımlanan kendi **türü** özelliği.  Her veri kaynağı için Hello belgelere ve çözüm ayrıntıları için her bir kayıt türü bakın.

## <a name="next-steps"></a>Sonraki Adımlar
* Hakkında bilgi edinin [çözümleri](log-analytics-add-solutions.md) işlevselliği tooLog Analytics eklemek ve de hello OMS depoya veri toplamak.
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.  
* Yapılandırma [uyarıları](log-analytics-alerts.md) tooproactively toplanan veri kaynakları ve çözümlerinin kritik verilerin bildirin.
