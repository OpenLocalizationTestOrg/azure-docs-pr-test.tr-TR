---
title: "Linux bilgisayarları Operations Management Suite (OMS) bağlanma | Microsoft Docs"
description: "Bu makalede, Azure, diğer Bulut veya şirket içi Linux için OMS Aracısı'nı kullanarak OMS barındırılan Linux bilgisayarları bağlamak açıklar."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: 1c05f68235aafd0fa098a3b0edaba1258df09380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-linux-computers-to-operations-management-suite-oms"></a><span data-ttu-id="e0d16-103">Linux bilgisayarları Operations Management Suite (OMS) bağlanma</span><span class="sxs-lookup"><span data-stu-id="e0d16-103">Connect your Linux Computers to Operations Management Suite (OMS)</span></span> 

<span data-ttu-id="e0d16-104">Microsoft Operations Management Suite (OMS) ile toplama ve hareket Linux bilgisayarları ve fiziksel sunucularda veya sanal makineleri, sanal makinelerinizde olarak şirket içi veri Merkezinize bulunan Docker gibi kapsayıcı çözümlerinden oluşturulan veriler üzerinde bir Amazon Web Hizmetleri (AWS) veya Microsoft Azure gibi bulutta barındırılan hizmet.</span><span class="sxs-lookup"><span data-stu-id="e0d16-104">With Microsoft Operations Management Suite (OMS), you can collect and act on data generated from Linux computers and container solutions like Docker, residing in your on-premises data center as physical servers or virtual machines, virtual machines in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure.</span></span> <span data-ttu-id="e0d16-105">Yönetim çözümleri OMS içinde kullanılabilir değişiklik izleme gibi yapılandırma değişiklikleri ve Linux VM'ler yaşam döngüsü ileriye dönük olarak yönetmek için yazılım güncelleştirmelerini yönetmek için güncelleştirme yönetimi tanımlamak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0d16-105">You can also use management solutions available in OMS such as Change Tracking, to identify configuration changes, and Update Management to manage software updates to proactively manage the lifecycle of your Linux VMs.</span></span> 

<span data-ttu-id="e0d16-106">Linux için OMS Aracısı TCP bağlantı noktası 443 giden OMS hizmetiyle iletişim kurar ve bilgisayar Internet üzerinden iletişim kurmak için bir güvenlik duvarı veya proxy sunucusu bağlanırsa gözden [aracı kullanmak için bir HTTP proxy sunucusu veya OMS ile yapılandırma Ağ geçidi](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) hangi yapılandırma değişiklikleri anlamak için uygulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-106">The OMS Agent for Linux communicates outbound with the OMS service over TCP port 443, and if the computer connects to a firewall or proxy server to communicate over the Internet, review [Configuring the agent for use with an HTTP proxy server or OMS Gateway](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) to understand what configuration changes will need to be applied.</span></span>  <span data-ttu-id="e0d16-107">System Center 2016 - Operations Manager veya Operations Manager 2012 R2'de, bilgisayarla izliyorsanız çok konaklı veri toplamak ve Hizmeti'ne iletmek ve Operations Manager tarafından yine izlenmesi için OMS hizmetiyle olabilir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-107">If you are monitoring the computer with System Center 2016 - Operations Manager or Operations Manager 2012 R2, it can be multi-homed with the OMS service to collect data and forward to the service and still be monitored by Operations Manager.</span></span>  <span data-ttu-id="e0d16-108">OMS ile tümleşik bir Operations Manager yönetim grubu tarafından izlenen Linux bilgisayarlar veri kaynakları için yapılandırma almaz ve yönetim grubu ile veri oplanan.</span><span class="sxs-lookup"><span data-stu-id="e0d16-108">Linux computers monitored by an Operations Manager management group that is integrated with OMS do not receive configuration for data sources and forward collected data through the management group.</span></span>  <span data-ttu-id="e0d16-109">Rapor birden fazla çalışma alanına OMS Aracısı yapılandırılamaz.</span><span class="sxs-lookup"><span data-stu-id="e0d16-109">The OMS agent cannot be configured to report to more than one workspace.</span></span>  

<span data-ttu-id="e0d16-110">BT güvenlik ilkelerinizi bilgisayarları Internet'e bağlanmak için ağınızdaki izin vermiyorsa, aracı yapılandırma bilgilerini almak ve etkinleştirdiğiniz çözümüne bağlı olarak toplanan verileri göndermek için OMS ağ geçidine bağlanmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-110">If your IT security policies do not allow computers on your network to connect to the Internet, the agent can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span></span> <span data-ttu-id="e0d16-111">Daha fazla bilgi ve OMS hizmetine bir OMS ağ geçidi üzerinden iletişim kurmak için OMS Linux aracınızı yapılandırma adımları için bkz: [OMS ağ geçidini kullanarak OMS bilgisayarları bağlamak](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="e0d16-111">For more information and steps on how to configure your OMS Linux Agent to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

<span data-ttu-id="e0d16-112">Aşağıdaki diyagram, OMS bağlantı noktaları ve yön dahil olmak üzere ve aracıyla yönetilen Linux bilgisayarlar arasındaki bağlantıyı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-112">The following diagram depicts the connection between the agent-managed Linux computers and OMS, including the direction and ports.</span></span>

![OMS diyagramı ile doğrudan aracı iletişimi](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a><span data-ttu-id="e0d16-114">Sistem gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="e0d16-114">System requirements</span></span>
<span data-ttu-id="e0d16-115">Başlamadan önce önkoşulları karşılaması doğrulamak için aşağıdaki ayrıntıları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="e0d16-115">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="supported-linux-operating-systems"></a><span data-ttu-id="e0d16-116">Desteklenen Linux işletim sistemleri</span><span class="sxs-lookup"><span data-stu-id="e0d16-116">Supported Linux operating systems</span></span>
<span data-ttu-id="e0d16-117">Aşağıdaki Linux dağıtımları resmi olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-117">The following Linux distributions are officially supported.</span></span>  <span data-ttu-id="e0d16-118">Ancak, OMS Aracısı Linux için listelenmeyen diğer dağıtımlar da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0d16-118">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="e0d16-119">Amazon Linux için 2015.09 2012.09 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="e0d16-119">Amazon Linux 2012.09 to 2015.09 (x86/x64)</span></span>
* <span data-ttu-id="e0d16-120">CentOS Linux 5, 6 ve 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="e0d16-120">CentOS Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="e0d16-121">Oracle Linux 5, 6 ve 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="e0d16-121">Oracle Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="e0d16-122">Red Hat Enterprise Linux Server 5, 6 ve 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="e0d16-122">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
* <span data-ttu-id="e0d16-123">Debian GNU/Linux 6, 7 ve 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="e0d16-123">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span></span>
* <span data-ttu-id="e0d16-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="e0d16-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span></span>
* <span data-ttu-id="e0d16-125">SUSE Linux Enterprise Server 11 ve 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="e0d16-125">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span></span>

### <a name="network"></a><span data-ttu-id="e0d16-126">Ağ</span><span class="sxs-lookup"><span data-stu-id="e0d16-126">Network</span></span>
<span data-ttu-id="e0d16-127">Aşağıdaki listeden OMS ile iletişim kurmak Linux aracısı için gerekli proxy ve güvenlik duvarı yapılandırma bilgilerini bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e0d16-127">The information below list the proxy and firewall configuration information required for the Linux agent to communicate with OMS.</span></span> <span data-ttu-id="e0d16-128">OMS hizmete ağınızdan giden trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-128">Traffic is outbound from your network to the OMS service.</span></span> 

|<span data-ttu-id="e0d16-129">Aracı Kaynağı</span><span class="sxs-lookup"><span data-stu-id="e0d16-129">Agent Resource</span></span>| <span data-ttu-id="e0d16-130">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="e0d16-130">Ports</span></span> |  
|------|---------|  
|<span data-ttu-id="e0d16-131">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="e0d16-131">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="e0d16-132">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="e0d16-132">Port 443</span></span>|   
|<span data-ttu-id="e0d16-133">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="e0d16-133">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="e0d16-134">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="e0d16-134">Port 443</span></span>|   
|<span data-ttu-id="e0d16-135">*.BLOB.Core.Windows.NET/</span><span class="sxs-lookup"><span data-stu-id="e0d16-135">*.blob.core.windows.net/</span></span> | <span data-ttu-id="e0d16-136">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="e0d16-136">Port 443</span></span>|   
|<span data-ttu-id="e0d16-137">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="e0d16-137">*.azure-automation.net</span></span> | <span data-ttu-id="e0d16-138">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="e0d16-138">Port 443</span></span>|  

### <a name="package-requirements"></a><span data-ttu-id="e0d16-139">Paket gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="e0d16-139">Package requirements</span></span>

 <span data-ttu-id="e0d16-140">**Gerekli paket**</span><span class="sxs-lookup"><span data-stu-id="e0d16-140">**Required package**</span></span>   | <span data-ttu-id="e0d16-141">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="e0d16-141">**Description**</span></span>   | <span data-ttu-id="e0d16-142">**En düşük sürüm**</span><span class="sxs-lookup"><span data-stu-id="e0d16-142">**Minimum version**</span></span>
--------------------- | --------------------- | -------------------
<span data-ttu-id="e0d16-143">Glibc</span><span class="sxs-lookup"><span data-stu-id="e0d16-143">Glibc</span></span> | <span data-ttu-id="e0d16-144">GNU C Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="e0d16-144">GNU C Library</span></span>   | <span data-ttu-id="e0d16-145">2.5-12</span><span class="sxs-lookup"><span data-stu-id="e0d16-145">2.5-12</span></span> 
<span data-ttu-id="e0d16-146">Openssl</span><span class="sxs-lookup"><span data-stu-id="e0d16-146">Openssl</span></span> | <span data-ttu-id="e0d16-147">OpenSSL kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="e0d16-147">OpenSSL Libraries</span></span> | <span data-ttu-id="e0d16-148">0.9.8E veya 1.0</span><span class="sxs-lookup"><span data-stu-id="e0d16-148">0.9.8e or 1.0</span></span>
<span data-ttu-id="e0d16-149">Curl</span><span class="sxs-lookup"><span data-stu-id="e0d16-149">Curl</span></span> | <span data-ttu-id="e0d16-150">cURL web istemcisi</span><span class="sxs-lookup"><span data-stu-id="e0d16-150">cURL web client</span></span> | <span data-ttu-id="e0d16-151">7.15.5</span><span class="sxs-lookup"><span data-stu-id="e0d16-151">7.15.5</span></span>
<span data-ttu-id="e0d16-152">Python ctypes</span><span class="sxs-lookup"><span data-stu-id="e0d16-152">Python-ctypes</span></span> | | 
<span data-ttu-id="e0d16-153">PAM</span><span class="sxs-lookup"><span data-stu-id="e0d16-153">PAM</span></span> | <span data-ttu-id="e0d16-154">Eklenebilir kimlik doğrulaması modülleri</span><span class="sxs-lookup"><span data-stu-id="e0d16-154">Pluggable authentication Modules</span></span> | 

> [!NOTE]
>  <span data-ttu-id="e0d16-155">Rsyslog veya syslog ng syslog iletileri toplamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-155">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="e0d16-156">Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e0d16-156">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="e0d16-157">Bu dağıtımları bu sürümünden Syslog verileri toplamak için rsyslog arka plan programı yüklenmeli ve sysklog değiştirmek üzere yapılandırılmamışsa,</span><span class="sxs-lookup"><span data-stu-id="e0d16-157">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog,</span></span> 

<span data-ttu-id="e0d16-158">Aracı birden çok paket içerir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-158">The agent includes multiple packages.</span></span> <span data-ttu-id="e0d16-159">Aşağıdaki paketler, kabuk Paketle çalıştırarak kullanılabilir sürüm dosyasını içeren `--extract`:</span><span class="sxs-lookup"><span data-stu-id="e0d16-159">The release file contains the following packages, available by running the shell bundle with `--extract`:</span></span>

<span data-ttu-id="e0d16-160">**Paket**</span><span class="sxs-lookup"><span data-stu-id="e0d16-160">**Package**</span></span> | <span data-ttu-id="e0d16-161">**Sürüm**</span><span class="sxs-lookup"><span data-stu-id="e0d16-161">**Version**</span></span> | <span data-ttu-id="e0d16-162">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="e0d16-162">**Description**</span></span>
----------- | ----------- | --------------
<span data-ttu-id="e0d16-163">omsagent</span><span class="sxs-lookup"><span data-stu-id="e0d16-163">omsagent</span></span> | <span data-ttu-id="e0d16-164">1.4.0</span><span class="sxs-lookup"><span data-stu-id="e0d16-164">1.4.0</span></span> | <span data-ttu-id="e0d16-165">Linux için Operations Management Suite Aracısı</span><span class="sxs-lookup"><span data-stu-id="e0d16-165">The Operations Management Suite Agent for Linux</span></span>
<span data-ttu-id="e0d16-166">omsconfig</span><span class="sxs-lookup"><span data-stu-id="e0d16-166">omsconfig</span></span> | <span data-ttu-id="e0d16-167">1.1.1</span><span class="sxs-lookup"><span data-stu-id="e0d16-167">1.1.1</span></span> | <span data-ttu-id="e0d16-168">OMS aracısı için yapılandırma aracısı</span><span class="sxs-lookup"><span data-stu-id="e0d16-168">Configuration agent for the OMS Agent</span></span>
<span data-ttu-id="e0d16-169">OMI</span><span class="sxs-lookup"><span data-stu-id="e0d16-169">omi</span></span> | <span data-ttu-id="e0d16-170">1.2.0</span><span class="sxs-lookup"><span data-stu-id="e0d16-170">1.2.0</span></span> | <span data-ttu-id="e0d16-171">Yönetim Altyapısı (OMI) - hafif bir CIM sunucusu açın</span><span class="sxs-lookup"><span data-stu-id="e0d16-171">Open Management Infrastructure (OMI) - a lightweight CIM Server</span></span>
<span data-ttu-id="e0d16-172">scx</span><span class="sxs-lookup"><span data-stu-id="e0d16-172">scx</span></span> | <span data-ttu-id="e0d16-173">1.6.3</span><span class="sxs-lookup"><span data-stu-id="e0d16-173">1.6.3</span></span> | <span data-ttu-id="e0d16-174">İşletim sistemi performans ölçümleri için OMI CIM sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="e0d16-174">OMI CIM Providers for operating system performance metrics</span></span>
<span data-ttu-id="e0d16-175">Apache cimprov</span><span class="sxs-lookup"><span data-stu-id="e0d16-175">apache-cimprov</span></span> | <span data-ttu-id="e0d16-176">1.0.1</span><span class="sxs-lookup"><span data-stu-id="e0d16-176">1.0.1</span></span> | <span data-ttu-id="e0d16-177">Apache HTTP Server performansı sağlayıcısı OMI için izleme.</span><span class="sxs-lookup"><span data-stu-id="e0d16-177">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="e0d16-178">Apache HTTP Server algılanırsa, yüklü.</span><span class="sxs-lookup"><span data-stu-id="e0d16-178">Installed if Apache HTTP Server is detected.</span></span>
<span data-ttu-id="e0d16-179">MySQL cimprov</span><span class="sxs-lookup"><span data-stu-id="e0d16-179">mysql-cimprov</span></span> | <span data-ttu-id="e0d16-180">1.0.1</span><span class="sxs-lookup"><span data-stu-id="e0d16-180">1.0.1</span></span> | <span data-ttu-id="e0d16-181">MySQL sunucusu performans sağlayıcısı OMI için izleme.</span><span class="sxs-lookup"><span data-stu-id="e0d16-181">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="e0d16-182">MySQL/MariaDB sunucu algılanırsa, yüklü.</span><span class="sxs-lookup"><span data-stu-id="e0d16-182">Installed if MySQL/MariaDB server is detected.</span></span>
<span data-ttu-id="e0d16-183">docker cimprov</span><span class="sxs-lookup"><span data-stu-id="e0d16-183">docker-cimprov</span></span> | <span data-ttu-id="e0d16-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e0d16-184">1.0.0</span></span> | <span data-ttu-id="e0d16-185">OMI docker sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e0d16-185">Docker provider for OMI.</span></span> <span data-ttu-id="e0d16-186">Docker algılanırsa, yüklü.</span><span class="sxs-lookup"><span data-stu-id="e0d16-186">Installed if Docker is detected.</span></span>

### <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="e0d16-187">System Center Operations Manager ile uyumluluk</span><span class="sxs-lookup"><span data-stu-id="e0d16-187">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="e0d16-188">Linux için OMS aracısının Aracısı ikili dosyaları System Center Operations Manager Aracısı ile paylaşır.</span><span class="sxs-lookup"><span data-stu-id="e0d16-188">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="e0d16-189">OMS Aracısı'nı Linux için bir sistem üzerinde şu anda yüklerseniz, SCX ve OMI paketleri daha yeni bir sürüme bilgisayarda Operations Manager tarafından yönetiliyor.</span><span class="sxs-lookup"><span data-stu-id="e0d16-189">If you install the OMS Agent for Linux on a system currently managed by Operations Manager, it the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="e0d16-190">Bu sürümde, OMS ve System Center 2016 - Operations Manager/Operations Manager 2012 R2 aracıları Linux için uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-190">In this release, the OMS and System Center 2016 - Operations Manager/Operations Manager 2012 R2 agents for Linux are compatible.</span></span> 

> [!NOTE]
> <span data-ttu-id="e0d16-191">System Center 2012 SP1 ve önceki sürümleri şu anda Linux için OMS Aracısı ile desteklenen veya uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-191">System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.</span></span><br>
> <span data-ttu-id="e0d16-192">Linux için OMS Aracısı şu anda Operations Manager tarafından izlenmeyen bir bilgisayara yüklenir ve ardından bilgisayarı Operations Manager ile izlemek istediğiniz, değiştirmeniz gerekir [OMI yapılandırma](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) keşfetme önce bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="e0d16-192">If the OMS Agent for Linux is installed to a computer that is not currently monitored by Operations Manager, and you then wish to monitor the computer with Operations Manager, you must modify the [OMI configuration](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) prior to discovering the computer.</span></span> <span data-ttu-id="e0d16-193">**Bu adım *değil* önce OMS Aracısı'nı Linux için Operations Manager Aracısı yüklüyse gerekli.**</span><span class="sxs-lookup"><span data-stu-id="e0d16-193">**This step is *not* needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>

### <a name="system-configuration-changes"></a><span data-ttu-id="e0d16-194">Sistem yapılandırması değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="e0d16-194">System configuration changes</span></span>
<span data-ttu-id="e0d16-195">Linux paketler için OMS Aracısı yükledikten sonra aşağıdaki ek sistem genelinde yapılandırma değişikliklerini uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e0d16-195">After installing the OMS Agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="e0d16-196">Bu yapıtların omsagent paket kaldırıldığında kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e0d16-196">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="e0d16-197">Adlı bir ayrıcalıklı olmayan kullanıcı: `omsagent` oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e0d16-197">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="e0d16-198">Olarak omsagent arka plan programı çalıştıran hesap budur.</span><span class="sxs-lookup"><span data-stu-id="e0d16-198">This is the account the omsagent daemon runs as.</span></span>
* <span data-ttu-id="e0d16-199">"Ekle" sudoers dosya /etc/sudoers.d/omsagent oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e0d16-199">A sudoers “include” file is created at /etc/sudoers.d/omsagent.</span></span> <span data-ttu-id="e0d16-200">Syslog ve omsagent Daemon başlatmayı omsagent yetkilendirir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-200">This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="e0d16-201">Sudo "Ekle" yönergeleri sudo yüklü sürümü desteklenmiyorsa, bu girişler için /etc/sudoers yazılır.</span><span class="sxs-lookup"><span data-stu-id="e0d16-201">If sudo “include” directives are not supported in the installed version of sudo, these entries are written to /etc/sudoers.</span></span>
* <span data-ttu-id="e0d16-202">Syslog yapılandırma aracıya bir alt olayların iletecek şekilde değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-202">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="e0d16-203">Daha fazla bilgi için bkz: **yapılandırma veri toplama** bölümüne bakın</span><span class="sxs-lookup"><span data-stu-id="e0d16-203">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="upgrade-from-a-previous-release"></a><span data-ttu-id="e0d16-204">Önceki bir sürümünden yükseltme</span><span class="sxs-lookup"><span data-stu-id="e0d16-204">Upgrade from a previous release</span></span>
<span data-ttu-id="e0d16-205">Bu sürümde 1.0.0-47 desteklenenden daha önceki sürümlerden yükseltin.</span><span class="sxs-lookup"><span data-stu-id="e0d16-205">Upgrade from versions earlier than 1.0.0-47 is supported in this release.</span></span> <span data-ttu-id="e0d16-206">Yükleme işlemine gerçekleştirme `--upgrade` komutu agent'ın tüm bileşenleri en son sürüme yükseltir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-206">Performing the installation with the `--upgrade` command upgrades all components of the agent to the latest version.</span></span>

## <a name="installing-the-agent"></a><span data-ttu-id="e0d16-207">Aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="e0d16-207">Installing the agent</span></span>

<span data-ttu-id="e0d16-208">Bu bölümde, Debian ve RPM paketlerini her aracı bileşenlerini içeren bir bunndle kullanarak Linux için OMS Aracısı'nı yüklemeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="e0d16-208">This section describes how to install the OMS Agent for Linux using a bunndle, which contains Debian and RPM packages for each of the agent components.</span></span>  <span data-ttu-id="e0d16-209">Doğrudan yüklü veya tek tek paketleri almaya ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="e0d16-209">It can be installed directly or extracted to retrieve the individual packages.</span></span>  

<span data-ttu-id="e0d16-210">Öncelikle, OMS çalışma alanı kimliği ve geçiş yaparak bulabilirsiniz anahtarınızı gerekir [OMS Klasik portal](https://mms.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e0d16-210">First you need your OMS workspace ID and key, which you can find by switching to the [OMS classic portal](https://mms.microsoft.com).</span></span>  <span data-ttu-id="e0d16-211">Üzerinde **genel bakış** sayfasından üst menü Seç **ayarları**ve ardından gidin **bağlı Sources\Linux sunuculara**.</span><span class="sxs-lookup"><span data-stu-id="e0d16-211">On the **Overview** page, from the top menu select **Settings**, and then navigate to **Connected Sources\Linux Servers**.</span></span>  <span data-ttu-id="e0d16-212">Değerin sağındaki bkz **çalışma alanı kimliği** ve **birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="e0d16-212">You see the value to the right of **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="e0d16-213">Kopyalayın ve her ikisi de, sık kullanılan düzenleyicisine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e0d16-213">Copy and paste both into your favorite editor.</span></span>    

1. <span data-ttu-id="e0d16-214">En son karşıdan [Linux (x64) için OMS aracısının](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) veya [Linux x86 için OMS aracısının](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) github'dan.</span><span class="sxs-lookup"><span data-stu-id="e0d16-214">Download the latest [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) or [OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) from GitHub.</span></span>  
2. <span data-ttu-id="e0d16-215">Uygun paket (x86 veya x64) scp/sftp kullanarak Linux bilgisayarınıza aktarın.</span><span class="sxs-lookup"><span data-stu-id="e0d16-215">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span></span>
3. <span data-ttu-id="e0d16-216">Kullanarak paket yükleme `--install` veya `--upgrade` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="e0d16-216">Install the bundle by using the `--install` or `--upgrade` argument.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e0d16-217">Varolan tüm paketler, ne zaman Linux için System Center Operations Manager Aracısı zaten yüklü gibi yüklediyseniz kullanın `--upgrade` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="e0d16-217">If any existing packages are installed such as when the System Center Operations Manager agent for Linux is already installed, use the `--upgrade` argument.</span></span> <span data-ttu-id="e0d16-218">Yükleme sırasında Operations Management Suite'e bağlamak için sağlamanız `-w <WorkspaceID>` ve `-s <Shared Key>` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="e0d16-218">To connect to Operations Management Suite during installation, provide the `-w <WorkspaceID>` and `-s <Shared Key>` parameters.</span></span>


#### <a name="to-install-and-onboard-directly"></a><span data-ttu-id="e0d16-219">Yüklemek için ve yerleşik doğrudan</span><span class="sxs-lookup"><span data-stu-id="e0d16-219">To install and onboard directly</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="to-upgrade-the-agent-package"></a><span data-ttu-id="e0d16-220">Aracı paketini yükseltmek için</span><span class="sxs-lookup"><span data-stu-id="e0d16-220">To upgrade the agent package</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="to-install-and-onboard-to-a-workspace-in-us-government-cloud"></a><span data-ttu-id="e0d16-221">Yüklemek için ve bir çalışma alanına US Government bulutta yerleşik</span><span class="sxs-lookup"><span data-stu-id="e0d16-221">To install and onboard to a workspace in US Government Cloud</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a><span data-ttu-id="e0d16-222">Aracı kullanmak için bir HTTP proxy sunucusu veya OMS ağ geçidi ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e0d16-222">Configuring the agent for use with an HTTP proxy server or OMS Gateway</span></span>
<span data-ttu-id="e0d16-223">Linux için OMS Aracısı, bir HTTP veya HTTPS proxy sunucusu veya OMS hizmetine OMS ağ geçidi ile iletişim kurmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e0d16-223">The OMS Agent for Linux supports communicating either through an HTTP or HTTPS proxy server or OMS Gateway to the OMS service.</span></span>  <span data-ttu-id="e0d16-224">Anonim ve temel kimlik doğrulaması (kullanıcı adı/parola) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-224">Both anonymous and basic authentication (username/password) is supported.</span></span>  

### <a name="proxy-configuration"></a><span data-ttu-id="e0d16-225">Proxy yapılandırması</span><span class="sxs-lookup"><span data-stu-id="e0d16-225">Proxy configuration</span></span>
<span data-ttu-id="e0d16-226">Proxy yapılandırma değeri sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e0d16-226">The proxy configuration value has the following syntax:</span></span>

`[protocol://][user:password@]proxyhost[:port]`

<span data-ttu-id="e0d16-227">Özellik</span><span class="sxs-lookup"><span data-stu-id="e0d16-227">Property</span></span>|<span data-ttu-id="e0d16-228">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e0d16-228">Description</span></span>
-|-
<span data-ttu-id="e0d16-229">Protokol</span><span class="sxs-lookup"><span data-stu-id="e0d16-229">Protocol</span></span>|<span data-ttu-id="e0d16-230">HTTP veya https</span><span class="sxs-lookup"><span data-stu-id="e0d16-230">http or https</span></span>
<span data-ttu-id="e0d16-231">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="e0d16-231">user</span></span>|<span data-ttu-id="e0d16-232">Proxy kimlik doğrulaması için isteğe bağlı kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="e0d16-232">Optional username for proxy authentication</span></span>
<span data-ttu-id="e0d16-233">password</span><span class="sxs-lookup"><span data-stu-id="e0d16-233">password</span></span>|<span data-ttu-id="e0d16-234">Proxy kimlik doğrulaması için isteğe bağlı parola</span><span class="sxs-lookup"><span data-stu-id="e0d16-234">Optional password for proxy authentication</span></span>
<span data-ttu-id="e0d16-235">proxyhost</span><span class="sxs-lookup"><span data-stu-id="e0d16-235">proxyhost</span></span>|<span data-ttu-id="e0d16-236">Adres veya proxy sunucu/OMS ağ geçidi FQDN'sini</span><span class="sxs-lookup"><span data-stu-id="e0d16-236">Address or FQDN of the proxy server/OMS Gateway</span></span>
<span data-ttu-id="e0d16-237">port</span><span class="sxs-lookup"><span data-stu-id="e0d16-237">port</span></span>|<span data-ttu-id="e0d16-238">Proxy sunucu/OMS ağ geçidi için isteğe bağlı bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="e0d16-238">Optional port number for the proxy server/OMS Gateway</span></span>

<span data-ttu-id="e0d16-239">Örneğin, `http://user01:password@proxy01.contoso.com:8080`</span><span class="sxs-lookup"><span data-stu-id="e0d16-239">For example: `http://user01:password@proxy01.contoso.com:8080`</span></span>

<span data-ttu-id="e0d16-240">Proxy sunucusu yüklemesi sırasında veya yükleme işleminden sonra proxy.conf yapılandırma dosyasını değiştirerek belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-240">The proxy server can be specified during installation or by modifying the proxy.conf configuration file after installation.</span></span>   

### <a name="specify-proxy-configuration-during-installation"></a><span data-ttu-id="e0d16-241">Yükleme sırasında proxy yapılandırmasını belirtin</span><span class="sxs-lookup"><span data-stu-id="e0d16-241">Specify proxy configuration during installation</span></span>
<span data-ttu-id="e0d16-242">`-p` Veya `--proxy` bağımsız değişkeni omsagent yükleme paket için kullanılacak proxy yapılandırması belirtir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-242">The `-p` or `--proxy` argument for the omsagent installation bundle specifies the proxy configuration to use.</span></span> 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-the-proxy-configuration-in-a-file"></a><span data-ttu-id="e0d16-243">Bir dosyada proxy yapılandırmasını tanımlayın</span><span class="sxs-lookup"><span data-stu-id="e0d16-243">Define the proxy configuration in a file</span></span>
<span data-ttu-id="e0d16-244">Proxy yapılandırma dosyalarında ayarlanabilir `/etc/opt/microsoft/omsagent/proxy.conf` ve `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span><span class="sxs-lookup"><span data-stu-id="e0d16-244">The proxy configuration can be set in the files `/etc/opt/microsoft/omsagent/proxy.conf`  and `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span></span> <span data-ttu-id="e0d16-245">Dosyaları doğrudan oluşturduğunuz veya düzenlediğiniz, ancak bunların izinlerini omiuser kullanıcı okuma dosyalarda izni vermek için güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-245">The files can be directly created or edited, but their permissions must be updated to grant the omiuser user read permission on the files.</span></span> <span data-ttu-id="e0d16-246">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e0d16-246">For example:</span></span>
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-the-proxy-configuration"></a><span data-ttu-id="e0d16-247">Proxy yapılandırması kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="e0d16-247">Removing the proxy configuration</span></span>
<span data-ttu-id="e0d16-248">Önceden tanımlanmış proxy yapılandırmasını kaldırın ve doğrudan bağlantı geri döndürmek için proxy.conf dosyayı kaldırın:</span><span class="sxs-lookup"><span data-stu-id="e0d16-248">To remove a previously defined proxy configuration and revert to direct connectivity, remove the proxy.conf file:</span></span>
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a><span data-ttu-id="e0d16-249">Operations Management Suite ile ekleme</span><span class="sxs-lookup"><span data-stu-id="e0d16-249">Onboarding with Operations Management Suite</span></span>
<span data-ttu-id="e0d16-250">Bir çalışma alanı kimliği ve anahtarı paket yükleme sırasında sağlanan değil, aracı sonradan Operations Management Suite ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-250">If a workspace ID and key were not provided during the bundle installation, the agent must be subsequently registered with Operations Management Suite.</span></span>

### <a name="onboarding-using-the-command-line"></a><span data-ttu-id="e0d16-251">Komut satırını kullanarak ekleme</span><span class="sxs-lookup"><span data-stu-id="e0d16-251">Onboarding using the command line</span></span>
<span data-ttu-id="e0d16-252">Çalışma alanınız için anahtarı ve çalışma alanı kimliği sağladığını omsadmin.sh komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e0d16-252">Run the omsadmin.sh command supplying the workspace id and key for your workspace.</span></span> <span data-ttu-id="e0d16-253">Bu komut (sudo yükseltmesi ile) kök olarak çalıştırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e0d16-253">This command must be run as root (with sudo elevation):</span></span>
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a><span data-ttu-id="e0d16-254">Bir dosyayı kullanarak ekleme</span><span class="sxs-lookup"><span data-stu-id="e0d16-254">Onboarding using a file</span></span>
1.  <span data-ttu-id="e0d16-255">Dosyayı oluşturma `/etc/omsagent-onboard.conf`.</span><span class="sxs-lookup"><span data-stu-id="e0d16-255">Create the file `/etc/omsagent-onboard.conf`.</span></span> <span data-ttu-id="e0d16-256">Dosya okunabilir ve yazılabilir bir kök olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e0d16-256">The file must be readable and writable for root.</span></span>
`sudo vi /etc/omsagent-onboard.conf`
2.  <span data-ttu-id="e0d16-257">Çalışma alanı kimliği ve paylaşılan anahtar ile dosyasında aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e0d16-257">Insert the following lines in the file with your Workspace ID and Shared Key:</span></span>

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  <span data-ttu-id="e0d16-258">OMS Onboard için aşağıdaki komutu çalıştırın:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span><span class="sxs-lookup"><span data-stu-id="e0d16-258">Run the following command to Onboard to OMS: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span></span>
4.  <span data-ttu-id="e0d16-259">Dosya üzerinde başarıyla Hazırlanmanız silinir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-259">The file is deleted on successful onboarding.</span></span>

## <a name="enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager"></a><span data-ttu-id="e0d16-260">System Center Operations Manager için rapor Linux için OMS aracısının etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e0d16-260">Enable the OMS Agent for Linux to report to System Center Operations Manager</span></span>
<span data-ttu-id="e0d16-261">System Center Operations Manager yönetim grubu için rapor Linux için OMS aracısının yapılandırmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="e0d16-261">Perform the following steps to configure the OMS Agent for Linux to report to a System Center Operations Manager management group.</span></span>  

1. <span data-ttu-id="e0d16-262">Dosyayı düzenleyin.`/etc/opt/omi/conf/omiserver.conf`</span><span class="sxs-lookup"><span data-stu-id="e0d16-262">Edit the file `/etc/opt/omi/conf/omiserver.conf`</span></span>
2. <span data-ttu-id="e0d16-263">Satır başlayarak emin **httpsport =** bağlantı noktası 1270 tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e0d16-263">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="e0d16-264">Örneğin:`httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="e0d16-264">Such as: `httpsport=1270`</span></span>
3. <span data-ttu-id="e0d16-265">OMI sunucuyu yeniden başlatın:`sudo /opt/omi/bin/service_control restart`</span><span class="sxs-lookup"><span data-stu-id="e0d16-265">Restart the OMI server: `sudo /opt/omi/bin/service_control restart`</span></span>

## <a name="agent-logs"></a><span data-ttu-id="e0d16-266">Aracı günlükleri</span><span class="sxs-lookup"><span data-stu-id="e0d16-266">Agent logs</span></span>
<span data-ttu-id="e0d16-267">Linux için OMS aracısının günlüklerinde bulunabilir: `/var/opt/microsoft/omsagent/<workspace id>/log/` omsconfig (Aracısı yapılandırması) programı günlüklerinde bulunabilir: `/var/opt/microsoft/omsconfig/log/` (performans ölçüm verilerini sağlayan) OMI ve scx farklı bileşenlerin günlüklerinde bulunabilir:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span><span class="sxs-lookup"><span data-stu-id="e0d16-267">The logs for the OMS Agent for Linux can be found at: `/var/opt/microsoft/omsagent/<workspace id>/log/` The logs for the omsconfig (agent configuration) program can be found at: `/var/opt/microsoft/omsconfig/log/` Logs for the OMI and SCX components (which provide performance metrics data) can be found at: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span></span>

### <a name="log-rotation-configuration"></a><span data-ttu-id="e0d16-268">Günlük döndürme yapılandırma ##</span><span class="sxs-lookup"><span data-stu-id="e0d16-268">Log rotation configuration##</span></span>
<span data-ttu-id="e0d16-269">Günlük döndürme yapılandırması omsagent için yolda bulunabilir:`/etc/logrotate.d/omsagent-<workspace id>`</span><span class="sxs-lookup"><span data-stu-id="e0d16-269">The log rotate configuration for omsagent can be found at: `/etc/logrotate.d/omsagent-<workspace id>`</span></span>

<span data-ttu-id="e0d16-270">Varsayılan ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e0d16-270">The default settings are:</span></span> 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-the-oms-agent-for-linux"></a><span data-ttu-id="e0d16-271">Linux için OMS aracısı kaldırma</span><span class="sxs-lookup"><span data-stu-id="e0d16-271">Uninstalling the OMS Agent for Linux</span></span>
<span data-ttu-id="e0d16-272">Paket .sh dosyasıyla çalıştırarak aracı paketlerini kaldırılabilir `--purge` aracı ve yapılandırmasıyla bilgisayarınızdan tamamen kaldırır bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="e0d16-272">The agent packages can be uninstalled by running the bundle .sh file with the `--purge` argument, which completely removes the agent and its configuration from the computer.</span></span>   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a><span data-ttu-id="e0d16-273">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e0d16-273">Troubleshooting</span></span>

### <a name="issue-unable-to-connect-through-proxy-to-oms"></a><span data-ttu-id="e0d16-274">Sorun: OMS proxy'si aracılığıyla bağlanılamıyor</span><span class="sxs-lookup"><span data-stu-id="e0d16-274">Issue: Unable to connect through proxy to OMS</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="e0d16-275">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="e0d16-275">Probable causes</span></span>
* <span data-ttu-id="e0d16-276">Onboarding işlemi sırasında belirtilen proxy yanlış</span><span class="sxs-lookup"><span data-stu-id="e0d16-276">The proxy specified during onboarding was incorrect</span></span>
* <span data-ttu-id="e0d16-277">OMS hizmet uç noktaları, veri merkezinizdeki whitelistested değildir</span><span class="sxs-lookup"><span data-stu-id="e0d16-277">The OMS Service Endpoints are not whitelistested in your datacenter</span></span> 

#### <a name="resolutions"></a><span data-ttu-id="e0d16-278">Çözümler</span><span class="sxs-lookup"><span data-stu-id="e0d16-278">Resolutions</span></span>
1. <span data-ttu-id="e0d16-279">Reonboard seçeneği ile aşağıdaki komutu kullanarak Linux için OMS Aracısı ile OMS hizmetine `-v` etkin.</span><span class="sxs-lookup"><span data-stu-id="e0d16-279">Reonboard to the OMS Service with the OMS Agent for Linux by using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="e0d16-280">Bu OMS hizmetine proxy üzerinden bağlanma Aracısı'nın ayrıntılı çıktı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0d16-280">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span> 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. <span data-ttu-id="e0d16-281">Bölümünü gözden [aracı kullanmak için bir HTTP Ara sunucusunu yapılandırma server(#configuring the-agent-for-use-with-a-http-proxy-server) düzgün bir şekilde yapılandırdığınız bir proxy sunucu üzerinden iletişim kurmak için aracıyı doğrulanamadı.</span><span class="sxs-lookup"><span data-stu-id="e0d16-281">Review the section [Configuring the agent for use with an HTTP proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) to verify you have properly configured the agent to communicate through a proxy server.</span></span>    
* <span data-ttu-id="e0d16-282">Aşağıdaki OMS hizmet uç noktalarına Güvenilenler listesine olduğunu kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="e0d16-282">Double check that the following OMS Service endpoints are whitelisted:</span></span>

    |<span data-ttu-id="e0d16-283">Aracı Kaynağı</span><span class="sxs-lookup"><span data-stu-id="e0d16-283">Agent Resource</span></span>| <span data-ttu-id="e0d16-284">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="e0d16-284">Ports</span></span> |  
    |------|---------|  
    |<span data-ttu-id="e0d16-285">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="e0d16-285">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="e0d16-286">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="e0d16-286">Port 443</span></span>|   
    |<span data-ttu-id="e0d16-287">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="e0d16-287">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="e0d16-288">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="e0d16-288">Port 443</span></span>|   
    |<span data-ttu-id="e0d16-289">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="e0d16-289">ods.systemcenteradvisor.com</span></span> | <span data-ttu-id="e0d16-290">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="e0d16-290">Port 443</span></span>|   
    |<span data-ttu-id="e0d16-291">*.BLOB.Core.Windows.NET/</span><span class="sxs-lookup"><span data-stu-id="e0d16-291">*.blob.core.windows.net/</span></span> | <span data-ttu-id="e0d16-292">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="e0d16-292">Port 443</span></span>|   

### <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a><span data-ttu-id="e0d16-293">Sorun: Bir 403 hatası için yerleşik çalışırken alıyorsunuz</span><span class="sxs-lookup"><span data-stu-id="e0d16-293">Issue: You receive a 403 error when trying to onboard</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="e0d16-294">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="e0d16-294">Probable causes</span></span>
* <span data-ttu-id="e0d16-295">Tarih ve saat, Linux sunucusu üzerinde yanlış</span><span class="sxs-lookup"><span data-stu-id="e0d16-295">Date and Time is incorrect on Linux Server</span></span> 
* <span data-ttu-id="e0d16-296">Çalışma alanı kimliği ve çalışma alanı anahtarı doğru değil</span><span class="sxs-lookup"><span data-stu-id="e0d16-296">Workspace ID and Workspace Key used are not correct</span></span>

#### <a name="resolution"></a><span data-ttu-id="e0d16-297">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e0d16-297">Resolution</span></span>

1. <span data-ttu-id="e0d16-298">Linux sunucunuzla komutu tarih zamanını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e0d16-298">Check the time on your Linux server with the command date.</span></span> <span data-ttu-id="e0d16-299">Saati geçerli saatten 15 dakika +/-ise ekleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e0d16-299">If the time is +/- 15 minutes from current time, then onboarding fails.</span></span> <span data-ttu-id="e0d16-300">Doğru Bu güncelleştirme için tarih ve/veya saat dilimi Linux sunucunuzun.</span><span class="sxs-lookup"><span data-stu-id="e0d16-300">To correct this update the date and/or timezone of your Linux server.</span></span> 
2. <span data-ttu-id="e0d16-301">Linux için OMS aracısının en son sürümünün yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e0d16-301">Verify you have installed the latest version of the OMS Agent for Linux.</span></span>  <span data-ttu-id="e0d16-302">En yeni sürümü şimdi zaman farkı, onboarding hataya neden olduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-302">The newest version now notifies you if time skew is causing the onboarding failure.</span></span>
3. <span data-ttu-id="e0d16-303">Doğru çalışma alanı kimliği ve çalışma alanı bu konunun önceki kısımlarında yükleme yönergeleri izleyerek anahtarı kullanarak Reonboard.</span><span class="sxs-lookup"><span data-stu-id="e0d16-303">Reonboard using correct Workspace ID and Workspace Key following the installation instructions earlier in this topic.</span></span>

### <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a><span data-ttu-id="e0d16-304">Sorun: Sağ onboarding sonra 500 ve 404 Hata günlük dosyasına bakın</span><span class="sxs-lookup"><span data-stu-id="e0d16-304">Issue: You see a 500 and 404 error in the log file right after onboarding</span></span>
<span data-ttu-id="e0d16-305">Bu OMS çalışma alanına Linux verilerin ilk karşıya yükleme sırasında oluşan bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="e0d16-305">This is a known issue that occurs on first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="e0d16-306">Bu verilerin gönderilen veya servis deneyimi olmasıyla etkilemez.</span><span class="sxs-lookup"><span data-stu-id="e0d16-306">This does not affect data being sent or service experience.</span></span>

### <a name="issue--you-are-not-seeing-any-data-in-the-oms-portal"></a><span data-ttu-id="e0d16-307">Sorun: Herhangi bir veri OMS portalında gördüğünüz değil</span><span class="sxs-lookup"><span data-stu-id="e0d16-307">Issue:  You are not seeing any data in the OMS portal</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="e0d16-308">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="e0d16-308">Probable causes</span></span>

- <span data-ttu-id="e0d16-309">OMS hizmetine ekleme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="e0d16-309">Onboarding to the OMS Service failed</span></span>
- <span data-ttu-id="e0d16-310">OMS hizmetine bağlantı engellendi</span><span class="sxs-lookup"><span data-stu-id="e0d16-310">Connection to the OMS Service is blocked</span></span>
- <span data-ttu-id="e0d16-311">Linux veriler için OMS aracısının yedeklenir</span><span class="sxs-lookup"><span data-stu-id="e0d16-311">OMS Agent for Linux data is backed up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="e0d16-312">Çözümler</span><span class="sxs-lookup"><span data-stu-id="e0d16-312">Resolutions</span></span>
1. <span data-ttu-id="e0d16-313">Aşağıdaki dosya olup olmadığını kontrol ederek ekleme OMS hizmetine başarılı olup olmadığını kontrol edin:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span><span class="sxs-lookup"><span data-stu-id="e0d16-313">Check if onboarding the OMS Service was successful by checking if the following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span></span>
2. <span data-ttu-id="e0d16-314">Reonboard kullanarak `omsadmin.sh` komut satırı yönergeleri</span><span class="sxs-lookup"><span data-stu-id="e0d16-314">Reonboard using the `omsadmin.sh` command-line instructions</span></span>
3. <span data-ttu-id="e0d16-315">Bir proxy sunucu kullanıyorsanız, daha önce sağlanan proxy çözüm adımlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="e0d16-315">If using a proxy, refer to the proxy resolution steps provided earlier.</span></span>
4. <span data-ttu-id="e0d16-316">Linux için OMS aracısının OMS hizmetiyle iletişim kuramadığında bazı durumlarda, aracı veri 50 MB'tır tam arabellek boyutu için sıraya alındı.</span><span class="sxs-lookup"><span data-stu-id="e0d16-316">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the agent is queued to the full buffer size, which is 50 MB.</span></span> <span data-ttu-id="e0d16-317">Linux için OMS aracısı aşağıdaki komutu çalıştırarak yeniden başlatılması gerekir: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span><span class="sxs-lookup"><span data-stu-id="e0d16-317">The OMS Agent for Linux should be restarted by running the following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="e0d16-318">Aracı sürümü 1.1.0-28 ve daha sonra bu sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e0d16-318">This issue is fixed in agent version 1.1.0-28 and later.</span></span>
> 