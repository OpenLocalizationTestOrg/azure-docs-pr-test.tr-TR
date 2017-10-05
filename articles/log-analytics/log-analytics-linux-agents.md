---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a><span data-ttu-id="9a31c-101">Linux bilgisayarlarınızı günlük Analizi'ne bağlayın</span><span class="sxs-lookup"><span data-stu-id="9a31c-101">Connect your Linux computers to Log Analytics</span></span>
<span data-ttu-id="9a31c-102">Günlük analizi kullanarak toplamak ve Linux bilgisayarları oluşturulan veri hareket.</span><span class="sxs-lookup"><span data-stu-id="9a31c-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="9a31c-103">Linux OMS için toplanan verileri eklemeye izin verir, Linux sistemleri ve nerede olursa olsun bilgisayarlarınızı Docker gibi kapsayıcı çözümleri yönetmek — neredeyse her yerden.</span><span class="sxs-lookup"><span data-stu-id="9a31c-103">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="9a31c-104">Veri kaynakları, Amazon Web Hizmetleri (AWS) veya Microsoft Azure veya hatta masanıza dizüstü bilgisayar gibi bir bulutta barındırılan hizmetindeki sanal bilgisayarlar fiziksel sunucuları olarak, şirket içi veri merkezinizde bulunması.</span><span class="sxs-lookup"><span data-stu-id="9a31c-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span></span> <span data-ttu-id="9a31c-105">Gerçekten karma BT ortamında destekler şekilde ek olarak, OMS ayrıca Windows bilgisayarlardan benzer şekilde, toplar.</span><span class="sxs-lookup"><span data-stu-id="9a31c-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="9a31c-106">Görüntüleme ve tüm OMS günlük analizi ile bu kaynakları tek bir Yönetim Portalı ile verileri yönetme.</span><span class="sxs-lookup"><span data-stu-id="9a31c-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="9a31c-107">Bu, birçok farklı sistemleri, kullanmak kolay ve hangi iş analiz çözümü veya zaten sistem istediğiniz herhangi bir veri verebilirsiniz yapar kullanarak izlemek için gereken azaltır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-107">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="9a31c-108">Bu makalede, bir hızlı başlangıç toplamak ve Linux için OMS Aracısı'nı kullanarak, Linux bilgisayarların verilerini yönetmenize yardımcı olacak Kılavuzu ' dir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span></span> <span data-ttu-id="9a31c-109">Proxy sunucu yapılandırması, CollectD ölçümleri ve özel JSON veri kaynakları hakkında bilgi gibi daha fazla teknik bilgi için bu bilgileri bulabilirsiniz [Linux genel bakış için OMS Aracısı](https://github.com/Microsoft/OMS-Agent-for-Linux) ve [Linux için OMS Aracısı tam belgelerine](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) github'da.</span><span class="sxs-lookup"><span data-stu-id="9a31c-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="9a31c-110">Şu anda aşağıdaki veri türlerini Linux bilgisayarlardan toplayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a31c-110">Currently, you can collect the following types of data from Linux computers:</span></span>

* <span data-ttu-id="9a31c-111">Performans ölçümleri</span><span class="sxs-lookup"><span data-stu-id="9a31c-111">Performance metrics</span></span>
* <span data-ttu-id="9a31c-112">Syslog olayları</span><span class="sxs-lookup"><span data-stu-id="9a31c-112">Syslog events</span></span>
* <span data-ttu-id="9a31c-113">Nagios ve Zabbix uyarıları</span><span class="sxs-lookup"><span data-stu-id="9a31c-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="9a31c-114">Docker kapsayıcısı performans ölçümleri, Envanter ve günlükleri</span><span class="sxs-lookup"><span data-stu-id="9a31c-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="9a31c-115">Desteklenen Linux sürümleri</span><span class="sxs-lookup"><span data-stu-id="9a31c-115">Supported Linux versions</span></span>
<span data-ttu-id="9a31c-116">Hem x86 hem x64 sürümleri Linux dağıtımları çeşitli resmi olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="9a31c-117">Ancak, OMS Aracısı Linux için listelenmeyen diğer dağıtımlar da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-117">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="9a31c-118">Amazon Linux 2015.09 aracılığıyla 2012.09</span><span class="sxs-lookup"><span data-stu-id="9a31c-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="9a31c-119">CentOS Linux 5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="9a31c-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="9a31c-120">Oracle Linux 5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="9a31c-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="9a31c-121">Red Hat Enterprise Linux Server 5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="9a31c-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="9a31c-122">Debian GNU/Linux 6, 7 ve 8</span><span class="sxs-lookup"><span data-stu-id="9a31c-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="9a31c-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="9a31c-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="9a31c-124">SUSE Linux Enterprise Server 11 ve 12</span><span class="sxs-lookup"><span data-stu-id="9a31c-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="9a31c-125">Linux için OMS Aracısı</span><span class="sxs-lookup"><span data-stu-id="9a31c-125">OMS Agent for Linux</span></span>
<span data-ttu-id="9a31c-126">Linux için Operations Management Suite Aracısı birden çok paket oluşur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-126">The Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="9a31c-127">Aşağıdaki paketler, kabuk Paketle çalıştırarak kullanılabilir sürüm dosyasını içeren `--extract`.</span><span class="sxs-lookup"><span data-stu-id="9a31c-127">The release file contains the following packages, available by running the shell bundle with `--extract`.</span></span>

| <span data-ttu-id="9a31c-128">**Paket**</span><span class="sxs-lookup"><span data-stu-id="9a31c-128">**Package**</span></span> | <span data-ttu-id="9a31c-129">**Sürüm**</span><span class="sxs-lookup"><span data-stu-id="9a31c-129">**Version**</span></span> | <span data-ttu-id="9a31c-130">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="9a31c-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9a31c-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="9a31c-131">omsagent</span></span> |<span data-ttu-id="9a31c-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9a31c-132">1.1.0</span></span> |<span data-ttu-id="9a31c-133">Linux için Operations Management Suite Aracısı</span><span class="sxs-lookup"><span data-stu-id="9a31c-133">The Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="9a31c-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="9a31c-134">omsconfig</span></span> |<span data-ttu-id="9a31c-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="9a31c-135">1.1.1</span></span> |<span data-ttu-id="9a31c-136">OMS aracısı için yapılandırma aracısı</span><span class="sxs-lookup"><span data-stu-id="9a31c-136">Configuration agent for the OMS Agent</span></span> |
| <span data-ttu-id="9a31c-137">OMI</span><span class="sxs-lookup"><span data-stu-id="9a31c-137">omi</span></span> |<span data-ttu-id="9a31c-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="9a31c-138">1.0.8.3</span></span> |<span data-ttu-id="9a31c-139">Açık Yönetim Altyapısı (OMI)--bir basit CIM sunucusu</span><span class="sxs-lookup"><span data-stu-id="9a31c-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="9a31c-140">scx</span><span class="sxs-lookup"><span data-stu-id="9a31c-140">scx</span></span> |<span data-ttu-id="9a31c-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="9a31c-141">1.6.2</span></span> |<span data-ttu-id="9a31c-142">İşletim sistemi performans ölçümleri için OMI CIM sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="9a31c-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="9a31c-143">Apache cimprov</span><span class="sxs-lookup"><span data-stu-id="9a31c-143">apache-cimprov</span></span> |<span data-ttu-id="9a31c-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9a31c-144">1.0.0</span></span> |<span data-ttu-id="9a31c-145">Apache HTTP Server performansı sağlayıcısı OMI için izleme.</span><span class="sxs-lookup"><span data-stu-id="9a31c-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="9a31c-146">Apache HTTP Server algılanırsa, yalnızca yüklü.</span><span class="sxs-lookup"><span data-stu-id="9a31c-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="9a31c-147">MySQL cimprov</span><span class="sxs-lookup"><span data-stu-id="9a31c-147">mysql-cimprov</span></span> |<span data-ttu-id="9a31c-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9a31c-148">1.0.0</span></span> |<span data-ttu-id="9a31c-149">MySQL sunucusu performans sağlayıcısı OMI için izleme.</span><span class="sxs-lookup"><span data-stu-id="9a31c-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="9a31c-150">MySQL/MariaDB sunucu algılanırsa, yalnızca yüklü.</span><span class="sxs-lookup"><span data-stu-id="9a31c-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="9a31c-151">docker cimprov</span><span class="sxs-lookup"><span data-stu-id="9a31c-151">docker-cimprov</span></span> |<span data-ttu-id="9a31c-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="9a31c-152">0.1.0</span></span> |<span data-ttu-id="9a31c-153">OMI docker sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-153">Docker provider for OMI.</span></span> <span data-ttu-id="9a31c-154">Docker algılanırsa, yalnızca yüklü.</span><span class="sxs-lookup"><span data-stu-id="9a31c-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="9a31c-155">Ek yükleme yapıları</span><span class="sxs-lookup"><span data-stu-id="9a31c-155">Additional installation artifacts</span></span>
<span data-ttu-id="9a31c-156">Linux paketler için OMS Aracısı yükledikten sonra aşağıdaki ek sistem genelinde yapılandırma değişikliklerini uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-156">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="9a31c-157">Bu yapıtların omsagent paket kaldırıldığında kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-157">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="9a31c-158">Adlı bir ayrıcalıklı olmayan kullanıcı: `omsagent` oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="9a31c-159">Bu olarak omsagent arka plan programı çalıştıran hesabıdır</span><span class="sxs-lookup"><span data-stu-id="9a31c-159">This is the account the omsagent daemon runs as</span></span>
* <span data-ttu-id="9a31c-160">"Ekle" sudoers dosyası oluşturulur /etc/sudoers.d/omsagent bu syslog ve omsagent Daemon başlatmayı omsagent yetkilendirir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="9a31c-161">Sudo "Ekle" yönergeleri sudo yüklü sürümünde desteklenmez Bu girdiler için /etc/sudoers yazılır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-161">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span></span>
* <span data-ttu-id="9a31c-162">Syslog yapılandırma aracıya bir alt olayların iletecek şekilde değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-162">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="9a31c-163">Daha fazla bilgi için bkz: **yapılandırma veri toplama** bölümüne bakın</span><span class="sxs-lookup"><span data-stu-id="9a31c-163">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="9a31c-164">Linux veri toplama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="9a31c-164">Linux data collection details</span></span>
<span data-ttu-id="9a31c-165">Aşağıdaki tabloda, veri toplama yöntemleri ve verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-165">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="9a31c-166">Kaynak</span><span class="sxs-lookup"><span data-stu-id="9a31c-166">source</span></span> | <span data-ttu-id="9a31c-167">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="9a31c-167">Direct Agent</span></span> | <span data-ttu-id="9a31c-168">SCOM Aracısı</span><span class="sxs-lookup"><span data-stu-id="9a31c-168">SCOM agent</span></span> | <span data-ttu-id="9a31c-169">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9a31c-169">Azure Storage</span></span> | <span data-ttu-id="9a31c-170">SCOM gerekli?</span><span class="sxs-lookup"><span data-stu-id="9a31c-170">SCOM required?</span></span> | <span data-ttu-id="9a31c-171">Yönetim grubu gönderilen SCOM Aracısı verileri</span><span class="sxs-lookup"><span data-stu-id="9a31c-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="9a31c-172">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="9a31c-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9a31c-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="9a31c-173">Zabbix</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9a31c-179">1 dakika</span><span class="sxs-lookup"><span data-stu-id="9a31c-179">1 minute</span></span> |
| <span data-ttu-id="9a31c-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="9a31c-180">Nagios</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9a31c-186">geldiğinde</span><span class="sxs-lookup"><span data-stu-id="9a31c-186">on arrival</span></span> |
| <span data-ttu-id="9a31c-187">syslog</span><span class="sxs-lookup"><span data-stu-id="9a31c-187">syslog</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9a31c-193">Azure depolama biriminden: 10 dakika; aracısından: işle</span><span class="sxs-lookup"><span data-stu-id="9a31c-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="9a31c-194">Linux performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="9a31c-194">Linux performance counters</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9a31c-200">Zamanlandığı gibi en az 10 saniye</span><span class="sxs-lookup"><span data-stu-id="9a31c-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="9a31c-201">değişiklik izleme</span><span class="sxs-lookup"><span data-stu-id="9a31c-201">change tracking</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="9a31c-207">saatlik</span><span class="sxs-lookup"><span data-stu-id="9a31c-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="9a31c-208">Paket gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="9a31c-208">Package Requirements</span></span>
| <span data-ttu-id="9a31c-209">**Gerekli paket**</span><span class="sxs-lookup"><span data-stu-id="9a31c-209">**Required package**</span></span> | <span data-ttu-id="9a31c-210">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="9a31c-210">**Description**</span></span> | <span data-ttu-id="9a31c-211">**En düşük sürüm**</span><span class="sxs-lookup"><span data-stu-id="9a31c-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9a31c-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="9a31c-212">Glibc</span></span> |<span data-ttu-id="9a31c-213">GNU C Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="9a31c-213">GNU C library</span></span> |<span data-ttu-id="9a31c-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="9a31c-214">2.5-12</span></span> |
| <span data-ttu-id="9a31c-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="9a31c-215">Openssl</span></span> |<span data-ttu-id="9a31c-216">OpenSSL kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="9a31c-216">OpenSSL libraries</span></span> |<span data-ttu-id="9a31c-217">0.9.8E veya 1.0</span><span class="sxs-lookup"><span data-stu-id="9a31c-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="9a31c-218">Curl</span><span class="sxs-lookup"><span data-stu-id="9a31c-218">Curl</span></span> |<span data-ttu-id="9a31c-219">cURL web istemcisi</span><span class="sxs-lookup"><span data-stu-id="9a31c-219">cURL web client</span></span> |<span data-ttu-id="9a31c-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="9a31c-220">7.15.5</span></span> |
| <span data-ttu-id="9a31c-221">Python ctypes</span><span class="sxs-lookup"><span data-stu-id="9a31c-221">Python-ctypes</span></span> |<span data-ttu-id="9a31c-222">işlev kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="9a31c-222">function libraries</span></span> |<span data-ttu-id="9a31c-223">yok</span><span class="sxs-lookup"><span data-stu-id="9a31c-223">n/a</span></span> |
| <span data-ttu-id="9a31c-224">PAM</span><span class="sxs-lookup"><span data-stu-id="9a31c-224">PAM</span></span> |<span data-ttu-id="9a31c-225">Eklenebilir kimlik doğrulaması modülleri</span><span class="sxs-lookup"><span data-stu-id="9a31c-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="9a31c-226">yok</span><span class="sxs-lookup"><span data-stu-id="9a31c-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="9a31c-227">Rsyslog veya syslog ng syslog iletileri toplamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-227">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="9a31c-228">Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9a31c-228">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="9a31c-229">Bu dağıtımları bu sürümünden Syslog verileri toplamak için rsyslog arka plan programı yüklenmeli ve sysklog değiştirmek için yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-229">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="9a31c-230">Hızlı yükleme</span><span class="sxs-lookup"><span data-stu-id="9a31c-230">Quick install</span></span>
<span data-ttu-id="9a31c-231">Omsagent indirin, sağlama toplamı doğrulama, daha sonra yüklemek için aşağıdaki komutları çalıştırın ve yerleşik aracı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-231">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span></span> <span data-ttu-id="9a31c-232">64 bit için komutlardır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-232">Commands are for 64-bit.</span></span> <span data-ttu-id="9a31c-233">Çalışma alanı kimliği ve birincil anahtar OMS portalında altında bulunan **ayarları** üzerinde **bağlı kaynakları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9a31c-233">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span></span>

![çalışma alanı ayrıntıları](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="9a31c-235">Çeşitli aracıyı yüklemek ve yükseltmek için diğer yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-235">There are a variety of other methods to install the agent and upgrade it.</span></span> <span data-ttu-id="9a31c-236">Daha fazla bilgiyi onları hakkında [Linux için OMS Aracısı'nı yüklemek için adımları](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="9a31c-236">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="9a31c-237">Ayrıca görüntüleyebilirsiniz [Azure videosu](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="9a31c-237">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="9a31c-238">Linux veri toplama yönteminizi seçin</span><span class="sxs-lookup"><span data-stu-id="9a31c-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="9a31c-239">Nasıl toplamak istediğiniz veri türlerini bağlı olarak çeşitli yapılandırma dosyalarını doğrudan Linux istemcileriniz düzenlemek istiyorsanız veya OMS portalı kullanmak isteyip istemediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-239">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="9a31c-240">Yapılandırma Portalı'nı kullanmayı tercih ederseniz, tüm Linux istemcileriniz otomatik olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-240">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span></span> <span data-ttu-id="9a31c-241">Farklı Linux istemcileri için farklı yapılandırmaları gerekiyorsa, istemci dosyalarını ayrı ayrı – düzenlemek veya PowerShell DSC, Chef veya Puppet gibi bir alternatif kullanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-241">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="9a31c-242">Syslog olayları ve Linux bilgisayarları yapılandırma dosyalarını kullanarak toplamak istediğiniz performans sayaçları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-242">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span></span> <span data-ttu-id="9a31c-243">*Veri toplama Aracısı Yapılandırma dosyalarını düzenleyerek yapılandırmak seçerseniz, merkezi yapılandırma devre dışı bırakmanız gerekir.*</span><span class="sxs-lookup"><span data-stu-id="9a31c-243">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span></span>  <span data-ttu-id="9a31c-244">Yönergeler aracısının yapılandırma dosyalarında veri toplamayı yapılandırmak için yanı sıra tüm OMS aracılar için merkezi yapılandırma Linux ya da ayrı bilgisayarlar için devre dışı bırakmak için aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-244">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="9a31c-245">Tek bir Linux bilgisayar için OMS yönetimi devre dışı</span><span class="sxs-lookup"><span data-stu-id="9a31c-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="9a31c-246">Yapılandırma verileri için merkezi veri toplama OMS_MetaConfigHelper.py betiği ile tek bir Linux bilgisayarı devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-246">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="9a31c-247">Bu, bilgisayarların alt ağlarından özel bir yapılandırmanız varsa yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="9a31c-248">Merkezi yapılandırma devre dışı bırakmak için:</span><span class="sxs-lookup"><span data-stu-id="9a31c-248">To disable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="9a31c-249">Merkezi yapılandırma yeniden etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="9a31c-249">To re-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="9a31c-250">Linux performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="9a31c-250">Linux performance counters</span></span>
<span data-ttu-id="9a31c-251">Linux performans sayaçları için Windows performans sayaçlarını benzer — her ikisi de aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-251">Linux performance counters are similar to Windows performance counters—both operate similarly.</span></span> <span data-ttu-id="9a31c-252">Ekleyin ve bunları yapılandırmak için aşağıdaki yordamları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-252">You can use the following procedures to add and configure them.</span></span> <span data-ttu-id="9a31c-253">Verileri için OMS eklendikten sonra bunlar için her 30 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-253">After they are added to OMS, data is collected for them every 30 seconds.</span></span>

### <a name="to-add-a-linux-performance-counter-in-oms"></a><span data-ttu-id="9a31c-254">Bir Linux performans sayacı OMS eklemek için</span><span class="sxs-lookup"><span data-stu-id="9a31c-254">To add a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="9a31c-255">OMS Portalı'nı kullanarak Linux için OMS aracısı yapılandırmak için Ayarlar sayfasında Linux performans sayaçlarını Ekle, tıklatın **veri**.</span><span class="sxs-lookup"><span data-stu-id="9a31c-255">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="9a31c-256">Üzerinde **ayarları** altında sayfa **veri** , tıklatın **Linux performans sayaçları** ve daha sonra seçin veya eklemek istediğiniz sayacının adını yazın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-256">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span></span>  
    <span data-ttu-id="9a31c-257">![veri](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="9a31c-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="9a31c-258">Sayacın tam adını bilmiyorsanız, kısmi bir ad yazarak başlatabilirsiniz ve kullanılabilir sayaçlarının listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-258">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="9a31c-259">Eklemek istediğiniz sayacı bulduğunuzda, listedeki adına tıklayın ve ardından sayaç eklemek için artı simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-259">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span></span>
4. <span data-ttu-id="9a31c-260">Sayaç ekledikten sonra renkli çubuk ile vurgulanan sayaçlarının listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-260">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="9a31c-261">Varsayılan olarak, **aşağıdaki yapılandırmayı makinelerime Uygula** seçeneği işaretlidir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-261">By default, the **Apply below configuration to my machines** option is selected.</span></span> <span data-ttu-id="9a31c-262">Gönderen yapılandırmasını devre dışı bırakmak seçimi temizleyin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-262">If you want to disable sending configuration data, clear the selection.</span></span>
6. <span data-ttu-id="9a31c-263">Değiştirme performans sayaçları, sayfanın sonundaki bittiğinde tıklatın **kaydetmek** değişikliklerinizi sona erdirmek için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-263">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="9a31c-264">Yaptığınız yapılandırma değişikliklerini OMS ile genellikle 5 dakika içinde kayıtlı Linux için OMS aracılara tüm sonra gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-264">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="9a31c-265">Linux performans sayaçları OMS yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9a31c-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="9a31c-266">Windows performans sayaçları için her performans sayacı için belirli bir örneği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="9a31c-267">Ancak, Linux performans sayaçları için ne olursa olsun, seçtiğiniz bir sayaç örneği üst sayacı tüm alt sayaçları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-267">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span></span> <span data-ttu-id="9a31c-268">Aşağıdaki tabloda, Linux ve Windows performans sayaçları için kullanılabilen ortak örnekleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-268">The following table shows the common instances available to both Linux and Windows performance counters.</span></span>

| <span data-ttu-id="9a31c-269">**Örnek adı**</span><span class="sxs-lookup"><span data-stu-id="9a31c-269">**Instance name**</span></span> | <span data-ttu-id="9a31c-270">**Anlamı**</span><span class="sxs-lookup"><span data-stu-id="9a31c-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="9a31c-271">\_Toplam</span><span class="sxs-lookup"><span data-stu-id="9a31c-271">\_Total</span></span> |<span data-ttu-id="9a31c-272">Tüm örnekleri toplamı</span><span class="sxs-lookup"><span data-stu-id="9a31c-272">Total of all the instances</span></span> |
| \* |<span data-ttu-id="9a31c-273">Tüm örnekleri</span><span class="sxs-lookup"><span data-stu-id="9a31c-273">All instances</span></span> |
| <span data-ttu-id="9a31c-274">(/ &#124; / var)</span><span class="sxs-lookup"><span data-stu-id="9a31c-274">(/&#124;/var)</span></span> |<span data-ttu-id="9a31c-275">Eşleşen adlandırılmış örnekleri: / veya /var</span><span class="sxs-lookup"><span data-stu-id="9a31c-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="9a31c-276">Benzer şekilde, bir üst sayaç için seçtiğiniz örnek aralığı, tüm alt sayaçlarını geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-276">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span></span> <span data-ttu-id="9a31c-277">Diğer bir deyişle, tüm alt sayacı örnek aralıklar ve örnekleri birbirine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-277">In other words, all the child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="9a31c-278">Ekleme ve performans ölçümleri Linux ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9a31c-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="9a31c-279">Performans ölçümleri toplamak için giriş/etc/opt/microsoft/omsagent yapılandırması tarafından denetlenen/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="9a31c-279">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="9a31c-280">Bkz: [kullanılabilir performans ölçümleri](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) kullanılabilir sınıfların ve Linux için OMS aracısının ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="9a31c-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span></span>

<span data-ttu-id="9a31c-281">Tek bir yapılandırma dosyasındaki her nesne veya toplamak için performans ölçümleri kategorisi tanımlanmalıdır `<source>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="9a31c-281">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span></span> <span data-ttu-id="9a31c-282">Sözdizimi deseni izler.</span><span class="sxs-lookup"><span data-stu-id="9a31c-282">The syntax follows the pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="9a31c-283">Bu öğenin yapılandırılabilir Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9a31c-283">The configurable parameters of this element are:</span></span>

* <span data-ttu-id="9a31c-284">**Nesne\_adı**: koleksiyon için nesne adı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-284">**Object\_name**: the object name for the collection.</span></span>
* <span data-ttu-id="9a31c-285">**Örnek\_regex**: bir *normal ifade* toplamak için hangi örnekleri tanımlama.</span><span class="sxs-lookup"><span data-stu-id="9a31c-285">**Instance\_regex**: a *regular expression* defining which instances to collect.</span></span> <span data-ttu-id="9a31c-286">Değer: `.*` tüm örneklerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-286">The value: `.*` specifies all instances.</span></span> <span data-ttu-id="9a31c-287">Yalnızca işlemci ölçümleri toplamak için \_toplam örneğini belirtmek `_Total`.</span><span class="sxs-lookup"><span data-stu-id="9a31c-287">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="9a31c-288">Yalnızca crond veya sshd örnekleri için işlem ölçümlerini toplamak için belirtebilirsiniz: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="9a31c-288">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="9a31c-289">**Sayaç\_adı\_regex**: bir *normal ifade* hangi toplamak için (nesne için) sayaçları tanımlama.</span><span class="sxs-lookup"><span data-stu-id="9a31c-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span></span> <span data-ttu-id="9a31c-290">Nesne için tüm sayaçlar toplanacak belirtin: `.*`.</span><span class="sxs-lookup"><span data-stu-id="9a31c-290">To collect all counters for the object, specify: `.*`.</span></span> <span data-ttu-id="9a31c-291">Yalnızca takas alanı sayaçları için bellek nesnesi toplanacak belirtebilirsiniz:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="9a31c-291">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="9a31c-292">**Aralığı:**: nesnesinin sayaçları toplanır sıklığı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-292">**Interval:**: the frequency at which the object's counters are collected.</span></span>

<span data-ttu-id="9a31c-293">Performans ölçümleri için varsayılan yapılandırmayı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9a31c-293">The default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="9a31c-294">MySQL performans sayaçlarını Linux komutlarını kullanarak etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9a31c-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="9a31c-295">Omsagent paketi yüklendiğinde, MySQL Server veya MariaDB Server bilgisayarda algılanırsa, bir performans izleme sağlayıcısı MySQL sunucusu için otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-295">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="9a31c-296">Bu sağlayıcı performans istatistiklerini kullanıma sunmak için yerel MySQL/MariaDB sunucusuna bağlanır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-296">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="9a31c-297">MySQL kullanıcı kimlik bilgileri sağlayıcısı MySQL Server erişebilmesi için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-297">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span></span>

<span data-ttu-id="9a31c-298">MySQL sunucusu için varsayılan bir kullanıcı hesabı üzerinde localhost tanımlamak için aşağıdaki komut örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-298">To define a default user account for the MySQL server on localhost, use the following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="9a31c-299">Kimlik bilgileri dosyası omsagent hesap tarafından okunabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-299">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="9a31c-300">Omsgent mycimprovauth komutunun çalıştırılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-300">Running the mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="9a31c-301">Bir dosyada dosya oluşturarak gerekli MySQL kimlik alternatif olarak, belirtebilirsiniz: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span><span class="sxs-lookup"><span data-stu-id="9a31c-301">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span></span> <span data-ttu-id="9a31c-302">Mysql auth dosyası aracılığıyla izleme MySQL kimlik bilgilerini yönetme hakkında daha fazla bilgi için bkz: [kimlik bilgileri kimlik doğrulama dosyasındaki İzleme MySQL yönetmek](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="9a31c-302">For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="9a31c-303">Bkz: [veritabanı için MySQL performans sayaçları gerekli izinler](#database-permissions-required-for-mysql-performance-counters) MySQL sunucusu performans verilerini toplamak için MySQL kullanıcı tarafından gerekli nesne izinleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-303">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="9a31c-304">Linux komutlarını kullanarak Apache HTTP Server performans sayaçları sağlar</span><span class="sxs-lookup"><span data-stu-id="9a31c-304">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="9a31c-305">Apache HTTP Server omsagent paket yüklü olduğunda bilgisayarda algılanırsa, bir performans izlemesi için Apache HTTP Server sağlayıcısı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-305">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="9a31c-306">Bu sağlayıcı Apache "Apache HTTP Server performans verilerini erişmek için yüklenmesi gereken modül" kullanır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-306">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span></span>

<span data-ttu-id="9a31c-307">Modül aşağıdaki komutu kullanarak yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a31c-307">You can load the module with the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="9a31c-308">Apache izleme modülü kaldırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9a31c-308">To unload the Apache monitoring module, run the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a><span data-ttu-id="9a31c-309">Günlük analizi ile performans verilerini görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="9a31c-309">To view performance data with Log Analytics</span></span>
1. <span data-ttu-id="9a31c-310">Operations Management Suite Portalı'nda günlük arama kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-310">In the Operations Management Suite portal, click the Log Search tile.</span></span>
2. <span data-ttu-id="9a31c-311">Arama çubuğuna `* (Type=Perf)` tüm performans sayaçlarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-311">In the search bar, type `* (Type=Perf)` to view all performance counters.</span></span>

<span data-ttu-id="9a31c-312">OMS aynı zamanda Windows performans sayacı verilerini toplar olduğundan, kapsam Linux'a özgü verileri aramayı aşağı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-312">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span></span> <span data-ttu-id="9a31c-313">Bu nedenle, aşağıdaki örnek performans verileri Chorizo21 adlandırılmış bir örnek Linux sunucusuna belirli gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-313">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![arama sonuçlarında gösterilen örnekte, sunucu](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="9a31c-315">Sonuçlarda tıklayabilirsiniz **ölçümleri** veri için toplanan sayaçlarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-315">In the results, you can click **Metrics** to view the counters that data was collected for.</span></span> <span data-ttu-id="9a31c-316">Gerçek zamanlı veri grafikleri her sayacı olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-316">Real-time data is shown as graphs for each counter.</span></span>

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="9a31c-318">Syslog</span><span class="sxs-lookup"><span data-stu-id="9a31c-318">Syslog</span></span>
<span data-ttu-id="9a31c-319">Syslog protokolüdür bir olay günlüğü Windows olay günlüklerini benzer — hem OMS görüntülendiğinde benzer şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-319">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="9a31c-320">OMS içinde yeni bir Linux syslog özelliğini eklemek için</span><span class="sxs-lookup"><span data-stu-id="9a31c-320">To add a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="9a31c-321">Üzerinde **ayarları** altında sayfa **veri** , tıklatın **Syslog** ve ardından artı simgesinin solunda eklemek istediğiniz syslog özelliğini adını yazın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-321">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span></span>
    <span data-ttu-id="9a31c-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="9a31c-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="9a31c-323">Tesis tam adını bilmiyorsanız, kısmi bir ad yazarak başlatabilirsiniz ve kullanılabilir syslog tesis listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-323">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="9a31c-324">Eklemek istediğiniz syslog özelliğini bulduğunuzda, listedeki adına tıklayın ve ardından syslog özelliğini eklemek için artı simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-324">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span></span>
3. <span data-ttu-id="9a31c-325">Listesinde görünür tesis ekledikten sonra renkli çubuk ile vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-325">After you add the facility, it appears in the list of highlighted with a colored bar.</span></span> <span data-ttu-id="9a31c-326">Ardından, toplamak istediğiniz önem derecelerinin (syslog tesis bilgi kategorilerde) seçin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-326">Next, choose the severities (categories of syslog facility information) that you want to collect.</span></span>
4. <span data-ttu-id="9a31c-327">Sayfanın alt kısmında tıklatın **kaydetmek** değişikliklerinizi sona erdirmek için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-327">At the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="9a31c-328">Yaptığınız yapılandırma değişikliklerini OMS ile genellikle 5 dakika içinde kayıtlı Linux için OMS aracılara tüm sonra gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-328">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="9a31c-329">Linux syslog Linux tesislerde yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9a31c-329">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="9a31c-330">Syslog olayları syslog arka plan programından, örneğin rsyslog veya syslog-ng, aracının dinlediği yerel bir bağlantı noktasına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-330">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span></span> <span data-ttu-id="9a31c-331">Varsayılan olarak, bağlantı noktası 25224.</span><span class="sxs-lookup"><span data-stu-id="9a31c-331">By default, port 25224.</span></span> <span data-ttu-id="9a31c-332">Aracıyı yüklediğinizde, varsayılan bir syslog yapılandırma uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-332">When the agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="9a31c-333">Bu da bulunur:</span><span class="sxs-lookup"><span data-stu-id="9a31c-333">This is found at:</span></span>

<span data-ttu-id="9a31c-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="9a31c-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="9a31c-335">Syslog ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="9a31c-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="9a31c-336">Varsayılan OMS Aracısı syslog yapılandırması tüm uyarı veya daha büyük bir önem derecesi araçlarıyla syslog olayları yükler.</span><span class="sxs-lookup"><span data-stu-id="9a31c-336">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="9a31c-337">Syslog yapılandırma düzenlerseniz, syslog arka plan programı değişikliklerin etkili olması yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-337">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

<span data-ttu-id="9a31c-338">Syslog için varsayılan yapılandırmayı OMS aracısı için Linux için OMS şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9a31c-338">The default syslog configuration for the OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="9a31c-339">rsyslog</span><span class="sxs-lookup"><span data-stu-id="9a31c-339">Rsyslog</span></span>
```
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
```

#### <a name="syslog-ng"></a><span data-ttu-id="9a31c-340">Syslog ng</span><span class="sxs-lookup"><span data-stu-id="9a31c-340">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a><span data-ttu-id="9a31c-341">Günlük analizi ile tüm Syslog olayları görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="9a31c-341">To view all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="9a31c-342">Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.</span><span class="sxs-lookup"><span data-stu-id="9a31c-342">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="9a31c-343">İçinde **Günlüğü Yönetimi** gruplandırma, önceden tanımlanmış syslog arama seçin ve sonra bir çalıştırmak için seçin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-343">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span></span>

<span data-ttu-id="9a31c-344">Bu örnekte tüm Syslog olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-344">This example shows all Syslog events.</span></span>

![Günlük aramada gösterilen Syslog olayları](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="9a31c-346">Şimdi arama sonuçlarında detaya inebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-346">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="9a31c-347">Linux uyarıları</span><span class="sxs-lookup"><span data-stu-id="9a31c-347">Linux alerts</span></span>
<span data-ttu-id="9a31c-348">Linux makineler yönetmek için Nagios veya Zabbix kullanırsanız, OMS bu Araçları'ndan oluşturulan uyarıların alabilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-348">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span></span> <span data-ttu-id="9a31c-349">Ancak, şu anda OMS Portalı'nı kullanarak gelen uyarı verileri yapılandırmak için yöntemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-349">However, there is currently no method to configure incoming alert data using the OMS portal.</span></span> <span data-ttu-id="9a31c-350">Bunun yerine, uyarılar için OMS gönderme başlamak için bir yapılandırma dosyasını düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-350">Instead, you will need to edit a config file to start sending alerts to OMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="9a31c-351">Nagios toplama uyarıları</span><span class="sxs-lookup"><span data-stu-id="9a31c-351">Collect alerts from Nagios</span></span>
<span data-ttu-id="9a31c-352">Nagios sunucudan uyarılarını toplamak için aşağıdaki yapılandırma değişiklikleri yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-352">To collect alerts from a Nagios server, you need to make the following configuration changes.</span></span>

1. <span data-ttu-id="9a31c-353">Kullanıcının izni **omsagent** Nagios günlük dosyasına (yani /var/log/nagios/nagios.log) okuma erişimi.</span><span class="sxs-lookup"><span data-stu-id="9a31c-353">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="9a31c-354">Nagios.log dosya varsayılarak grupla sahibi **nagios** , kullanıcı ekleyebilir **omsagent** için **nagios** grubu.</span><span class="sxs-lookup"><span data-stu-id="9a31c-354">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="9a31c-355">Omsagent.confconfiguration dosyasını değiştirme (/ etc/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="9a31c-355">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="9a31c-356">Mevcut ve kullanıma açıklamalı aşağıdaki girdileri çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="9a31c-356">Ensure the following entries are present and not commented out:</span></span>

    ```
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
    ```
3. <span data-ttu-id="9a31c-357">Omsagent arka plan programı yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="9a31c-357">Restart the omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="9a31c-358">Zabbix toplama uyarıları</span><span class="sxs-lookup"><span data-stu-id="9a31c-358">Collect alerts from Zabbix</span></span>
<span data-ttu-id="9a31c-359">Bir kullanıcı ve parola belirtmeniz gerekir dışında Zabbix sunucudan uyarılarını toplamak için yukarıdaki Nagios için olanlar için benzer adımları gerçekleştirirsiniz *açık metin*.</span><span class="sxs-lookup"><span data-stu-id="9a31c-359">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="9a31c-360">Bu ideal olmayan, ancak büyük olasılıkla yakında değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-360">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="9a31c-361">Bu sorunu gidermek için kullanıcı oluşturun ve onu yalnızca izlemek için izni öneririz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-361">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span></span>

<span data-ttu-id="9a31c-362">Bir örnek bölüm omsagent.conf yapılandırma dosyasının (/ etc/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf) Zabbix aşağıdaki benzemelidir için:</span><span class="sxs-lookup"><span data-stu-id="9a31c-362">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="9a31c-363">Günlük analizi arama uyarıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="9a31c-363">View alerts in Log Analytics search</span></span>
<span data-ttu-id="9a31c-364">OMS için uyarıları göndermek üzere, Linux Bilgisayarları yapılandırdıktan sonra birkaç basit günlük arama sorguları uyarıları görüntülemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-364">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span></span> <span data-ttu-id="9a31c-365">Aşağıdaki arama sorgusu örneğinde oluşturulan tüm kayıtlı uyarıların döndürür.</span><span class="sxs-lookup"><span data-stu-id="9a31c-365">The following search query example returns all the recorded alerts that were generated.</span></span> <span data-ttu-id="9a31c-366">BT altyapınızın sorun çeşit meydana gelirse, örneğin, ardından aşağıdaki örnek sorgu sonuçlarını sorunun nerede kaynaklanan gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-366">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span></span> <span data-ttu-id="9a31c-367">Ve, kolayca uyarılara daraltmaya yardımcı olmak için kaynak sistem tarafından araştırmanızı inebilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-367">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span></span> <span data-ttu-id="9a31c-368">Avantajı, mutlaka başından çeşitli yönetim sistemleri için Git gerekmemesidir — uyarılarınızı için OMS gönderilen koşuluyla var. başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-368">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="9a31c-369">Günlük analizi ile tüm Nagios uyarıları görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="9a31c-369">To view all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="9a31c-370">Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.</span><span class="sxs-lookup"><span data-stu-id="9a31c-370">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="9a31c-371">Sorgu çubuğuna aşağıdaki arama sorgusu yazın</span><span class="sxs-lookup"><span data-stu-id="9a31c-371">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Günlük aramada gösterilen Nagios uyarıları](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="9a31c-373">Arama sonuçlarını gördükten sonra ek ayrıntılar gibi inebilir *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="9a31c-373">After you see the search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="9a31c-374">Günlük analizi ile tüm Zabbix uyarıları görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="9a31c-374">To view all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="9a31c-375">Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.</span><span class="sxs-lookup"><span data-stu-id="9a31c-375">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="9a31c-376">Sorgu çubuğuna aşağıdaki arama sorgusu yazın</span><span class="sxs-lookup"><span data-stu-id="9a31c-376">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Günlük aramada gösterilen Zabbix uyarıları](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="9a31c-378">Arama sonuçlarını gördükten sonra ek ayrıntılar gibi inebilir *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="9a31c-378">After you see the search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="9a31c-379">System Center Operations Manager ile uyumluluk</span><span class="sxs-lookup"><span data-stu-id="9a31c-379">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="9a31c-380">Linux için OMS aracısının Aracısı ikili dosyaları System Center Operations Manager Aracısı ile paylaşır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-380">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="9a31c-381">Şu anda Operations Manager tarafından yönetilen bir sistemde Linux için OMS Aracısı'nı yükleme bilgisayardaki OMI ve SCX paketleri daha yeni bir sürüme yükseltir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-381">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="9a31c-382">Linux ve System Center 2012 R2 için OMS aracısının uyumlu olur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-382">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="9a31c-383">Ancak, **System Center 2012 SP1 ve önceki sürümleri olmayan şu anda uyumlu ya da desteklenen Linux için OMS Aracısı ile.**</span><span class="sxs-lookup"><span data-stu-id="9a31c-383">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="9a31c-384">Bilgisayar Bul önce Linux için OMS aracısının şu anda Operations Manager tarafından yönetilmeyen bir bilgisayara yüklü olduğundan ve daha sonra bilgisayar Operations Manager ile yönetmek istediğiniz, OMI yapılandırma değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-384">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span></span> <span data-ttu-id="9a31c-385">**Linux için Operations Manager Aracısı önce OMS Aracısı yüklüyse, bu adım gerekli değildir.**</span><span class="sxs-lookup"><span data-stu-id="9a31c-385">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a><span data-ttu-id="9a31c-386">Operations Manager ile iletişim kurmak Linux için OMS Aracısı etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="9a31c-386">To enable the OMS Agent for Linux to communicate with Operations Manager</span></span>
1. <span data-ttu-id="9a31c-387">Dosya /etc/opt/omi/conf/omiserver.conf Düzenle</span><span class="sxs-lookup"><span data-stu-id="9a31c-387">Edit the file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="9a31c-388">Satır başlayarak emin **httpsport =** bağlantı noktası 1270 tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9a31c-388">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="9a31c-389">Gibi`httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="9a31c-389">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="9a31c-390">OMI sunucuyu yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="9a31c-390">Restart the OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="9a31c-391">MySQL performans sayaçları için gereken veritabanı izinleri</span><span class="sxs-lookup"><span data-stu-id="9a31c-391">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="9a31c-392">Bir MySQL izleme kullanıcı izinlerini vermek için izni veriliyor kullanıcının verilmeden ayrıcalık yanı sıra, 'GRANT option' ayrıcalığı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-392">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span></span>

<span data-ttu-id="9a31c-393">MySQL kullanıcının kullanıcı performans verileri döndürmek sırayla aşağıdaki sorguları erişimi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9a31c-393">In order for the MySQL User to return performance data the user will need access to the following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="9a31c-394">Bu sorguları MySQL yanı sıra kullanıcı aşağıdaki varsayılan tabloları seçme erişimi gerektirir:</span><span class="sxs-lookup"><span data-stu-id="9a31c-394">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span></span>

* <span data-ttu-id="9a31c-395">INFORMATION_SCHEMA</span><span class="sxs-lookup"><span data-stu-id="9a31c-395">information_schema</span></span>
* <span data-ttu-id="9a31c-396">MySQL</span><span class="sxs-lookup"><span data-stu-id="9a31c-396">mysql</span></span>

<span data-ttu-id="9a31c-397">Bu ayrıcalıklar aşağıdaki grant komutlarını çalıştırarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-397">These privileges can be granted by running the following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a><span data-ttu-id="9a31c-398">Kimlik doğrulama dosyasını kimlik bilgilerini izleme MySQL yönetme</span><span class="sxs-lookup"><span data-stu-id="9a31c-398">Manage MySQL monitoring credentials in the authentication file</span></span>
<span data-ttu-id="9a31c-399">Aşağıdaki bölümlerde MySQL kimlik bilgilerini yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-399">The following sections help you manage MySQL credentials.</span></span>

### <a name="configure-the-mysql-omi-provider"></a><span data-ttu-id="9a31c-400">MySQL OMI sağlayıcı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9a31c-400">Configure the MySQL OMI provider</span></span>
<span data-ttu-id="9a31c-401">MySQL OMI sağlayıcı önceden yapılandırılmış bir MySQL kullanıcının gerektiren ve MySQL örneğine performans/sistem durumu bilgileri sorgulamak için MySQL istemci kitaplıkları yüklü.</span><span class="sxs-lookup"><span data-stu-id="9a31c-401">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="9a31c-402">MySQL OMI kimlik doğrulaması dosyası</span><span class="sxs-lookup"><span data-stu-id="9a31c-402">MySQL OMI authentication file</span></span>
<span data-ttu-id="9a31c-403">Hangi bağlama adresini belirlemek ve örnek dinlediği MySQL ve ne ölçümleri toplamak için kullanılacak kimlik bilgileri bağlantı noktası için bir kimlik doğrulama dosyasını MySQL OMI sağlayıcısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-403">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span> <span data-ttu-id="9a31c-404">MySQL OMI yükleme sırasında sağlayıcısı bağ adresi ve bağlantı noktası için MySQL my.cnf yapılandırma dosyalarını (varsayılan konumları) tarama ve kısmen MySQL OMI kimlik doğrulama dosyasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-404">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="9a31c-405">MySQL sunucusu örneğini izleme tamamlamak için önceden oluşturulmuş bir MySQL OMI kimlik doğrulaması dosya doğru dizine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-405">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="9a31c-406">Kimlik doğrulama dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="9a31c-406">Authentication file format</span></span>
<span data-ttu-id="9a31c-407">MySQL OMI kimlik doğrulama dosyasını hakkında bilgi içeren bir metin dosyasıdır:</span><span class="sxs-lookup"><span data-stu-id="9a31c-407">The MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="9a31c-408">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="9a31c-408">Port</span></span>
* <span data-ttu-id="9a31c-409">Bağ adresi</span><span class="sxs-lookup"><span data-stu-id="9a31c-409">Bind-Address</span></span>
* <span data-ttu-id="9a31c-410">MySQL kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="9a31c-410">MySQL username</span></span>
* <span data-ttu-id="9a31c-411">Base64 ile kodlanmış parola</span><span class="sxs-lookup"><span data-stu-id="9a31c-411">Base64 encoded password</span></span>

<span data-ttu-id="9a31c-412">MySQL OMI kimlik doğrulama dosyasını okuma/yazma için ayrıcalıkları oluşturan Linux kullanıcı yalnızca verir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-412">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="9a31c-413">Varsayılan MySQL OMI kimlik doğrulama dosyasını varsayılan bir örnek ve bağlı olarak hangi bilgilerin bulunan MySQL yapılandırma dosyasından ayrıştırılmış ve kullanılabilir bir bağlantı noktası numarası içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9a31c-413">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span></span>

<span data-ttu-id="9a31c-414">Varsayılan örneği daha kolay bir Linux ana bilgisayarda birden çok MySQL örneklerini yönetme yapmak için bir araçtır ve bağlantı noktası 0 ile örneği tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-414">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span></span> <span data-ttu-id="9a31c-415">Tüm ek örneklerini varsayılan örneğinden ayarlanan özellikleri devralır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-415">All added instances will inherit properties set from the default instance.</span></span> <span data-ttu-id="9a31c-416">MySQL örneği '3308' numaralı bağlantı noktasını dinlemeye eklediyseniz, örneğin, varsayılan örneğinin bağ adresi, kullanıcı adı ve Base64 ile kodlanmış parola deneyin ve 3308 üzerinde dinleme örneği izlemek için kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="9a31c-416">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="9a31c-417">3308 örneğinde başka bir adres bağlanıp ve aynı MySQL kullanıcı adı ve parola çifti kullanıyorsa yalnızca bağlama adresinin respecification gereklidir ve diğer özellikleri devralınır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-417">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span></span>

<span data-ttu-id="9a31c-418">Kimlik doğrulama dosyasını örnekleri aşağıdakine benzer.</span><span class="sxs-lookup"><span data-stu-id="9a31c-418">Examples of the authentication file resemble the following.</span></span>

<span data-ttu-id="9a31c-419">Varsayılan örneği ve bağlantı noktası 3308 ile örneği:</span><span class="sxs-lookup"><span data-stu-id="9a31c-419">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="9a31c-420">Varsayılan örneği ve bağlantı noktası 3308 + farklı Base 64 örneğiyle parola kodlanmış:</span><span class="sxs-lookup"><span data-stu-id="9a31c-420">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="9a31c-421">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="9a31c-421">**Property**</span></span> | <span data-ttu-id="9a31c-422">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="9a31c-422">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="9a31c-423">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="9a31c-423">Port</span></span> |<span data-ttu-id="9a31c-424">Bağlantı noktası MySQL örneği üzerinde dinleme geçerli bağlantı noktası temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9a31c-424">Port represents the current port the MySQL instance is listening on.</span></span>  <span data-ttu-id="9a31c-425">0 bağlantı noktası, aşağıdaki özellikler varsayılan örnek için kullanıldığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-425">The port 0 implies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="9a31c-426">Bağ adresi</span><span class="sxs-lookup"><span data-stu-id="9a31c-426">Bind-Address</span></span> |<span data-ttu-id="9a31c-427">Geçerli MySQL bağ adresi bağlamak adresidir</span><span class="sxs-lookup"><span data-stu-id="9a31c-427">the Bind Address is the current MySQL bind-address</span></span> |
| <span data-ttu-id="9a31c-428">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="9a31c-428">username</span></span> |<span data-ttu-id="9a31c-429">Bu MySQL server örneği izlemek için kullanmak istediğiniz MySQL kullanıcının kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-429">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="9a31c-430">Parola Base64 ile kodlanmış</span><span class="sxs-lookup"><span data-stu-id="9a31c-430">Base64 encoded Password</span></span> |<span data-ttu-id="9a31c-431">Base64 ile kodlanmış MySQL izleme kullanıcının parolası budur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-431">This is the password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="9a31c-432">Otomatik güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9a31c-432">AutoUpdate</span></span> |<span data-ttu-id="9a31c-433">MySQL OMI sağlayıcı yükseltildiğinde sağlayıcı my.cnf dosyasındaki değişiklikleri için yeniden tarayın ve MySQL OMI kimlik doğrulaması bu dosyanın üzerine.</span><span class="sxs-lookup"><span data-stu-id="9a31c-433">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span></span> <span data-ttu-id="9a31c-434">Bu bayrak true veya false MySQL OMI kimlik doğrulama dosyasını gerekli güncelleştirmeler bağlı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-434">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="9a31c-435">Kimlik doğrulama dosya konumu</span><span class="sxs-lookup"><span data-stu-id="9a31c-435">Authentication file location</span></span>
<span data-ttu-id="9a31c-436">MySQL OMI kimlik doğrulaması dosyası şu konumda bulunan ve "auth mysql" adlı:</span><span class="sxs-lookup"><span data-stu-id="9a31c-436">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span></span>

<span data-ttu-id="9a31c-437">/var/OPT/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth</span><span class="sxs-lookup"><span data-stu-id="9a31c-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="9a31c-438">Dosya (ve kimlik doğrulama/omsagent dizin) omsagent kullanıcıya ait.</span><span class="sxs-lookup"><span data-stu-id="9a31c-438">The file (and auth/omsagent directory) should be owned by the omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="9a31c-439">Aracı günlükleri</span><span class="sxs-lookup"><span data-stu-id="9a31c-439">Agent logs</span></span>
<span data-ttu-id="9a31c-440">Linux için OMS aracısı için günlükleri olduğuna:</span><span class="sxs-lookup"><span data-stu-id="9a31c-440">The logs for the OMS Agent for Linux is at:</span></span>

<span data-ttu-id="9a31c-441">/ var/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="9a31c-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="9a31c-442">Linux için OMS aracısının günlükleri omsconfig (Aracısı yapılandırması) programı için aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9a31c-442">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="9a31c-443">/ var/opt/microsoft/omsconfig/log /</span><span class="sxs-lookup"><span data-stu-id="9a31c-443">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="9a31c-444">Günlükleri (performans ölçüm verilerini sağlayan) OMI ve scx farklı bileşenlerin olduğuna:</span><span class="sxs-lookup"><span data-stu-id="9a31c-444">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="9a31c-445">/ var/opt/OMI/log/ve /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="9a31c-445">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-the-oms-agent-for-linux"></a><span data-ttu-id="9a31c-446">Linux için OMS Aracısı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9a31c-446">Troubleshooting the OMS Agent for Linux</span></span>
<span data-ttu-id="9a31c-447">Tanılamak ve sık karşılaşılan sorunları gidermek için aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-447">Use the following information to diagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="9a31c-448">Bu bölümdeki sorun giderme bilgileri hiçbiri yardımcı olur, sorunu gidermek için aşağıdaki kaynaklara da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-448">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span></span>

* <span data-ttu-id="9a31c-449">Müşteriler ile Premier Destek aracılığıyla bir destek talebi oturum açabilir [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="9a31c-449">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="9a31c-450">Azure destek anlaşmaları sahip müşteriler oturum destek olaylarının [Azure portalı](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="9a31c-450">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="9a31c-451">Dosya bir [GitHub sorunu](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="9a31c-451">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="9a31c-452">Geri bildirim Forumunda fikirleri ve bir hata raporu oluşturmak için [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="9a31c-452">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="9a31c-453">Önemli günlük konumları</span><span class="sxs-lookup"><span data-stu-id="9a31c-453">Important log locations</span></span>
| <span data-ttu-id="9a31c-454">Dosya</span><span class="sxs-lookup"><span data-stu-id="9a31c-454">File</span></span> | <span data-ttu-id="9a31c-455">Yol</span><span class="sxs-lookup"><span data-stu-id="9a31c-455">Path</span></span> |
| --- | --- |
| <span data-ttu-id="9a31c-456">Linux günlük dosyası için OMS Aracısı</span><span class="sxs-lookup"><span data-stu-id="9a31c-456">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="9a31c-457">OMS Aracısı Yapılandırma günlük dosyasını</span><span class="sxs-lookup"><span data-stu-id="9a31c-457">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="9a31c-458">Önemli yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="9a31c-458">Important configuration files</span></span>
| <span data-ttu-id="9a31c-459">Catergory</span><span class="sxs-lookup"><span data-stu-id="9a31c-459">Catergory</span></span> | <span data-ttu-id="9a31c-460">Dosya konumu</span><span class="sxs-lookup"><span data-stu-id="9a31c-460">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="9a31c-461">Syslog</span><span class="sxs-lookup"><span data-stu-id="9a31c-461">Syslog</span></span> |<span data-ttu-id="9a31c-462">`/etc/syslog-ng/syslog-ng.conf`veya `/etc/rsyslog.conf` veya`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="9a31c-462">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="9a31c-463">Performans, Nagios, Zabbix, OMS çıkış ve genel Aracısı</span><span class="sxs-lookup"><span data-stu-id="9a31c-463">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="9a31c-464">Ek yapılandırmalar</span><span class="sxs-lookup"><span data-stu-id="9a31c-464">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="9a31c-465">OMS portalı yapılandırması etkinse, performans sayaçları ve syslog için düzenleme yapılandırma dosyalarının üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-465">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="9a31c-466">Yapılandırma portalında OMS (tüm düğümler) devre dışı bırakabilir veya aşağıdaki çalıştırarak tek düğümler için:</span><span class="sxs-lookup"><span data-stu-id="9a31c-466">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="9a31c-467">Hata ayıklama günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="9a31c-467">Enable debug logging</span></span>
<span data-ttu-id="9a31c-468">Hata ayıklama günlüğünü etkinleştirmek için OMS çıkış eklentisi ve ayrıntılı çıktı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a31c-468">To enable debug logging, you can use the OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="9a31c-469">OMS çıkış eklentisi</span><span class="sxs-lookup"><span data-stu-id="9a31c-469">OMS output plugin</span></span>
<span data-ttu-id="9a31c-470">FluentD girişleri ve çıkışları için farklı günlük düzeyleri için günlüğe kaydetme düzeyini belirtmek eklenti sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a31c-470">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="9a31c-471">OMS çıktı için farklı günlük düzeyini belirtmek için genel Aracısı yapılandırmasında Düzenle `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="9a31c-471">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="9a31c-472">Yapılandırma dosyası altına değiştirme `log_level` özelliğinden `info` için `debug`.</span><span class="sxs-lookup"><span data-stu-id="9a31c-472">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="9a31c-473">Hata ayıklama günlüğünü sayısı veri öğeleri ve göndermek için harcanan süre türü tarafından ayrılmış OMS hizmetine toplu yüklemeleri görmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a31c-473">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span></span>

<span data-ttu-id="9a31c-474">*Örnek etkin hata ayıklama günlüğü:*</span><span class="sxs-lookup"><span data-stu-id="9a31c-474">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="9a31c-475">Ayrıntılı çıktı</span><span class="sxs-lookup"><span data-stu-id="9a31c-475">Verbose output</span></span>
<span data-ttu-id="9a31c-476">OMS çıkış eklentisini kullanmak yerine, ayrıca veri öğeleri doğrudan çıkarabilirsiniz `stdout`, Linux günlük dosyası için OMS aracısının görünür olduğu.</span><span class="sxs-lookup"><span data-stu-id="9a31c-476">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span></span>

<span data-ttu-id="9a31c-477">OMS genel Aracısı Yapılandırma dosyasında `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, yorum kullanıma OMS çıktı eklentisi ekleyerek bir `#` her satırın önünde.</span><span class="sxs-lookup"><span data-stu-id="9a31c-477">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="9a31c-478">Çıktı eklentisi yorum aşağıdaki bölümde kaldırmak `#` her satırın başındaki simgesi.</span><span class="sxs-lookup"><span data-stu-id="9a31c-478">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a><span data-ttu-id="9a31c-479">İletilen Syslog iletilerini günlüğe görünmez</span><span class="sxs-lookup"><span data-stu-id="9a31c-479">Forwarded Syslog messages do not appear in the log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9a31c-480">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="9a31c-480">Probable causes</span></span>
* <span data-ttu-id="9a31c-481">Linux sunucuya uygulanan yapılandırma gönderilen tesis ve/veya günlük düzeyleri koleksiyonunu izin verme</span><span class="sxs-lookup"><span data-stu-id="9a31c-481">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span></span>
* <span data-ttu-id="9a31c-482">Syslog doğru Linux sunucusuna İletiliyor değil</span><span class="sxs-lookup"><span data-stu-id="9a31c-482">Syslog is not being forwarded correctly to the Linux server</span></span>
* <span data-ttu-id="9a31c-483">Saniye başına iletilen iletilerin sayısını işlemek Linux için OMS aracısının temel yapılandırması için çok büyük</span><span class="sxs-lookup"><span data-stu-id="9a31c-483">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9a31c-484">Çözümler</span><span class="sxs-lookup"><span data-stu-id="9a31c-484">Resolutions</span></span>
* <span data-ttu-id="9a31c-485">Syslog OMS portalında yapılandırması tüm özellikleri ve doğru günlük düzeyleri sahip olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="9a31c-485">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span></span>
  * <span data-ttu-id="9a31c-486">**OMS portalı > ayarları > veri > Syslog**</span><span class="sxs-lookup"><span data-stu-id="9a31c-486">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="9a31c-487">Bu yerel syslog arka plan programları Mesajlaşma doğrulayın (`rsyslog`, `syslog-ng`) yönlendirilmiş iletiler alabilir</span><span class="sxs-lookup"><span data-stu-id="9a31c-487">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span></span>
* <span data-ttu-id="9a31c-488">İletileri engellenmediğinden emin olmak için Syslog sunucusunda güvenlik duvarı ayarlarını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="9a31c-488">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span></span>
* <span data-ttu-id="9a31c-489">OMS kullanarak bir Syslog iletisi benzetimini `logger` command - örneğin:</span><span class="sxs-lookup"><span data-stu-id="9a31c-489">Simulate a Syslog message to OMS using the `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a><span data-ttu-id="9a31c-490">Bir proxy kullanılırken için OMS bağlantısı sorunları</span><span class="sxs-lookup"><span data-stu-id="9a31c-490">Problems connecting to OMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9a31c-491">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="9a31c-491">Probable causes</span></span>
* <span data-ttu-id="9a31c-492">Proxy aracısı yükleme ve yapılandırma yanlış olduğunda belirtilen</span><span class="sxs-lookup"><span data-stu-id="9a31c-492">The proxy specified when installing and configuring the agent is incorrect</span></span>
* <span data-ttu-id="9a31c-493">OMS hizmet uç noktaları, veri merkezinizdeki whitelistested değildir</span><span class="sxs-lookup"><span data-stu-id="9a31c-493">The OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9a31c-494">Çözümler</span><span class="sxs-lookup"><span data-stu-id="9a31c-494">Resolutions</span></span>
* <span data-ttu-id="9a31c-495">Seçeneğiyle aşağıdaki komutu kullanarak Linux için OMS Aracısı'nı yeniden `-v` etkin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-495">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="9a31c-496">Bu OMS hizmetine proxy üzerinden bağlanma Aracısı'nın ayrıntılı çıktı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a31c-496">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="9a31c-497">OMS proxy belgelerini gözden [aracı kullanmak için bir HTTP proxy sunucusu yapılandırma](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="9a31c-497">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="9a31c-498">Aşağıdaki OMS hizmet uç noktalarına Güvenilenler listesine olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="9a31c-498">Verify that the following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="9a31c-499">Aracı Kaynağı</span><span class="sxs-lookup"><span data-stu-id="9a31c-499">Agent Resource</span></span> | <span data-ttu-id="9a31c-500">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="9a31c-500">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="9a31c-501">&#42;. ods.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="9a31c-501">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="9a31c-502">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="9a31c-502">Port 443</span></span> |
| <span data-ttu-id="9a31c-503">&#42;. OMS.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="9a31c-503">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="9a31c-504">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="9a31c-504">Port 443</span></span> |
| <span data-ttu-id="9a31c-505">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="9a31c-505">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="9a31c-506">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="9a31c-506">Port 443</span></span> |
| <span data-ttu-id="9a31c-507">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="9a31c-507">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="9a31c-508">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="9a31c-508">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="9a31c-509">Bir 403 hatası görüntülenir, ekleme</span><span class="sxs-lookup"><span data-stu-id="9a31c-509">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9a31c-510">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="9a31c-510">Probable causes</span></span>
* <span data-ttu-id="9a31c-511">Tarih ve saat Linux sunucusu üzerinde yanlış</span><span class="sxs-lookup"><span data-stu-id="9a31c-511">The date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="9a31c-512">Kullanılan çalışma alanı kimliği ve çalışma alanı anahtarı yanlış</span><span class="sxs-lookup"><span data-stu-id="9a31c-512">The Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="9a31c-513">Çözüm</span><span class="sxs-lookup"><span data-stu-id="9a31c-513">Resolution</span></span>
* <span data-ttu-id="9a31c-514">Linux sunucunuzla zamanında doğrulayın `date` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a31c-514">Verify the time on your Linux server with the `date` command.</span></span> <span data-ttu-id="9a31c-515">Veri değerinden büyük veya geçerli saatten az 15 dakika sonra ekleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-515">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span></span> <span data-ttu-id="9a31c-516">Bu sorunu gidermek için tarih ve/veya saat dilimi Linux sunucunuzun güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-516">To correct this, update the date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="9a31c-517">Bir zaman farkı ekleme hatasına neden oluyorsa Linux için OMS aracısının en son sürümünü sizi bilgilendirir</span><span class="sxs-lookup"><span data-stu-id="9a31c-517">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="9a31c-518">RE-doğru çalışma alanı kimliği ve çalışma alanı anahtarı kullanarak yerleşik.</span><span class="sxs-lookup"><span data-stu-id="9a31c-518">Re-onboard using the correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="9a31c-519">Bkz: [komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-519">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a><span data-ttu-id="9a31c-520">500 hata veya 404 hatası günlük dosyasında ekleme sonra görünür.</span><span class="sxs-lookup"><span data-stu-id="9a31c-520">A 500 error or 404 error appears in the log file after onboarding</span></span>
<span data-ttu-id="9a31c-521">Bu OMS çalışma alanına Linux verilerin ilk yükleme sırasında oluşan bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-521">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="9a31c-522">Bu, gönderilen veriler ya da diğer sorunlar etkilemez.</span><span class="sxs-lookup"><span data-stu-id="9a31c-522">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="9a31c-523">İlk defa hataları yoksayabilirsiniz ekleme.</span><span class="sxs-lookup"><span data-stu-id="9a31c-523">You can ignore the errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="9a31c-524">Nagios veriler OMS Portalı'nda görünmüyor</span><span class="sxs-lookup"><span data-stu-id="9a31c-524">Nagios data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9a31c-525">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="9a31c-525">Probable causes</span></span>
* <span data-ttu-id="9a31c-526">Omsagent kullanıcının Nagios günlük dosyasından okuma izni yok</span><span class="sxs-lookup"><span data-stu-id="9a31c-526">The omsagent user does not have permissions to read from the Nagios log file</span></span>
* <span data-ttu-id="9a31c-527">Nagios kaynak ve filtre bölümleri hala omsagent.conf dosyasında bırakılır</span><span class="sxs-lookup"><span data-stu-id="9a31c-527">The Nagios source and filter sections are still commented in the omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9a31c-528">Çözümler</span><span class="sxs-lookup"><span data-stu-id="9a31c-528">Resolutions</span></span>
* <span data-ttu-id="9a31c-529">Nagios dosyadan okunan için omsagent kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-529">Add the omsagent user in order to read from the Nagios file.</span></span> <span data-ttu-id="9a31c-530">Bkz: [Nagios uyarıları](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-530">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="9a31c-531">Linux genel yapılandırma dosyasını OMS Aracısı içinde `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, emin olun **her ikisi de** açıklamaları kaldırılan, aşağıdaki örneğe benzer şekilde Nagios kaynak ve filtre bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-531">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a><span data-ttu-id="9a31c-532">Linux veri OMS Portalı'nda görünmüyor</span><span class="sxs-lookup"><span data-stu-id="9a31c-532">Linux data doesn't appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9a31c-533">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="9a31c-533">Probable causes</span></span>
* <span data-ttu-id="9a31c-534">OMS hizmetine ekleme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="9a31c-534">Onboarding to the OMS Service failed</span></span>
* <span data-ttu-id="9a31c-535">OMS hizmetine bağlantı engellendi</span><span class="sxs-lookup"><span data-stu-id="9a31c-535">Connection to the OMS Service is blocked</span></span>
* <span data-ttu-id="9a31c-536">Yedeklenen Linux veriler için OMS Aracısı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-536">The OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9a31c-537">Çözümler</span><span class="sxs-lookup"><span data-stu-id="9a31c-537">Resolutions</span></span>
* <span data-ttu-id="9a31c-538">Doğrulayın, ekleme OMS hizmetine başarılı olduğunu doğrulayarak `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-538">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="9a31c-539">RE-omsadmin.sh komut satırını kullanarak yerleşik.</span><span class="sxs-lookup"><span data-stu-id="9a31c-539">Re-onboard using the omsadmin.sh command line.</span></span> <span data-ttu-id="9a31c-540">Bkz: [komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-540">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="9a31c-541">Bir proxy sunucu kullanıyorsanız, yukarıdaki adımları sorun giderme proxy kullanın</span><span class="sxs-lookup"><span data-stu-id="9a31c-541">If using a proxy, use the proxy troubleshooting steps above</span></span>
* <span data-ttu-id="9a31c-542">Bazı durumlarda, Linux için OMS aracısının OMS hizmetiyle iletişim kuramadığında aracı veri 50 MB tam arabellek boyutunu yedeklenmiş.</span><span class="sxs-lookup"><span data-stu-id="9a31c-542">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span></span> <span data-ttu-id="9a31c-543">OMS Aracısı'nı çalıştırarak Linux için yeniden `/opt/microsoft/omsagent/bin/service_control restart` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a31c-543">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="9a31c-544">Aracı sürümü 1.1.0-28 ve daha sonra bu sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-544">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a><span data-ttu-id="9a31c-545">Syslog Linux performans sayacı yapılandırması OMS portalında uygulanmaz</span><span class="sxs-lookup"><span data-stu-id="9a31c-545">Syslog Linux performance counter configuration is not applied in the OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9a31c-546">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="9a31c-546">Probable causes</span></span>
* <span data-ttu-id="9a31c-547">Linux için OMS aracısının yapılandırma aracısı en son yapılandırma OMS Portalı'ndan alınmamış.</span><span class="sxs-lookup"><span data-stu-id="9a31c-547">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span></span>
* <span data-ttu-id="9a31c-548">Değiştirilen ayarlar portalında uygulanmadı</span><span class="sxs-lookup"><span data-stu-id="9a31c-548">The revised settings in the portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9a31c-549">Çözümler</span><span class="sxs-lookup"><span data-stu-id="9a31c-549">Resolutions</span></span>
<span data-ttu-id="9a31c-550">`omsconfig`5 dakikada bir OMS portalı yapılandırma değişiklikleri alır Linux için OMS aracısının içinde yapılandırma aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-550">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="9a31c-551">Linux yapılandırma dosyalarını konumunda bulunan için bu yapılandırma için OMS aracısının sonra uygulanır `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="9a31c-551">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="9a31c-552">Bazı durumlarda, Linux yapılandırma aracı için OMS Aracısı uygulanmıyor son yapılandırmasında kaynaklanan portal yapılandırma hizmetiyle iletişim mümkün olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-552">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="9a31c-553">Doğrulayın `omsconfig` Aracısı, aşağıdakilerle yüklenir:</span><span class="sxs-lookup"><span data-stu-id="9a31c-553">Verify that the `omsconfig` agent is installed with the following:</span></span>

  * <span data-ttu-id="9a31c-554">`dpkg --list omsconfig` veya `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="9a31c-554">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="9a31c-555">Yüklü değilse, Linux için OMS aracısının en son sürümünü yeniden yükleyin</span><span class="sxs-lookup"><span data-stu-id="9a31c-555">If not installed, reinstall the latest version of the OMS Agent for Linux</span></span>
* <span data-ttu-id="9a31c-556">Doğrulayın `omsconfig` agent OMS hizmetiyle iletişim</span><span class="sxs-lookup"><span data-stu-id="9a31c-556">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="9a31c-557">Çalıştırma `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` komutu</span><span class="sxs-lookup"><span data-stu-id="9a31c-557">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="9a31c-558">Yukarıdaki komut, bu aracı yapılandırmasını döndürür Syslog ayarları, Linux performans sayaçları ve özel günlükleri gibi portaldan alır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-558">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="9a31c-559">Yukarıdaki komut başarısız olursa, çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a31c-559">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="9a31c-560">Bu komut, en son yapılandırmayı almak için OMS hizmetiyle iletişim kurmak için omsconfig Aracısı zorlar.</span><span class="sxs-lookup"><span data-stu-id="9a31c-560">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="9a31c-561">Özel Linux günlük verilerini OMS Portalı'nda görünmüyor</span><span class="sxs-lookup"><span data-stu-id="9a31c-561">Custom Linux log data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="9a31c-562">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="9a31c-562">Probable causes</span></span>
* <span data-ttu-id="9a31c-563">OMS hizmetine ekleme başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="9a31c-563">Onboarding to OMS Service failed</span></span>
* <span data-ttu-id="9a31c-564">**Aşağıdaki yapılandırmayı Linux Sunucularım uygulamak** ayarı seçilmediğinden</span><span class="sxs-lookup"><span data-stu-id="9a31c-564">The **Apply the following configuration to my Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="9a31c-565">omsconfig Portalı'ndan en son özel günlük yukarı çekilen değil</span><span class="sxs-lookup"><span data-stu-id="9a31c-565">omsconfig has not picked up the latest custom log from the portal</span></span>
* <span data-ttu-id="9a31c-566">`omsagent` Kullanılmasıdır izinlerle ilgili bir sorun nedeniyle özel günlük erişemiyor veya `omsagent` bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-566">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="9a31c-567">Bu durumda, aşağıdaki çıkış görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="9a31c-567">In this case, you'll see the following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="9a31c-568">Bu OMS Aracısı Linux sürüm 1.1.0-217 için düzeltildi yarış durumu ile ilgili bilinen bir sorun olduğu</span><span class="sxs-lookup"><span data-stu-id="9a31c-568">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="9a31c-569">Çözümler</span><span class="sxs-lookup"><span data-stu-id="9a31c-569">Resolutions</span></span>
* <span data-ttu-id="9a31c-570">Belirleyerek, edildi başarıyla olduğunuz doğrulayın olup olmadığını `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` dosya yok.</span><span class="sxs-lookup"><span data-stu-id="9a31c-570">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="9a31c-571">Gerekli olduğunda, yerleşik yeniden omsadmin.sh komut satırını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9a31c-571">If needed, onboard again using the omsadmin.sh command line.</span></span> <span data-ttu-id="9a31c-572">Bkz: [komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9a31c-572">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="9a31c-573">OMS portalında altında **ayarları** üzerinde **veri** sekmesinde, emin **aşağıdaki yapılandırmayı Linux Sunucularım uygulamak** ayarı seçildiğinde</span><span class="sxs-lookup"><span data-stu-id="9a31c-573">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="9a31c-574">![yapılandırmasını Uygula](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="9a31c-574">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="9a31c-575">Doğrulayın `omsconfig` agent OMS hizmetiyle iletişim</span><span class="sxs-lookup"><span data-stu-id="9a31c-575">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="9a31c-576">Çalıştırma `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` komutu</span><span class="sxs-lookup"><span data-stu-id="9a31c-576">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="9a31c-577">Yukarıdaki komut, bu aracı yapılandırmasını döndürür Syslog ayarları, Linux performans sayaçları ve özel günlükleri gibi portaldan alır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-577">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="9a31c-578">Yukarıdaki komut başarısız olursa, çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a31c-578">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="9a31c-579">Bu komut, OMS hizmetiyle iletişim kurmak ve en son yapılandırmayı almak için omsconfig Aracısı zorlar.</span><span class="sxs-lookup"><span data-stu-id="9a31c-579">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span></span>

<span data-ttu-id="9a31c-580">Ayrıcalıklı bir kullanıcı olarak çalışan Linux kullanıcı için OMS aracısının yerine `root`, Linux için OMS aracısının çalışır `omsagent` kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="9a31c-580">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span></span> <span data-ttu-id="9a31c-581">Çoğu durumda, açık kullanıcıya belirli dosyaları okumak için izni verilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-581">In most cases, explicit permission must be granted to the user in order to read certain files.</span></span>

<span data-ttu-id="9a31c-582">İzni vermek için `omsagent` kullanıcı, aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9a31c-582">To grant permission to `omsagent` user, run the following commands:</span></span>

1. <span data-ttu-id="9a31c-583">Ekleme `omsagent` ile belirli bir grup kullanıcı`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="9a31c-583">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="9a31c-584">Gerekli dosyasıyla Evrensel okuma erişimi verin`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="9a31c-584">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="9a31c-585">Linux sürüm 1.1.0-217 için OMS Aracısı giderilmiştir yarış durumu ile ilgili bilinen bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="9a31c-585">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="9a31c-586">En son aracı güncelleştirdikten sonra çıktı eklentisi son sürümünü almak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9a31c-586">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="9a31c-587">Bilinen sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="9a31c-587">Known limitations</span></span>
<span data-ttu-id="9a31c-588">Linux için OMS Aracısı'nın geçerli sınırlamalar hakkında bilgi edinmek için aşağıdaki bölümleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-588">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="9a31c-589">Azure Tanılama</span><span class="sxs-lookup"><span data-stu-id="9a31c-589">Azure Diagnostics</span></span>
<span data-ttu-id="9a31c-590">Azure'da çalışan Linux sanal makineleri için ek adımlar veri toplama izin vermek için Azure tanılama ve Operations Management Suite tarafından gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-590">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="9a31c-591">**Sürüm 2.2** Linux tanılama uzantısını Linux için OMS Aracısı ile uyumluluk için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-591">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span></span>

<span data-ttu-id="9a31c-592">Yükleme ve Linux için tanılama uzantısını yapılandırma hakkında daha fazla bilgi için bkz: [Linux tanılama uzantısını etkinleştirmek için Azure CLI komutunu kullanın](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="9a31c-592">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="9a31c-593">**Linux tanılama uzantısını 2.2 Azure CLI ASM 2. 0'ı yükseltme:**</span><span class="sxs-lookup"><span data-stu-id="9a31c-593">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="9a31c-594">**ARM**</span><span class="sxs-lookup"><span data-stu-id="9a31c-594">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="9a31c-595">Bu komut örnekleri PrivateConfig.json adlı bir dosyaya başvuru.</span><span class="sxs-lookup"><span data-stu-id="9a31c-595">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="9a31c-596">Bu dosya biçiminin aşağıdaki örneğe benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-596">The format of that file should resemble the following sample.</span></span>

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="9a31c-597">Sysklog desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="9a31c-597">Sysklog is not supported</span></span>
<span data-ttu-id="9a31c-598">Rsyslog veya syslog ng syslog iletileri toplamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9a31c-598">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="9a31c-599">Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9a31c-599">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="9a31c-600">Bu dağıtımları bu sürümünden Syslog verileri toplamak için rsyslog arka plan programı yüklenmeli ve sysklog değiştirmek için yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a31c-600">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span> <span data-ttu-id="9a31c-601">Sysklog rsyslog ile değiştirerek daha fazla bilgi için bkz: [yeni oluşturulan rsyslog RPM yüklemek](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="9a31c-601">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a31c-602">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9a31c-602">Next Steps</span></span>
* <span data-ttu-id="9a31c-603">İşlev eklemek ve veri toplamak için bkz. [Çözüm Galerisinden Log Analytics çözümleri ekleme](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="9a31c-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="9a31c-604">Çözümler tarafından toplanan ayrıntılı bilgileri görüntülemek için [günlük aramaları](log-analytics-log-searches.md) hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9a31c-604">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="9a31c-605">Özel aramalarınızı kaydetmek ve görüntülemek için [panolar](log-analytics-dashboards.md)ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a31c-605">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span></span>
