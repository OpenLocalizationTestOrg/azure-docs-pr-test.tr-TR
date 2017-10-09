---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="34814-101">Linux bilgisayarları tooLog Analytics Bağlan</span><span class="sxs-lookup"><span data-stu-id="34814-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="34814-102">Günlük analizi kullanarak toplamak ve Linux bilgisayarları oluşturulan veri hareket.</span><span class="sxs-lookup"><span data-stu-id="34814-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="34814-103">Linux tooOMS ' toplanan verileri eklemeye izin verir, toomanage Linux sistemleri ve nerede olursa olsun bilgisayarlarınızı kapsayıcı çözümleri Docker gibi — neredeyse her yerden.</span><span class="sxs-lookup"><span data-stu-id="34814-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="34814-104">Veri kaynakları, fiziksel sunucuları, Amazon Web Hizmetleri (AWS) veya Microsoft Azure gibi bir bulutta barındırılan hizmetindeki sanal bilgisayarlar olarak, şirket içi veri merkezinizde bulunabilir veya bile dizüstü masanıza hello.</span><span class="sxs-lookup"><span data-stu-id="34814-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="34814-105">Gerçekten karma BT ortamında destekler şekilde ek olarak, OMS ayrıca Windows bilgisayarlardan benzer şekilde, toplar.</span><span class="sxs-lookup"><span data-stu-id="34814-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="34814-106">Görüntüleme ve tüm OMS günlük analizi ile bu kaynakları tek bir Yönetim Portalı ile verileri yönetme.</span><span class="sxs-lookup"><span data-stu-id="34814-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="34814-107">Bu hello ihtiyacını azaltır toomonitor birçok farklı sistemleri kullanarak kılar kolay tooconsume ve sahip olduğunuz toowhatever iş analiz çözümü veya sistem gibi herhangi bir veriyi dışa aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="34814-108">Bu makalede toplamak ve Linux için OMS aracısının hello kullanarak, Linux bilgisayarların verilerini yönetmenize yardımcı olacak bir Hızlı Başlangıç Kılavuzu ' dir.</span><span class="sxs-lookup"><span data-stu-id="34814-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="34814-109">Proxy sunucu yapılandırması, CollectD ölçümleri ve özel JSON veri kaynakları hakkında bilgi gibi daha fazla teknik bilgi için bu bilgileri bulabilirsiniz [Linux genel bakış için OMS Aracısı](https://github.com/Microsoft/OMS-Agent-for-Linux) ve [Linux için OMS Aracısı tam belgelerine](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) github'da.</span><span class="sxs-lookup"><span data-stu-id="34814-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="34814-110">Şu anda veri türleri Linux bilgisayarları izleyen hello toplayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34814-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="34814-111">Performans ölçümleri</span><span class="sxs-lookup"><span data-stu-id="34814-111">Performance metrics</span></span>
* <span data-ttu-id="34814-112">Syslog olayları</span><span class="sxs-lookup"><span data-stu-id="34814-112">Syslog events</span></span>
* <span data-ttu-id="34814-113">Nagios ve Zabbix uyarıları</span><span class="sxs-lookup"><span data-stu-id="34814-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="34814-114">Docker kapsayıcısı performans ölçümleri, Envanter ve günlükleri</span><span class="sxs-lookup"><span data-stu-id="34814-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="34814-115">Desteklenen Linux sürümleri</span><span class="sxs-lookup"><span data-stu-id="34814-115">Supported Linux versions</span></span>
<span data-ttu-id="34814-116">Hem x86 hem x64 sürümleri Linux dağıtımları çeşitli resmi olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="34814-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="34814-117">Ancak, hello OMS Aracısı Linux için listelenmeyen diğer dağıtımlar da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="34814-118">Amazon Linux 2015.09 aracılığıyla 2012.09</span><span class="sxs-lookup"><span data-stu-id="34814-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="34814-119">CentOS Linux 5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="34814-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="34814-120">Oracle Linux 5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="34814-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="34814-121">Red Hat Enterprise Linux Server 5, 6 ve 7</span><span class="sxs-lookup"><span data-stu-id="34814-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="34814-122">Debian GNU/Linux 6, 7 ve 8</span><span class="sxs-lookup"><span data-stu-id="34814-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="34814-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="34814-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="34814-124">SUSE Linux Enterprise Server 11 ve 12</span><span class="sxs-lookup"><span data-stu-id="34814-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="34814-125">Linux için OMS Aracısı</span><span class="sxs-lookup"><span data-stu-id="34814-125">OMS Agent for Linux</span></span>
<span data-ttu-id="34814-126">Merhaba Linux için Operations Management Suite Aracısı birden çok paket oluşur.</span><span class="sxs-lookup"><span data-stu-id="34814-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="34814-127">Merhaba yayın dosyasını içeren paketler, çalışan hello Kabuk Paketle tarafından kullanılabilen aşağıdaki hello `--extract`.</span><span class="sxs-lookup"><span data-stu-id="34814-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="34814-128">**Paket**</span><span class="sxs-lookup"><span data-stu-id="34814-128">**Package**</span></span> | <span data-ttu-id="34814-129">**Sürüm**</span><span class="sxs-lookup"><span data-stu-id="34814-129">**Version**</span></span> | <span data-ttu-id="34814-130">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="34814-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34814-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="34814-131">omsagent</span></span> |<span data-ttu-id="34814-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="34814-132">1.1.0</span></span> |<span data-ttu-id="34814-133">Merhaba Linux için Operations Management Suite Aracısı</span><span class="sxs-lookup"><span data-stu-id="34814-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="34814-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="34814-134">omsconfig</span></span> |<span data-ttu-id="34814-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="34814-135">1.1.1</span></span> |<span data-ttu-id="34814-136">Merhaba OMS aracısı için yapılandırma aracısı</span><span class="sxs-lookup"><span data-stu-id="34814-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="34814-137">OMI</span><span class="sxs-lookup"><span data-stu-id="34814-137">omi</span></span> |<span data-ttu-id="34814-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="34814-138">1.0.8.3</span></span> |<span data-ttu-id="34814-139">Açık Yönetim Altyapısı (OMI)--bir basit CIM sunucusu</span><span class="sxs-lookup"><span data-stu-id="34814-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="34814-140">scx</span><span class="sxs-lookup"><span data-stu-id="34814-140">scx</span></span> |<span data-ttu-id="34814-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="34814-141">1.6.2</span></span> |<span data-ttu-id="34814-142">İşletim sistemi performans ölçümleri için OMI CIM sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="34814-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="34814-143">Apache cimprov</span><span class="sxs-lookup"><span data-stu-id="34814-143">apache-cimprov</span></span> |<span data-ttu-id="34814-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="34814-144">1.0.0</span></span> |<span data-ttu-id="34814-145">Apache HTTP Server performansı sağlayıcısı OMI için izleme.</span><span class="sxs-lookup"><span data-stu-id="34814-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="34814-146">Apache HTTP Server algılanırsa, yalnızca yüklü.</span><span class="sxs-lookup"><span data-stu-id="34814-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="34814-147">MySQL cimprov</span><span class="sxs-lookup"><span data-stu-id="34814-147">mysql-cimprov</span></span> |<span data-ttu-id="34814-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="34814-148">1.0.0</span></span> |<span data-ttu-id="34814-149">MySQL sunucusu performans sağlayıcısı OMI için izleme.</span><span class="sxs-lookup"><span data-stu-id="34814-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="34814-150">MySQL/MariaDB sunucu algılanırsa, yalnızca yüklü.</span><span class="sxs-lookup"><span data-stu-id="34814-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="34814-151">docker cimprov</span><span class="sxs-lookup"><span data-stu-id="34814-151">docker-cimprov</span></span> |<span data-ttu-id="34814-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="34814-152">0.1.0</span></span> |<span data-ttu-id="34814-153">OMI docker sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="34814-153">Docker provider for OMI.</span></span> <span data-ttu-id="34814-154">Docker algılanırsa, yalnızca yüklü.</span><span class="sxs-lookup"><span data-stu-id="34814-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="34814-155">Ek yükleme yapıları</span><span class="sxs-lookup"><span data-stu-id="34814-155">Additional installation artifacts</span></span>
<span data-ttu-id="34814-156">Linux paketler için Hello OMS Aracısı yüklendikten sonra hello aşağıdaki ek sistem genelinde yapılandırma değişiklikleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="34814-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="34814-157">Bu yapıtların Hello omsagent paket kaldırıldığında kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="34814-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="34814-158">Adlı bir ayrıcalıklı olmayan kullanıcı: `omsagent` oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="34814-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="34814-159">Merhaba hesap hello omsagent arka plan programı çalışırken budur</span><span class="sxs-lookup"><span data-stu-id="34814-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="34814-160">"Ekle" sudoers dosyası oluşturulur omsagent toorestart hello syslog ve omsagent deamon'lar /etc/sudoers.d/omsagent bu yetkilendirir.</span><span class="sxs-lookup"><span data-stu-id="34814-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="34814-161">Sudo "Ekle" yönergeleri sudo yüklü hello sürümünde desteklenmez, bu girişler çok/etc/sudoers yazılır.</span><span class="sxs-lookup"><span data-stu-id="34814-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="34814-162">Değiştirilen tooforward olayları toohello Aracısı'nın bir alt Hello syslog yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="34814-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="34814-163">Merhaba daha fazla bilgi için bkz: **yapılandırma veri toplama** bölümüne bakın</span><span class="sxs-lookup"><span data-stu-id="34814-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="34814-164">Linux veri toplama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="34814-164">Linux data collection details</span></span>
<span data-ttu-id="34814-165">Merhaba aşağıdaki tabloda veri toplama yöntemleri ve verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="34814-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="34814-166">Kaynak</span><span class="sxs-lookup"><span data-stu-id="34814-166">source</span></span> | <span data-ttu-id="34814-167">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="34814-167">Direct Agent</span></span> | <span data-ttu-id="34814-168">SCOM Aracısı</span><span class="sxs-lookup"><span data-stu-id="34814-168">SCOM agent</span></span> | <span data-ttu-id="34814-169">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="34814-169">Azure Storage</span></span> | <span data-ttu-id="34814-170">SCOM gerekli?</span><span class="sxs-lookup"><span data-stu-id="34814-170">SCOM required?</span></span> | <span data-ttu-id="34814-171">Yönetim grubu gönderilen SCOM Aracısı verileri</span><span class="sxs-lookup"><span data-stu-id="34814-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="34814-172">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="34814-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="34814-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="34814-173">Zabbix</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="34814-179">1 dakika</span><span class="sxs-lookup"><span data-stu-id="34814-179">1 minute</span></span> |
| <span data-ttu-id="34814-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="34814-180">Nagios</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="34814-186">geldiğinde</span><span class="sxs-lookup"><span data-stu-id="34814-186">on arrival</span></span> |
| <span data-ttu-id="34814-187">syslog</span><span class="sxs-lookup"><span data-stu-id="34814-187">syslog</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="34814-193">Azure depolama biriminden: 10 dakika; aracısından: işle</span><span class="sxs-lookup"><span data-stu-id="34814-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="34814-194">Linux performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="34814-194">Linux performance counters</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="34814-200">Zamanlandığı gibi en az 10 saniye</span><span class="sxs-lookup"><span data-stu-id="34814-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="34814-201">değişiklik izleme</span><span class="sxs-lookup"><span data-stu-id="34814-201">change tracking</span></span> |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="34814-207">saatlik</span><span class="sxs-lookup"><span data-stu-id="34814-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="34814-208">Paket gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="34814-208">Package Requirements</span></span>
| <span data-ttu-id="34814-209">**Gerekli paket**</span><span class="sxs-lookup"><span data-stu-id="34814-209">**Required package**</span></span> | <span data-ttu-id="34814-210">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="34814-210">**Description**</span></span> | <span data-ttu-id="34814-211">**En düşük sürüm**</span><span class="sxs-lookup"><span data-stu-id="34814-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34814-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="34814-212">Glibc</span></span> |<span data-ttu-id="34814-213">GNU C Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="34814-213">GNU C library</span></span> |<span data-ttu-id="34814-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="34814-214">2.5-12</span></span> |
| <span data-ttu-id="34814-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="34814-215">Openssl</span></span> |<span data-ttu-id="34814-216">OpenSSL kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="34814-216">OpenSSL libraries</span></span> |<span data-ttu-id="34814-217">0.9.8E veya 1.0</span><span class="sxs-lookup"><span data-stu-id="34814-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="34814-218">Curl</span><span class="sxs-lookup"><span data-stu-id="34814-218">Curl</span></span> |<span data-ttu-id="34814-219">cURL web istemcisi</span><span class="sxs-lookup"><span data-stu-id="34814-219">cURL web client</span></span> |<span data-ttu-id="34814-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="34814-220">7.15.5</span></span> |
| <span data-ttu-id="34814-221">Python ctypes</span><span class="sxs-lookup"><span data-stu-id="34814-221">Python-ctypes</span></span> |<span data-ttu-id="34814-222">işlev kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="34814-222">function libraries</span></span> |<span data-ttu-id="34814-223">yok</span><span class="sxs-lookup"><span data-stu-id="34814-223">n/a</span></span> |
| <span data-ttu-id="34814-224">PAM</span><span class="sxs-lookup"><span data-stu-id="34814-224">PAM</span></span> |<span data-ttu-id="34814-225">Eklenebilir kimlik doğrulaması modülleri</span><span class="sxs-lookup"><span data-stu-id="34814-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="34814-226">yok</span><span class="sxs-lookup"><span data-stu-id="34814-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="34814-227">Rsyslog veya syslog ng gerekli toocollect syslog iletileri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="34814-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="34814-228">Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü Hello varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="34814-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="34814-229">Bu sürümü bu dağıtımları toocollect syslog verileri hello rsyslog arka plan programı yüklenmelidir ve tooreplace sysklog yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="34814-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="34814-230">Hızlı yükleme</span><span class="sxs-lookup"><span data-stu-id="34814-230">Quick install</span></span>
<span data-ttu-id="34814-231">Aşağıdaki komutları toodownload hello omsagent hello çalıştırın, hello sağlama toplamı, sonra Yükle ve yerleşik hello Aracısı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="34814-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="34814-232">64 bit için komutlardır.</span><span class="sxs-lookup"><span data-stu-id="34814-232">Commands are for 64-bit.</span></span> <span data-ttu-id="34814-233">Merhaba çalışma alanı kimliği ve birincil anahtar hello OMS portalında altında bulunan **ayarları** hello üzerinde **bağlı kaynakları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="34814-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![çalışma alanı ayrıntıları](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="34814-235">Diğer yöntemleri tooinstall çeşitli vardır hello aracısı ve bunu yükseltin.</span><span class="sxs-lookup"><span data-stu-id="34814-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="34814-236">Daha fazla bilgiyi onları hakkında [adımları tooinstall hello Linux için OMS aracısının](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="34814-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="34814-237">Merhaba de görüntüleyebilirsiniz [Azure videosu](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="34814-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="34814-238">Linux veri toplama yönteminizi seçin</span><span class="sxs-lookup"><span data-stu-id="34814-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="34814-239">Nasıl hello toouse hello OMS portalı isteyip istemediğinizi toocollect bağlıdır gibi ya da Linux istemcileri doğrudan üzerinde çeşitli yapılandırma dosyalarını düzenlemek istiyorsanız yaptığınız veri türlerini seçin.</span><span class="sxs-lookup"><span data-stu-id="34814-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="34814-240">Merhaba yapılandırma toouse hello portal seçerseniz, Linux istemcilerinizin tooall otomatik olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="34814-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="34814-241">Farklı Linux istemcileri için farklı yapılandırmaları gerekiyorsa, bunu tooedit istemci dosyalarını ayrı ayrı – gerekir veya alternatif PowerShell DSC, Chef veya Puppet gibi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="34814-242">Merhaba Linux bilgisayarlarda yapılandırma dosyalarını kullanarak toocollect istediğiniz performans sayaçları ve hello syslog olayları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="34814-243">*Tooconfigure veri toplama Aracısı Yapılandırma dosyalarını düzenleyerek seçerseniz, hello Merkezi yapılandırma devre dışı bırakmanız gerekir.*</span><span class="sxs-lookup"><span data-stu-id="34814-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="34814-244">Yönergeler tooconfigure veri koleksiyonunda hello aracısının yapılandırma dosyalarının yanı sıra toodisable Linux ya da ayrı bilgisayarlar için tüm OMS aracılar için merkezi yapılandırma aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="34814-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="34814-245">Tek bir Linux bilgisayar için OMS yönetimi devre dışı</span><span class="sxs-lookup"><span data-stu-id="34814-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="34814-246">Yapılandırma verileri için merkezi veri toplama hello OMS_MetaConfigHelper.py betik ile tek bir Linux bilgisayarı devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="34814-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="34814-247">Bu, bilgisayarların alt ağlarından özel bir yapılandırmanız varsa yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="34814-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="34814-248">toodisable Merkezi yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="34814-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="34814-249">Merkezi yapılandırma toore etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="34814-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="34814-250">Linux performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="34814-250">Linux performance counters</span></span>
<span data-ttu-id="34814-251">Linux performans sayaçları olan benzer tooWindows performans sayaçları — her ikisi de aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="34814-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="34814-252">Aşağıdaki yordamlar tooadd hello kullanın ve bunları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="34814-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="34814-253">Verileri tooOMS eklendikten sonra bunlar için her 30 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="34814-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="34814-254">tooadd OMS Linux performans sayacında</span><span class="sxs-lookup"><span data-stu-id="34814-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="34814-255">tooconfigure hello OMS portalı kullanarak Linux için OMS aracıları, Linux performans sayaçlarını ekleme yapabilir hello Ayarları sayfasında, tıklatın **veri**.</span><span class="sxs-lookup"><span data-stu-id="34814-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="34814-256">Merhaba üzerinde **ayarları** altında sayfa **veri** , tıklatın **Linux performans sayaçları** ve ardından seçin ya da türü hello adı tooadd istediğiniz hello sayacını da.</span><span class="sxs-lookup"><span data-stu-id="34814-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="34814-257">![veri](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="34814-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="34814-258">Merhaba tam hello sayacının adını bilmiyorsanız, kısmi bir ad yazarak başlatabilirsiniz ve kullanılabilir sayaçlarının listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="34814-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="34814-259">Merhaba sayaç bulduğunuzda, tooadd, hello listesinde hello adına tıklayın ve ardından hello artı simgesine tooadd hello sayacı.</span><span class="sxs-lookup"><span data-stu-id="34814-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="34814-260">Merhaba sayaç ekledikten sonra hello renkli çubuk ile vurgulanan sayaçlarının listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="34814-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="34814-261">Varsayılan olarak, hello **aşağıdaki yapılandırma toomy makineler Uygula** seçeneği işaretlidir.</span><span class="sxs-lookup"><span data-stu-id="34814-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="34814-262">Yapılandırma verileri gönderme toodisable istiyorsanız hello seçimi temizleyin.</span><span class="sxs-lookup"><span data-stu-id="34814-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="34814-263">Merhaba sayfanın hello sonundaki değiştirme performans sayaçları bittiğinde tıklatın **kaydetmek** toofinalize değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="34814-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="34814-264">yapmış olduğunuz hello yapılandırma değişiklikleri, OMS ile genellikle 5 dakika içinde kayıtlı Linux tooall hello OMS Aracısı sonra gönderilir.</span><span class="sxs-lookup"><span data-stu-id="34814-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="34814-265">Linux performans sayaçları OMS yapılandırın</span><span class="sxs-lookup"><span data-stu-id="34814-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="34814-266">Windows performans sayaçları için her performans sayacı için belirli bir örneği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="34814-267">Ancak, Linux performans sayaçlarını tooall alt sayaçları hello üst sayacının ne olursa olsun, seçtiğiniz bir sayaç örneği geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="34814-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="34814-268">Merhaba aşağıdaki tabloda hello ortak örnekleri kullanılabilir tooboth Linux ve Windows performans sayaçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="34814-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="34814-269">**Örnek adı**</span><span class="sxs-lookup"><span data-stu-id="34814-269">**Instance name**</span></span> | <span data-ttu-id="34814-270">**Anlamı**</span><span class="sxs-lookup"><span data-stu-id="34814-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="34814-271">\_Toplam</span><span class="sxs-lookup"><span data-stu-id="34814-271">\_Total</span></span> |<span data-ttu-id="34814-272">Tüm hello örnekleri toplamı</span><span class="sxs-lookup"><span data-stu-id="34814-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="34814-273">Tüm örnekleri</span><span class="sxs-lookup"><span data-stu-id="34814-273">All instances</span></span> |
| <span data-ttu-id="34814-274">(/ &#124; / var)</span><span class="sxs-lookup"><span data-stu-id="34814-274">(/&#124;/var)</span></span> |<span data-ttu-id="34814-275">Eşleşen adlandırılmış örnekleri: / veya /var</span><span class="sxs-lookup"><span data-stu-id="34814-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="34814-276">Benzer şekilde, seçtiğiniz bir üst sayacının hello örnekleme aralığı, alt sayaçlarını tooall geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="34814-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="34814-277">Diğer bir deyişle, tüm hello alt sayacı örnek aralıklar ve örnekleri birbirine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="34814-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="34814-278">Ekleme ve performans ölçümleri Linux ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34814-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="34814-279">Performans ölçümleri toocollect hello yapılandırma içinde/etc/opt/microsoft/omsagent tarafından denetlenen/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="34814-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="34814-280">Bkz: [kullanılabilir performans ölçümleri](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) kullanılabilir sınıfların ve hello Linux için OMS aracısı için ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="34814-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="34814-281">Tek bir olarak hello yapılandırma dosyasındaki her nesne veya kategorisi, performans ölçümleri toocollect tanımlanmalıdır `<source>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="34814-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="34814-282">Merhaba sözdizimi aşağıdaki hello deseni izler.</span><span class="sxs-lookup"><span data-stu-id="34814-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="34814-283">Bu öğenin Hello yapılandırılabilir Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="34814-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="34814-284">**Nesne\_adı**: hello koleksiyonu için hello nesne adı.</span><span class="sxs-lookup"><span data-stu-id="34814-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="34814-285">**Örnek\_regex**: bir *normal ifade* hangi örnekleri toocollect tanımlama.</span><span class="sxs-lookup"><span data-stu-id="34814-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="34814-286">Merhaba değeri: `.*` tüm örneklerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="34814-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="34814-287">yalnızca hello için toocollect işlemci ölçümleri \_toplam örneğini belirtmek `_Total`.</span><span class="sxs-lookup"><span data-stu-id="34814-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="34814-288">toocollect işlem ölçümlerini yalnızca hello crond veya sshd örneği, belirtebilirsiniz: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="34814-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="34814-289">**Sayaç\_adı\_regex**: bir *normal ifade* hangi (Merhaba nesnesi) sayaçları toocollect tanımlama.</span><span class="sxs-lookup"><span data-stu-id="34814-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="34814-290">Merhaba nesnesi için tüm sayaçlar toocollect belirtin: `.*`.</span><span class="sxs-lookup"><span data-stu-id="34814-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="34814-291">toocollect hello bellek nesnesi için yalnızca alanı sayaçları değiştirme, belirtebilirsiniz:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="34814-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="34814-292">**Aralığı:**: Merhaba sıklığı hangi hello nesnesinin sayaçları toplanır.</span><span class="sxs-lookup"><span data-stu-id="34814-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="34814-293">Performans ölçümleri Hello varsayılan yapılandırmasını şöyledir:</span><span class="sxs-lookup"><span data-stu-id="34814-293">hello default configuration for performance metrics is:</span></span>

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="34814-294">MySQL performans sayaçlarını Linux komutlarını kullanarak etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="34814-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="34814-295">Hello omsagent paketi yüklendiğinde, MySQL Server veya MariaDB Server hello bilgisayarında algılanırsa, bir performans izleme sağlayıcısı MySQL sunucusu için otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="34814-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="34814-296">Bu sağlayıcı toohello yerel MySQL/MariaDB sunucu tooexpose performans istatistikleri bağlanır.</span><span class="sxs-lookup"><span data-stu-id="34814-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="34814-297">Merhaba sağlayıcısı hello MySQL Server erişebilmesi için tooconfigure MySQL kullanıcı kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="34814-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="34814-298">toodefine varsayılan kullanıcı hello MySQL sunucusu için aşağıdaki komutu örneğine kullanım hello localhost üzerinde hesap.</span><span class="sxs-lookup"><span data-stu-id="34814-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="34814-299">Merhaba kimlik bilgileri dosyası hello omsagent hesabı tarafından okunabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="34814-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="34814-300">Omsgent Hello mycimprovauth komutunun çalıştırılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="34814-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="34814-301">Alternatif olarak, hello hello dosya oluşturarak bir dosyada MySQL kimlik bilgileri gerekli belirtebilirsiniz: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Merhaba mysql auth dosyası aracılığıyla izleme MySQL kimlik bilgilerini yönetme hakkında daha fazla bilgi için bkz: [hello authentication dosyasındaki kimlik bilgilerini izleme MySQL yönetmek](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="34814-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="34814-302">Bkz: [veritabanı için MySQL performans sayaçları gerekli izinler](#database-permissions-required-for-mysql-performance-counters) hello MySQL kullanıcı toocollect MySQL sunucu performans verisi gerekli nesne izinler hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="34814-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="34814-303">Linux komutlarını kullanarak Apache HTTP Server performans sayaçları sağlar</span><span class="sxs-lookup"><span data-stu-id="34814-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="34814-304">Hello omsagent paketi yüklendiğinde, Apache HTTP Server hello bilgisayarında algılanırsa, bir performans izlemesi için Apache HTTP Server sağlayıcısı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="34814-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="34814-305">Bu sağlayıcı bir Apache "Merhaba Apache HTTP Server sipariş tooaccess performans verilerindeki içine yüklenmesi gereken modül" kullanır.</span><span class="sxs-lookup"><span data-stu-id="34814-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="34814-306">Merhaba modülü komutu aşağıdaki hello ile yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34814-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="34814-307">komutu aşağıdaki hello çalıştırmak toounload hello Apache izleme Modülü'nü:</span><span class="sxs-lookup"><span data-stu-id="34814-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="34814-308">Günlük analizi ile tooview performans verileri</span><span class="sxs-lookup"><span data-stu-id="34814-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="34814-309">Merhaba Operations Management Suite Portalı'nda hello günlük arama kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="34814-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="34814-310">Merhaba Arama çubuğuna `* (Type=Perf)` tooview tüm performans sayaçları.</span><span class="sxs-lookup"><span data-stu-id="34814-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="34814-311">OMS aynı zamanda Windows performans sayacı verilerini toplar olduğundan, kapsam aşağı hello arama tooLinux özgü verileri.</span><span class="sxs-lookup"><span data-stu-id="34814-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="34814-312">Bu nedenle, hello aşağıdaki örnek performans veri belirli tooan Örnek Linux sunucusu Chorizo21 adlı gösterir.</span><span class="sxs-lookup"><span data-stu-id="34814-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![arama sonuçlarında gösterilen örnekte, sunucu](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="34814-314">Merhaba sonuçlarında tıklayabilirsiniz **ölçümleri** veri için toplanan tooview hello sayaçları.</span><span class="sxs-lookup"><span data-stu-id="34814-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="34814-315">Gerçek zamanlı veri grafikleri her sayacı olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="34814-315">Real-time data is shown as graphs for each counter.</span></span>

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="34814-317">Syslog</span><span class="sxs-lookup"><span data-stu-id="34814-317">Syslog</span></span>
<span data-ttu-id="34814-318">Syslog olan bir olay günlüğü Protokolü benzer tooWindows olay günlükleri — hem OMS görüntülendiğinde benzer şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="34814-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="34814-319">tooadd OMS yeni bir Linux syslog yerde</span><span class="sxs-lookup"><span data-stu-id="34814-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="34814-320">Merhaba üzerinde **ayarları** altında sayfa **veri** , tıklatın **Syslog** ve toohello sol hello artı simgesine yazın tooadd istediğiniz hello syslog özelliğini hello adı.</span><span class="sxs-lookup"><span data-stu-id="34814-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="34814-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="34814-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="34814-322">Merhaba tesis hello tam adını bilmiyorsanız, kısmi bir ad yazarak başlatabilirsiniz ve kullanılabilir syslog tesis listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="34814-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="34814-323">Bul zaman, tooadd istediğiniz, hello listesinde hello adını tıklatın ve sonra hello artı simgesine tooadd hello hello syslog özelliğini syslog özelliğini.</span><span class="sxs-lookup"><span data-stu-id="34814-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="34814-324">Merhaba listesinde görüntülenir hello tesis ekledikten sonra renkli çubuk ile vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="34814-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="34814-325">Ardından, hello önem derecelerinin (syslog tesis bilgi kategorilerde) seçin toocollect istiyor.</span><span class="sxs-lookup"><span data-stu-id="34814-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="34814-326">Merhaba hello sayfa sonunda tıklatın **kaydetmek** toofinalize değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="34814-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="34814-327">yapmış olduğunuz hello yapılandırma değişiklikleri, OMS ile genellikle 5 dakika içinde kayıtlı Linux tooall hello OMS Aracısı sonra gönderilir.</span><span class="sxs-lookup"><span data-stu-id="34814-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="34814-328">Linux syslog Linux tesislerde yapılandırın</span><span class="sxs-lookup"><span data-stu-id="34814-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="34814-329">Syslog olayları hello syslog arka plan programından gönderilir, örneğin rsyslog veya syslog ng, tooa yerel bağlantı noktası, hello aracısının dinlediği.</span><span class="sxs-lookup"><span data-stu-id="34814-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="34814-330">Varsayılan olarak, bağlantı noktası 25224.</span><span class="sxs-lookup"><span data-stu-id="34814-330">By default, port 25224.</span></span> <span data-ttu-id="34814-331">Merhaba Aracısı yüklendiğinde, varsayılan bir syslog yapılandırma uygulanır.</span><span class="sxs-lookup"><span data-stu-id="34814-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="34814-332">Bu da bulunur:</span><span class="sxs-lookup"><span data-stu-id="34814-332">This is found at:</span></span>

<span data-ttu-id="34814-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="34814-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="34814-334">Syslog ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="34814-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="34814-335">Merhaba varsayılan OMS Aracısı syslog yapılandırması tüm uyarı veya daha büyük bir önem derecesi araçlarıyla syslog olayları yükler.</span><span class="sxs-lookup"><span data-stu-id="34814-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="34814-336">Merhaba syslog yapılandırma düzenlerseniz, hello değişiklikleri tootake etkisi hello syslog arka plan yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="34814-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="34814-337">Merhaba syslog için varsayılan yapılandırmayı hello OMS aracısı için Linux için OMS şöyledir:</span><span class="sxs-lookup"><span data-stu-id="34814-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="34814-338">rsyslog</span><span class="sxs-lookup"><span data-stu-id="34814-338">Rsyslog</span></span>
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

#### <a name="syslog-ng"></a><span data-ttu-id="34814-339">Syslog ng</span><span class="sxs-lookup"><span data-stu-id="34814-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="34814-340">tooview günlük analizi ile tüm Syslog olayları</span><span class="sxs-lookup"><span data-stu-id="34814-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="34814-341">Merhaba Hello Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.</span><span class="sxs-lookup"><span data-stu-id="34814-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="34814-342">Merhaba, **Günlüğü Yönetimi** gruplandırma, önceden tanımlanmış syslog arama seçin ve ardından bir toorun seçin.</span><span class="sxs-lookup"><span data-stu-id="34814-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="34814-343">Bu örnekte tüm Syslog olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="34814-343">This example shows all Syslog events.</span></span>

![Günlük aramada gösterilen Syslog olayları](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="34814-345">Şimdi arama sonuçlarında detaya inebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="34814-346">Linux uyarıları</span><span class="sxs-lookup"><span data-stu-id="34814-346">Linux alerts</span></span>
<span data-ttu-id="34814-347">Nagios veya Zabbix toomanage kullanırsanız, Linux makineler sonra OMS bu Araçları'ndan oluşturulan hello uyarıları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="34814-348">Ancak, hello OMS portalı kullanarak şu anda yöntemi tooconfigure gelen uyarı verisi yok.</span><span class="sxs-lookup"><span data-stu-id="34814-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="34814-349">Bunun yerine, bir yapılandırma dosyası toostart gönderen uyarılar tooOMS tooedit gerekir.</span><span class="sxs-lookup"><span data-stu-id="34814-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="34814-350">Nagios toplama uyarıları</span><span class="sxs-lookup"><span data-stu-id="34814-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="34814-351">Nagios sunucusundan toocollect uyarıları, aşağıdaki yapılandırma değişiklikler toomake hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="34814-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="34814-352">GRANT hello kullanıcı **omsagent** okuma erişimi toohello Nagios günlük dosyası (yani /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="34814-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="34814-353">Merhaba nagios.log dosya hello grupla ait olduğu varsayılarak **nagios** , hello kullanıcı ekleyebilir **omsagent** toohello **nagios** grubu.</span><span class="sxs-lookup"><span data-stu-id="34814-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="34814-354">Merhaba omsagent.confconfiguration dosyasını değiştirme (/ etc/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="34814-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="34814-355">Mevcut ve kullanıma açıklamalı girişleri aşağıdaki hello çalıştığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="34814-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
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
    ```
3. <span data-ttu-id="34814-356">Merhaba omsagent arka plan programı yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="34814-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="34814-357">Zabbix toplama uyarıları</span><span class="sxs-lookup"><span data-stu-id="34814-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="34814-358">toocollect, gerçekleştireceğiniz benzer adımları toothose Nagios yukarıdaki toospecify bir kullanıcı ve parola gerekir dışında bir Zabbix sunucusundan uyarıları *açık metin*.</span><span class="sxs-lookup"><span data-stu-id="34814-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="34814-359">Bu ideal olmayan, ancak büyük olasılıkla yakında değiştirir.</span><span class="sxs-lookup"><span data-stu-id="34814-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="34814-360">tooaddress bu sorunu hello kullanıcı oluşturun ve yalnızca izin toomonitor vermek öneririz.</span><span class="sxs-lookup"><span data-stu-id="34814-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="34814-361">Bir örnek bölüm hello omsagent.conf yapılandırma dosyasının (/ etc/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf) Zabbix hello aşağıdaki benzemelidir için:</span><span class="sxs-lookup"><span data-stu-id="34814-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

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

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="34814-362">Günlük analizi arama uyarıları görüntüle</span><span class="sxs-lookup"><span data-stu-id="34814-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="34814-363">Linux bilgisayarları toosend uyarıları tooOMS yapılandırdıktan sonra birkaç basit günlük arama sorguları tooview hello uyarıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="34814-364">Merhaba aşağıdaki arama sorgusu örneğinde oluşturulan tüm kayıtlı hello uyarıların döndürür.</span><span class="sxs-lookup"><span data-stu-id="34814-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="34814-365">Örneğin, BT altyapınızın sorun çeşit meydana gelirse, ardından aşağıdaki sorgu hello sorun nerede kaynaklanan gösterebilir örneğine Merhaba sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="34814-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="34814-366">Ve, kolayca toohello uyarılar kaynak sistem toohelp tarafından dar araştırmanızı inebilir.</span><span class="sxs-lookup"><span data-stu-id="34814-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="34814-367">Merhaba hello başından toogo toovarious yönetim sistemleri mutlaka yok avantajdır — uyarılarınızı tooOMS gönderilen koşuluyla var. başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="34814-368">Tüm Nagios uyarıları günlük analizi ile tooview</span><span class="sxs-lookup"><span data-stu-id="34814-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="34814-369">Merhaba Hello Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.</span><span class="sxs-lookup"><span data-stu-id="34814-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="34814-370">Arama sorgusu aşağıdaki hello Hello sorgu çubuğuna yazın</span><span class="sxs-lookup"><span data-stu-id="34814-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Günlük aramada gösterilen Nagios uyarıları](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="34814-372">Merhaba arama sonuçlarını sonra ek ayrıntılar gibi inebilir *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="34814-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="34814-373">tooview günlük analizi ile tüm Zabbix uyarıları</span><span class="sxs-lookup"><span data-stu-id="34814-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="34814-374">Merhaba Hello Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.</span><span class="sxs-lookup"><span data-stu-id="34814-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="34814-375">Arama sorgusu aşağıdaki hello Hello sorgu çubuğuna yazın</span><span class="sxs-lookup"><span data-stu-id="34814-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Günlük aramada gösterilen Zabbix uyarıları](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="34814-377">Merhaba arama sonuçlarını sonra ek ayrıntılar gibi inebilir *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="34814-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="34814-378">System Center Operations Manager ile uyumluluk</span><span class="sxs-lookup"><span data-stu-id="34814-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="34814-379">Merhaba OMS Aracısı Linux Aracısı ikili dosyalarının hello System Center Operations Manager Aracısı ile paylaşır.</span><span class="sxs-lookup"><span data-stu-id="34814-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="34814-380">Linux için şu anda Operations Manager tarafından yönetilen bir sistemi Hello OMS Aracısı yüklenmesi yükseltmeler hello bilgisayar tooa daha yeni sürümü OMI ve SCX paketleri hello.</span><span class="sxs-lookup"><span data-stu-id="34814-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="34814-381">Merhaba Linux ve System Center 2012 R2 için OMS aracısının uyumlu.</span><span class="sxs-lookup"><span data-stu-id="34814-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="34814-382">Ancak, **System Center 2012 SP1 ve önceki sürümleri olmayan şu anda desteklenen veya uyumlu hello Linux için OMS Aracısı ile.**</span><span class="sxs-lookup"><span data-stu-id="34814-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="34814-383">Merhaba bilgisayarını Bul önce hello OMS Aracısı Linux için Operations Manager tarafından yönetilen değil yüklü tooa bilgisayardır ve daha sonra toomanage hello bilgisayar Operations Manager ile istiyorsanız hello OMI yapılandırma değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="34814-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="34814-384">**Linux için OMS Aracısı hello önce Hello Operations Manager Aracısı yüklüyse, bu adım gerekli değildir.**</span><span class="sxs-lookup"><span data-stu-id="34814-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="34814-385">Operations Manager ile Linux toocommunicate tooenable Merhaba OMS Aracısı</span><span class="sxs-lookup"><span data-stu-id="34814-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="34814-386">Merhaba dosya /etc/opt/omi/conf/omiserver.conf Düzenle</span><span class="sxs-lookup"><span data-stu-id="34814-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="34814-387">Bu hello satır başlayarak olun **httpsport =** hello bağlantı noktası 1270 tanımlar.</span><span class="sxs-lookup"><span data-stu-id="34814-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="34814-388">Gibi`httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="34814-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="34814-389">Merhaba OMI sunucuyu yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="34814-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="34814-390">MySQL performans sayaçları için gereken veritabanı izinleri</span><span class="sxs-lookup"><span data-stu-id="34814-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="34814-391">toogrant izinlerini tooa MySQL izleme kullanıcıya, hello izni veriliyor kullanıcı verilmeden hello ayrıcalık yanı sıra hello 'GRANT option' ayrıcalığına sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34814-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="34814-392">Merhaba MySQL kullanıcı için sırayla tooreturn performans verileri hello kullanıcı sorguları aşağıdaki toohello erişecek:</span><span class="sxs-lookup"><span data-stu-id="34814-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="34814-393">Ayrıca toothese sorguları hello MySQL kullanıcı varsayılan tabloları aşağıdaki SELECT erişim toohello gerektirir:</span><span class="sxs-lookup"><span data-stu-id="34814-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="34814-394">INFORMATION_SCHEMA</span><span class="sxs-lookup"><span data-stu-id="34814-394">information_schema</span></span>
* <span data-ttu-id="34814-395">MySQL</span><span class="sxs-lookup"><span data-stu-id="34814-395">mysql</span></span>

<span data-ttu-id="34814-396">Bu ayrıcalıkları verme komutları aşağıdaki hello çalıştırarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="34814-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="34814-397">Kimlik bilgileri hello authentication dosyasındaki İzleme MySQL yönetme</span><span class="sxs-lookup"><span data-stu-id="34814-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="34814-398">MySQL kimlik bilgilerini yönetmenize yardımcı Hello aşağıdaki bölümler.</span><span class="sxs-lookup"><span data-stu-id="34814-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="34814-399">Merhaba MySQL OMI sağlayıcı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34814-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="34814-400">Merhaba MySQL OMI sağlayıcısı önceden yapılandırılmış bir MySQL kullanıcının gerektiren ve MySQL istemci kitaplıkları sipariş tooquery hello performans/sistem durumu bilgilerini hello MySQL örneğinden yüklenir.</span><span class="sxs-lookup"><span data-stu-id="34814-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="34814-401">MySQL OMI kimlik doğrulaması dosyası</span><span class="sxs-lookup"><span data-stu-id="34814-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="34814-402">MySQL OMI sağlayıcısı hangi bağlama adresi ve bağlantı noktası hello MySQL örneği dinlediği bir kimlik doğrulama dosya toodetermine ve ne toouse toogather ölçümleri kimlik bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="34814-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="34814-403">Yükleme hello MySQL OMI sırasında bağlama adresi ve bağlantı noktası kümesi hello MySQL OMI kimlik doğrulama dosyasını için ve kısmen MySQL my.cnf yapılandırma dosyalarını (varsayılan konumları) sağlayıcısı tarar.</span><span class="sxs-lookup"><span data-stu-id="34814-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="34814-404">bir MySQL server örneğini toocomplete izleme hello doğru dizine önceden oluşturulmuş bir MySQL OMI kimlik doğrulaması dosya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34814-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="34814-405">Kimlik doğrulama dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="34814-405">Authentication file format</span></span>
<span data-ttu-id="34814-406">Merhaba MySQL OMI kimlik doğrulama dosyasını hakkında bilgi içeren bir metin dosyasıdır:</span><span class="sxs-lookup"><span data-stu-id="34814-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="34814-407">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="34814-407">Port</span></span>
* <span data-ttu-id="34814-408">Bağ adresi</span><span class="sxs-lookup"><span data-stu-id="34814-408">Bind-Address</span></span>
* <span data-ttu-id="34814-409">MySQL kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="34814-409">MySQL username</span></span>
* <span data-ttu-id="34814-410">Base64 ile kodlanmış parola</span><span class="sxs-lookup"><span data-stu-id="34814-410">Base64 encoded password</span></span>

<span data-ttu-id="34814-411">Merhaba MySQL OMI kimlik doğrulama dosyasını yalnızca oluşturulduğu okuma/yazma toohello Linux kullanıcı ayrıcalıkları verir.</span><span class="sxs-lookup"><span data-stu-id="34814-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="34814-412">Varsayılan MySQL OMI kimlik doğrulama dosyasını varsayılan bir örnek ve hangi bilgilerin kullanılabilir ve MySQL yapılandırma dosyası buldu hello öğesinden Ayrıştırılan bağlı olarak bir bağlantı noktası numarası içeriyor.</span><span class="sxs-lookup"><span data-stu-id="34814-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="34814-413">Merhaba varsayılan örneği daha kolay bir Linux ana bilgisayarda birden çok MySQL örneklerini yönetme anlamına gelir toomake ve bağlantı noktası 0 ile Merhaba örneği tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="34814-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="34814-414">Tüm ek örneklerini hello varsayılan örneğinden ayarlanan özellikleri devralır.</span><span class="sxs-lookup"><span data-stu-id="34814-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="34814-415">Örneğin, '3308' numaralı bağlantı noktasını dinlemeye MySQL örneği eklediyseniz, hello varsayılan örneğinin bağ adresi, kullanıcı adı ve Base64 ile kodlanmış parola kullanılan tootry olması ve 3308 üzerinde dinleme hello örneği izleme.</span><span class="sxs-lookup"><span data-stu-id="34814-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="34814-416">Bağlanmadıysa tooanother adresi 3308 Hello örneğinde ve kullandığı hello aynı MySQL kullanıcı adı ve parola çiftinin yalnızca hello respecification hello bağ adresi gereklidir ve hello diğer özellikleri devralınır.</span><span class="sxs-lookup"><span data-stu-id="34814-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="34814-417">Merhaba kimlik doğrulama dosyasını örnekleri hello aşağıdakine benzer.</span><span class="sxs-lookup"><span data-stu-id="34814-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="34814-418">Varsayılan örneği ve bağlantı noktası 3308 ile örneği:</span><span class="sxs-lookup"><span data-stu-id="34814-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="34814-419">Varsayılan örneği ve bağlantı noktası 3308 + farklı Base 64 örneğiyle parola kodlanmış:</span><span class="sxs-lookup"><span data-stu-id="34814-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="34814-420">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="34814-420">**Property**</span></span> | <span data-ttu-id="34814-421">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="34814-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="34814-422">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="34814-422">Port</span></span> |<span data-ttu-id="34814-423">Bağlantı noktası hello geçerli bağlantı noktası hello örneğinin dinlediği MySQL temsil eder.</span><span class="sxs-lookup"><span data-stu-id="34814-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="34814-424">başlangıç bağlantı noktası 0 hello özellikler aşağıdaki varsayılan örnek için kullanıldığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="34814-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="34814-425">Bağ adresi</span><span class="sxs-lookup"><span data-stu-id="34814-425">Bind-Address</span></span> |<span data-ttu-id="34814-426">Merhaba bağlamak adresi hello geçerli MySQL bağlama-adresidir</span><span class="sxs-lookup"><span data-stu-id="34814-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="34814-427">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="34814-427">username</span></span> |<span data-ttu-id="34814-428">Bu hello kullanıcı adını hello MySQL toouse toomonitor hello MySQL server örneği istiyor.</span><span class="sxs-lookup"><span data-stu-id="34814-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="34814-429">Parola Base64 ile kodlanmış</span><span class="sxs-lookup"><span data-stu-id="34814-429">Base64 encoded Password</span></span> |<span data-ttu-id="34814-430">Bu hello hello MySQL izleme kullanıcının Base64 ile kodlanmış paroladır.</span><span class="sxs-lookup"><span data-stu-id="34814-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="34814-431">Otomatik güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="34814-431">AutoUpdate</span></span> |<span data-ttu-id="34814-432">Merhaba MySQL OMI sağlayıcı yükseltildiğinde hello sağlayıcısı hello my.cnf dosyasındaki değişiklikleri için yeniden tara ve hello MySQL OMI kimlik doğrulaması dosyanın üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="34814-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="34814-433">Bu bayrak tootrue ya da yanlış gerekli güncelleştirmeleri toohello MySQL OMI bağlı olarak kimlik doğrulama dosyasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="34814-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="34814-434">Kimlik doğrulama dosya konumu</span><span class="sxs-lookup"><span data-stu-id="34814-434">Authentication file location</span></span>
<span data-ttu-id="34814-435">Merhaba MySQL OMI kimlik doğrulaması dosya konumu aşağıdaki hello bulunan ve "auth mysql" adlı:</span><span class="sxs-lookup"><span data-stu-id="34814-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="34814-436">/var/OPT/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth</span><span class="sxs-lookup"><span data-stu-id="34814-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="34814-437">Merhaba dosya (ve kimlik doğrulama/omsagent dizin) hello omsagent kullanıcıya ait.</span><span class="sxs-lookup"><span data-stu-id="34814-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="34814-438">Aracı günlükleri</span><span class="sxs-lookup"><span data-stu-id="34814-438">Agent logs</span></span>
<span data-ttu-id="34814-439">Hello günlükleri hello Linux için OMS aracısı için aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="34814-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="34814-440">/ var/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="34814-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="34814-441">Merhaba günlükleri hello için Linux omsconfig (Aracısı yapılandırması) programı için OMS aracısının altındadır:</span><span class="sxs-lookup"><span data-stu-id="34814-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="34814-442">/ var/opt/microsoft/omsconfig/log /</span><span class="sxs-lookup"><span data-stu-id="34814-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="34814-443">Günlükleri (performans ölçüm verilerini sağlayan) hello OMI ve scx farklı bileşenlerin olduğuna:</span><span class="sxs-lookup"><span data-stu-id="34814-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="34814-444">/ var/opt/OMI/log/ve /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="34814-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="34814-445">Merhaba OMS Aracısı Linux için sorun giderme</span><span class="sxs-lookup"><span data-stu-id="34814-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="34814-446">Sık rastlanan sorunları giderme ve bilgi toodiagnose aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="34814-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="34814-447">Bu bölümdeki bilgiler, sorun giderme hello hiçbiri yardımcı olur, sorununuzu kaynakları toohelp Çöz aşağıdaki hello de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="34814-448">Müşteriler ile Premier Destek aracılığıyla bir destek talebi oturum açabilir [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="34814-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="34814-449">Azure destek anlaşmaları müşterilerle destek olaylarının hello oturum [Azure portalı](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="34814-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="34814-450">Dosya bir [GitHub sorunu](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="34814-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="34814-451">Geri bildirim Forumunda fikirleri ve toocreate bir hata raporu [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="34814-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="34814-452">Önemli günlük konumları</span><span class="sxs-lookup"><span data-stu-id="34814-452">Important log locations</span></span>
| <span data-ttu-id="34814-453">Dosya</span><span class="sxs-lookup"><span data-stu-id="34814-453">File</span></span> | <span data-ttu-id="34814-454">Yol</span><span class="sxs-lookup"><span data-stu-id="34814-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="34814-455">Linux günlük dosyası için OMS Aracısı</span><span class="sxs-lookup"><span data-stu-id="34814-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="34814-456">OMS Aracısı Yapılandırma günlük dosyasını</span><span class="sxs-lookup"><span data-stu-id="34814-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="34814-457">Önemli yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="34814-457">Important configuration files</span></span>
| <span data-ttu-id="34814-458">Catergory</span><span class="sxs-lookup"><span data-stu-id="34814-458">Catergory</span></span> | <span data-ttu-id="34814-459">Dosya konumu</span><span class="sxs-lookup"><span data-stu-id="34814-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="34814-460">Syslog</span><span class="sxs-lookup"><span data-stu-id="34814-460">Syslog</span></span> |<span data-ttu-id="34814-461">`/etc/syslog-ng/syslog-ng.conf`veya `/etc/rsyslog.conf` veya`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="34814-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="34814-462">Performans, Nagios, Zabbix, OMS çıkış ve genel Aracısı</span><span class="sxs-lookup"><span data-stu-id="34814-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="34814-463">Ek yapılandırmalar</span><span class="sxs-lookup"><span data-stu-id="34814-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="34814-464">OMS portalı yapılandırması etkinse, performans sayaçları ve syslog için düzenleme yapılandırma dosyalarının üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="34814-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="34814-465">Merhaba OMS portalı (tüm düğümler) yapılandırmasında devre dışı bırakabilir veya hello aşağıdaki çalıştırarak tek düğümler için:</span><span class="sxs-lookup"><span data-stu-id="34814-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="34814-466">Hata ayıklama günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="34814-466">Enable debug logging</span></span>
<span data-ttu-id="34814-467">tooenable hata ayıklama günlüğü, hello OMS çıkış eklentisi ve ayrıntılı çıktı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34814-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="34814-468">OMS çıkış eklentisi</span><span class="sxs-lookup"><span data-stu-id="34814-468">OMS output plugin</span></span>
<span data-ttu-id="34814-469">FluentD hello eklentisi toospecify girişleri ve çıkışları için farklı günlük düzeyleri için günlüğe kaydetme düzeylerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="34814-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="34814-470">toospecify OMS çıktı için farklı günlük düzeyi Düzenle hello hello genel Aracısı yapılandırmasında `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` dosya.</span><span class="sxs-lookup"><span data-stu-id="34814-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="34814-471">Merhaba yapılandırma dosyası Hello altına hello değiştirme `log_level` özelliğinden `info` çok`debug`.</span><span class="sxs-lookup"><span data-stu-id="34814-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

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

<span data-ttu-id="34814-472">Hata ayıklama günlüğünü OMS hizmetine veri öğeleri ve toosend geçen süre sayısını türüne göre ayrılmış toplu hale toosee karşıya toohello sağlar.</span><span class="sxs-lookup"><span data-stu-id="34814-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="34814-473">*Örnek etkin hata ayıklama günlüğü:*</span><span class="sxs-lookup"><span data-stu-id="34814-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="34814-474">Ayrıntılı çıktı</span><span class="sxs-lookup"><span data-stu-id="34814-474">Verbose output</span></span>
<span data-ttu-id="34814-475">Merhaba OMS çıkış eklentisini kullanmak yerine, ayrıca veri öğeleri doğrudan çok çıkarabilirsiniz`stdout`, olduğu hello OMS Aracısı Linux günlük dosyası için görünür.</span><span class="sxs-lookup"><span data-stu-id="34814-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="34814-476">Hello OMS genel Aracısı Yapılandırma dosyasındaki `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, yorum kullanıma hello OMS çıktı eklentisi ekleyerek bir `#` her satırın önünde.</span><span class="sxs-lookup"><span data-stu-id="34814-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

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

<span data-ttu-id="34814-477">Aşağıdaki çıkış eklentisi Merhaba, hello yorum hello kaldırarak bölümü aşağıdaki hello kaldırmak `#` hello her satırın başındaki simgesi.</span><span class="sxs-lookup"><span data-stu-id="34814-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="34814-478">İletilen Syslog iletileri hello günlüğüne görünmez</span><span class="sxs-lookup"><span data-stu-id="34814-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="34814-479">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="34814-479">Probable causes</span></span>
* <span data-ttu-id="34814-480">Merhaba uygulanan yapılandırma toohello Linux sunucusu değil gönderilen hello olanaklarının toplanmasına izin vermek ve/veya düzeyleri oturum</span><span class="sxs-lookup"><span data-stu-id="34814-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="34814-481">Syslog doğru toohello Linux sunucusuna iletilmez değil</span><span class="sxs-lookup"><span data-stu-id="34814-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="34814-482">saniye başına iletilen iletilerinin Hello sayısı Linux toohandle için OMS aracısının hello hello temel yapılandırması için çok büyük</span><span class="sxs-lookup"><span data-stu-id="34814-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="34814-483">Çözümler</span><span class="sxs-lookup"><span data-stu-id="34814-483">Resolutions</span></span>
* <span data-ttu-id="34814-484">Syslog tüm hello tesis ve hello doğru günlük düzeyleri için hello OMS portalı o hello yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="34814-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="34814-485">**OMS portalı > ayarları > veri > Syslog**</span><span class="sxs-lookup"><span data-stu-id="34814-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="34814-486">Bu yerel syslog arka plan programları Mesajlaşma doğrulayın (`rsyslog`, `syslog-ng`) mümkün tooreceive iletilen Merhaba iletileri olan</span><span class="sxs-lookup"><span data-stu-id="34814-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="34814-487">İletileri engellenmediğinden hello Syslog sunucusu tooensure üzerinde güvenlik duvarı ayarlarını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="34814-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="34814-488">Hello kullanarak Syslog iletisi tooOMS benzetimini `logger` command - örneğin:</span><span class="sxs-lookup"><span data-stu-id="34814-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="34814-489">Bir proxy kullanılırken tooOMS bağlantısı sorunları</span><span class="sxs-lookup"><span data-stu-id="34814-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="34814-490">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="34814-490">Probable causes</span></span>
* <span data-ttu-id="34814-491">Yükleme ve yapılandırma hello Aracısı yanlış olduğunda Hello proxy belirtildi</span><span class="sxs-lookup"><span data-stu-id="34814-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="34814-492">Merhaba OMS hizmet uç noktaları, veri merkezinizdeki whitelistested değildir</span><span class="sxs-lookup"><span data-stu-id="34814-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="34814-493">Çözümler</span><span class="sxs-lookup"><span data-stu-id="34814-493">Resolutions</span></span>
* <span data-ttu-id="34814-494">Merhaba seçeneğiyle komut aşağıdaki hello kullanarak Linux için Hello OMS aracısı yeniden `-v` etkin.</span><span class="sxs-lookup"><span data-stu-id="34814-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="34814-495">Bu ayrıntılı çıktı hello proxy toohello OMS hizmeti bağlanma hello Aracısı'nın sağlar.</span><span class="sxs-lookup"><span data-stu-id="34814-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="34814-496">OMS proxy için hello belgelerini gözden [bir HTTP proxy sunucusu ile kullanmak için yapılandırma hello Aracısı](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="34814-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="34814-497">OMS hizmet uç noktaları aşağıdaki o hello Güvenilenler listesine doğrulayın</span><span class="sxs-lookup"><span data-stu-id="34814-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="34814-498">Aracı Kaynağı</span><span class="sxs-lookup"><span data-stu-id="34814-498">Agent Resource</span></span> | <span data-ttu-id="34814-499">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="34814-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="34814-500">&#42;. ods.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="34814-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="34814-501">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="34814-501">Port 443</span></span> |
| <span data-ttu-id="34814-502">&#42;. OMS.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="34814-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="34814-503">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="34814-503">Port 443</span></span> |
| <span data-ttu-id="34814-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="34814-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="34814-505">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="34814-505">Port 443</span></span> |
| <span data-ttu-id="34814-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="34814-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="34814-507">Bağlantı noktası 443</span><span class="sxs-lookup"><span data-stu-id="34814-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="34814-508">Bir 403 hatası görüntülenir, ekleme</span><span class="sxs-lookup"><span data-stu-id="34814-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="34814-509">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="34814-509">Probable causes</span></span>
* <span data-ttu-id="34814-510">Başlangıç tarihi ve saati Linux sunucusu üzerinde yanlış</span><span class="sxs-lookup"><span data-stu-id="34814-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="34814-511">Merhaba çalışma alanı kimliği ve çalışma alanı anahtarı yanlış</span><span class="sxs-lookup"><span data-stu-id="34814-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="34814-512">Çözüm</span><span class="sxs-lookup"><span data-stu-id="34814-512">Resolution</span></span>
* <span data-ttu-id="34814-513">Linux sunucunuzla hello Hello zamanında doğrulayın `date` komutu.</span><span class="sxs-lookup"><span data-stu-id="34814-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="34814-514">Merhaba veri değerinden daha büyük ya da 15 dakikadan kısa geçerli saati hello sonra ekleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="34814-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="34814-515">toocorrect Bu, başlangıç tarihi ve/veya saat dilimi Linux sunucunuzun güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="34814-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="34814-516">bir zaman farkı ekleme hatasına neden oluyorsa hello Linux için OMS aracısının en son sürümünü hello sizi bilgilendirir</span><span class="sxs-lookup"><span data-stu-id="34814-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="34814-517">RE yerleşik kullanarak doğru çalışma alanı kimliği ve çalışma alanı anahtarı hello.</span><span class="sxs-lookup"><span data-stu-id="34814-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="34814-518">Bkz: [hello komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="34814-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="34814-519">500 hata veya 404 hatası hello günlük dosyasında ekleme sonra görünür.</span><span class="sxs-lookup"><span data-stu-id="34814-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="34814-520">Bu hello bir OMS çalışma alanına Linux verilerin ilk yükleme sırasında oluşan bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="34814-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="34814-521">Bu, gönderilen veriler ya da diğer sorunlar etkilemez.</span><span class="sxs-lookup"><span data-stu-id="34814-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="34814-522">Merhaba hataları ilk defa yoksayabilirsiniz ekleme.</span><span class="sxs-lookup"><span data-stu-id="34814-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="34814-523">Nagios veriler hello OMS portalı görünmüyor</span><span class="sxs-lookup"><span data-stu-id="34814-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="34814-524">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="34814-524">Probable causes</span></span>
* <span data-ttu-id="34814-525">Merhaba omsagent kullanıcının izinleri tooread hello Nagios günlük dosyasından yok</span><span class="sxs-lookup"><span data-stu-id="34814-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="34814-526">Merhaba Nagios kaynak ve filtre bölümleri hello omsagent.conf dosyasında hala bırakılır</span><span class="sxs-lookup"><span data-stu-id="34814-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="34814-527">Çözümler</span><span class="sxs-lookup"><span data-stu-id="34814-527">Resolutions</span></span>
* <span data-ttu-id="34814-528">Merhaba omsagent kullanıcı sipariş tooread hello Nagios dosyasından ekleyin.</span><span class="sxs-lookup"><span data-stu-id="34814-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="34814-529">Bkz: [Nagios uyarıları](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="34814-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="34814-530">İçinde Linux genel yapılandırma dosyasını için OMS aracısının hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, emin **her ikisi de** kaynak ve filtre bölümleri kaldırıldı, Yorumlar sahip Nagios aşağıdaki örneğine benzer toohello hello.</span><span class="sxs-lookup"><span data-stu-id="34814-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="34814-531">Linux veri hello OMS portalı görünmüyor</span><span class="sxs-lookup"><span data-stu-id="34814-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="34814-532">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="34814-532">Probable causes</span></span>
* <span data-ttu-id="34814-533">Onboarding toohello OMS hizmeti başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="34814-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="34814-534">Bağlantı toohello OMS hizmetine engellendi</span><span class="sxs-lookup"><span data-stu-id="34814-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="34814-535">Yedeklenen Hello OMS Aracısı Linux veriler için</span><span class="sxs-lookup"><span data-stu-id="34814-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="34814-536">Çözümler</span><span class="sxs-lookup"><span data-stu-id="34814-536">Resolutions</span></span>
* <span data-ttu-id="34814-537">Bu ekleme toohello OMS hizmetine başarılı oldu, hello doğrulayarak doğrulayın `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="34814-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="34814-538">RE yerleşik kullanarak hello omsadmin.sh komut satırı.</span><span class="sxs-lookup"><span data-stu-id="34814-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="34814-539">Bkz: [hello komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="34814-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="34814-540">Bir proxy sunucu kullanıyorsanız, hello proxy sorun giderme adımlarını yukarıdaki kullanın</span><span class="sxs-lookup"><span data-stu-id="34814-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="34814-541">Merhaba Linux için OMS aracısının hello OMS hizmeti ile iletişim kuramadığında bazı durumlarda, hello aracı üzerindeki yedeklenen toohello tam arabellek boyutu 50 MB verilerdir.</span><span class="sxs-lookup"><span data-stu-id="34814-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="34814-542">Merhaba çalıştırarak Hello OMS Aracısı Linux için yeniden `/opt/microsoft/omsagent/bin/service_control restart` komutu.</span><span class="sxs-lookup"><span data-stu-id="34814-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="34814-543">Aracı sürümü 1.1.0-28 ve daha sonra bu sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="34814-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="34814-544">Syslog Linux performans sayacı yapılandırması hello OMS portalında uygulanmaz</span><span class="sxs-lookup"><span data-stu-id="34814-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="34814-545">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="34814-545">Probable causes</span></span>
* <span data-ttu-id="34814-546">Linux için OMS aracısının hello Hello yapılandırma aracı hello en son yapılandırma hello OMS Portalı'ndan alınmamış.</span><span class="sxs-lookup"><span data-stu-id="34814-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="34814-547">Merhaba hello portalında değiştirilen ayarlar uygulanmadı</span><span class="sxs-lookup"><span data-stu-id="34814-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="34814-548">Çözümler</span><span class="sxs-lookup"><span data-stu-id="34814-548">Resolutions</span></span>
<span data-ttu-id="34814-549">`omsconfig`Merhaba OMS Aracısı Hello yapılandırma aracı her 5 dakikada bir OMS portalı yapılandırma değişiklikleri alır Linux için ' dir.</span><span class="sxs-lookup"><span data-stu-id="34814-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="34814-550">Linux yapılandırma dosyaları için uygulanan toohello OMS Aracısı konumundaki sonra bu yapılandırmadır `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="34814-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="34814-551">Bazı durumlarda mümkün toocommunicate uygulanmıyor son yapılandırmasında kaynaklanan hello portal Yapılandırma hizmeti ile Merhaba OMS Aracısı Linux yapılandırma aracı için olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="34814-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="34814-552">Bu hello doğrulayın `omsconfig` aracısının hello aşağıdakilerle yüklü:</span><span class="sxs-lookup"><span data-stu-id="34814-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="34814-553">`dpkg --list omsconfig` veya `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="34814-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="34814-554">Yüklü değilse, Linux için hello hello OMS aracısının en son sürümünü yeniden yükleyin</span><span class="sxs-lookup"><span data-stu-id="34814-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="34814-555">Bu hello doğrulayın `omsconfig` aracı hello OMS hizmeti ile iletişim</span><span class="sxs-lookup"><span data-stu-id="34814-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="34814-556">Merhaba çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` komutu</span><span class="sxs-lookup"><span data-stu-id="34814-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="34814-557">Merhaba yukarıdaki komutu hello yapılandırmasını bu aracı döndürür Syslog ayarları, Linux performans sayaçları ve özel günlükleri gibi hello Portalı'ndan alır.</span><span class="sxs-lookup"><span data-stu-id="34814-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="34814-558">Yukarıdaki Hello komutu başarısız olursa, hello çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` komutu.</span><span class="sxs-lookup"><span data-stu-id="34814-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="34814-559">Bu komut hello omsconfig Aracısı toocommunicate hello OMS hizmet tooretrieve hello en son yapılandırmayla zorlar.</span><span class="sxs-lookup"><span data-stu-id="34814-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="34814-560">Özel Linux günlük verilerini hello OMS portalı görünmüyor</span><span class="sxs-lookup"><span data-stu-id="34814-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="34814-561">Olası nedenler</span><span class="sxs-lookup"><span data-stu-id="34814-561">Probable causes</span></span>
* <span data-ttu-id="34814-562">Hizmet Onboarding tooOMS başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="34814-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="34814-563">Merhaba **yapılandırma toomy Linux sunucuları aşağıdaki Uygula hello** ayarı seçilmediğinden</span><span class="sxs-lookup"><span data-stu-id="34814-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="34814-564">omsconfig hello son özel günlük hello portalından yukarı çekilen değil</span><span class="sxs-lookup"><span data-stu-id="34814-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="34814-565">Merhaba `omsagent` kullanılmasıdır oluşturulamıyor tooaccess hello özel günlük tooa izinlerle ilgili bir sorun nedeniyle veya `omsagent` bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="34814-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="34814-566">Bu durumda, çıktı aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="34814-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="34814-567">Bu hello hello OMS Aracısı Linux sürüm 1.1.0-217 için düzeltildi yarış durumu ile ilgili bilinen bir sorun olduğu</span><span class="sxs-lookup"><span data-stu-id="34814-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="34814-568">Çözümler</span><span class="sxs-lookup"><span data-stu-id="34814-568">Resolutions</span></span>
* <span data-ttu-id="34814-569">Merhaba olup olmadığını belirleme, edildi başarıyla olduğunuz doğrulayın `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` dosya yok.</span><span class="sxs-lookup"><span data-stu-id="34814-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="34814-570">Gerekli olduğunda, yerleşik yeniden hello omsadmin.sh komut satırını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="34814-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="34814-571">Bkz: [hello komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="34814-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="34814-572">Merhaba altında OMS portalı içinde **ayarları** hello üzerinde **veri** sekmesinde, bu hello olun **yapılandırma toomy Linux sunucuları aşağıdaki Uygula hello** ayarı seçildiğinde</span><span class="sxs-lookup"><span data-stu-id="34814-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="34814-573">![yapılandırmasını Uygula](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="34814-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="34814-574">Bu hello doğrulayın `omsconfig` aracı hello OMS hizmeti ile iletişim</span><span class="sxs-lookup"><span data-stu-id="34814-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="34814-575">Merhaba çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` komutu</span><span class="sxs-lookup"><span data-stu-id="34814-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="34814-576">Merhaba yukarıdaki komutu hello yapılandırmasını bu aracı döndürür hello Syslog ayarları, Linux performans sayaçları ve özel günlükleri de dahil olmak üzere Portalı'ndan alır</span><span class="sxs-lookup"><span data-stu-id="34814-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="34814-577">Yukarıdaki Hello komutu başarısız olursa, hello çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` komutu.</span><span class="sxs-lookup"><span data-stu-id="34814-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="34814-578">Bu komut, OMS hizmeti ile Merhaba omsconfig Aracısı toocommunicate zorlar ve hello en son yapılandırmayı almak.</span><span class="sxs-lookup"><span data-stu-id="34814-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="34814-579">Ayrıcalıklı bir kullanıcı olarak çalışan Linux kullanıcı için OMS aracısının hello yerine `root`, hello Linux çalıştıran için OMS aracısının hello `omsagent` kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="34814-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="34814-580">Çoğu durumda, açık izni olmalıdır belirli dosyaları sipariş tooread toohello kullanıcı izni.</span><span class="sxs-lookup"><span data-stu-id="34814-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="34814-581">toogrant izni çok`omsagent` kullanıcı, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="34814-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="34814-582">Merhaba eklemek `omsagent` kullanıcı tooa belirli grubuyla`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="34814-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="34814-583">Evrensel okuma erişimi toohello gerekli dosyasıyla verin`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="34814-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="34814-584">Merhaba hello OMS Aracısı Linux sürüm 1.1.0-217 için düzeltildi yarış durumu ile ilgili bilinen bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="34814-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="34814-585">Toohello son aracısını güncelleştirdikten sonra komut tooget hello en son sürümünü hello çıkış eklentisi aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="34814-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="34814-586">Bilinen sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="34814-586">Known limitations</span></span>
<span data-ttu-id="34814-587">Aşağıdaki bölümlerde toolearn Linux hello OMS Aracısı, geçerli sınırlamalar hakkında hello gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="34814-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="34814-588">Azure Tanılama</span><span class="sxs-lookup"><span data-stu-id="34814-588">Azure Diagnostics</span></span>
<span data-ttu-id="34814-589">Azure'da çalışan Linux sanal makineleri için ek adımlar gerekli tooallow veri toplama işlemi Azure tanılama ve Operations Management Suite tarafından olabilir.</span><span class="sxs-lookup"><span data-stu-id="34814-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="34814-590">**Sürüm 2.2** Merhaba hello Linux için OMS Aracısı ile uyumluluk için tanılama uzantısını Linux için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="34814-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="34814-591">Yükleme ve Linux için hello tanılama uzantısını yapılandırma hakkında daha fazla bilgi için bkz: [hello Azure CLI komutu tooenable Linux tanılama uzantısını kullanmak](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="34814-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="34814-592">**Merhaba Linux tanılama uzantısını 2.0 too2.2 Azure CLI ASM yükseltme:**</span><span class="sxs-lookup"><span data-stu-id="34814-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="34814-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="34814-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="34814-594">Bu komut örnekleri PrivateConfig.json adlı bir dosyaya başvuru.</span><span class="sxs-lookup"><span data-stu-id="34814-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="34814-595">Bu dosya biçiminin Hello örnek aşağıdaki hello benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="34814-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="34814-596">Sysklog desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="34814-596">Sysklog is not supported</span></span>
<span data-ttu-id="34814-597">Rsyslog veya syslog ng gerekli toocollect syslog iletileri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="34814-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="34814-598">Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü Hello varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="34814-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="34814-599">Bu sürümü bu dağıtımları toocollect syslog verileri hello rsyslog arka plan programı yüklenmelidir ve tooreplace sysklog yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="34814-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="34814-600">Sysklog rsyslog ile değiştirerek daha fazla bilgi için bkz: [yeni yerleşik hello rsyslog RPM yüklemek](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="34814-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34814-601">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="34814-601">Next Steps</span></span>
* <span data-ttu-id="34814-602">[Günlük analizi çözümleri Çözümleri Galerisi hello eklemek](log-analytics-add-solutions.md) tooadd işlevselliği ve toplama verileri.</span><span class="sxs-lookup"><span data-stu-id="34814-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="34814-603">İle tanışın [oturum aramaları](log-analytics-log-searches.md) tooview ayrıntılı çözümler tarafından toplanan bilgiler.</span><span class="sxs-lookup"><span data-stu-id="34814-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="34814-604">Kullanım [panolar](log-analytics-dashboards.md) toosave ve görüntü kendi özel arar.</span><span class="sxs-lookup"><span data-stu-id="34814-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
