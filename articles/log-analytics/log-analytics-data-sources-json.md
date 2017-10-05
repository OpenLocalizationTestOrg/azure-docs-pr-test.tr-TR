---
title: "OMS günlük analizi özel JSON verileri toplama | Microsoft Docs"
description: "Özel JSON veri kaynakları için Linux OMS Aracısı'nı kullanarak günlük analizi içine toplanabilir.  Bu özel veri kaynaklarının basit betik dosyalarını curl veya FluentD'ın 300 + eklentileri gibi JSON döndürüyor olabilir. Bu makalede, bu veri koleksiyonu için gerekli yapılandırmayı açıklar."
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
ms.openlocfilehash: 800ee1269556e7c2d56fbbf2b497c10509b5c78c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="4ee78-105">Günlük analizi Linux için OMS aracısının özel JSON veri kaynaklarıyla toplama</span><span class="sxs-lookup"><span data-stu-id="4ee78-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="4ee78-106">Özel JSON veri kaynakları için Linux OMS Aracısı'nı kullanarak günlük analizi içine toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="4ee78-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="4ee78-107">Bu özel veri kaynaklarının JSON gibi döndüren basit betik dosyalarını olabilir [curl](https://curl.haxx.se/) veya biri [FluentD'ın 300 + eklentileri](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="4ee78-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="4ee78-108">Bu makalede, bu veri koleksiyonu için gerekli yapılandırmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="4ee78-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="4ee78-109">Linux v1.1.0 için OMS aracısının-217 + özel JSON verileri için gerekli</span><span class="sxs-lookup"><span data-stu-id="4ee78-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="4ee78-110">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4ee78-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="4ee78-111">Giriş eklentisi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4ee78-111">Configure input plugin</span></span>

<span data-ttu-id="4ee78-112">Günlük analizi JSON verileri toplamak için ekleme `oms.api.` giriş eklentisi FluentD etiketinde başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="4ee78-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="4ee78-113">Örneğin, aşağıdaki ayrı yapılandırma dosyası `exec-json.conf` içinde `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="4ee78-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="4ee78-114">Bu FluentD eklentisi kullanır `exec` her 30 saniyede bir curl komutunu çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="4ee78-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="4ee78-115">Bu komutun çıktısı, JSON çıkış eklenti tarafından toplanır.</span><span class="sxs-lookup"><span data-stu-id="4ee78-115">The output from this command is collected by the JSON output plugin.</span></span>

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
<span data-ttu-id="4ee78-116">Yapılandırma dosyası altında eklenen `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` aşağıdaki komutla değiştirilen sahipliğini olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4ee78-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="4ee78-117">Çıktı eklentisi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4ee78-117">Configure output plugin</span></span> 
<span data-ttu-id="4ee78-118">Ana yapılandırmasında aşağıdaki çıktı eklentisi yapılandırma eklemek `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` ya da ayrı yapılandırma dosyası yerleştirilen gibi`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="4ee78-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

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

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="4ee78-119">Linux için OMS aracıyı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="4ee78-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="4ee78-120">OMS aracısı aşağıdaki komutla Linux hizmeti yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="4ee78-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="4ee78-121">Çıktı</span><span class="sxs-lookup"><span data-stu-id="4ee78-121">Output</span></span>
<span data-ttu-id="4ee78-122">Verileri bir kayıt türü ile günlük analizi toplanacağını `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="4ee78-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="4ee78-123">Örneğin, özel etiket `tag oms.api.tomcat` kayıt türüne sahip günlük analytics'te `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="4ee78-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="4ee78-124">Aşağıdaki günlük arama ile bu türdeki tüm kayıtları alınamadı.</span><span class="sxs-lookup"><span data-stu-id="4ee78-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="4ee78-125">İç içe JSON veri kaynakları desteklenir, ancak dizini üst alanı dışına temel.</span><span class="sxs-lookup"><span data-stu-id="4ee78-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="4ee78-126">Örneğin, aşağıdaki JSON verilerini bir günlük analizi aramadan döndürülen `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="4ee78-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="4ee78-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ee78-127">Next steps</span></span>
* <span data-ttu-id="4ee78-128">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) veri kaynakları ve çözümleri toplanan verileri çözümlemek için.</span><span class="sxs-lookup"><span data-stu-id="4ee78-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 