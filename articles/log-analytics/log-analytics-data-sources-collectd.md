---
title: "OMS günlük analizi CollectD veri toplamak | Microsoft Docs"
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
ms.openlocfilehash: a63b15ca5126b45451f0694c9ee75d7b67b1ceaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="e4c4e-104">Veri günlük analizi Linux aracıları CollectD Topla</span><span class="sxs-lookup"><span data-stu-id="e4c4e-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="e4c4e-105">[CollectD](https://collectd.org/) uygulamaları ve sistem düzeyi bilgileri düzenli aralıklarla performans ölçümleri toplayan bir açık kaynak Linux arka plan programı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="e4c4e-106">Örnek uygulamalar, Java sanal makine (JVM), MySQL Server ve Nginx içerir.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="e4c4e-107">Bu makalede günlük analizi CollectD gelen performans verileri toplama hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="e4c4e-108">Kullanılabilen eklentileri tam listesi bulunabilir [tablo, eklenti](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="e4c4e-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![CollectD genel bakış](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="e4c4e-110">Aşağıdaki CollectD yapılandırma OMS Aracısı Linux için OMS aracısının rota CollectD verilere Linux için dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="e4c4e-111">Ayrıca, bunun yerine aşağıdaki yapılandırma 5.5 kullanmadan önce bir collectD sürümleri kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="e4c4e-112">Varsayılan CollectD yapılandırmasını kullanan`write_http` performans ölçüm verilerini 26000 bağlantı noktası üzerinden Linux için OMS Aracısı'na göndermek için eklenti.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="e4c4e-113">Gerekirse, bu bağlantı noktası özel tanımlı bir bağlantı noktası için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-113">This port can be configured to a custom-defined port if needed.</span></span>

<span data-ttu-id="e4c4e-114">Linux için OMS aracısının de CollectD ölçümünün 26000 numaralı bağlantı noktasında dinler ve bunları OMS şema ölçümlere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span></span> <span data-ttu-id="e4c4e-115">Linux yapılandırması için OMS aracısının aşağıdadır `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="e4c4e-116">Desteklenen sürümleri</span><span class="sxs-lookup"><span data-stu-id="e4c4e-116">Versions supported</span></span>
- <span data-ttu-id="e4c4e-117">Günlük analizi, şu anda CollectD sürüm 4.8 destekler ve üstü.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="e4c4e-118">Yukarıdaki veya Linux v1.1.0-217 için OMS aracısının CollectD ölçüm koleksiyonu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="e4c4e-119">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e4c4e-119">Configuration</span></span>
<span data-ttu-id="e4c4e-120">Günlük analizi CollectD veri koleksiyonunu yapılandırmak için temel adımlar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="e4c4e-121">OMS Aracısı write_http eklentisi kullanarak Linux veri göndermesini CollectD yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span></span>  
2. <span data-ttu-id="e4c4e-122">CollectD veri uygun bağlantı noktasında dinlemek Linux için OMS Aracısı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span></span>
3. <span data-ttu-id="e4c4e-123">CollectD ve Linux için OMS aracısı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-to-forward-data"></a><span data-ttu-id="e4c4e-124">Veri iletmek için CollectD yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e4c4e-124">Configure CollectD to forward data</span></span> 

1. <span data-ttu-id="e4c4e-125">Linux için OMS aracısının rota CollectD verilere `oms.conf` CollectD'ın yapılandırma dizinine eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span></span> <span data-ttu-id="e4c4e-126">Bu dosya hedef makinenizi Linux distro üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-126">The destination of this file depends on the Linux  distro of your machine.</span></span>

    <span data-ttu-id="e4c4e-127">CollectD yapılandırma dizininize /etc/collectd.d/ içinde yer alıyorsa:</span><span class="sxs-lookup"><span data-stu-id="e4c4e-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="e4c4e-128">CollectD yapılandırma dizininize /etc/collectd/collectd.conf.d/ içinde yer alıyorsa:</span><span class="sxs-lookup"><span data-stu-id="e4c4e-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="e4c4e-129">5.5 önce CollectD sürümleri için etiketleri değiştirmek zorunda kalacaksınız `oms.conf` yukarıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="e4c4e-130">Collectd.conf istenen Workspace'in omsagent yapılandırma dizinine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="e4c4e-131">Linux için CollectD ve OMS aracısı aşağıdaki komutlarla yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-131">Restart CollectD and OMS Agent for Linux with the following commands.</span></span>

    <span data-ttu-id="e4c4e-132">sudo hizmet collectd yeniden sudo /opt/microsoft/omsagent/bin/service_control yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="e4c4e-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-to-log-analytics-schema-conversion"></a><span data-ttu-id="e4c4e-133">Günlük analizi şema dönüştürme CollectD ölçümleri</span><span class="sxs-lookup"><span data-stu-id="e4c4e-133">CollectD metrics to Log Analytics schema conversion</span></span>
<span data-ttu-id="e4c4e-134">Bilinen bir model zaten Linux için OMS aracısı tarafından toplanan altyapı Ölçümler ve yeni ölçümler arasında aşağıdaki şema eşleme CollectD tarafından toplanan korumak için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="e4c4e-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span></span>

| <span data-ttu-id="e4c4e-135">CollectD ölçüm alan</span><span class="sxs-lookup"><span data-stu-id="e4c4e-135">CollectD Metric field</span></span> | <span data-ttu-id="e4c4e-136">Günlük analizi alan</span><span class="sxs-lookup"><span data-stu-id="e4c4e-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="e4c4e-137">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="e4c4e-137">host</span></span> | <span data-ttu-id="e4c4e-138">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="e4c4e-138">Computer</span></span> |
| <span data-ttu-id="e4c4e-139">Eklentisi</span><span class="sxs-lookup"><span data-stu-id="e4c4e-139">plugin</span></span> | <span data-ttu-id="e4c4e-140">None</span><span class="sxs-lookup"><span data-stu-id="e4c4e-140">None</span></span> |
| <span data-ttu-id="e4c4e-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="e4c4e-141">plugin_instance</span></span> | <span data-ttu-id="e4c4e-142">Örnek adı</span><span class="sxs-lookup"><span data-stu-id="e4c4e-142">Instance Name</span></span><br><span data-ttu-id="e4c4e-143">Varsa **plugin_instance** olan *null* sonra InstanceName = "*_Total*"</span><span class="sxs-lookup"><span data-stu-id="e4c4e-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="e4c4e-144">type</span><span class="sxs-lookup"><span data-stu-id="e4c4e-144">type</span></span> | <span data-ttu-id="e4c4e-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="e4c4e-145">ObjectName</span></span> |
| <span data-ttu-id="e4c4e-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="e4c4e-146">type_instance</span></span> | <span data-ttu-id="e4c4e-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="e4c4e-147">CounterName</span></span><br><span data-ttu-id="e4c4e-148">Varsa **type_instance** olan *null* sonra CounterName =**boş**</span><span class="sxs-lookup"><span data-stu-id="e4c4e-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="e4c4e-149">dsnames]</span><span class="sxs-lookup"><span data-stu-id="e4c4e-149">dsnames[]</span></span> | <span data-ttu-id="e4c4e-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="e4c4e-150">CounterName</span></span> |
| <span data-ttu-id="e4c4e-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="e4c4e-151">dstypes</span></span> | <span data-ttu-id="e4c4e-152">None</span><span class="sxs-lookup"><span data-stu-id="e4c4e-152">None</span></span> |
| <span data-ttu-id="e4c4e-153">değerler]</span><span class="sxs-lookup"><span data-stu-id="e4c4e-153">values[]</span></span> | <span data-ttu-id="e4c4e-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="e4c4e-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e4c4e-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4c4e-155">Next steps</span></span>
* <span data-ttu-id="e4c4e-156">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) veri kaynakları ve çözümleri toplanan verileri çözümlemek için.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="e4c4e-157">Kullanım [özel alanlar](log-analytics-custom-fields.md) tek tek alanlarına syslog kayıtları verilerden ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="e4c4e-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>

