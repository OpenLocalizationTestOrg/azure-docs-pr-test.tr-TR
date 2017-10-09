---
title: "aaaCollect ve OMS günlük analizi Syslog iletileri analiz | Microsoft Docs"
description: "Syslog ortak tooLinux olan bir olay günlüğü protokolüdür. Bu makalede nasıl günlük analizi Syslog iletileri tooconfigure koleksiyonunu ve hello kayıtları ayrıntılarını hello OMS deposunda oluşturdukları açıklanmaktadır."
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
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="494dd-104">Syslog veri kaynaklarında günlük analizi</span><span class="sxs-lookup"><span data-stu-id="494dd-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="494dd-105">Syslog ortak tooLinux olan bir olay günlüğü protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="494dd-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="494dd-106">Uygulamaları hello yerel makine üzerinde depolanan olabilir veya tooa Syslog Toplayıcı teslim iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="494dd-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="494dd-107">Merhaba Linux için OMS Aracısı yüklendiğinde hello yerel Syslog arka plan programı tooforward iletileri toohello aracı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="494dd-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="494dd-108">Merhaba aracı karşılık gelen bir kayıt hello OMS deposunda oluşturulduğu hello ileti tooLog Analytics sonra gönderir.</span><span class="sxs-lookup"><span data-stu-id="494dd-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="494dd-109">Günlük analizi rsyslog hello varsayılan arka plan programı olduğu rsyslog veya syslog-ng tarafından gönderilen iletileri koleksiyonu destekler.</span><span class="sxs-lookup"><span data-stu-id="494dd-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="494dd-110">Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü Hello varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="494dd-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="494dd-111">Bu sürümü bu dağıtımları toocollect syslog verileri hello [rsyslog arka plan programı](http://rsyslog.com) yüklü olmalıdır ve tooreplace sysklog yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="494dd-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Syslog koleksiyonu](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="494dd-113">Syslog yapılandırma</span><span class="sxs-lookup"><span data-stu-id="494dd-113">Configuring Syslog</span></span>
<span data-ttu-id="494dd-114">Merhaba Linux için OMS aracısının yalnızca hello tesis ve yapılandırmasıyla belirtilen önem derecelerine sahip olayları toplar.</span><span class="sxs-lookup"><span data-stu-id="494dd-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="494dd-115">Syslog hello OMS portalı üzerinden veya Linux aracıları yapılandırma dosyalarını yönetme tarafından yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494dd-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="494dd-116">Syslog hello OMS portalında yapılandırın</span><span class="sxs-lookup"><span data-stu-id="494dd-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="494dd-117">Syslog hello yapılandırma [günlük analizi ayarları veri menüde](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="494dd-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="494dd-118">Bu yapılandırma her Linux Aracısı toohello yapılandırma dosyası teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="494dd-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="494dd-119">Adını yazıp'yi tıklatarak yeni bir tesis ekleyebilirsiniz  **+** .</span><span class="sxs-lookup"><span data-stu-id="494dd-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="494dd-120">Her özelliği için seçilen hello önem derecelerine sahip yalnızca iletileri toplanacaktır.</span><span class="sxs-lookup"><span data-stu-id="494dd-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="494dd-121">Merhaba önem derecelerine toocollect istediğiniz hello belirli olanağı için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="494dd-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="494dd-122">Herhangi bir ek ölçütü toofilter iletileri sağlayamaz.</span><span class="sxs-lookup"><span data-stu-id="494dd-122">You cannot provide any additional criteria toofilter messages.</span></span>

![Syslog yapılandırın](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="494dd-124">Varsayılan olarak, tüm yapılandırma değişiklikleri otomatik olarak tooall aracıları gönderilir.</span><span class="sxs-lookup"><span data-stu-id="494dd-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="494dd-125">Her Linux aracısında el ile tooconfigure Syslog istiyorsanız hello kutunun işaretini *aşağıdaki yapılandırma toomy Linux makineler Uygula*.</span><span class="sxs-lookup"><span data-stu-id="494dd-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="494dd-126">Syslog Linux Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="494dd-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="494dd-127">Ne zaman hello [OMS Aracısı Linux istemcide yüklü](log-analytics-linux-agents.md)hello tesis tanımlayan bir varsayılan syslog yapılandırma dosyası yükler ve önem derecesi hello iletileri toplanır.</span><span class="sxs-lookup"><span data-stu-id="494dd-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="494dd-128">Bu dosya toochange hello yapılandırmasını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494dd-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="494dd-129">Merhaba yapılandırma dosyası istemci hello arka plan programı yüklediği Syslog hello bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="494dd-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="494dd-130">Merhaba syslog yapılandırma düzenlerseniz, hello değişiklikleri tootake etkisi hello syslog arka plan yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="494dd-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="494dd-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="494dd-131">rsyslog</span></span>
<span data-ttu-id="494dd-132">Merhaba rsyslog için yapılandırma dosyası bulunur **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="494dd-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="494dd-133">Varsayılan içeriğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="494dd-133">Its default contents are shown below.</span></span>  <span data-ttu-id="494dd-134">Bu, uyarı ya da daha yüksek bir düzeyinde tüm tesisler için yerel hello Aracısı'ndan gönderilen syslog iletileri toplar.</span><span class="sxs-lookup"><span data-stu-id="494dd-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="494dd-135">Kendi hello yapılandırma dosyası bölümünü kaldırarak bir tesis kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494dd-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="494dd-136">Bu tesis 's girdisini değiştirerek belirli olanağını toplanan hello önem derecelerine sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494dd-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="494dd-137">Örneğin, toolimit hello kullanıcı tesis toomessages hata veya daha büyük bir önem derecesi aşağıdaki hello yapılandırma dosyası toohello satırını değiştirirsiniz:</span><span class="sxs-lookup"><span data-stu-id="494dd-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="494dd-138">Syslog ng</span><span class="sxs-lookup"><span data-stu-id="494dd-138">syslog-ng</span></span>
<span data-ttu-id="494dd-139">syslog ng Hello yapılandırma dosyası olduğu konumda **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="494dd-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="494dd-140">Varsayılan içeriğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="494dd-140">Its default contents are shown below.</span></span>  <span data-ttu-id="494dd-141">Tüm Tesisler ve tüm önem dereceleridir için yerel hello Aracısı'ndan gönderilen syslog iletileri toplar.</span><span class="sxs-lookup"><span data-stu-id="494dd-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="494dd-142">Kendi hello yapılandırma dosyası bölümünü kaldırarak bir tesis kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494dd-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="494dd-143">Belirli bir özellik için listeden kaldırarak toplanır hello önem derecelerine sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494dd-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="494dd-144">Örneğin, toolimit hello kullanıcı tesis toojust uyarı ve kritik iletileri aşağıdaki hello yapılandırma dosyası toohello ilgili bölümünü değiştirmek:</span><span class="sxs-lookup"><span data-stu-id="494dd-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="494dd-145">Ek Syslog bağlantı noktalarından verileri toplama</span><span class="sxs-lookup"><span data-stu-id="494dd-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="494dd-146">Merhaba OMS Aracısı Syslog iletileri hello yerel istemci 25224 bağlantı noktasında dinler.</span><span class="sxs-lookup"><span data-stu-id="494dd-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="494dd-147">Merhaba Aracısı yüklendiğinde varsayılan syslog yapılandırması uygulanan ve konumu aşağıdaki hello bulundu:</span><span class="sxs-lookup"><span data-stu-id="494dd-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="494dd-148">Rsyslog:`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="494dd-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="494dd-149">Syslog-ng:`/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="494dd-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="494dd-150">İki yapılandırma dosyası oluşturarak başlangıç bağlantı noktası numarasını değiştirebilirsiniz: FluentD yapılandırma dosyası ve bir rsyslog veya syslog ng dosyası hello Syslog arka plan programı yüklediğiniz bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="494dd-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="494dd-151">Merhaba FluentD yapılandırma dosyasında bulunan yeni bir dosya olmalıdır: `/etc/opt/microsoft/omsagent/conf/omsagent.d` ve hello hello değerinde değiştirme **bağlantı noktası** giriş, özel bir bağlantı noktası numarasına sahip.</span><span class="sxs-lookup"><span data-stu-id="494dd-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="494dd-152">Rsyslog için bulunan yeni bir yapılandırma dosyası oluşturmanız gerekir: `/etc/rsyslog.d/` ve hello % SYSLOG_PORT % değerini, özel bir bağlantı noktası numarasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="494dd-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="494dd-153">Merhaba yapılandırma dosyasında bu değeri değiştirirseniz, `95-omsagent.conf`, hello Aracısı varsayılan bir yapılandırma uyguladığında üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="494dd-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="494dd-154">Merhaba syslog ng config aşağıda gösterilen hello örnek yapılandırma kopyalayarak değiştirilmesi gerektiğini ve bulunan hello syslog ng.conf yapılandırma dosyasının sonuna hello özel değiştirilen ayarlar toohello ekleme `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="494dd-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="494dd-155">Yapmak **değil** hello varsayılan etiket **% WORKSPACE_ID % _oms** veya **% WORKSPACE_ID_OMS**, özel tanımlama etiket toohelp yaptığınız değişiklikleri ayırt etmek.</span><span class="sxs-lookup"><span data-stu-id="494dd-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="494dd-156">Hello yapılandırma dosyasındaki hello varsayılan değerleri değiştirirseniz, varsayılan bir yapılandırma hello Aracısı geçerli olduğu durumlarda bunların üzerine yazılacak.</span><span class="sxs-lookup"><span data-stu-id="494dd-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="494dd-157">Merhaba değişiklikler, hello Syslog ve hello tamamladıktan sonra OMS Aracısı hizmeti yeniden toobe tooensure hello yapılandırma değişiklikleri etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="494dd-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="494dd-158">Syslog kaydı Özellikler</span><span class="sxs-lookup"><span data-stu-id="494dd-158">Syslog record properties</span></span>
<span data-ttu-id="494dd-159">Syslog kayıtları sahip bir tür **Syslog** ve aşağıdaki tablonun hello hello özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="494dd-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="494dd-160">Özellik</span><span class="sxs-lookup"><span data-stu-id="494dd-160">Property</span></span> | <span data-ttu-id="494dd-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="494dd-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="494dd-162">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="494dd-162">Computer</span></span> |<span data-ttu-id="494dd-163">Olay hello bilgisayar toplandığı.</span><span class="sxs-lookup"><span data-stu-id="494dd-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="494dd-164">Tesis</span><span class="sxs-lookup"><span data-stu-id="494dd-164">Facility</span></span> |<span data-ttu-id="494dd-165">Merhaba selamlama iletisine oluşturulan hello sisteminin parçası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="494dd-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="494dd-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="494dd-166">HostIP</span></span> |<span data-ttu-id="494dd-167">Merhaba ileti gönderme hello sistem IP adresi.</span><span class="sxs-lookup"><span data-stu-id="494dd-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="494dd-168">Ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="494dd-168">HostName</span></span> |<span data-ttu-id="494dd-169">Merhaba ileti gönderme hello sistem adı.</span><span class="sxs-lookup"><span data-stu-id="494dd-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="494dd-170">Önem düzeyi</span><span class="sxs-lookup"><span data-stu-id="494dd-170">SeverityLevel</span></span> |<span data-ttu-id="494dd-171">Merhaba olay önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="494dd-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="494dd-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="494dd-172">SyslogMessage</span></span> |<span data-ttu-id="494dd-173">Merhaba ileti metni.</span><span class="sxs-lookup"><span data-stu-id="494dd-173">Text of hello message.</span></span> |
| <span data-ttu-id="494dd-174">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="494dd-174">ProcessID</span></span> |<span data-ttu-id="494dd-175">Selamlama iletisine oluşturulan hello işlemin kimliği.</span><span class="sxs-lookup"><span data-stu-id="494dd-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="494dd-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="494dd-176">EventTime</span></span> |<span data-ttu-id="494dd-177">Tarih ve saat olay hello üretilmiştir.</span><span class="sxs-lookup"><span data-stu-id="494dd-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="494dd-178">Syslog kayıtlarla günlük sorguları</span><span class="sxs-lookup"><span data-stu-id="494dd-178">Log queries with Syslog records</span></span>
<span data-ttu-id="494dd-179">Hello aşağıdaki tabloda, Syslog kayıtları almak günlük sorgularının farklı örnekler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="494dd-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="494dd-180">Sorgu</span><span class="sxs-lookup"><span data-stu-id="494dd-180">Query</span></span> | <span data-ttu-id="494dd-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="494dd-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="494dd-182">Türü Syslog =</span><span class="sxs-lookup"><span data-stu-id="494dd-182">Type=Syslog</span></span> |<span data-ttu-id="494dd-183">Tüm Syslog modüllerini.</span><span class="sxs-lookup"><span data-stu-id="494dd-183">All Syslogs.</span></span> |
| <span data-ttu-id="494dd-184">Türü Syslog önem düzeyi = hata =</span><span class="sxs-lookup"><span data-stu-id="494dd-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="494dd-185">Tüm Syslog kayıtları hata önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="494dd-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="494dd-186">Tür = Syslog &#124; Bilgisayar tarafından ölçü Count() işlevi</span><span class="sxs-lookup"><span data-stu-id="494dd-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="494dd-187">Bilgisayar tarafından sayısı, Syslog kaydeder.</span><span class="sxs-lookup"><span data-stu-id="494dd-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="494dd-188">Tür = Syslog &#124; Ölçü count() tesis tarafından</span><span class="sxs-lookup"><span data-stu-id="494dd-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="494dd-189">Tesis tarafından sayısı, Syslog kaydeder.</span><span class="sxs-lookup"><span data-stu-id="494dd-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="494dd-190">Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra.</span><span class="sxs-lookup"><span data-stu-id="494dd-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="494dd-191">Sorgu</span><span class="sxs-lookup"><span data-stu-id="494dd-191">Query</span></span> | <span data-ttu-id="494dd-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="494dd-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="494dd-193">Syslog</span><span class="sxs-lookup"><span data-stu-id="494dd-193">Syslog</span></span> |<span data-ttu-id="494dd-194">Tüm Syslog modüllerini.</span><span class="sxs-lookup"><span data-stu-id="494dd-194">All Syslogs.</span></span> |
| <span data-ttu-id="494dd-195">Syslog &#124; Burada önem düzeyi "error" ==</span><span class="sxs-lookup"><span data-stu-id="494dd-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="494dd-196">Tüm Syslog kayıtları hata önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="494dd-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="494dd-197">Syslog &#124; AggregatedValue özetlemek bilgisayar tarafından count() =</span><span class="sxs-lookup"><span data-stu-id="494dd-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="494dd-198">Bilgisayar tarafından sayısı, Syslog kaydeder.</span><span class="sxs-lookup"><span data-stu-id="494dd-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="494dd-199">Syslog &#124; AggregatedValue özetlemek tesis tarafından count() =</span><span class="sxs-lookup"><span data-stu-id="494dd-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="494dd-200">Tesis tarafından sayısı, Syslog kaydeder.</span><span class="sxs-lookup"><span data-stu-id="494dd-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="494dd-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="494dd-201">Next steps</span></span>
* <span data-ttu-id="494dd-202">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.</span><span class="sxs-lookup"><span data-stu-id="494dd-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="494dd-203">Kullanım [özel alanlar](log-analytics-custom-fields.md) syslog kayıtları tek tek alanlara tooparse verileri.</span><span class="sxs-lookup"><span data-stu-id="494dd-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="494dd-204">[Linux aracılarını yapılandırma](log-analytics-linux-agents.md) toocollect diğer veri türleri.</span><span class="sxs-lookup"><span data-stu-id="494dd-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
