---
title: "OMS günlük analizi CollectD aaaCollect verilerden | Microsoft Docs"
description: "CollectD düzenli aralıklarla veri uygulamaları ve sistem düzeyi bilgileri toplayan bir açık kaynak Linux arka plan programı kullanılır.  Bu makalede, günlük analizi CollectD gelen veri toplama hakkında bilgi sağlar."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Veri günlük analizi Linux aracıları CollectD Topla
[CollectD](https://collectd.org/) uygulamaları ve sistem düzeyi bilgileri düzenli aralıklarla performans ölçümleri toplayan bir açık kaynak Linux arka plan programı kullanılır. Örnek uygulamalar hello Java sanal makine (JVM), MySQL Server ve Nginx içerir. Bu makalede günlük analizi CollectD gelen performans verileri toplama hakkında bilgi sağlar.

Kullanılabilen eklentileri tam listesi bulunabilir [tablo, eklenti](https://collectd.org/wiki/index.php/Table_of_Plugins).

![CollectD genel bakış](media/log-analytics-data-sources-collectd/overview.png)

Merhaba aşağıdaki CollectD yapılandırma hello OMS Aracısı Linux tooroute CollectD veri toohello OMS aracısı için Linux için dahil edilmiştir.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

Ayrıca, yapılandırma bunun yerine aşağıdaki hello 5.5 kullanmadan önce bir collectD sürümleri kullanıyorsanız.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

Merhaba CollectD yapılandırmasını kullanan hello varsayılan`write_http` eklentisi toosend performans ölçüm verilerini bağlantı noktası 26000 tooOMS Linux Aracısı üzerinden. 

> [!NOTE]
> Gerekirse, bu bağlantı noktası özel tanımlı yapılandırılmış tooa bağlantı noktası olabilir.

Hello Linux için OMS aracısı ayrıca CollectD ölçümünün 26000 numaralı bağlantı noktasında dinler ve bunları tooOMS şema ölçümleri dönüştürür. Merhaba Linux yapılandırması için OMS aracısının hello aşağıdadır `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Desteklenen sürümleri
- Günlük analizi, şu anda CollectD sürüm 4.8 destekler ve üstü.
- Yukarıdaki veya Linux v1.1.0-217 için OMS aracısının CollectD ölçüm koleksiyonu için gereklidir.


## <a name="configuration"></a>Yapılandırma
Merhaba, temel adımlar tooconfigure günlük analizi CollectD veri koleksiyonunu verilmiştir.

1. CollectD toosend veri toohello OMS Aracısı hello write_http eklentisi kullanarak Linux için yapılandırın.  
2. Linux toolisten hello CollectD veri için OMS aracısının Merhaba hello uygun bağlantı noktasını yapılandırın.
3. CollectD ve Linux için OMS aracısı yeniden başlatın.

### <a name="configure-collectd-tooforward-data"></a>CollectD tooforward verileri yapılandırma 

1. tooroute CollectD veri toohello Linux için OMS aracısının `oms.conf` gereksinimlerini toobe eklenen tooCollectD'ın yapılandırma dizini. Bu dosyanın Hello hedef üzerinde makinenizin hello Linux distro bağlıdır.

    CollectD yapılandırma dizininize /etc/collectd.d/ içinde yer alıyorsa:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    CollectD yapılandırma dizininize /etc/collectd/collectd.conf.d/ içinde yer alıyorsa:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >5.5 önce CollectD sürümleri için toomodify hello etiketleri gerekir `oms.conf` yukarıda gösterildiği gibi.
    >

2. Collectd.conf istenen toohello Workspace'in omsagent yapılandırma dizini kopyalayın.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. Linux için CollectD ve OMS Aracısı komutları aşağıdaki hello ile yeniden başlatın.

    sudo hizmet collectd yeniden sudo /opt/microsoft/omsagent/bin/service_control yeniden başlatma

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>CollectD ölçümleri tooLog Analytics şema dönüştürme
toomaintain bilinen bir model zaten Linux ve hello yeni ölçümler OMS aracısı tarafından toplanan altyapı ölçümler arasında şema eşleme aşağıdaki hello kullanılan CollectD tarafından toplanan:

| CollectD ölçüm alan | Günlük analizi alan |
|:--|:--|
| ana bilgisayar | Bilgisayar |
| Eklentisi | None |
| plugin_instance | Örnek adı<br>Varsa **plugin_instance** olan *null* sonra InstanceName = "*_Total*" |
| type | ObjectName |
| type_instance | CounterName<br>Varsa **type_instance** olan *null* sonra CounterName =**boş** |
| dsnames] | CounterName |
| dstypes | None |
| değerler] | CounterValue |

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler. 
* Kullanım [özel alanlar](log-analytics-custom-fields.md) syslog kayıtları tek tek alanlara tooparse verileri.

