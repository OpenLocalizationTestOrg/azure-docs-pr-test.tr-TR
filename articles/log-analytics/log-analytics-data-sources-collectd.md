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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="0583b-104">Veri günlük analizi Linux aracıları CollectD Topla</span><span class="sxs-lookup"><span data-stu-id="0583b-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="0583b-105">[CollectD](https://collectd.org/) uygulamaları ve sistem düzeyi bilgileri düzenli aralıklarla performans ölçümleri toplayan bir açık kaynak Linux arka plan programı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0583b-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="0583b-106">Örnek uygulamalar hello Java sanal makine (JVM), MySQL Server ve Nginx içerir.</span><span class="sxs-lookup"><span data-stu-id="0583b-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="0583b-107">Bu makalede günlük analizi CollectD gelen performans verileri toplama hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0583b-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="0583b-108">Kullanılabilen eklentileri tam listesi bulunabilir [tablo, eklenti](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="0583b-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![CollectD genel bakış](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="0583b-110">Merhaba aşağıdaki CollectD yapılandırma hello OMS Aracısı Linux tooroute CollectD veri toohello OMS aracısı için Linux için dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0583b-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="0583b-111">Ayrıca, yapılandırma bunun yerine aşağıdaki hello 5.5 kullanmadan önce bir collectD sürümleri kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="0583b-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="0583b-112">Merhaba CollectD yapılandırmasını kullanan hello varsayılan`write_http` eklentisi toosend performans ölçüm verilerini bağlantı noktası 26000 tooOMS Linux Aracısı üzerinden.</span><span class="sxs-lookup"><span data-stu-id="0583b-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="0583b-113">Gerekirse, bu bağlantı noktası özel tanımlı yapılandırılmış tooa bağlantı noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="0583b-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="0583b-114">Hello Linux için OMS aracısı ayrıca CollectD ölçümünün 26000 numaralı bağlantı noktasında dinler ve bunları tooOMS şema ölçümleri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0583b-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="0583b-115">Merhaba Linux yapılandırması için OMS aracısının hello aşağıdadır `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="0583b-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="0583b-116">Desteklenen sürümleri</span><span class="sxs-lookup"><span data-stu-id="0583b-116">Versions supported</span></span>
- <span data-ttu-id="0583b-117">Günlük analizi, şu anda CollectD sürüm 4.8 destekler ve üstü.</span><span class="sxs-lookup"><span data-stu-id="0583b-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="0583b-118">Yukarıdaki veya Linux v1.1.0-217 için OMS aracısının CollectD ölçüm koleksiyonu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0583b-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="0583b-119">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0583b-119">Configuration</span></span>
<span data-ttu-id="0583b-120">Merhaba, temel adımlar tooconfigure günlük analizi CollectD veri koleksiyonunu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0583b-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="0583b-121">CollectD toosend veri toohello OMS Aracısı hello write_http eklentisi kullanarak Linux için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0583b-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="0583b-122">Linux toolisten hello CollectD veri için OMS aracısının Merhaba hello uygun bağlantı noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0583b-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="0583b-123">CollectD ve Linux için OMS aracısı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0583b-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="0583b-124">CollectD tooforward verileri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0583b-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="0583b-125">tooroute CollectD veri toohello Linux için OMS aracısının `oms.conf` gereksinimlerini toobe eklenen tooCollectD'ın yapılandırma dizini.</span><span class="sxs-lookup"><span data-stu-id="0583b-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="0583b-126">Bu dosyanın Hello hedef üzerinde makinenizin hello Linux distro bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0583b-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="0583b-127">CollectD yapılandırma dizininize /etc/collectd.d/ içinde yer alıyorsa:</span><span class="sxs-lookup"><span data-stu-id="0583b-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="0583b-128">CollectD yapılandırma dizininize /etc/collectd/collectd.conf.d/ içinde yer alıyorsa:</span><span class="sxs-lookup"><span data-stu-id="0583b-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="0583b-129">5.5 önce CollectD sürümleri için toomodify hello etiketleri gerekir `oms.conf` yukarıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="0583b-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="0583b-130">Collectd.conf istenen toohello Workspace'in omsagent yapılandırma dizini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0583b-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="0583b-131">Linux için CollectD ve OMS Aracısı komutları aşağıdaki hello ile yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0583b-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="0583b-132">sudo hizmet collectd yeniden sudo /opt/microsoft/omsagent/bin/service_control yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="0583b-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="0583b-133">CollectD ölçümleri tooLog Analytics şema dönüştürme</span><span class="sxs-lookup"><span data-stu-id="0583b-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="0583b-134">toomaintain bilinen bir model zaten Linux ve hello yeni ölçümler OMS aracısı tarafından toplanan altyapı ölçümler arasında şema eşleme aşağıdaki hello kullanılan CollectD tarafından toplanan:</span><span class="sxs-lookup"><span data-stu-id="0583b-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="0583b-135">CollectD ölçüm alan</span><span class="sxs-lookup"><span data-stu-id="0583b-135">CollectD Metric field</span></span> | <span data-ttu-id="0583b-136">Günlük analizi alan</span><span class="sxs-lookup"><span data-stu-id="0583b-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="0583b-137">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="0583b-137">host</span></span> | <span data-ttu-id="0583b-138">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="0583b-138">Computer</span></span> |
| <span data-ttu-id="0583b-139">Eklentisi</span><span class="sxs-lookup"><span data-stu-id="0583b-139">plugin</span></span> | <span data-ttu-id="0583b-140">None</span><span class="sxs-lookup"><span data-stu-id="0583b-140">None</span></span> |
| <span data-ttu-id="0583b-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="0583b-141">plugin_instance</span></span> | <span data-ttu-id="0583b-142">Örnek adı</span><span class="sxs-lookup"><span data-stu-id="0583b-142">Instance Name</span></span><br><span data-ttu-id="0583b-143">Varsa **plugin_instance** olan *null* sonra InstanceName = "*_Total*"</span><span class="sxs-lookup"><span data-stu-id="0583b-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="0583b-144">type</span><span class="sxs-lookup"><span data-stu-id="0583b-144">type</span></span> | <span data-ttu-id="0583b-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="0583b-145">ObjectName</span></span> |
| <span data-ttu-id="0583b-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="0583b-146">type_instance</span></span> | <span data-ttu-id="0583b-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="0583b-147">CounterName</span></span><br><span data-ttu-id="0583b-148">Varsa **type_instance** olan *null* sonra CounterName =**boş**</span><span class="sxs-lookup"><span data-stu-id="0583b-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="0583b-149">dsnames]</span><span class="sxs-lookup"><span data-stu-id="0583b-149">dsnames[]</span></span> | <span data-ttu-id="0583b-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="0583b-150">CounterName</span></span> |
| <span data-ttu-id="0583b-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="0583b-151">dstypes</span></span> | <span data-ttu-id="0583b-152">None</span><span class="sxs-lookup"><span data-stu-id="0583b-152">None</span></span> |
| <span data-ttu-id="0583b-153">değerler]</span><span class="sxs-lookup"><span data-stu-id="0583b-153">values[]</span></span> | <span data-ttu-id="0583b-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="0583b-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0583b-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0583b-155">Next steps</span></span>
* <span data-ttu-id="0583b-156">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.</span><span class="sxs-lookup"><span data-stu-id="0583b-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="0583b-157">Kullanım [özel alanlar](log-analytics-custom-fields.md) syslog kayıtları tek tek alanlara tooparse verileri.</span><span class="sxs-lookup"><span data-stu-id="0583b-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

