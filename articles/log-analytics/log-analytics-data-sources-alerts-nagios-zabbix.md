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
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="87ee3-105">Linux için Nagios ve günlük analizi OMS aracısından Zabbix uyarılarını Topla</span><span class="sxs-lookup"><span data-stu-id="87ee3-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="87ee3-106">[Nagios](https://www.nagios.org/) ve [Zabbix](http://www.zabbix.com/) olan açık kaynak izleme araçları.</span><span class="sxs-lookup"><span data-stu-id="87ee3-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="87ee3-107">Toplama uyarıları bu Araçları'ndan günlük analizi sipariş tooanalyze bunları ile birlikte [diğer kaynaklardan uyarıları](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="87ee3-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="87ee3-108">Bu makalede, Linux toocollect tooconfigure Merhaba OMS Aracısı bu sistemlerden nasıl uyarıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="87ee3-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="87ee3-109">Uyarı koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="87ee3-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="87ee3-110">Nagios uyarı koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="87ee3-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="87ee3-111">Merhaba hello Nagios sunucu toocollect uyarıları üzerinde aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="87ee3-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="87ee3-112">GRANT hello kullanıcı **omsagent** okuma erişimi toohello Nagios günlük dosyası (yani `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="87ee3-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="87ee3-113">Merhaba nagios.log dosya hello grupla ait olduğu varsayılarak `nagios`, hello kullanıcı ekleyebilir **omsagent** toohello **nagios** grubu.</span><span class="sxs-lookup"><span data-stu-id="87ee3-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="87ee3-114">sudo usermod - a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="87ee3-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="87ee3-115">Merhaba yapılandırma dosyasını değiştirme (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="87ee3-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="87ee3-116">Mevcut ve kullanıma açıklamalı girişleri aşağıdaki hello çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="87ee3-116">Ensure hello following entries are present and not commented out:</span></span>  

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

3. <span data-ttu-id="87ee3-117">Merhaba omsagent arka plan programı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="87ee3-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="87ee3-118">Zabbix uyarı koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="87ee3-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="87ee3-119">Zabbix sunucusundan toocollect uyarıları, gereksinim duyduğunuz toospecify bir kullanıcıyı ve parolayı *açık metin*.</span><span class="sxs-lookup"><span data-stu-id="87ee3-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="87ee3-120">Bu ideal değildir, ancak hello kullanıcı oluşturun ve izinleri toomonitor onlu vermek öneririz.</span><span class="sxs-lookup"><span data-stu-id="87ee3-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="87ee3-121">Merhaba hello Nagios sunucu toocollect uyarıları üzerinde aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="87ee3-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="87ee3-122">Merhaba yapılandırma dosyasını değiştirme (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="87ee3-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="87ee3-123">Mevcut ve kullanıma açıklamalı girişleri aşağıdaki hello olduğundan emin olun.  Zabbix ortamınız için Hello kullanıcı adı ve parola toovalues değiştirin.</span><span class="sxs-lookup"><span data-stu-id="87ee3-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="87ee3-124">Merhaba omsagent arka plan programı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="87ee3-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="87ee3-125">sudo Paylaş /opt/microsoft/omsagent/bin/service_control yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="87ee3-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="87ee3-126">Uyarı kaydeder</span><span class="sxs-lookup"><span data-stu-id="87ee3-126">Alert records</span></span>
<span data-ttu-id="87ee3-127">Nagios ve Zabbix uyarı kayıtları almak kullanarak [oturum aramaları](log-analytics-log-searches.md) günlük analizi içinde.</span><span class="sxs-lookup"><span data-stu-id="87ee3-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="87ee3-128">Nagios uyarı kaydeder</span><span class="sxs-lookup"><span data-stu-id="87ee3-128">Nagios Alert records</span></span>

<span data-ttu-id="87ee3-129">Nagios tarafından toplanan kayıtları uyarı bir **türü** , **uyarı** ve **SourceSystem** , **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="87ee3-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="87ee3-130">Bunlar, aşağıdaki tablonun hello hello özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="87ee3-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="87ee3-131">Özellik</span><span class="sxs-lookup"><span data-stu-id="87ee3-131">Property</span></span> | <span data-ttu-id="87ee3-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ee3-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="87ee3-133">Tür</span><span class="sxs-lookup"><span data-stu-id="87ee3-133">Type</span></span> |<span data-ttu-id="87ee3-134">*Uyarı*</span><span class="sxs-lookup"><span data-stu-id="87ee3-134">*Alert*</span></span> |
| <span data-ttu-id="87ee3-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="87ee3-135">SourceSystem</span></span> |<span data-ttu-id="87ee3-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="87ee3-136">*Nagios*</span></span> |
| <span data-ttu-id="87ee3-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="87ee3-137">AlertName</span></span> |<span data-ttu-id="87ee3-138">Merhaba uyarı adı.</span><span class="sxs-lookup"><span data-stu-id="87ee3-138">Name of hello alert.</span></span> |
| <span data-ttu-id="87ee3-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="87ee3-139">AlertDescription</span></span> | <span data-ttu-id="87ee3-140">Merhaba uyarı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="87ee3-140">Description of hello alert.</span></span> |
| <span data-ttu-id="87ee3-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="87ee3-141">AlertState</span></span> | <span data-ttu-id="87ee3-142">Merhaba hizmet veya ana bilgisayar durumu.</span><span class="sxs-lookup"><span data-stu-id="87ee3-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="87ee3-143">TAMAM</span><span class="sxs-lookup"><span data-stu-id="87ee3-143">OK</span></span><br><span data-ttu-id="87ee3-144">UYARI</span><span class="sxs-lookup"><span data-stu-id="87ee3-144">WARNING</span></span><br><span data-ttu-id="87ee3-145">AYARLAMA</span><span class="sxs-lookup"><span data-stu-id="87ee3-145">UP</span></span><br><span data-ttu-id="87ee3-146">AŞAĞI</span><span class="sxs-lookup"><span data-stu-id="87ee3-146">DOWN</span></span> |
| <span data-ttu-id="87ee3-147">Ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="87ee3-147">HostName</span></span> | <span data-ttu-id="87ee3-148">Merhaba uyarı oluşturulan hello ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="87ee3-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="87ee3-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="87ee3-149">PriorityNumber</span></span> | <span data-ttu-id="87ee3-150">Merhaba uyarı öncelik düzeyi.</span><span class="sxs-lookup"><span data-stu-id="87ee3-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="87ee3-151">StateType</span><span class="sxs-lookup"><span data-stu-id="87ee3-151">StateType</span></span> | <span data-ttu-id="87ee3-152">Merhaba uyarının durumunu Hello türü.</span><span class="sxs-lookup"><span data-stu-id="87ee3-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="87ee3-153">SOFT - değil yeniden sorun.</span><span class="sxs-lookup"><span data-stu-id="87ee3-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="87ee3-154">Sabit - bırakıldı sorunu belirtilen kaç kez yeniden.</span><span class="sxs-lookup"><span data-stu-id="87ee3-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="87ee3-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="87ee3-155">TimeGenerated</span></span> |<span data-ttu-id="87ee3-156">Tarih ve saat hello uyarı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="87ee3-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="87ee3-157">Zabbix uyarı kaydeder</span><span class="sxs-lookup"><span data-stu-id="87ee3-157">Zabbix alert records</span></span>
<span data-ttu-id="87ee3-158">Zabbix tarafından toplanan kayıtları uyarı bir **türü** , **uyarı** ve **SourceSystem** , **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="87ee3-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="87ee3-159">Bunlar, aşağıdaki tablonun hello hello özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="87ee3-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="87ee3-160">Özellik</span><span class="sxs-lookup"><span data-stu-id="87ee3-160">Property</span></span> | <span data-ttu-id="87ee3-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87ee3-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="87ee3-162">Tür</span><span class="sxs-lookup"><span data-stu-id="87ee3-162">Type</span></span> |<span data-ttu-id="87ee3-163">*Uyarı*</span><span class="sxs-lookup"><span data-stu-id="87ee3-163">*Alert*</span></span> |
| <span data-ttu-id="87ee3-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="87ee3-164">SourceSystem</span></span> |<span data-ttu-id="87ee3-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="87ee3-165">*Zabbix*</span></span> |
| <span data-ttu-id="87ee3-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="87ee3-166">AlertName</span></span> | <span data-ttu-id="87ee3-167">Merhaba uyarı adı.</span><span class="sxs-lookup"><span data-stu-id="87ee3-167">Name of hello alert.</span></span> |
| <span data-ttu-id="87ee3-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="87ee3-168">AlertPriority</span></span> | <span data-ttu-id="87ee3-169">Uyarının önem derecesini hello.</span><span class="sxs-lookup"><span data-stu-id="87ee3-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="87ee3-170">Sınıflandırılmamış</span><span class="sxs-lookup"><span data-stu-id="87ee3-170">not classified</span></span><br><span data-ttu-id="87ee3-171">Bilgi</span><span class="sxs-lookup"><span data-stu-id="87ee3-171">information</span></span><br><span data-ttu-id="87ee3-172">Uyarı</span><span class="sxs-lookup"><span data-stu-id="87ee3-172">warning</span></span><br><span data-ttu-id="87ee3-173">Ortalama</span><span class="sxs-lookup"><span data-stu-id="87ee3-173">average</span></span><br><span data-ttu-id="87ee3-174">Yüksek</span><span class="sxs-lookup"><span data-stu-id="87ee3-174">high</span></span><br><span data-ttu-id="87ee3-175">Olağanüstü durum</span><span class="sxs-lookup"><span data-stu-id="87ee3-175">disaster</span></span>  |
| <span data-ttu-id="87ee3-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="87ee3-176">AlertState</span></span> | <span data-ttu-id="87ee3-177">Merhaba uyarı durumu.</span><span class="sxs-lookup"><span data-stu-id="87ee3-177">State of hello alert.</span></span><br><br><span data-ttu-id="87ee3-178">0 - toodate durumudur.</span><span class="sxs-lookup"><span data-stu-id="87ee3-178">0 - State is up toodate.</span></span><br><span data-ttu-id="87ee3-179">1 - durumu bilinmiyor.</span><span class="sxs-lookup"><span data-stu-id="87ee3-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="87ee3-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="87ee3-180">AlertTypeNumber</span></span> | <span data-ttu-id="87ee3-181">Uyarı birden çok sorun Olay Oluştur olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="87ee3-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="87ee3-182">0 - toodate durumudur.</span><span class="sxs-lookup"><span data-stu-id="87ee3-182">0 - State is up toodate.</span></span><br><span data-ttu-id="87ee3-183">1 - durumu bilinmiyor.</span><span class="sxs-lookup"><span data-stu-id="87ee3-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="87ee3-184">Yorumlar</span><span class="sxs-lookup"><span data-stu-id="87ee3-184">Comments</span></span> | <span data-ttu-id="87ee3-185">Ek açıklamalar uyarı için.</span><span class="sxs-lookup"><span data-stu-id="87ee3-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="87ee3-186">Ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="87ee3-186">HostName</span></span> | <span data-ttu-id="87ee3-187">Merhaba uyarı oluşturulan hello ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="87ee3-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="87ee3-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="87ee3-188">PriorityNumber</span></span> | <span data-ttu-id="87ee3-189">Merhaba uyarının önem derecesini belirten değer.</span><span class="sxs-lookup"><span data-stu-id="87ee3-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="87ee3-190">0 - Sınıflandırılmamış</span><span class="sxs-lookup"><span data-stu-id="87ee3-190">0 - not classified</span></span><br><span data-ttu-id="87ee3-191">1 - bilgileri</span><span class="sxs-lookup"><span data-stu-id="87ee3-191">1 - information</span></span><br><span data-ttu-id="87ee3-192">2 - uyarı</span><span class="sxs-lookup"><span data-stu-id="87ee3-192">2 - warning</span></span><br><span data-ttu-id="87ee3-193">3 - ortalama</span><span class="sxs-lookup"><span data-stu-id="87ee3-193">3 - average</span></span><br><span data-ttu-id="87ee3-194">4 - yüksek</span><span class="sxs-lookup"><span data-stu-id="87ee3-194">4 - high</span></span><br><span data-ttu-id="87ee3-195">5 - olağanüstü durum</span><span class="sxs-lookup"><span data-stu-id="87ee3-195">5 - disaster</span></span> |
| <span data-ttu-id="87ee3-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="87ee3-196">TimeGenerated</span></span> |<span data-ttu-id="87ee3-197">Tarih ve saat hello uyarı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="87ee3-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="87ee3-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="87ee3-198">TimeLastModified</span></span> |<span data-ttu-id="87ee3-199">Tarih ve saat hello durumu hello uyarının son değişti.</span><span class="sxs-lookup"><span data-stu-id="87ee3-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="87ee3-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="87ee3-200">Next steps</span></span>
* <span data-ttu-id="87ee3-201">Hakkında bilgi edinin [uyarıları](log-analytics-alerts.md) günlük analizi içinde.</span><span class="sxs-lookup"><span data-stu-id="87ee3-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="87ee3-202">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.</span><span class="sxs-lookup"><span data-stu-id="87ee3-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
