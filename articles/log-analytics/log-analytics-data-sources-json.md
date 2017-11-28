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
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="e10d7-105">Günlük analizi Linux için hello OMS Aracısı özel JSON veri kaynaklarıyla toplama</span><span class="sxs-lookup"><span data-stu-id="e10d7-105">Collecting custom JSON data sources with hello OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="e10d7-106">Özel JSON veri kaynakları hello OMS aracısı kullanarak Linux için günlük analizi içine toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="e10d7-106">Custom JSON data sources can be collected into Log Analytics using hello OMS Agent for Linux.</span></span>  <span data-ttu-id="e10d7-107">Bu özel veri kaynaklarının JSON gibi döndüren basit betik dosyalarını olabilir [curl](https://curl.haxx.se/) veya biri [FluentD'ın 300 + eklentileri](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="e10d7-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="e10d7-108">Bu makalede bu veri toplama için gereken hello yapılandırmasını açıklar.</span><span class="sxs-lookup"><span data-stu-id="e10d7-108">This article describes hello configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="e10d7-109">Linux v1.1.0 için OMS aracısının-217 + özel JSON verileri için gerekli</span><span class="sxs-lookup"><span data-stu-id="e10d7-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="e10d7-110">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e10d7-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="e10d7-111">Giriş eklentisi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e10d7-111">Configure input plugin</span></span>

<span data-ttu-id="e10d7-112">Günlük analizi toocollect JSON verilerde ekleme `oms.api.` giriş eklentisi FluentD etiketinde toohello başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="e10d7-112">toocollect JSON data in Log Analytics, add `oms.api.` toohello start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="e10d7-113">Örneğin, aşağıdaki ayrı yapılandırma dosyası `exec-json.conf` içinde `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="e10d7-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="e10d7-114">Bu hello FluentD eklentisi kullanır `exec` toorun curl komutunu her 30 saniyede.</span><span class="sxs-lookup"><span data-stu-id="e10d7-114">This uses hello FluentD plugin `exec` toorun a curl command every 30 seconds.</span></span>  <span data-ttu-id="e10d7-115">Bu komutun çıktısı Hello hello JSON çıkış eklenti tarafından toplanır.</span><span class="sxs-lookup"><span data-stu-id="e10d7-115">hello output from this command is collected by hello JSON output plugin.</span></span>

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
<span data-ttu-id="e10d7-116">Merhaba yapılandırma dosyası altında eklenen `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` sahipliğini komutu aşağıdaki hello ile değiştirilen toohave gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e10d7-116">hello configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require toohave its ownership changed with hello following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="e10d7-117">Çıktı eklentisi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e10d7-117">Configure output plugin</span></span> 
<span data-ttu-id="e10d7-118">Çıktı eklentisi yapılandırma toohello ana yapılandırmasında aşağıdaki hello eklemek `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ya da ayrı yapılandırma dosyası yerleştirilen gibi`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="e10d7-118">Add hello following output plugin configuration toohello main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

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

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="e10d7-119">Linux için OMS aracıyı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="e10d7-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="e10d7-120">Merhaba OMS Aracısı Linux hizmeti için komutu aşağıdaki hello ile yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e10d7-120">Restart hello OMS Agent for Linux service with hello following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="e10d7-121">Çıktı</span><span class="sxs-lookup"><span data-stu-id="e10d7-121">Output</span></span>
<span data-ttu-id="e10d7-122">Merhaba veri toplanacak günlük analizi kayıt türü `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="e10d7-122">hello data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="e10d7-123">Örneğin, özel etiket hello `tag oms.api.tomcat` kayıt türüne sahip günlük analytics'te `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="e10d7-123">For example, hello custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="e10d7-124">Bu türdeki tüm kayıtları günlük arama aşağıdaki hello ile alınamadı.</span><span class="sxs-lookup"><span data-stu-id="e10d7-124">You could retrieve all records of this type with hello following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="e10d7-125">İç içe JSON veri kaynakları desteklenir, ancak dizini üst alanı dışına temel.</span><span class="sxs-lookup"><span data-stu-id="e10d7-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="e10d7-126">Örneğin, JSON verilerini aşağıdaki hello bir günlük analizi aramadan döndürülür `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="e10d7-126">For example, hello following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="e10d7-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e10d7-127">Next steps</span></span>
* <span data-ttu-id="e10d7-128">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.</span><span class="sxs-lookup"><span data-stu-id="e10d7-128">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
 