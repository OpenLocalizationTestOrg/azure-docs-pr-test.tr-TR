---
title: "OMS günlük analizi aaaCollecting özel JSON verileri | Microsoft Docs"
description: "Özel JSON veri kaynakları hello OMS aracısı kullanarak Linux için günlük analizi içine toplanabilir.  Bu özel veri kaynaklarının basit betik dosyalarını curl veya FluentD'ın 300 + eklentileri gibi JSON döndürüyor olabilir. Bu makalede bu veri toplama için gereken hello yapılandırmasını açıklar."
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
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Günlük analizi Linux için hello OMS Aracısı özel JSON veri kaynaklarıyla toplama
Özel JSON veri kaynakları hello OMS aracısı kullanarak Linux için günlük analizi içine toplanabilir.  Bu özel veri kaynaklarının JSON gibi döndüren basit betik dosyalarını olabilir [curl](https://curl.haxx.se/) veya biri [FluentD'ın 300 + eklentileri](http://www.fluentd.org/plugins/all). Bu makalede bu veri toplama için gereken hello yapılandırmasını açıklar.

> [!NOTE]
> Linux v1.1.0 için OMS aracısının-217 + özel JSON verileri için gerekli

## <a name="configuration"></a>Yapılandırma

### <a name="configure-input-plugin"></a>Giriş eklentisi yapılandırma

Günlük analizi toocollect JSON verilerde ekleme `oms.api.` giriş eklentisi FluentD etiketinde toohello başlangıcı.

Örneğin, aşağıdaki ayrı yapılandırma dosyası `exec-json.conf` içinde `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  Bu hello FluentD eklentisi kullanır `exec` toorun curl komutunu her 30 saniyede.  Bu komutun çıktısı Hello hello JSON çıkış eklenti tarafından toplanır.

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
Merhaba yapılandırma dosyası altında eklenen `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` sahipliğini komutu aşağıdaki hello ile değiştirilen toohave gerektirir.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Çıktı eklentisi yapılandırma 
Çıktı eklentisi yapılandırma toohello ana yapılandırmasında aşağıdaki hello eklemek `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ya da ayrı yapılandırma dosyası yerleştirilen gibi`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a>Linux için OMS aracıyı yeniden başlatın
Merhaba OMS Aracısı Linux hizmeti için komutu aşağıdaki hello ile yeniden başlatın.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Çıktı
Merhaba veri toplanacak günlük analizi kayıt türü `<FLUENTD_TAG>_CL`.

Örneğin, özel etiket hello `tag oms.api.tomcat` kayıt türüne sahip günlük analytics'te `tomcat_CL`.  Bu türdeki tüm kayıtları günlük arama aşağıdaki hello ile alınamadı.

    Type=tomcat_CL

İç içe JSON veri kaynakları desteklenir, ancak dizini üst alanı dışına temel. Örneğin, JSON verilerini aşağıdaki hello bir günlük analizi aramadan döndürülür `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler. 
 