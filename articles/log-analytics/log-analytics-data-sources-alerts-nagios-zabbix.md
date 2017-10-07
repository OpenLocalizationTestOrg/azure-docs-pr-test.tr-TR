---
title: "OMS günlük analizi aaaCollect Nagios ve Zabbix uyarılar | Microsoft Docs"
description: "Nagios ve Zabbix izleme araçları açık kaynaktır. Toplama uyarıları bu Araçları'ndan sipariş tooanalyze günlük analizi içine bunları uyarıları diğer kaynaklardan birlikte.  Bu makalede, Linux toocollect tooconfigure Merhaba OMS Aracısı bu sistemlerden nasıl uyarıları açıklanmaktadır."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Linux için Nagios ve günlük analizi OMS aracısından Zabbix uyarılarını Topla 
[Nagios](https://www.nagios.org/) ve [Zabbix](http://www.zabbix.com/) olan açık kaynak izleme araçları.  Toplama uyarıları bu Araçları'ndan günlük analizi sipariş tooanalyze bunları ile birlikte [diğer kaynaklardan uyarıları](log-analytics-alerts.md).  Bu makalede, Linux toocollect tooconfigure Merhaba OMS Aracısı bu sistemlerden nasıl uyarıları açıklanmaktadır.
 
## <a name="configure-alert-collection"></a>Uyarı koleksiyonunu yapılandırma

### <a name="configuring-nagios-alert-collection"></a>Nagios uyarı koleksiyonunu yapılandırma
Merhaba hello Nagios sunucu toocollect uyarıları üzerinde aşağıdaki adımları gerçekleştirin.

1. GRANT hello kullanıcı **omsagent** okuma erişimi toohello Nagios günlük dosyası (yani `/var/log/nagios/nagios.log`). Merhaba nagios.log dosya hello grupla ait olduğu varsayılarak `nagios`, hello kullanıcı ekleyebilir **omsagent** toohello **nagios** grubu. 

    sudo usermod - a -G nagios omsagent

2.  Merhaba yapılandırma dosyasını değiştirme (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Mevcut ve kullanıma açıklamalı girişleri aşağıdaki hello çalıştığından emin olun:  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. Merhaba omsagent arka plan programı yeniden başlatın

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Zabbix uyarı koleksiyonunu yapılandırma
Zabbix sunucusundan toocollect uyarıları, gereksinim duyduğunuz toospecify bir kullanıcıyı ve parolayı *açık metin*. Bu ideal değildir, ancak hello kullanıcı oluşturun ve izinleri toomonitor onlu vermek öneririz.

Merhaba hello Nagios sunucu toocollect uyarıları üzerinde aşağıdaki adımları gerçekleştirin.

1. Merhaba yapılandırma dosyasını değiştirme (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Mevcut ve kullanıma açıklamalı girişleri aşağıdaki hello olduğundan emin olun.  Zabbix ortamınız için Hello kullanıcı adı ve parola toovalues değiştirin.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Merhaba omsagent arka plan programı yeniden başlatın

    sudo Paylaş /opt/microsoft/omsagent/bin/service_control yeniden başlatın


## <a name="alert-records"></a>Uyarı kaydeder
Nagios ve Zabbix uyarı kayıtları almak kullanarak [oturum aramaları](log-analytics-log-searches.md) günlük analizi içinde.

### <a name="nagios-alert-records"></a>Nagios uyarı kaydeder

Nagios tarafından toplanan kayıtları uyarı bir **türü** , **uyarı** ve **SourceSystem** , **Nagios**.  Bunlar, aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
|:--- |:--- |
| Tür |*Uyarı* |
| SourceSystem |*Nagios* |
| AlertName |Merhaba uyarı adı. |
| AlertDescription | Merhaba uyarı açıklaması. |
| AlertState | Merhaba hizmet veya ana bilgisayar durumu.<br><br>TAMAM<br>UYARI<br>AYARLAMA<br>AŞAĞI |
| Ana bilgisayar adı | Merhaba uyarı oluşturulan hello ana bilgisayar adı. |
| PriorityNumber | Merhaba uyarı öncelik düzeyi. |
| StateType | Merhaba uyarının durumunu Hello türü.<br><br>SOFT - değil yeniden sorun.<br>Sabit - bırakıldı sorunu belirtilen kaç kez yeniden.  |
| TimeGenerated |Tarih ve saat hello uyarı oluşturuldu. |


### <a name="zabbix-alert-records"></a>Zabbix uyarı kaydeder
Zabbix tarafından toplanan kayıtları uyarı bir **türü** , **uyarı** ve **SourceSystem** , **Zabbix**.  Bunlar, aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
|:--- |:--- |
| Tür |*Uyarı* |
| SourceSystem |*Zabbix* |
| AlertName | Merhaba uyarı adı. |
| AlertPriority | Uyarının önem derecesini hello.<br><br>Sınıflandırılmamış<br>Bilgi<br>Uyarı<br>Ortalama<br>Yüksek<br>Olağanüstü durum  |
| AlertState | Merhaba uyarı durumu.<br><br>0 - toodate durumudur.<br>1 - durumu bilinmiyor.  |
| AlertTypeNumber | Uyarı birden çok sorun Olay Oluştur olup olmadığını belirtir.<br><br>0 - toodate durumudur.<br>1 - durumu bilinmiyor.    |
| Yorumlar | Ek açıklamalar uyarı için. |
| Ana bilgisayar adı | Merhaba uyarı oluşturulan hello ana bilgisayar adı. |
| PriorityNumber | Merhaba uyarının önem derecesini belirten değer.<br><br>0 - Sınıflandırılmamış<br>1 - bilgileri<br>2 - uyarı<br>3 - ortalama<br>4 - yüksek<br>5 - olağanüstü durum |
| TimeGenerated |Tarih ve saat hello uyarı oluşturuldu. |
| TimeLastModified |Tarih ve saat hello durumu hello uyarının son değişti. |


## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [uyarıları](log-analytics-alerts.md) günlük analizi içinde.
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler. 
