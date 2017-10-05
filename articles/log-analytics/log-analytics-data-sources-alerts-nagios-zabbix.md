---
title: "OMS günlük analizi Nagios ve Zabbix uyarıları Topla | Microsoft Docs"
description: "Nagios ve Zabbix izleme araçları açık kaynaktır. Bunları yanı sıra diğer kaynaklardan uyarıları çözümlemek amacıyla yararlı günlük analizi bu Araçları'ndan uyarıları toplayabilirsiniz.  Bu makalede, bu sistemlerden uyarılarını toplamak Linux için OMS aracısının yapılandırma açıklar."
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="cf185-105">Linux için Nagios ve günlük analizi OMS aracısından Zabbix uyarılarını Topla</span><span class="sxs-lookup"><span data-stu-id="cf185-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="cf185-106">[Nagios](https://www.nagios.org/) ve [Zabbix](http://www.zabbix.com/) olan açık kaynak izleme araçları.</span><span class="sxs-lookup"><span data-stu-id="cf185-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="cf185-107">Uyarıları bu Araçları'ndan günlük analizi ile birlikte çözümlemek için toplayabilirsiniz [diğer kaynaklardan uyarıları](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="cf185-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="cf185-108">Bu makalede, bu sistemlerden uyarılarını toplamak Linux için OMS aracısının yapılandırma açıklar.</span><span class="sxs-lookup"><span data-stu-id="cf185-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="cf185-109">Uyarı koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cf185-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="cf185-110">Nagios uyarı koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cf185-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="cf185-111">Uyarılarını toplamak için Nagios sunucusunda aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf185-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="cf185-112">Kullanıcının izni **omsagent** okuma erişimi Nagios günlük dosyasına (yani `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="cf185-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="cf185-113">Nagios.log dosya varsayılarak grupla sahibi `nagios`, kullanıcı ekleyebilir **omsagent** için **nagios** grubu.</span><span class="sxs-lookup"><span data-stu-id="cf185-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="cf185-114">sudo usermod - a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="cf185-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="cf185-115">Konumunda yapılandırma dosyasını değiştirme (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="cf185-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="cf185-116">Mevcut ve kullanıma açıklamalı aşağıdaki girdileri çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="cf185-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="cf185-117">Omsagent arka plan programı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="cf185-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="cf185-118">Zabbix uyarı koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cf185-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="cf185-119">Zabbix sunucudan uyarılarını toplamak için bir kullanıcı ve parola belirtmeniz gerekir *açık metin*.</span><span class="sxs-lookup"><span data-stu-id="cf185-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="cf185-120">Bu ideal değildir, ancak kullanıcı oluşturmak ve onlu izlemek için izinleri öneririz.</span><span class="sxs-lookup"><span data-stu-id="cf185-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="cf185-121">Uyarılarını toplamak için Nagios sunucusunda aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf185-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="cf185-122">Konumunda yapılandırma dosyasını değiştirme (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="cf185-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="cf185-123">Mevcut ve kullanıma açıklamalı aşağıdaki girdileri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cf185-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="cf185-124">Kullanıcı adı ve parola Zabbix ortamınız için değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cf185-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="cf185-125">Omsagent arka plan programı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="cf185-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="cf185-126">sudo Paylaş /opt/microsoft/omsagent/bin/service_control yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="cf185-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="cf185-127">Uyarı kaydeder</span><span class="sxs-lookup"><span data-stu-id="cf185-127">Alert records</span></span>
<span data-ttu-id="cf185-128">Nagios ve Zabbix uyarı kayıtları almak kullanarak [oturum aramaları](log-analytics-log-searches.md) günlük analizi içinde.</span><span class="sxs-lookup"><span data-stu-id="cf185-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="cf185-129">Nagios uyarı kaydeder</span><span class="sxs-lookup"><span data-stu-id="cf185-129">Nagios Alert records</span></span>

<span data-ttu-id="cf185-130">Nagios tarafından toplanan kayıtları uyarı bir **türü** , **uyarı** ve **SourceSystem** , **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="cf185-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="cf185-131">Aşağıdaki tabloda özellikleri sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="cf185-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="cf185-132">Özellik</span><span class="sxs-lookup"><span data-stu-id="cf185-132">Property</span></span> | <span data-ttu-id="cf185-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cf185-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cf185-134">Tür</span><span class="sxs-lookup"><span data-stu-id="cf185-134">Type</span></span> |<span data-ttu-id="cf185-135">*Uyarı*</span><span class="sxs-lookup"><span data-stu-id="cf185-135">*Alert*</span></span> |
| <span data-ttu-id="cf185-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="cf185-136">SourceSystem</span></span> |<span data-ttu-id="cf185-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="cf185-137">*Nagios*</span></span> |
| <span data-ttu-id="cf185-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="cf185-138">AlertName</span></span> |<span data-ttu-id="cf185-139">Uyarı adı.</span><span class="sxs-lookup"><span data-stu-id="cf185-139">Name of the alert.</span></span> |
| <span data-ttu-id="cf185-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="cf185-140">AlertDescription</span></span> | <span data-ttu-id="cf185-141">Uyarı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="cf185-141">Description of the alert.</span></span> |
| <span data-ttu-id="cf185-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="cf185-142">AlertState</span></span> | <span data-ttu-id="cf185-143">Hizmet veya ana bilgisayar durumu.</span><span class="sxs-lookup"><span data-stu-id="cf185-143">Status of the service or host.</span></span><br><br><span data-ttu-id="cf185-144">TAMAM</span><span class="sxs-lookup"><span data-stu-id="cf185-144">OK</span></span><br><span data-ttu-id="cf185-145">UYARI</span><span class="sxs-lookup"><span data-stu-id="cf185-145">WARNING</span></span><br><span data-ttu-id="cf185-146">AYARLAMA</span><span class="sxs-lookup"><span data-stu-id="cf185-146">UP</span></span><br><span data-ttu-id="cf185-147">AŞAĞI</span><span class="sxs-lookup"><span data-stu-id="cf185-147">DOWN</span></span> |
| <span data-ttu-id="cf185-148">Ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="cf185-148">HostName</span></span> | <span data-ttu-id="cf185-149">Uyarı oluşturan ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="cf185-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="cf185-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="cf185-150">PriorityNumber</span></span> | <span data-ttu-id="cf185-151">Uyarı öncelik düzeyi.</span><span class="sxs-lookup"><span data-stu-id="cf185-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="cf185-152">StateType</span><span class="sxs-lookup"><span data-stu-id="cf185-152">StateType</span></span> | <span data-ttu-id="cf185-153">Uyarının durumunu türü.</span><span class="sxs-lookup"><span data-stu-id="cf185-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="cf185-154">SOFT - değil yeniden sorun.</span><span class="sxs-lookup"><span data-stu-id="cf185-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="cf185-155">Sabit - bırakıldı sorunu belirtilen kaç kez yeniden.</span><span class="sxs-lookup"><span data-stu-id="cf185-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="cf185-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="cf185-156">TimeGenerated</span></span> |<span data-ttu-id="cf185-157">Uyarının oluşturulduğu tarih ve saat.</span><span class="sxs-lookup"><span data-stu-id="cf185-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="cf185-158">Zabbix uyarı kaydeder</span><span class="sxs-lookup"><span data-stu-id="cf185-158">Zabbix alert records</span></span>
<span data-ttu-id="cf185-159">Zabbix tarafından toplanan kayıtları uyarı bir **türü** , **uyarı** ve **SourceSystem** , **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="cf185-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="cf185-160">Aşağıdaki tabloda özellikleri sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="cf185-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="cf185-161">Özellik</span><span class="sxs-lookup"><span data-stu-id="cf185-161">Property</span></span> | <span data-ttu-id="cf185-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cf185-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cf185-163">Tür</span><span class="sxs-lookup"><span data-stu-id="cf185-163">Type</span></span> |<span data-ttu-id="cf185-164">*Uyarı*</span><span class="sxs-lookup"><span data-stu-id="cf185-164">*Alert*</span></span> |
| <span data-ttu-id="cf185-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="cf185-165">SourceSystem</span></span> |<span data-ttu-id="cf185-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="cf185-166">*Zabbix*</span></span> |
| <span data-ttu-id="cf185-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="cf185-167">AlertName</span></span> | <span data-ttu-id="cf185-168">Uyarı adı.</span><span class="sxs-lookup"><span data-stu-id="cf185-168">Name of the alert.</span></span> |
| <span data-ttu-id="cf185-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="cf185-169">AlertPriority</span></span> | <span data-ttu-id="cf185-170">Uyarının önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="cf185-170">Severity of the alert.</span></span><br><br><span data-ttu-id="cf185-171">Sınıflandırılmamış</span><span class="sxs-lookup"><span data-stu-id="cf185-171">not classified</span></span><br><span data-ttu-id="cf185-172">Bilgi</span><span class="sxs-lookup"><span data-stu-id="cf185-172">information</span></span><br><span data-ttu-id="cf185-173">Uyarı</span><span class="sxs-lookup"><span data-stu-id="cf185-173">warning</span></span><br><span data-ttu-id="cf185-174">Ortalama</span><span class="sxs-lookup"><span data-stu-id="cf185-174">average</span></span><br><span data-ttu-id="cf185-175">Yüksek</span><span class="sxs-lookup"><span data-stu-id="cf185-175">high</span></span><br><span data-ttu-id="cf185-176">Olağanüstü durum</span><span class="sxs-lookup"><span data-stu-id="cf185-176">disaster</span></span>  |
| <span data-ttu-id="cf185-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="cf185-177">AlertState</span></span> | <span data-ttu-id="cf185-178">Uyarı durumu.</span><span class="sxs-lookup"><span data-stu-id="cf185-178">State of the alert.</span></span><br><br><span data-ttu-id="cf185-179">0 - durumu güncel değil.</span><span class="sxs-lookup"><span data-stu-id="cf185-179">0 - State is up to date.</span></span><br><span data-ttu-id="cf185-180">1 - durumu bilinmiyor.</span><span class="sxs-lookup"><span data-stu-id="cf185-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="cf185-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="cf185-181">AlertTypeNumber</span></span> | <span data-ttu-id="cf185-182">Uyarı birden çok sorun Olay Oluştur olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cf185-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="cf185-183">0 - durumu güncel değil.</span><span class="sxs-lookup"><span data-stu-id="cf185-183">0 - State is up to date.</span></span><br><span data-ttu-id="cf185-184">1 - durumu bilinmiyor.</span><span class="sxs-lookup"><span data-stu-id="cf185-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="cf185-185">Yorumlar</span><span class="sxs-lookup"><span data-stu-id="cf185-185">Comments</span></span> | <span data-ttu-id="cf185-186">Ek açıklamalar uyarı için.</span><span class="sxs-lookup"><span data-stu-id="cf185-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="cf185-187">Ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="cf185-187">HostName</span></span> | <span data-ttu-id="cf185-188">Uyarı oluşturan ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="cf185-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="cf185-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="cf185-189">PriorityNumber</span></span> | <span data-ttu-id="cf185-190">Uyarının önem derecesini belirten değer.</span><span class="sxs-lookup"><span data-stu-id="cf185-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="cf185-191">0 - Sınıflandırılmamış</span><span class="sxs-lookup"><span data-stu-id="cf185-191">0 - not classified</span></span><br><span data-ttu-id="cf185-192">1 - bilgileri</span><span class="sxs-lookup"><span data-stu-id="cf185-192">1 - information</span></span><br><span data-ttu-id="cf185-193">2 - uyarı</span><span class="sxs-lookup"><span data-stu-id="cf185-193">2 - warning</span></span><br><span data-ttu-id="cf185-194">3 - ortalama</span><span class="sxs-lookup"><span data-stu-id="cf185-194">3 - average</span></span><br><span data-ttu-id="cf185-195">4 - yüksek</span><span class="sxs-lookup"><span data-stu-id="cf185-195">4 - high</span></span><br><span data-ttu-id="cf185-196">5 - olağanüstü durum</span><span class="sxs-lookup"><span data-stu-id="cf185-196">5 - disaster</span></span> |
| <span data-ttu-id="cf185-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="cf185-197">TimeGenerated</span></span> |<span data-ttu-id="cf185-198">Uyarının oluşturulduğu tarih ve saat.</span><span class="sxs-lookup"><span data-stu-id="cf185-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="cf185-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="cf185-199">TimeLastModified</span></span> |<span data-ttu-id="cf185-200">Tarih ve saat uyarının durumunu en son değiştirildiği.</span><span class="sxs-lookup"><span data-stu-id="cf185-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="cf185-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf185-201">Next steps</span></span>
* <span data-ttu-id="cf185-202">Hakkında bilgi edinin [uyarıları](log-analytics-alerts.md) günlük analizi içinde.</span><span class="sxs-lookup"><span data-stu-id="cf185-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="cf185-203">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) veri kaynakları ve çözümleri toplanan verileri çözümlemek için.</span><span class="sxs-lookup"><span data-stu-id="cf185-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
