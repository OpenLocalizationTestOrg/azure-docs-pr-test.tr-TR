---
title: "Günlük analizi veri çözümde aaaWire | Microsoft Docs"
description: "Kablo verileri birleştirilmiş ağ ve performans OMS aracısının, Operations Manager ve Windows bağlı aracılar dahil olmak üzere bilgisayar verilerdir. Ağ verileri birlikte, günlük veri toohelp ile verilerin bağıntısını."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="c0f98-104">Kablo verileri 2.0 (Önizleme) çözümüne günlük analizi</span><span class="sxs-lookup"><span data-stu-id="c0f98-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Kablo verileri simgesi](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="c0f98-106">Kablo verileri Operations Manager, Windows bağlı dahil olmak üzere, OMS aracılarla ve Linux aracılarını bilgisayarlardan birleştirilmiş ağ ve performans verilerini ' dir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="c0f98-107">Ağ verileri birlikte, diğer günlük veri toohelp ile verilerin bağıntısını.</span><span class="sxs-lookup"><span data-stu-id="c0f98-107">Network data is combined with your other log data toohelp you correlate data.</span></span>

<span data-ttu-id="c0f98-108">Ayrıca tooOMS aracıları hello kablo verileri çözüm BT altyapınızın bilgisayarlara yüklemek Microsoft Dependency aracıları kullanır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-108">In addition tooOMS agents, hello Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="c0f98-109">Bağımlılık aracıları İzleyici ağ gönderilen veriler tooand ağ için bilgisayarlardan düzeyleri 2-3 içinde hello [OSI modeli](https://en.wikipedia.org/wiki/OSI_model), da dahil olmak üzere hello çeşitli protokoller ve bağlantı noktaları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-109">Dependency Agents monitor network data sent tooand from your computers for network levels 2-3 in hello [OSI model](https://en.wikipedia.org/wiki/OSI_model), including hello various protocols and ports used.</span></span> <span data-ttu-id="c0f98-110">Veri tooLog Analytics sonra gönderilen aracıları kullanma.</span><span class="sxs-lookup"><span data-stu-id="c0f98-110">Data is then sent tooLog Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="c0f98-111">Merhaba kablo verileri çözüm toonew çalışma alanları önceki sürümü hello ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-111">You cannot add hello previous version of hello Wire Data solution toonew workspaces.</span></span> <span data-ttu-id="c0f98-112">Etkin hello özgün kablo verileri çözüm varsa, toouse devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-112">If you have hello original Wire Data solution enabled, you can continue toouse it.</span></span> <span data-ttu-id="c0f98-113">Ancak, toouse kablo verileri 2.0, önce kaldırmalısınız hello özgün sürümü.</span><span class="sxs-lookup"><span data-stu-id="c0f98-113">However, toouse Wire Data 2.0, you must first remove hello original version.</span></span>

<span data-ttu-id="c0f98-114">Varsayılan olarak, günlük analizi günlüğe kaydedilen veri CPU, bellek, disk ve ağ performans verileri için yerleşik sayaçları toplar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="c0f98-115">Ağ ve diğer veri toplama gerçekleştirilir gerçek zamanlı alt ağları ve hello bilgisayar tarafından kullanılan uygulama düzeyi protokolleri de dahil olmak üzere her bir aracının için.</span><span class="sxs-lookup"><span data-stu-id="c0f98-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by hello computer.</span></span> <span data-ttu-id="c0f98-116">Merhaba günlükleri sekmesinde hello Ayarları sayfasında diğer performans sayaçları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-116">You can add other performance counters on hello Settings page on hello Logs tab.</span></span>

<span data-ttu-id="c0f98-117">Kullandıysanız [sFlow](http://www.sflow.org/) veya diğer yazılımlarla [Cisco'nın NetFlow Protokolü](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html)istatistikleri hello ve kablo verileri gördüğünüz veri tanıdık tooyou olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then hello statistics and data you see from wire data will be familiar tooyou.</span></span>

<span data-ttu-id="c0f98-118">Yerleşik günlük arama sorguları hello türlerini bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c0f98-118">Some of hello types of built-in Log search queries include:</span></span>

- <span data-ttu-id="c0f98-119">Kablo verileri sağlayan aracılar</span><span class="sxs-lookup"><span data-stu-id="c0f98-119">Agents that provide wire data</span></span>
- <span data-ttu-id="c0f98-120">Kablo verileri sağlayan aracıların IP adresi</span><span class="sxs-lookup"><span data-stu-id="c0f98-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="c0f98-121">IP adresleriyle giden iletişimler</span><span class="sxs-lookup"><span data-stu-id="c0f98-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="c0f98-122">Uygulama protokolleri tarafından gönderilen bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="c0f98-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="c0f98-123">Bir uygulama hizmeti tarafından gönderilen bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="c0f98-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="c0f98-124">Farklı protokoller tarafından alınan bayt</span><span class="sxs-lookup"><span data-stu-id="c0f98-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="c0f98-125">Gönderilen ve IP sürümü tarafından alınan toplam bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="c0f98-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="c0f98-126">Güvenilir bir şekilde ölçülen bağlantıları için ortalama gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="c0f98-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="c0f98-127">Bilgisayar başlatan veya alan ağ trafiğinin işler</span><span class="sxs-lookup"><span data-stu-id="c0f98-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="c0f98-128">Bir işlem için ağ trafiği miktarı</span><span class="sxs-lookup"><span data-stu-id="c0f98-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="c0f98-129">Kablo verileri kullanarak aradığınızda, filtre uygulayabilirsiniz ve Grup veri tooview bilgilerini hello üst aracıları ve üst protokoller.</span><span class="sxs-lookup"><span data-stu-id="c0f98-129">When you search using wire data, you can filter and group data tooview information about hello top agents and top protocols.</span></span> <span data-ttu-id="c0f98-130">Veya ne zaman görüntüleyebilirsiniz birbirleri ile nasıl için uzun iletilen belirli bilgisayarlara (IP adresleri/MAC adresleri) ve ne kadar veri gönderildiği — temel olarak, arama tabanlı ağ trafiğiyle ilgili meta verileri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="c0f98-131">Meta verileri görüntülediğiniz olduğundan, ancak bunu ayrıntılı sorun giderme için mutlaka kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="c0f98-132">Günlük analizi kablo verileri ağ verilerin tam bir yakalama değil.</span><span class="sxs-lookup"><span data-stu-id="c0f98-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="c0f98-133">Bu nedenle, paket düzeyinde ayrıntılı sorun giderme için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="c0f98-134">Merhaba Aracısı kullanmanın avantajı Merhaba, tooother koleksiyon yöntemleri karşılaştırıldığında, yok tooinstall gereçlerine sahip, ağ anahtarlarını yeniden yapılandırma ya da karmaşık yapılandırmalar yeniden olduğunu.</span><span class="sxs-lookup"><span data-stu-id="c0f98-134">hello advantage of using hello agent, compared tooother collection methods, is that you don't have tooinstall appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="c0f98-135">Kablo verileri yalnızca Aracısı tabanlı — hello Aracısı bir bilgisayara yükleyin ve kendi ağ trafiğini izlemek.</span><span class="sxs-lookup"><span data-stu-id="c0f98-135">Wire data is simply agent-based—you install hello agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="c0f98-136">Başka bir avantajı, bulut sağlayıcılarının veya barındırma hizmeti sağlayıcısı veya hello kullanıcı hello doku katman burada sahip değil, Microsoft Azure çalışan toomonitor iş yükleri istediğiniz durumdur.</span><span class="sxs-lookup"><span data-stu-id="c0f98-136">Another advantage is when you want toomonitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where hello user doesn't own hello fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="c0f98-137">Bağlı kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c0f98-137">Connected sources</span></span>

<span data-ttu-id="c0f98-138">Kablo verileri hello Microsoft bağımlılık Aracısı ' verileri alır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-138">Wire Data gets its data from hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="c0f98-139">Merhaba bağımlılık Aracısı hello OMS aracısı için kendi bağlantıları tooLog Analytics bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-139">hello Dependency Agent depends on hello OMS Agent for its connections tooLog Analytics.</span></span> <span data-ttu-id="c0f98-140">Bu, bir sunucu OMS Aracısı yüklenir ve ilk yapılandırılmış hello olması gerekir ve ardından hello bağımlılık aracısı yükleyin anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-140">This means that a server must have hello OMS Agent installed and configured first, and then you install hello Dependency Agent.</span></span> <span data-ttu-id="c0f98-141">Merhaba aşağıdaki tabloda hello kablo verileri çözümünü destekler hello bağlı kaynakları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-141">hello following table describes hello connected sources that hello Wire Data solution supports.</span></span>

| <span data-ttu-id="c0f98-142">**Bağlı kaynak**</span><span class="sxs-lookup"><span data-stu-id="c0f98-142">**Connected source**</span></span> | <span data-ttu-id="c0f98-143">**Destekleniyor**</span><span class="sxs-lookup"><span data-stu-id="c0f98-143">**Supported**</span></span> | <span data-ttu-id="c0f98-144">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c0f98-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0f98-145">Windows aracıları</span><span class="sxs-lookup"><span data-stu-id="c0f98-145">Windows agents</span></span> | <span data-ttu-id="c0f98-146">Evet</span><span class="sxs-lookup"><span data-stu-id="c0f98-146">Yes</span></span> | <span data-ttu-id="c0f98-147">Kablo verileri analiz eder ve Windows Aracısı bilgisayarlardan verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="c0f98-148">Toplama toohello içinde [OMS Aracısı](log-analytics-windows-agents.md), Windows aracıları hello Microsoft bağımlılık Aracısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-148">In addition toohello [OMS Agent](log-analytics-windows-agents.md), Windows agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="c0f98-149">Merhaba bkz [desteklenen işletim sistemleri](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) işletim sistemi sürümleri tam bir listesi.</span><span class="sxs-lookup"><span data-stu-id="c0f98-149">See hello [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="c0f98-150">Linux aracıları</span><span class="sxs-lookup"><span data-stu-id="c0f98-150">Linux agents</span></span> | <span data-ttu-id="c0f98-151">Evet</span><span class="sxs-lookup"><span data-stu-id="c0f98-151">Yes</span></span> | <span data-ttu-id="c0f98-152">Kablo verileri analiz eder ve Linux Aracısı bilgisayarlardan verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="c0f98-153">Toplama toohello içinde [OMS Aracısı](log-analytics-linux-agents.md), Linux aracılarını hello Microsoft bağımlılık Aracısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-153">In addition toohello [OMS Agent](log-analytics-linux-agents.md), Linux agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="c0f98-154">Merhaba bkz [desteklenen işletim sistemleri](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) işletim sistemi sürümleri tam bir listesi.</span><span class="sxs-lookup"><span data-stu-id="c0f98-154">See hello [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="c0f98-155">System Center Operations Manager yönetim grubu</span><span class="sxs-lookup"><span data-stu-id="c0f98-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="c0f98-156">Evet</span><span class="sxs-lookup"><span data-stu-id="c0f98-156">Yes</span></span> | <span data-ttu-id="c0f98-157">Kablo verileri analiz eder ve Windows ve Linux aracıları bağlı bir veri toplar [System Center Operations Manager yönetim grubu](log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="c0f98-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="c0f98-158">Merhaba System Center Operations Manager Aracısı bilgisayar tooLog arasında doğrudan bağlantı Analytics gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-158">A direct connection from hello System Center Operations Manager agent computer tooLog Analytics is required.</span></span> <span data-ttu-id="c0f98-159">Veri hello yönetim grubu tooLog Analytics iletilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-159">Data is forwarded from hello management group tooLog Analytics.</span></span> |
| <span data-ttu-id="c0f98-160">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="c0f98-160">Azure storage account</span></span> | <span data-ttu-id="c0f98-161">Hayır</span><span class="sxs-lookup"><span data-stu-id="c0f98-161">No</span></span> | <span data-ttu-id="c0f98-162">Hiçbir verilerden gelir kablo verileri Azure depolama biriminden toocollect Aracısı bilgisayarlardan verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-162">Wire Data collects data from agent computers, so there is no data from it toocollect from Azure Storage.</span></span> |

<span data-ttu-id="c0f98-163">Windows hello Microsoft İzleme Aracısı'nı (MMA) hem System Center Operations Manager hem de günlük analizi toogather tarafından kullanılır ve verileri gönder.</span><span class="sxs-lookup"><span data-stu-id="c0f98-163">On Windows, hello Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics toogather and send data.</span></span> <span data-ttu-id="c0f98-164">Merhaba bağlamı bağlı olarak, hello Aracısı hello System Center Operations Manager Aracısı, OMS Aracısı, günlük analizi Aracısı, MMA veya doğrudan aracı adı verilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-164">Depending on hello context, hello agent is called hello System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="c0f98-165">System Center Operations Manager ve günlük analizi hello MMA biraz farklı sürümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-165">System Center Operations Manager and Log Analytics provide slightly different versions of hello MMA.</span></span> <span data-ttu-id="c0f98-166">Bu sürümleri her tooSystem Center Operations Manager, tooLog Analytics veya tooboth bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-166">These versions can each report tooSystem Center Operations Manager, tooLog Analytics, or tooboth.</span></span>

<span data-ttu-id="c0f98-167">Linux üzerinde hello Linux için OMS aracısının toplar ve veri tooLog Analytics gönderir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-167">On Linux, hello OMS Agent for Linux gathers and sends data tooLog Analytics.</span></span> <span data-ttu-id="c0f98-168">Kablo verileri OMS doğrudan aracılarıyla sunucularda veya System Center Operations Manager Yönetim grupları aracılığıyla ekli tooLog Analytics olan sunucular kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached tooLog Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="c0f98-169">Bu makalede, tooall aracıları olup başvuran Linux veya Windows, bağlı tooa System Center Operations Manager yönetim grubu veya doğrudan tooLog Analytics ifade olup olmadığını hello _OMS Aracısı_.</span><span class="sxs-lookup"><span data-stu-id="c0f98-169">In this article, references tooall agents, whether Linux or Windows, whether connected tooa System Center Operations Manager management group or directly tooLog Analytics are termed hello _OMS agent_.</span></span> <span data-ttu-id="c0f98-170">Bağlam için yalnızca gerekli ise hello belirli dağıtım adı hello Aracısı'nın kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c0f98-170">We'll use hello specific deployment name of hello agent only if it's needed for context.</span></span>

<span data-ttu-id="c0f98-171">Merhaba bağımlılık Aracısı tüm verileri aktarmaz ve herhangi bir değişiklik toofirewalls veya bağlantı noktalarını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="c0f98-171">hello Dependency Agent does not transmit any data itself, and it does not require any changes toofirewalls or ports.</span></span> <span data-ttu-id="c0f98-172">Kablo verileri Hello verileri her zaman hello OMS Aracısı tooLog Analytics, ya da doğrudan aktarılan veya hello OMS ağ geçidi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c0f98-172">hello data in Wire Data is always transmitted by hello OMS agent tooLog Analytics, either directly or using hello OMS Gateway.</span></span>

![Aracı diyagramı](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="c0f98-174">Bir yönetim grubu bağlı tooLog Analytics System Center Operations Manager kullanıcıyla varsa:</span><span class="sxs-lookup"><span data-stu-id="c0f98-174">If you are a System Center Operations Manager user with a management group connected tooLog Analytics:</span></span>

- <span data-ttu-id="c0f98-175">System Center Operations Manager aracıları hello Internet tooconnect tooLog Analytics erişebiliyorsa ek yapılandırma gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-175">No additional configuration is required when your System Center Operations Manager agents can access hello Internet tooconnect tooLog Analytics.</span></span>
- <span data-ttu-id="c0f98-176">System Center Operations Manager aracıları hello Internet günlük analizi erişemediğinde tooconfigure hello OMS ağ geçidi toowork System Center Operations Manager ile gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-176">You need tooconfigure hello OMS Gateway toowork with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over hello Internet.</span></span>

<span data-ttu-id="c0f98-177">Merhaba doğrudan aracı kullanıyorsanız, tooconnect tooLog Analytics veya tooyour OMS ağ geçidi tooconfigure hello OMS Aracısı kendisini gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-177">If you are using hello Direct Agent, you need tooconfigure hello OMS agent itself tooconnect tooLog Analytics or tooyour OMS Gateway.</span></span> <span data-ttu-id="c0f98-178">Merhaba OMS ağ geçidi hello indirebilirsiniz [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span><span class="sxs-lookup"><span data-stu-id="c0f98-178">You can download hello OMS Gateway from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0f98-179">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c0f98-179">Prerequisites</span></span>

- <span data-ttu-id="c0f98-180">Merhaba gerektirir [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) çözümü sunar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-180">Requires hello [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="c0f98-181">Hello hello kablo verileri çözüm önceki sürümünü kullanıyorsanız, önce onu kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-181">If you're using hello previous version of hello Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="c0f98-182">Ancak, hello özgün kablo verileri çözüm yakalanan tüm veriler kablo verileri 2.0 ve günlük arama hala mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="c0f98-182">However, all data captured through hello original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="c0f98-183">Yönetici ayrıcalıkları gerekli tooinstall ya da hello bağımlılık Aracısı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-183">Administrator privileges are required tooinstall or uninstall hello Dependency Agent.</span></span>
- <span data-ttu-id="c0f98-184">Merhaba bağımlılık Aracısı, bir 64-bit işletim sistemine sahip bir bilgisayara yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-184">hello Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="c0f98-185">İşletim sistemleri</span><span class="sxs-lookup"><span data-stu-id="c0f98-185">Operating systems</span></span>

<span data-ttu-id="c0f98-186">Merhaba aşağıdaki bölümlerde hello bağımlılık aracısı için hello desteklenen işletim sistemleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-186">hello following sections list hello supported operating systems for hello Dependency Agent.</span></span> <span data-ttu-id="c0f98-187">Kablo verileri 32-bit mimariler için herhangi bir işletim sistemini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="c0f98-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="c0f98-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="c0f98-188">Windows Server</span></span>

- <span data-ttu-id="c0f98-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c0f98-189">Windows Server 2016</span></span>
- <span data-ttu-id="c0f98-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c0f98-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="c0f98-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c0f98-191">Windows Server 2012</span></span>
- <span data-ttu-id="c0f98-192">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="c0f98-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="c0f98-193">Windows masaüstü</span><span class="sxs-lookup"><span data-stu-id="c0f98-193">Windows desktop</span></span>

- <span data-ttu-id="c0f98-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c0f98-194">Windows 10</span></span>
- <span data-ttu-id="c0f98-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c0f98-195">Windows 8.1</span></span>
- <span data-ttu-id="c0f98-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="c0f98-196">Windows 8</span></span>
- <span data-ttu-id="c0f98-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c0f98-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="c0f98-198">Red Hat Enterprise Linux, CentOS Linux ve Oracle Linux (ile RHEL çekirdek)</span><span class="sxs-lookup"><span data-stu-id="c0f98-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="c0f98-199">Yalnızca varsayılan ve SMP Linux çekirdek sürümleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="c0f98-200">PAE ve Xen, desteklenmez için tüm Linux dağıtım gibi standart olmayan çekirdek serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="c0f98-201">Örneğin, bir sistem hello sürüm dizesi ile _2.6.16.21-0.8-xen_ desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c0f98-201">For example, a system with hello release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="c0f98-202">Standart çekirdekleri yeniden derlemelerinin dahil olmak üzere özel çekirdekleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="c0f98-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="c0f98-203">CentOSPlus çekirdek desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c0f98-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="c0f98-204">Oracle kesilemeyen kurumsal çekirdek (UEK), bu makalenin sonraki bölümlerde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="c0f98-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="c0f98-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="c0f98-206">**İşletim sistemi sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-206">**OS version**</span></span> | <span data-ttu-id="c0f98-207">**Çekirdek sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-208">7.0</span><span class="sxs-lookup"><span data-stu-id="c0f98-208">7.0</span></span> | <span data-ttu-id="c0f98-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="c0f98-209">3.10.0-123</span></span> |
| <span data-ttu-id="c0f98-210">7.1</span><span class="sxs-lookup"><span data-stu-id="c0f98-210">7.1</span></span> | <span data-ttu-id="c0f98-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="c0f98-211">3.10.0-229</span></span> |
| <span data-ttu-id="c0f98-212">7.2</span><span class="sxs-lookup"><span data-stu-id="c0f98-212">7.2</span></span> | <span data-ttu-id="c0f98-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="c0f98-213">3.10.0-327</span></span> |
| <span data-ttu-id="c0f98-214">7.3</span><span class="sxs-lookup"><span data-stu-id="c0f98-214">7.3</span></span> | <span data-ttu-id="c0f98-215">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="c0f98-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="c0f98-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="c0f98-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="c0f98-217">**İşletim sistemi sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-217">**OS version**</span></span> | <span data-ttu-id="c0f98-218">**Çekirdek sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-219">6.0</span><span class="sxs-lookup"><span data-stu-id="c0f98-219">6.0</span></span> | <span data-ttu-id="c0f98-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="c0f98-220">2.6.32-71</span></span> |
| <span data-ttu-id="c0f98-221">6.1</span><span class="sxs-lookup"><span data-stu-id="c0f98-221">6.1</span></span> | <span data-ttu-id="c0f98-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="c0f98-222">2.6.32-131</span></span> |
| <span data-ttu-id="c0f98-223">6.2</span><span class="sxs-lookup"><span data-stu-id="c0f98-223">6.2</span></span> | <span data-ttu-id="c0f98-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="c0f98-224">2.6.32-220</span></span> |
| <span data-ttu-id="c0f98-225">6.3</span><span class="sxs-lookup"><span data-stu-id="c0f98-225">6.3</span></span> | <span data-ttu-id="c0f98-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="c0f98-226">2.6.32-279</span></span> |
| <span data-ttu-id="c0f98-227">6.4</span><span class="sxs-lookup"><span data-stu-id="c0f98-227">6.4</span></span> | <span data-ttu-id="c0f98-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="c0f98-228">2.6.32-358</span></span> |
| <span data-ttu-id="c0f98-229">6.5</span><span class="sxs-lookup"><span data-stu-id="c0f98-229">6.5</span></span> | <span data-ttu-id="c0f98-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="c0f98-230">2.6.32-431</span></span> |
| <span data-ttu-id="c0f98-231">6.6</span><span class="sxs-lookup"><span data-stu-id="c0f98-231">6.6</span></span> | <span data-ttu-id="c0f98-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="c0f98-232">2.6.32-504</span></span> |
| <span data-ttu-id="c0f98-233">6.7</span><span class="sxs-lookup"><span data-stu-id="c0f98-233">6.7</span></span> | <span data-ttu-id="c0f98-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="c0f98-234">2.6.32-573</span></span> |
| <span data-ttu-id="c0f98-235">6.8</span><span class="sxs-lookup"><span data-stu-id="c0f98-235">6.8</span></span> | <span data-ttu-id="c0f98-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="c0f98-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="c0f98-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="c0f98-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="c0f98-238">**İşletim sistemi sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-238">**OS version**</span></span> | <span data-ttu-id="c0f98-239">**Çekirdek sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-240">5.8</span><span class="sxs-lookup"><span data-stu-id="c0f98-240">5.8</span></span> | <span data-ttu-id="c0f98-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="c0f98-241">2.6.18-308</span></span> |
| <span data-ttu-id="c0f98-242">5.9</span><span class="sxs-lookup"><span data-stu-id="c0f98-242">5.9</span></span> | <span data-ttu-id="c0f98-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="c0f98-243">2.6.18-348</span></span> |
| <span data-ttu-id="c0f98-244">5.10</span><span class="sxs-lookup"><span data-stu-id="c0f98-244">5.10</span></span> | <span data-ttu-id="c0f98-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="c0f98-245">2.6.18-371</span></span> |
| <span data-ttu-id="c0f98-246">5.11</span><span class="sxs-lookup"><span data-stu-id="c0f98-246">5.11</span></span> | <span data-ttu-id="c0f98-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="c0f98-247">2.6.18-398</span></span> <br> <span data-ttu-id="c0f98-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="c0f98-248">2.6.18-400</span></span> <br><span data-ttu-id="c0f98-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="c0f98-249">2.6.18-402</span></span> <br><span data-ttu-id="c0f98-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="c0f98-250">2.6.18-404</span></span> <br><span data-ttu-id="c0f98-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="c0f98-251">2.6.18-406</span></span> <br> <span data-ttu-id="c0f98-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="c0f98-252">2.6.18-407</span></span> <br> <span data-ttu-id="c0f98-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="c0f98-253">2.6.18-408</span></span> <br> <span data-ttu-id="c0f98-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="c0f98-254">2.6.18-409</span></span> <br> <span data-ttu-id="c0f98-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="c0f98-255">2.6.18-410</span></span> <br> <span data-ttu-id="c0f98-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="c0f98-256">2.6.18-411</span></span> <br> <span data-ttu-id="c0f98-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="c0f98-257">2.6.18-412</span></span> <br> <span data-ttu-id="c0f98-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="c0f98-258">2.6.18-416</span></span> <br> <span data-ttu-id="c0f98-259">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="c0f98-259">2.6.18-417</span></span> <br> <span data-ttu-id="c0f98-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="c0f98-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="c0f98-261">Oracle Enterprise Linux kesilemeyen kurumsal çekirdek ile</span><span class="sxs-lookup"><span data-stu-id="c0f98-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="c0f98-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="c0f98-262">Oracle Linux 6</span></span>

| <span data-ttu-id="c0f98-263">**İşletim sistemi sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-263">**OS version**</span></span> | <span data-ttu-id="c0f98-264">**Çekirdek sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-265">6.2</span><span class="sxs-lookup"><span data-stu-id="c0f98-265">6.2</span></span> | <span data-ttu-id="c0f98-266">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="c0f98-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="c0f98-267">6.3</span><span class="sxs-lookup"><span data-stu-id="c0f98-267">6.3</span></span> | <span data-ttu-id="c0f98-268">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="c0f98-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="c0f98-269">6.4</span><span class="sxs-lookup"><span data-stu-id="c0f98-269">6.4</span></span> | <span data-ttu-id="c0f98-270">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="c0f98-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="c0f98-271">6.5</span><span class="sxs-lookup"><span data-stu-id="c0f98-271">6.5</span></span> | <span data-ttu-id="c0f98-272">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="c0f98-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="c0f98-273">6.6</span><span class="sxs-lookup"><span data-stu-id="c0f98-273">6.6</span></span> | <span data-ttu-id="c0f98-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="c0f98-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="c0f98-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="c0f98-275">Oracle Linux 5</span></span>

| <span data-ttu-id="c0f98-276">**İşletim sistemi sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-276">**OS version**</span></span> | <span data-ttu-id="c0f98-277">**Çekirdek sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-278">5.8</span><span class="sxs-lookup"><span data-stu-id="c0f98-278">5.8</span></span> | <span data-ttu-id="c0f98-279">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="c0f98-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="c0f98-280">5.9</span><span class="sxs-lookup"><span data-stu-id="c0f98-280">5.9</span></span> | <span data-ttu-id="c0f98-281">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="c0f98-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="c0f98-282">5.10</span><span class="sxs-lookup"><span data-stu-id="c0f98-282">5.10</span></span> | <span data-ttu-id="c0f98-283">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="c0f98-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="c0f98-284">5.11</span><span class="sxs-lookup"><span data-stu-id="c0f98-284">5.11</span></span> | <span data-ttu-id="c0f98-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="c0f98-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="c0f98-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="c0f98-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="c0f98-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="c0f98-287">SUSE Linux 11</span></span>

| <span data-ttu-id="c0f98-288">**İşletim sistemi sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-288">**OS version**</span></span> | <span data-ttu-id="c0f98-289">**Çekirdek sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-290">11</span><span class="sxs-lookup"><span data-stu-id="c0f98-290">11</span></span> | <span data-ttu-id="c0f98-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="c0f98-291">2.6.27</span></span> |
| <span data-ttu-id="c0f98-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="c0f98-292">11 SP1</span></span> | <span data-ttu-id="c0f98-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="c0f98-293">2.6.32</span></span> |
| <span data-ttu-id="c0f98-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="c0f98-294">11 SP2</span></span> | <span data-ttu-id="c0f98-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="c0f98-295">3.0.13</span></span> |
| <span data-ttu-id="c0f98-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="c0f98-296">11 SP3</span></span> | <span data-ttu-id="c0f98-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="c0f98-297">3.0.76</span></span> |
| <span data-ttu-id="c0f98-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="c0f98-298">11 SP4</span></span> | <span data-ttu-id="c0f98-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="c0f98-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="c0f98-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="c0f98-300">SUSE Linux 10</span></span>

| <span data-ttu-id="c0f98-301">**İşletim sistemi sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-301">**OS version**</span></span> | <span data-ttu-id="c0f98-302">**Çekirdek sürümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="c0f98-303">10 SP4</span></span> | <span data-ttu-id="c0f98-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="c0f98-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="c0f98-305">Bağımlılık Aracısı indirir</span><span class="sxs-lookup"><span data-stu-id="c0f98-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="c0f98-306">**Dosya**</span><span class="sxs-lookup"><span data-stu-id="c0f98-306">**File**</span></span> | <span data-ttu-id="c0f98-307">**İŞLETİM SİSTEMİ**</span><span class="sxs-lookup"><span data-stu-id="c0f98-307">**OS**</span></span> | <span data-ttu-id="c0f98-308">**Sürüm**</span><span class="sxs-lookup"><span data-stu-id="c0f98-308">**Version**</span></span> | <span data-ttu-id="c0f98-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="c0f98-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="c0f98-310">InstallDependencyAgent Windows.exe</span><span class="sxs-lookup"><span data-stu-id="c0f98-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="c0f98-311">Windows</span><span class="sxs-lookup"><span data-stu-id="c0f98-311">Windows</span></span> | <span data-ttu-id="c0f98-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="c0f98-312">9.0.5</span></span> | <span data-ttu-id="c0f98-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="c0f98-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="c0f98-314">InstallDependencyAgent Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="c0f98-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="c0f98-315">Linux</span><span class="sxs-lookup"><span data-stu-id="c0f98-315">Linux</span></span> | <span data-ttu-id="c0f98-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="c0f98-316">9.0.5</span></span> | <span data-ttu-id="c0f98-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="c0f98-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="c0f98-318">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c0f98-318">Configuration</span></span>

<span data-ttu-id="c0f98-319">Aşağıdaki adımları tooconfigure hello kablo verileri çözümü alanlarınızı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-319">Perform hello following steps tooconfigure hello Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="c0f98-320">Merhaba etkinlik günlük analizi hello çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="c0f98-320">Enable hello Activity Log Analytics solution from hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="c0f98-321">Merhaba bağımlılık Aracısı tooget verilerin istediğiniz her bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-321">Install hello Dependency Agent on each computer where you want tooget data.</span></span> <span data-ttu-id="c0f98-322">her bilgisayarda bir aracı gerekmeyebilir şekilde hello bağımlılık Aracısı bağlantıları tooimmediate Komşuları olarak izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-322">hello Dependency Agent can monitor connections tooimmediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-hello-dependency-agent-on-windows"></a><span data-ttu-id="c0f98-323">Windows Hello bağımlılık Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="c0f98-323">Install hello Dependency Agent on Windows</span></span>

<span data-ttu-id="c0f98-324">Yönetici ayrıcalıkları gerekli tooinstall ya da hello aracısını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-324">Administrator privileges are required tooinstall or uninstall hello agent.</span></span>

<span data-ttu-id="c0f98-325">Merhaba bağımlılık Aracısı InstallDependencyAgent Windows.exe Windows çalıştıran bilgisayarlara yüklenir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-325">hello Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="c0f98-326">Bu yürütülebilir dosya seçenekleri olmadan çalıştırırsanız, tooinstall etkileşimli olarak izleyebileceğiniz bir sihirbazı başlatır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-326">If you run this executable file without any options, it starts a wizard that you can follow tooinstall interactively.</span></span>

<span data-ttu-id="c0f98-327">Windows çalıştıran her bilgisayarda adımları tooinstall hello bağımlılık aracısı aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="c0f98-327">Use hello following steps tooinstall hello Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="c0f98-328">Yükleme hello yönergeleri kullanarak OMS Aracısı hello [bağlanmak Windows bilgisayarları toohello Azure günlük analizi hizmeti](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="c0f98-328">Install hello OMS Agent by using hello instructions at [Connect Windows computers toohello Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="c0f98-329">Merhaba önceki bölümde Hello bağlantıyı kullanarak hello Windows aracıyı indirin ve çalıştırın komutu aşağıdaki hello kullanarak: InstallDependencyAgent Windows.exe</span><span class="sxs-lookup"><span data-stu-id="c0f98-329">Download hello Windows agent using hello link in hello previous section and then run it by using hello following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="c0f98-330">Merhaba Sihirbazı tooinstall hello Aracısı izleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-330">Follow hello wizard tooinstall hello agent.</span></span>
4. <span data-ttu-id="c0f98-331">Merhaba bağımlılık Aracısı toostart başarısız olursa, ayrıntılı hata bilgileri için hello günlüklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-331">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="c0f98-332">Windows aracısında %Programfiles%\Microsoft bağımlılık Agent\logs hello günlük dizindir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-332">On Windows agents, hello log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="c0f98-333">Windows komut satırı</span><span class="sxs-lookup"><span data-stu-id="c0f98-333">Windows command line</span></span>

<span data-ttu-id="c0f98-334">Merhaba tablo tooinstall komut satırından aşağıdaki seçenekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-334">Use options from hello following table tooinstall from a command line.</span></span> <span data-ttu-id="c0f98-335">toosee hello kullanarak hello yükleyiciyi çalıştırmak, hello yükleme bayrakları listesini /?</span><span class="sxs-lookup"><span data-stu-id="c0f98-335">toosee a list of hello installation flags, run hello installer by using hello /?</span></span> <span data-ttu-id="c0f98-336">aşağıdaki gibi bayrak.</span><span class="sxs-lookup"><span data-stu-id="c0f98-336">flag as follows.</span></span>

<span data-ttu-id="c0f98-337">InstallDependencyAgent Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="c0f98-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="c0f98-338">**Bayrağı**</span><span class="sxs-lookup"><span data-stu-id="c0f98-338">**Flag**</span></span> | <span data-ttu-id="c0f98-339">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c0f98-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="c0f98-340">Merhaba komut satırı seçeneklerinin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-340">Get a list of hello command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="c0f98-341">Kullanıcı etkileşimi ile sessiz bir yükleme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="c0f98-342">Merhaba Windows bağımlılık aracısı için dosyalar varsayılan olarak C:\Program Files\Microsoft bağımlılık Aracısı yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-342">Files for hello Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-hello-dependency-agent-on-linux"></a><span data-ttu-id="c0f98-343">Linux'ta Hello bağımlılık Aracısı yükleme</span><span class="sxs-lookup"><span data-stu-id="c0f98-343">Install hello Dependency Agent on Linux</span></span>

<span data-ttu-id="c0f98-344">Kök erişimi gerekli tooinstall ya da hello Aracısı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-344">Root access is required tooinstall or configure hello agent.</span></span>

<span data-ttu-id="c0f98-345">Merhaba bağımlılık Aracısı InstallDependencyAgent Linux64.bin, kendiliğinden açılan bir ikili içeren bir kabuk betiği aracılığıyla Linux bilgisayarlara yüklenir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-345">hello Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="c0f98-346">Merhaba dosyasını kullanarak çalıştırabilirsiniz _paylaş_ veya ekleme izinleri toohello dosyasının kendisini yürütün.</span><span class="sxs-lookup"><span data-stu-id="c0f98-346">You can run hello file by using _sh_ or add execute permissions toohello file itself.</span></span>

<span data-ttu-id="c0f98-347">Adımları tooinstall hello bağımlılık Aracısı her bir Linux bilgisayarda aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="c0f98-347">Use hello following steps tooinstall hello Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="c0f98-348">Yükleme hello yönergeleri kullanarak OMS Aracısı hello [toplamak ve Linux bilgisayarları veri yönetmek](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c0f98-348">Install hello OMS Agent by using hello instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="c0f98-349">Merhaba önceki bölümde Hello bağlantıyı kullanarak hello Linux bağımlılık aracıyı indirin ve ardından komut aşağıdaki hello kullanarak kök olarak yükleyin: Paylaş InstallDependencyAgent Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="c0f98-349">Download hello Linux Dependency agent using hello link in hello previous section and then install it as root by using hello following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="c0f98-350">Merhaba bağımlılık Aracısı toostart başarısız olursa, ayrıntılı hata bilgileri için hello günlüklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-350">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="c0f98-351">Linux aracısında hello günlük dizini:: /var/opt/microsoft/dependency-agent/log.</span><span class="sxs-lookup"><span data-stu-id="c0f98-351">On Linux agents, hello log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="c0f98-352">toosee ile Merhaba hello yükleme programını çalıştırmak, hello yükleme bayrakları listesini `-help` gibi bayrak.</span><span class="sxs-lookup"><span data-stu-id="c0f98-352">toosee a list of hello installation flags, run hello installation program with hello `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="c0f98-353">**Bayrağı**</span><span class="sxs-lookup"><span data-stu-id="c0f98-353">**Flag**</span></span> | <span data-ttu-id="c0f98-354">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c0f98-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="c0f98-355">Merhaba komut satırı seçeneklerinin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-355">Get a list of hello command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="c0f98-356">Kullanıcı etkileşimi ile sessiz bir yükleme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="c0f98-357">İzinler ve hello işletim sistemi denetle, ancak hello Aracısı yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-357">Check permissions and hello operating system but do not install hello agent.</span></span> |

<span data-ttu-id="c0f98-358">Merhaba bağımlılık aracısı için dosyalar dizinleri izleyen hello yerleştirilir:</span><span class="sxs-lookup"><span data-stu-id="c0f98-358">Files for hello Dependency Agent are placed in hello following directories:</span></span>

| <span data-ttu-id="c0f98-359">**Dosyaları**</span><span class="sxs-lookup"><span data-stu-id="c0f98-359">**Files**</span></span> | <span data-ttu-id="c0f98-360">**Konum**</span><span class="sxs-lookup"><span data-stu-id="c0f98-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-361">Çekirdek dosyaları</span><span class="sxs-lookup"><span data-stu-id="c0f98-361">Core files</span></span> | <span data-ttu-id="c0f98-362">/OPT/Microsoft/Dependency-Agent</span><span class="sxs-lookup"><span data-stu-id="c0f98-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="c0f98-363">Günlük dosyaları</span><span class="sxs-lookup"><span data-stu-id="c0f98-363">Log files</span></span> | <span data-ttu-id="c0f98-364">/var/OPT/Microsoft/Dependency-Agent/log</span><span class="sxs-lookup"><span data-stu-id="c0f98-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="c0f98-365">Yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="c0f98-365">Config files</span></span> | <span data-ttu-id="c0f98-366">/etc/OPT/Microsoft/Dependency-Agent/config</span><span class="sxs-lookup"><span data-stu-id="c0f98-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="c0f98-367">Hizmet yürütülebilir dosyalar</span><span class="sxs-lookup"><span data-stu-id="c0f98-367">Service executable files</span></span> | <span data-ttu-id="c0f98-368">/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent</span><span class="sxs-lookup"><span data-stu-id="c0f98-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="c0f98-369">/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent-Manager</span><span class="sxs-lookup"><span data-stu-id="c0f98-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="c0f98-370">İkili depolama dosyaları</span><span class="sxs-lookup"><span data-stu-id="c0f98-370">Binary storage files</span></span> | <span data-ttu-id="c0f98-371">/var/OPT/Microsoft/Dependency-Agent/Storage</span><span class="sxs-lookup"><span data-stu-id="c0f98-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="c0f98-372">Yükleme komut dosyası örnekleri</span><span class="sxs-lookup"><span data-stu-id="c0f98-372">Installation script examples</span></span>

<span data-ttu-id="c0f98-373">tooeasily hello bağımlılık Aracısı pek çok sunucu üzerinde aynı anda dağıtabilir, bir komut dosyası toouse yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c0f98-373">tooeasily deploy hello Dependency Agent on many servers at once, it helps toouse a script.</span></span> <span data-ttu-id="c0f98-374">Aşağıdaki komut örnekleri toodownload hello kullanın ve Windows ya da Linux hello bağımlılık aracısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c0f98-374">You can use hello following script examples toodownload and install hello Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="c0f98-375">Windows PowerShell Betiği</span><span class="sxs-lookup"><span data-stu-id="c0f98-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="c0f98-376">Linux için kabuk komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c0f98-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="c0f98-377">İstenen Durum Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="c0f98-377">Desired State Configuration</span></span>

<span data-ttu-id="c0f98-378">toodeploy hello bağımlılık Aracısı istenen durum yapılandırması hello xPSDesiredStateConfiguration modülü ve biraz kod hello aşağıdaki gibi kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0f98-378">toodeploy hello Dependency Agent via Desired State Configuration, you can use hello xPSDesiredStateConfiguration module and a bit of code like hello following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a><span data-ttu-id="c0f98-379">Merhaba bağımlılık aracısı kaldırma</span><span class="sxs-lookup"><span data-stu-id="c0f98-379">Uninstall hello Dependency Agent</span></span>

<span data-ttu-id="c0f98-380">Aşağıdaki bölümlerde toohelp hello bağımlılık aracısı kaldırma hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-380">Use hello following sections toohelp you remove hello Dependency Agent.</span></span>

#### <a name="uninstall-hello-dependency-agent-on-windows"></a><span data-ttu-id="c0f98-381">Bağımlılık Aracısı'nı Windows Hello kaldırma</span><span class="sxs-lookup"><span data-stu-id="c0f98-381">Uninstall hello Dependency Agent on Windows</span></span>

<span data-ttu-id="c0f98-382">Bir yönetici için hello bağımlılık Aracısı Windows Denetim Masası'ndan kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-382">An administrator can uninstall hello Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="c0f98-383">Bir yönetici, %Programfiles%\Microsoft bağımlılık Agent\Uninstall.exe toouninstall hello bağımlılık aracısı olarak da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe toouninstall hello Dependency Agent.</span></span>

#### <a name="uninstall-hello-dependency-agent-on-linux"></a><span data-ttu-id="c0f98-384">Merhaba bağımlılık Aracısı'nı Linux kaldırma</span><span class="sxs-lookup"><span data-stu-id="c0f98-384">Uninstall hello Dependency Agent on Linux</span></span>

<span data-ttu-id="c0f98-385">Bağımlılık Aracısı'ndan Linux toocompletely kaldırma Merhaba, hello aracı ile otomatik olarak yüklenen bağlayıcı hello ve hello aracının kendisi kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-385">toocompletely uninstall hello Dependency Agent from Linux, you must remove hello agent itself and hello connector, which is installed automatically with hello agent.</span></span> <span data-ttu-id="c0f98-386">Hem tek bir komut aşağıdaki hello kullanarak kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0f98-386">You can uninstall both by using hello following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="c0f98-387">Yönetim paketleri</span><span class="sxs-lookup"><span data-stu-id="c0f98-387">Management packs</span></span>

<span data-ttu-id="c0f98-388">Kablo verileri bir günlük analizi çalışma alanındaki etkinleştirildiğinde, 300-KB Yönetim Paketi bu çalışma alanında tooall hello Windows sunucularına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent tooall hello Windows servers in that workspace.</span></span> <span data-ttu-id="c0f98-389">System Center Operations Manager aracıları kullanıyorsanız, bir [bağlı yönetim grubu](log-analytics-om-agents.md), hello bağımlılık İzleyicisi Yönetim Paketi System Center Operations Manager'dan dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), hello Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="c0f98-390">Merhaba aracıları doğrudan bağlıysanız, günlük analizi hello Yönetim Paketi sunar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-390">If hello agents are directly connected, Log Analytics delivers hello management pack.</span></span>

<span data-ttu-id="c0f98-391">Merhaba Yönetim Paketi Microsoft.IntelligencePacks.ApplicationDependencyMonitor olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-391">hello management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="c0f98-392">Öğesine yazılır: %Programfiles%\Microsoft izleme Agent\Agent\Health hizmet State\Management paketleri.</span><span class="sxs-lookup"><span data-stu-id="c0f98-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="c0f98-393">Merhaba Yönetim Paketi kullanan hello veri kaynağı: % Program files%\Microsoft izleme Agent\Agent\Health hizmet State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span><span class="sxs-lookup"><span data-stu-id="c0f98-393">hello data source that hello management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-hello-solution"></a><span data-ttu-id="c0f98-394">Merhaba çözümünü kullanarak</span><span class="sxs-lookup"><span data-stu-id="c0f98-394">Using hello solution</span></span>

<span data-ttu-id="c0f98-395">**Yükleme ve yapılandırma hello çözümü**</span><span class="sxs-lookup"><span data-stu-id="c0f98-395">**Installing and configuring hello solution**</span></span>

<span data-ttu-id="c0f98-396">Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-396">Use hello following information tooinstall and configure hello solution.</span></span>

- <span data-ttu-id="c0f98-397">Merhaba kablo verileri çözüm Windows Server 2012 R2, Windows 8.1 ve sonraki işletim sistemleri çalıştıran bilgisayarların verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-397">hello Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="c0f98-398">Tooacquire kablo verileri istediğiniz bilgisayarlarda Microsoft .NET Framework 4.0 veya sonraki sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-398">Microsoft .NET Framework 4.0 or later is required on computers where you want tooacquire wire data from.</span></span>
- <span data-ttu-id="c0f98-399">Açıklanan başlangıç işlemini kullanarak hello kablo verileri çözüm tooyour günlük analizi çalışma Ekle [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="c0f98-399">Add hello Wire Data solution tooyour Log Analytics workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="c0f98-400">Başka bir yapılandırma işlemi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c0f98-400">There is no further configuration required.</span></span>
- <span data-ttu-id="c0f98-401">Belirli bir çözüm için tooview kablo verileri istiyorsanız, zaten eklenmiş toohave hello çözüm gerekir tooyour çalışma.</span><span class="sxs-lookup"><span data-stu-id="c0f98-401">If you want tooview wire data for a specific solution, you need toohave hello solution already added tooyour workspace.</span></span>

<span data-ttu-id="c0f98-402">Aracıları yüklü olan ve hello çözüm yükledikten sonra hello kablo verileri 2.0 döşeme çalışma alanında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-402">After you have agents installed and you install hello solution, hello Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="c0f98-403">Şu anda hello OMS portalı tooview kablo verileri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-403">Currently, you must use hello OMS portal tooview wire data.</span></span> <span data-ttu-id="c0f98-404">Hello Azure portal tooview kablo verileri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="c0f98-404">You cannot use hello Azure portal tooview wire data.</span></span>

![Kablo verileri döşeme](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a><span data-ttu-id="c0f98-406">Merhaba kablo verileri 2.0 çözümünü kullanarak</span><span class="sxs-lookup"><span data-stu-id="c0f98-406">Using hello Wire Data 2.0 solution</span></span>

<span data-ttu-id="c0f98-407">Merhaba OMS portalında hello tıklatın **kablo verileri 2.0** döşeme tooopen hello kablo verileri Pano.</span><span class="sxs-lookup"><span data-stu-id="c0f98-407">In hello OMS portal, click hello **Wire Data 2.0** tile tooopen hello Wire Data dashboard.</span></span> <span data-ttu-id="c0f98-408">Merhaba Pano aşağıdaki tablonun hello hello Kanatlar içerir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-408">hello dashboard includes hello blades in hello following table.</span></span> <span data-ttu-id="c0f98-409">Her dikey penceresinde hello dikey'nın ölçütlerine kapsam ve zaman aralığını belirtilen eşleşen too10 öğeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="c0f98-409">Each blade lists up too10 items matching that blade's criteria for hello specified scope and time range.</span></span> <span data-ttu-id="c0f98-410">Tıklayarak tüm kayıtları döndüren bir günlük arama çalıştırabilirsiniz **tümünü görmek** hello altındaki hello dikey veya hello dikey penceresi Başlığı tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="c0f98-410">You can run a log search that returns all records by clicking **See all** at hello bottom of hello blade or by clicking hello blade header.</span></span>

| <span data-ttu-id="c0f98-411">**Dikey penceresi**</span><span class="sxs-lookup"><span data-stu-id="c0f98-411">**Blade**</span></span> | <span data-ttu-id="c0f98-412">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="c0f98-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c0f98-413">Ağ trafiğini yakalayan aracılar</span><span class="sxs-lookup"><span data-stu-id="c0f98-413">Agents capturing network traffic</span></span> | <span data-ttu-id="c0f98-414">Ağ trafiğini yakalayan aracılar Hello sayısını gösterir ve trafiği yakalama hello üst 10 bilgisayarları listeler.</span><span class="sxs-lookup"><span data-stu-id="c0f98-414">Shows hello number of agents that are capturing network traffic and lists hello top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="c0f98-415">Bir günlük Ara Hello numara toorun <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span><span class="sxs-lookup"><span data-stu-id="c0f98-415">Click hello number toorun a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="c0f98-416">Hello listesi toorun bir bilgisayarda yakalanan baytların toplam sayısıdır hello döndüren bir günlük Ara'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-416">Click a computer in hello list toorun a log search returning hello total number of bytes captured.</span></span> |
| <span data-ttu-id="c0f98-417">Yerel alt ağları</span><span class="sxs-lookup"><span data-stu-id="c0f98-417">Local Subnets</span></span> | <span data-ttu-id="c0f98-418">Aracıları bulunmuş yerel alt ağları Hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-418">Shows hello number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="c0f98-419">Bir günlük Ara Hello numara toorun <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> , listeleri tüm alt ağlar ile Merhaba her biri gönderilen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="c0f98-419">Click hello number toorun a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with hello number of bytes sent over each one.</span></span> <span data-ttu-id="c0f98-420">Bir alt ağda hello listesi toorun hello toplam hello alt ağ gönderilen bayt sayısı döndüren bir günlük Ara'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-420">Click a subnet in hello list toorun a log search returning hello total number of bytes sent over hello subnet.</span></span> |
| <span data-ttu-id="c0f98-421">Uygulama düzeyi protokolleri</span><span class="sxs-lookup"><span data-stu-id="c0f98-421">Application-level Protocols</span></span> | <span data-ttu-id="c0f98-422">Uygulama düzeyi protokolleri Hello sayısını kullanımda, aracıları tarafından bulunan olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-422">Shows hello number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="c0f98-423">Bir günlük Ara Hello numara toorun <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span><span class="sxs-lookup"><span data-stu-id="c0f98-423">Click hello number toorun a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="c0f98-424">Bir protokol toorun hello toplam hello protokolü kullanılarak gönderilen bayt sayısı döndüren bir günlük Ara'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-424">Click a protocol toorun a log search returning hello total number of bytes sent using hello protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Kablo verileri Panosu](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="c0f98-426">Merhaba kullanabilirsiniz **ağ trafiğini yakalayan aracılar** dikey toodetermine ne kadar ağ bant genişliği, bilgisayarlar tarafından tüketilen.</span><span class="sxs-lookup"><span data-stu-id="c0f98-426">You can use hello **Agents capturing network traffic** blade toodetermine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="c0f98-427">Bu dikey kolayca Bul hello yardımcı olabilecek _chattiest_ bilgisayar ortamınızdaki.</span><span class="sxs-lookup"><span data-stu-id="c0f98-427">This blade can help you easily find hello _chattiest_ computer in your environment.</span></span> <span data-ttu-id="c0f98-428">Bu bilgisayarlar, anormal olarak davranan veya normalden daha fazla ağ kaynaklarını kullanan aşırı yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="c0f98-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![Günlük arama örneği](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="c0f98-430">Benzer şekilde, hello kullanabilirsiniz **yerel alt ağları** dikey toodetermine ne kadar ağ trafiğini, alt ağlar arasında taşıma.</span><span class="sxs-lookup"><span data-stu-id="c0f98-430">Similarly, you can use hello **Local Subnets** blade toodetermine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="c0f98-431">Kullanıcıların uygulamaları için kritik alanları geçici alt ağlar genellikle tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="c0f98-432">Bu dikey bu alanlara görünüme sunar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-432">This blade offers a view into those areas.</span></span>

![Günlük arama örneği](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="c0f98-434">Merhaba **uygulama düzeyi protokolleri** dikey yararlıdır yardımcı olduğundan ne protokolleri kullanımda olduğunu biliyor.</span><span class="sxs-lookup"><span data-stu-id="c0f98-434">hello **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="c0f98-435">Örneğin, SSH toonot, ağ ortamınızda kullanılacak bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-435">For example, you might expect SSH toonot be in use in your network environment.</span></span> <span data-ttu-id="c0f98-436">Merhaba dikey penceresinde kullanılabilir bilgilerini görüntüleme hızlı bir şekilde Onayla veya, Beklenti disprove.</span><span class="sxs-lookup"><span data-stu-id="c0f98-436">Viewing information available in hello blade can quickly confirm or disprove your expectation.</span></span>

![Günlük arama örneği](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="c0f98-438">Bu örnekte, SSH ayrıntıları toosee ayrıntıya hangi bilgisayarların SSH ve diğer birçok iletişim ayrıntılarını kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-438">In this example, you could drill-into SSH details toosee which computers are using SSH and many other communication details.</span></span>

![Paylaş arama sonuçları](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="c0f98-440">Protokol trafiğini artan veya azalan zamanla varsa yararlı tooknow de olabilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-440">It's also useful tooknow if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="c0f98-441">Bir uygulama tarafından aktarılan veri miktarını Hello artırılması, örneğin, bilincinde olmanız gereken bir şey olması veya dikkate değer bulabileceğiniz emin olabilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-441">For example, if hello amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="c0f98-442">Giriş verisi</span><span class="sxs-lookup"><span data-stu-id="c0f98-442">Input data</span></span>

<span data-ttu-id="c0f98-443">Kablo verileri etkinleştirdiğiniz hello aracıları kullanarak ağ trafiğini hakkındaki meta verileri toplar.</span><span class="sxs-lookup"><span data-stu-id="c0f98-443">Wire data collects metadata about network traffic using hello agents that you have enabled.</span></span> <span data-ttu-id="c0f98-444">Her bir aracının 15 dakikada hakkındaki verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="c0f98-445">Çıktı verileri</span><span class="sxs-lookup"><span data-stu-id="c0f98-445">Output data</span></span>

<span data-ttu-id="c0f98-446">Türüne sahip bir kayıt _WireData_ her giriş veri türü için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c0f98-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="c0f98-447">WireData kayıtları, aşağıdaki tablonun hello gösterilen özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c0f98-447">WireData records have properties shown in hello following table:</span></span>

| <span data-ttu-id="c0f98-448">Özellik</span><span class="sxs-lookup"><span data-stu-id="c0f98-448">Property</span></span> | <span data-ttu-id="c0f98-449">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c0f98-449">Description</span></span> |
|---|---|
| <span data-ttu-id="c0f98-450">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="c0f98-450">Computer</span></span> | <span data-ttu-id="c0f98-451">Burada veri toplanan bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="c0f98-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="c0f98-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="c0f98-452">TimeGenerated</span></span> | <span data-ttu-id="c0f98-453">Merhaba kayıt zamanı</span><span class="sxs-lookup"><span data-stu-id="c0f98-453">Time of hello record</span></span> |
| <span data-ttu-id="c0f98-454">Yerel IP</span><span class="sxs-lookup"><span data-stu-id="c0f98-454">LocalIP</span></span> | <span data-ttu-id="c0f98-455">Merhaba yerel bilgisayarın IP adresi</span><span class="sxs-lookup"><span data-stu-id="c0f98-455">IP address of hello local computer</span></span> |
| <span data-ttu-id="c0f98-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="c0f98-456">SessionState</span></span> | <span data-ttu-id="c0f98-457">Bağlantısı kesilmiş veya bağlı</span><span class="sxs-lookup"><span data-stu-id="c0f98-457">Connected or disconnected</span></span> |
| <span data-ttu-id="c0f98-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="c0f98-458">ReceivedBytes</span></span> | <span data-ttu-id="c0f98-459">Alınan bayt miktarı</span><span class="sxs-lookup"><span data-stu-id="c0f98-459">Amount of bytes received</span></span> |
| <span data-ttu-id="c0f98-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="c0f98-460">ProtocolName</span></span> | <span data-ttu-id="c0f98-461">Kullanılan hello ağ protokolü adı</span><span class="sxs-lookup"><span data-stu-id="c0f98-461">Name of hello network protocol used</span></span> |
| <span data-ttu-id="c0f98-462">İpversion değeri</span><span class="sxs-lookup"><span data-stu-id="c0f98-462">IPVersion</span></span> | <span data-ttu-id="c0f98-463">IP sürümü</span><span class="sxs-lookup"><span data-stu-id="c0f98-463">IP version</span></span> |
| <span data-ttu-id="c0f98-464">Yön</span><span class="sxs-lookup"><span data-stu-id="c0f98-464">Direction</span></span> | <span data-ttu-id="c0f98-465">Gelen veya giden</span><span class="sxs-lookup"><span data-stu-id="c0f98-465">Inbound or outbound</span></span> |
| <span data-ttu-id="c0f98-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="c0f98-466">MaliciousIP</span></span> | <span data-ttu-id="c0f98-467">Bilinen kötü amaçlı bir kaynak IP adresi</span><span class="sxs-lookup"><span data-stu-id="c0f98-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="c0f98-468">Önem Derecesi</span><span class="sxs-lookup"><span data-stu-id="c0f98-468">Severity</span></span> | <span data-ttu-id="c0f98-469">Amaçlı olduğundan kuşkulanılan yazılımın önem derecesi</span><span class="sxs-lookup"><span data-stu-id="c0f98-469">Suspected malware severity</span></span> |
| <span data-ttu-id="c0f98-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="c0f98-470">RemoteIPCountry</span></span> | <span data-ttu-id="c0f98-471">Ülke / bölge hello uzak IP adresi</span><span class="sxs-lookup"><span data-stu-id="c0f98-471">Country of hello remote IP address</span></span> |
| <span data-ttu-id="c0f98-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="c0f98-472">ManagementGroupName</span></span> | <span data-ttu-id="c0f98-473">Merhaba Operations Manager yönetim grubunun adı</span><span class="sxs-lookup"><span data-stu-id="c0f98-473">Name of hello Operations Manager management group</span></span> |
| <span data-ttu-id="c0f98-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="c0f98-474">SourceSystem</span></span> | <span data-ttu-id="c0f98-475">Burada veri toplanan kaynak</span><span class="sxs-lookup"><span data-stu-id="c0f98-475">Source where data was collected</span></span> |
| <span data-ttu-id="c0f98-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="c0f98-476">SessionStartTime</span></span> | <span data-ttu-id="c0f98-477">Oturum başlangıç saati</span><span class="sxs-lookup"><span data-stu-id="c0f98-477">Start time of session</span></span> |
| <span data-ttu-id="c0f98-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="c0f98-478">SessionEndTime</span></span> | <span data-ttu-id="c0f98-479">Oturumun bitiş saati</span><span class="sxs-lookup"><span data-stu-id="c0f98-479">End time of session</span></span> |
| <span data-ttu-id="c0f98-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="c0f98-480">LocalSubnet</span></span> | <span data-ttu-id="c0f98-481">Burada veri toplanan alt ağ</span><span class="sxs-lookup"><span data-stu-id="c0f98-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="c0f98-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="c0f98-482">LocalPortNumber</span></span> | <span data-ttu-id="c0f98-483">Yerel bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="c0f98-483">Local port number</span></span> |
| <span data-ttu-id="c0f98-484">Uzak IP</span><span class="sxs-lookup"><span data-stu-id="c0f98-484">RemoteIP</span></span> | <span data-ttu-id="c0f98-485">Merhaba uzak bilgisayar tarafından kullanılan uzak IP adresi</span><span class="sxs-lookup"><span data-stu-id="c0f98-485">Remote IP address used by hello remote computer</span></span> |
| <span data-ttu-id="c0f98-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="c0f98-486">RemotePortNumber</span></span> | <span data-ttu-id="c0f98-487">Merhaba uzak IP adresi tarafından kullanılan bağlantı noktası numarası</span><span class="sxs-lookup"><span data-stu-id="c0f98-487">Port number used by hello remote IP address</span></span> |
| <span data-ttu-id="c0f98-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="c0f98-488">SessionID</span></span> | <span data-ttu-id="c0f98-489">İki IP adresi arasındaki iletişimi oturumunu tanımlayan benzersiz bir değer</span><span class="sxs-lookup"><span data-stu-id="c0f98-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="c0f98-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="c0f98-490">SentBytes</span></span> | <span data-ttu-id="c0f98-491">Gönderilen bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="c0f98-491">Number of bytes sent</span></span> |
| <span data-ttu-id="c0f98-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="c0f98-492">TotalBytes</span></span> | <span data-ttu-id="c0f98-493">Toplam oturum sırasında gönderilen bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="c0f98-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="c0f98-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="c0f98-494">ApplicationProtocol</span></span> | <span data-ttu-id="c0f98-495">Kullanılan ağ protokol türü</span><span class="sxs-lookup"><span data-stu-id="c0f98-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="c0f98-496">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="c0f98-496">ProcessID</span></span> | <span data-ttu-id="c0f98-497">Windows işlem kimliği</span><span class="sxs-lookup"><span data-stu-id="c0f98-497">Windows process ID</span></span> |
| <span data-ttu-id="c0f98-498">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="c0f98-498">ProcessName</span></span> | <span data-ttu-id="c0f98-499">Merhaba işlemin yolu ve dosya adı</span><span class="sxs-lookup"><span data-stu-id="c0f98-499">Path and file name of hello process</span></span> |
| <span data-ttu-id="c0f98-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="c0f98-500">RemoteIPLongitude</span></span> | <span data-ttu-id="c0f98-501">IP boylam değeri</span><span class="sxs-lookup"><span data-stu-id="c0f98-501">IP longitude value</span></span> |
| <span data-ttu-id="c0f98-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="c0f98-502">RemoteIPLatitude</span></span> | <span data-ttu-id="c0f98-503">IP enlem değeri</span><span class="sxs-lookup"><span data-stu-id="c0f98-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c0f98-504">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0f98-504">Next steps</span></span>

- <span data-ttu-id="c0f98-505">[Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı kablo veri arama kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c0f98-505">[Search logs](log-analytics-log-searches.md) tooview detailed wire data search records.</span></span>
