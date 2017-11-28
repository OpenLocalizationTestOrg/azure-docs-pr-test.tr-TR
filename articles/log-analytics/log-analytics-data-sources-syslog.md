---
title: "Toplamak ve analiz etmek OMS günlük analizi Syslog iletileri | Microsoft Docs"
description: "Syslog Linux için ortak bir olay günlüğü protokolüdür. Bu makalede, Syslog iletileri koleksiyonu günlük analizi ve OMS depoya oluşturdukları kayıtları ayrıntılarını yapılandırmak açıklar."
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
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="91d0d-104">Syslog veri kaynaklarında günlük analizi</span><span class="sxs-lookup"><span data-stu-id="91d0d-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="91d0d-105">Syslog Linux için ortak bir olay günlüğü protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="91d0d-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="91d0d-106">Uygulamaları yerel makinede depolanan olabilir veya bir Syslog Toplayıcıya teslim iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="91d0d-107">Linux için OMS Aracısı yüklendiğinde, aracıya iletilerini iletmek için yerel Syslog arka plan programı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="91d0d-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="91d0d-108">Aracı bu durumda günlük karşılık gelen bir kayıt OMS depoya oluşturulduğu analizi iletiyi gönderir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="91d0d-109">Günlük analizi rsyslog varsayılan arka plan programı olduğu rsyslog veya syslog-ng tarafından gönderilen iletileri koleksiyonu destekler.</span><span class="sxs-lookup"><span data-stu-id="91d0d-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="91d0d-110">Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="91d0d-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="91d0d-111">Bu dağıtımları bu sürümünden Syslog verileri toplamak için [rsyslog arka plan programı](http://rsyslog.com) sysklog değiştirmek için yapılandırılmış ve yüklü gerekir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Syslog koleksiyonu](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="91d0d-113">Syslog yapılandırma</span><span class="sxs-lookup"><span data-stu-id="91d0d-113">Configuring Syslog</span></span>
<span data-ttu-id="91d0d-114">Linux için OMS aracısının yalnızca tesisler ve yapılandırmasıyla belirtilen önem derecelerine sahip olayları toplar.</span><span class="sxs-lookup"><span data-stu-id="91d0d-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="91d0d-115">OMS portalı üzerinden veya Linux aracıları yapılandırma dosyalarını yönetme tarafından Syslog yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91d0d-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="91d0d-116">Syslog OMS portalında yapılandırın</span><span class="sxs-lookup"><span data-stu-id="91d0d-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="91d0d-117">Syslog gelen yapılandırma [günlük analizi ayarları veri menüde](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="91d0d-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="91d0d-118">Bu yapılandırma her Linux Aracısı yapılandırma dosyasına teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="91d0d-119">Adını yazıp'yi tıklatarak yeni bir tesis ekleyebilirsiniz  **+** .</span><span class="sxs-lookup"><span data-stu-id="91d0d-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="91d0d-120">Her özelliği için yalnızca seçili önem derecelerine sahip iletileri toplanacaktır.</span><span class="sxs-lookup"><span data-stu-id="91d0d-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="91d0d-121">Toplamak istediğiniz belirli olanağı için önem derecelerine denetleyin.</span><span class="sxs-lookup"><span data-stu-id="91d0d-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="91d0d-122">İletileri Filtrele için herhangi bir ek ölçüt sağlayamaz.</span><span class="sxs-lookup"><span data-stu-id="91d0d-122">You cannot provide any additional criteria to filter messages.</span></span>

![Syslog yapılandırın](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="91d0d-124">Varsayılan olarak, tüm yapılandırma değişiklikleri otomatik olarak tüm aracıları için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="91d0d-125">Syslog her Linux Aracısı'nı el ile yapılandırmak istiyorsanız, kutunun işaretini *aşağıdaki yapılandırmayı Linux makinelerime Uygula*.</span><span class="sxs-lookup"><span data-stu-id="91d0d-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="91d0d-126">Syslog Linux Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="91d0d-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="91d0d-127">Zaman [OMS Aracısı Linux istemcide yüklü](log-analytics-linux-agents.md), tesis ve toplanan iletileri önemini tanımlayan bir varsayılan syslog yapılandırma dosyası yükler.</span><span class="sxs-lookup"><span data-stu-id="91d0d-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="91d0d-128">Yapılandırmasını değiştirmek için bu dosyayı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91d0d-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="91d0d-129">Yapılandırma dosyası, istemcinin yüklediği Syslog arka plan programı bağlı olarak farklıdır.</span><span class="sxs-lookup"><span data-stu-id="91d0d-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="91d0d-130">Syslog yapılandırma düzenlerseniz, syslog arka plan programı değişikliklerin etkili olması yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="91d0d-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="91d0d-131">rsyslog</span></span>
<span data-ttu-id="91d0d-132">Rsyslog yapılandırma dosyası şu konumdadır **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="91d0d-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="91d0d-133">Varsayılan içeriğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-133">Its default contents are shown below.</span></span>  <span data-ttu-id="91d0d-134">Bu, uyarı ya da daha yüksek bir düzeyinde tüm tesisler için yerel Aracısı'ndan gönderilen syslog iletileri toplar.</span><span class="sxs-lookup"><span data-stu-id="91d0d-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

<span data-ttu-id="91d0d-135">Yapılandırma dosyasının kendi bölümü kaldırarak bir tesis kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91d0d-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="91d0d-136">Bu tesis 's girdisini değiştirerek belirli olanağını toplanan önem derecelerine sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91d0d-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="91d0d-137">Örneğin, iletilere kullanıcı tesis hata veya daha büyük bir önem derecesi ile sınırlandırmak için aşağıdaki yapılandırma dosyasına satırını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="91d0d-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="91d0d-138">Syslog ng</span><span class="sxs-lookup"><span data-stu-id="91d0d-138">syslog-ng</span></span>
<span data-ttu-id="91d0d-139">Syslog ng için yapılandırma dosyası konumdadır **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="91d0d-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="91d0d-140">Varsayılan içeriğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-140">Its default contents are shown below.</span></span>  <span data-ttu-id="91d0d-141">Tüm Tesisler ve tüm önem dereceleridir için yerel Aracısı'ndan gönderilen syslog iletileri toplar.</span><span class="sxs-lookup"><span data-stu-id="91d0d-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="91d0d-142">Yapılandırma dosyasının kendi bölümü kaldırarak bir tesis kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91d0d-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="91d0d-143">Belirli bir özellik için listeden kaldırarak toplanır önem derecelerine sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91d0d-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="91d0d-144">Örneğin, yalnızca uyarı ve kritik iletileri için kullanıcı tesis sınırlamak için şu yapılandırma dosyasının bu bölümü değiştirin:</span><span class="sxs-lookup"><span data-stu-id="91d0d-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="91d0d-145">Ek Syslog bağlantı noktalarından verileri toplama</span><span class="sxs-lookup"><span data-stu-id="91d0d-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="91d0d-146">OMS Aracısı bağlantı noktası 25224 yerel istemcide Syslog iletileri dinler.</span><span class="sxs-lookup"><span data-stu-id="91d0d-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="91d0d-147">Aracıyı yüklediğinizde, varsayılan bir syslog yapılandırma uygulanır ve şu konumda bulunamadı:</span><span class="sxs-lookup"><span data-stu-id="91d0d-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="91d0d-148">Rsyslog:`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="91d0d-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="91d0d-149">Syslog-ng:`/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="91d0d-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="91d0d-150">Bağlantı noktası numarasını iki yapılandırma dosyası oluşturarak değiştirebilirsiniz: FluentD yapılandırma dosyası ve bir rsyslog veya syslog ng dosyası yüklediğiniz Syslog arka plan programı bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="91d0d-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="91d0d-151">FluentD yapılandırma dosyası bulunan yeni bir dosya olmalıdır: `/etc/opt/microsoft/omsagent/conf/omsagent.d` ve değeri değiştirin **bağlantı noktası** giriş, özel bir bağlantı noktası numarası.</span><span class="sxs-lookup"><span data-stu-id="91d0d-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* <span data-ttu-id="91d0d-152">Rsyslog için bulunan yeni bir yapılandırma dosyası oluşturmanız gerekir: `/etc/rsyslog.d/` ve % SYSLOG_PORT % değerini, özel bir bağlantı noktası numarasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="91d0d-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="91d0d-153">Yapılandırma dosyasında bu değeri değiştirirseniz, `95-omsagent.conf`, varsayılan bir yapılandırma aracının geçerli olduğu durumlarda üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="91d0d-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="91d0d-154">Aşağıda gösterilen örnek yapılandırma kopyalayarak syslog ng config değiştirilmemelidir ve özel değiştirilmiş ayarları syslog ng.conf yapılandırma dosyasının sonuna ekleme bulunan `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="91d0d-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="91d0d-155">Yapmak **değil** varsayılan etiket **% WORKSPACE_ID % _oms** veya **% WORKSPACE_ID_OMS**, yaptığınız değişiklikleri ayırt etmeye yardımcı olması için bir özel etiket tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="91d0d-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="91d0d-156">Yapılandırma dosyasındaki varsayılan değerleri değiştirirseniz, varsayılan bir yapılandırma aracının geçerli olduğu durumlarda bunların üzerine yazılacak.</span><span class="sxs-lookup"><span data-stu-id="91d0d-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="91d0d-157">Değişiklikler, Syslog ve OMS Aracısı'nı tamamladıktan sonra hizmet yapılandırma değişikliklerinin etkinleşmesi emin olmak için yeniden başlatılması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="91d0d-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="91d0d-158">Syslog kaydı Özellikler</span><span class="sxs-lookup"><span data-stu-id="91d0d-158">Syslog record properties</span></span>
<span data-ttu-id="91d0d-159">Syslog kayıtları sahip bir tür **Syslog** ve aşağıdaki tabloda özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="91d0d-160">Özellik</span><span class="sxs-lookup"><span data-stu-id="91d0d-160">Property</span></span> | <span data-ttu-id="91d0d-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="91d0d-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="91d0d-162">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="91d0d-162">Computer</span></span> |<span data-ttu-id="91d0d-163">Olay toplandığı bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="91d0d-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="91d0d-164">Tesis</span><span class="sxs-lookup"><span data-stu-id="91d0d-164">Facility</span></span> |<span data-ttu-id="91d0d-165">İleti oluşturulan sisteminin parçası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="91d0d-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="91d0d-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="91d0d-166">HostIP</span></span> |<span data-ttu-id="91d0d-167">İleti gönderilirken sistem IP adresi.</span><span class="sxs-lookup"><span data-stu-id="91d0d-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="91d0d-168">Ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="91d0d-168">HostName</span></span> |<span data-ttu-id="91d0d-169">İleti gönderilirken sistem adı.</span><span class="sxs-lookup"><span data-stu-id="91d0d-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="91d0d-170">Önem düzeyi</span><span class="sxs-lookup"><span data-stu-id="91d0d-170">SeverityLevel</span></span> |<span data-ttu-id="91d0d-171">Olay önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="91d0d-171">Severity level of the event.</span></span> |
| <span data-ttu-id="91d0d-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="91d0d-172">SyslogMessage</span></span> |<span data-ttu-id="91d0d-173">İleti metni.</span><span class="sxs-lookup"><span data-stu-id="91d0d-173">Text of the message.</span></span> |
| <span data-ttu-id="91d0d-174">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="91d0d-174">ProcessID</span></span> |<span data-ttu-id="91d0d-175">İleti oluşturulan işlemin kimliği.</span><span class="sxs-lookup"><span data-stu-id="91d0d-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="91d0d-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="91d0d-176">EventTime</span></span> |<span data-ttu-id="91d0d-177">Tarih ve olayın oluşturulduğu saat.</span><span class="sxs-lookup"><span data-stu-id="91d0d-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="91d0d-178">Syslog kayıtlarla günlük sorguları</span><span class="sxs-lookup"><span data-stu-id="91d0d-178">Log queries with Syslog records</span></span>
<span data-ttu-id="91d0d-179">Aşağıdaki tabloda, Syslog kayıtları almak günlük sorgularının farklı örnekler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="91d0d-180">Sorgu</span><span class="sxs-lookup"><span data-stu-id="91d0d-180">Query</span></span> | <span data-ttu-id="91d0d-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="91d0d-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="91d0d-182">Türü Syslog =</span><span class="sxs-lookup"><span data-stu-id="91d0d-182">Type=Syslog</span></span> |<span data-ttu-id="91d0d-183">Tüm Syslog modüllerini.</span><span class="sxs-lookup"><span data-stu-id="91d0d-183">All Syslogs.</span></span> |
| <span data-ttu-id="91d0d-184">Türü Syslog önem düzeyi = hata =</span><span class="sxs-lookup"><span data-stu-id="91d0d-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="91d0d-185">Tüm Syslog kayıtları hata önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="91d0d-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="91d0d-186">Tür = Syslog &#124; Bilgisayar tarafından ölçü Count() işlevi</span><span class="sxs-lookup"><span data-stu-id="91d0d-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="91d0d-187">Bilgisayar tarafından sayısı, Syslog kaydeder.</span><span class="sxs-lookup"><span data-stu-id="91d0d-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="91d0d-188">Tür = Syslog &#124; Ölçü count() tesis tarafından</span><span class="sxs-lookup"><span data-stu-id="91d0d-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="91d0d-189">Tesis tarafından sayısı, Syslog kaydeder.</span><span class="sxs-lookup"><span data-stu-id="91d0d-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="91d0d-190">Çalışma alanınız [yeni Log Analytics sorgu diline](log-analytics-log-search-upgrade.md) yükseltilmişse, yukarıdaki sorguların aşağıdaki gibi değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="91d0d-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="91d0d-191">Sorgu</span><span class="sxs-lookup"><span data-stu-id="91d0d-191">Query</span></span> | <span data-ttu-id="91d0d-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="91d0d-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="91d0d-193">Syslog</span><span class="sxs-lookup"><span data-stu-id="91d0d-193">Syslog</span></span> |<span data-ttu-id="91d0d-194">Tüm Syslog modüllerini.</span><span class="sxs-lookup"><span data-stu-id="91d0d-194">All Syslogs.</span></span> |
| <span data-ttu-id="91d0d-195">Syslog &#124; Burada önem düzeyi "error" ==</span><span class="sxs-lookup"><span data-stu-id="91d0d-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="91d0d-196">Tüm Syslog kayıtları hata önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="91d0d-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="91d0d-197">Syslog &#124; AggregatedValue özetlemek bilgisayar tarafından count() =</span><span class="sxs-lookup"><span data-stu-id="91d0d-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="91d0d-198">Bilgisayar tarafından sayısı, Syslog kaydeder.</span><span class="sxs-lookup"><span data-stu-id="91d0d-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="91d0d-199">Syslog &#124; AggregatedValue özetlemek tesis tarafından count() =</span><span class="sxs-lookup"><span data-stu-id="91d0d-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="91d0d-200">Tesis tarafından sayısı, Syslog kaydeder.</span><span class="sxs-lookup"><span data-stu-id="91d0d-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="91d0d-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91d0d-201">Next steps</span></span>
* <span data-ttu-id="91d0d-202">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) veri kaynakları ve çözümleri toplanan verileri çözümlemek için.</span><span class="sxs-lookup"><span data-stu-id="91d0d-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="91d0d-203">Kullanım [özel alanlar](log-analytics-custom-fields.md) tek tek alanlarına syslog kayıtları verilerden ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="91d0d-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="91d0d-204">[Linux aracılarını yapılandırma](log-analytics-linux-agents.md) diğer veri türleri toplanacak.</span><span class="sxs-lookup"><span data-stu-id="91d0d-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
