---
title: "hdınsight'ta - Azure aaaUnderstand ve çözümleme WebHCat hatalarını | Microsoft Docs"
description: "Hdınsight üzerinde WebHCat tarafından döndürülen tooabout ortak hataları nasıl ve ne öğrenin tooresolve bunları."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>Anlama ve hdınsight'ta WebHCat gelen karşılaşılan hataları çözme

Tooresolve WebHCat Hdınsight ile kullanırken ve nasıl alınan hataları hakkında bilgi edinin bunları. WebHCat dahili olarak Azure PowerShell ve hello Data Lake araçları gibi istemci tarafı araçları Visual Studio için kullanılıyor.

## <a name="what-is-webhcat"></a>WebHCat nedir

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) bir REST API için [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), tablo ve Hadoop için Depolama Yönetimi katmanı. WebHCat Hdınsight kümelerinde varsayılan olarak etkindir ve çeşitli araçlar toosubmit işleri tarafından kullanılır, iş durumu, vb. toohello kümede günlüğe kaydetmeden Al.

## <a name="modifying-configuration"></a>Yapılandırmasını değiştirme

> [!IMPORTANT]
> Yapılandırılan en aştığından birkaç bu belgede listelenen hello hataları oluşur. Bir değer değiştirebileceğiniz Hello çözümleme adım değinmektedir kullanırken, tooperform hello değişikliğinden sonra hello birini kullanmanız gerekir:

* İçin **Windows** kümeleri: küme oluşturma sırasında bir betik eylemi tooconfigure hello değeri kullanın. Daha fazla bilgi için bkz: [betik eylemleri geliştirmeniz](hdinsight-hadoop-script-actions.md).

* İçin **Linux** kümeleri: kullanım Ambari (web veya REST API) toomodify hello değeri. Daha fazla bilgi için bkz: [Ambari kullanarak Hdınsight yönetme](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="default-configuration"></a>Varsayılan yapılandırma

Varsayılan değerleri aşağıdaki hello aşılırsa, WebHCat performansı düşebilir veya hatalara neden olabilir:

| Ayar | Neler yapar? | Varsayılan değer |
| --- | --- | --- |
| [yarn.Scheduler.Capacity.Maximum-uygulamalar][maximum-applications] |Merhaba eşzamanlı olarak etkinleştirilebilir iş sayısı üst sınırını (Beklemede veya çalışan) |10,000 |
| [templeton.Exec.max yakalar][max-procs] |Merhaba en fazla eşzamanlı olarak sunulan istek sayısı |20 |
| [mapreduce.jobhistory.max yaş ms][max-age-ms] |Geçmiş işi gün sayısı Hello korunur |7 gün |

## <a name="too-many-requests"></a>Çok fazla istek

**HTTP durum kodu**: 429

| Nedeni | Çözüm |
| --- | --- |
| (Varsayılan 20) dakika başına WebHCat tarafından sunulan hello maksimum eşzamanlı istek sınırı aşıldı |Değil gönderme birden fazla hello en fazla eş zamanlı istek sayısını veya değiştirerek hello eşzamanlı istek sınırı artırmak olduğunu, iş yükü tooensure azaltmak `templeton.exec.max-procs`. Daha fazla bilgi için bkz: [değiştirme yapılandırma](#modifying-configuration) |

## <a name="server-unavailable"></a>Sunucu kullanılamıyor

**HTTP durum kodu**: 503

| Nedeni | Çözüm |
| --- | --- |
| Bu durum kodu genellikle hello birincil ve ikincil arasında yük devretme sırasında oluşup HeadNode hello kümesi için |İki dakika bekleyin, sonra hello işlemi yeniden deneyin |

## <a name="bad-request-content-could-not-find-job"></a>Hatalı istek içeriği: işi bulunamadı.

**HTTP durum kodu**: 400

| Nedeni | Çözüm |
| --- | --- |
| İş ayrıntılarını hello iş geçmişi tarafından temizleyici temizlendi |iş geçmişi için Hello varsayılan saklama dönemi 7 gündür. Merhaba varsayılan saklama dönemi değiştirerek değiştirilebilir `mapreduce.jobhistory.max-age-ms`. Daha fazla bilgi için bkz: [değiştirme yapılandırma](#modifying-configuration) |
| İş tooa yük devretme sonlandırıldı |Tootwo dakika yedeklemek için iş gönderme yeniden deneyin |
| Geçersiz iş kimliği kullanıldı |Merhaba iş kimliği doğru olup olmadığını denetleyin |

## <a name="bad-gateway"></a>Hatalı ağ geçidi

**HTTP durum kodu**: 502

| Nedeni | Çözüm |
| --- | --- |
| İç çöp toplama hello WebHCat işlem içinde gerçekleşen |Çöp toplama toofinish için bekleyin veya hello WebHCat hizmetini yeniden başlatın |
| Merhaba ResourceManager hizmeti bilgisayarından yanıt beklenirken zaman aşımı. Etkin uygulama Hello sayısı hello yapılandırılmış en büyük (varsayılan 10.000) olduğunda bu hata oluşabilir |İşlerini toocomplete çalışmakta bekleyin veya değiştirerek hello eşzamanlı iş sınırını artırın `yarn.scheduler.capacity.maximum-applications`. Daha fazla bilgi için bkz: Merhaba [değiştirme yapılandırma](#modifying-configuration) bölümü. |
| Merhaba aracılığıyla tüm işleri tooretrieve çalışırken [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) çağrısı sırasında `Fields` çok ayarlama`*` |Alamadı *tüm* iş ayrıntıları. Bunun yerine kullanın `jobid` tooretrieve ayrıntılarını işler yalnızca belirli iş kimliği büyük. Ya da kullanmayın`Fields` |
| HeadNode yük devretme sırasında Hello WebHCat hizmeti çalışmıyor |İki dakika bekleyin ve hello işlemi yeniden deneyin |
| WebHCat gönderilen 500'den fazla bekleyen iş |Daha fazla iş göndermeden önce şu anda bekleyen işler tamamlanana kadar bekleyin |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
