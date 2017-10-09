---
title: "bir SQL veritabanı çok kiracılı uygulama ile aaaUse günlük analizi | Microsoft Docs"
description: "Kurulum ve günlük analizi (OMS) hello Azure SQL Database örnek Wingtip SaaS uygulaması ile kullanma"
keywords: "sql veritabanı öğreticisi"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a><span data-ttu-id="b6698-104">Kurulum ve günlük analizi (OMS) hello Wingtip SaaS uygulama ile kullanma</span><span class="sxs-lookup"><span data-stu-id="b6698-104">Setup and use Log Analytics (OMS) with hello Wingtip SaaS app</span></span>

<span data-ttu-id="b6698-105">Bu öğreticide ayarlama ve kullanma *günlük analizi ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* esnek havuzlar ve veritabanları izleme.</span><span class="sxs-lookup"><span data-stu-id="b6698-105">In this tutorial, you set up and use *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* for monitoring elastic pools and databases.</span></span> <span data-ttu-id="b6698-106">Merhaba üzerinde derlemeler [performans izleme ve yönetim öğretici](sql-database-saas-tutorial-performance-monitoring.md)ve gösterir nasıl toouse *günlük analizi* tooaugment hello izleme ve uyarma sağlanan hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="b6698-106">It builds on hello [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md), and shows how toouse *Log Analytics* tooaugment hello monitoring and alerting provided in hello Azure portal.</span></span> <span data-ttu-id="b6698-107">Log Analytics, yüzlerce havuz ve yüz binlerce veritabanını desteklediğinden özellikle büyük ölçekli izleme ve uyarı özellikleri için uygundur.</span><span class="sxs-lookup"><span data-stu-id="b6698-107">Log Analytics is particularly suitable for monitoring and alerting at scale because it supports hundreds of pools and hundreds of thousands of databases.</span></span> <span data-ttu-id="b6698-108">Ayrıca, birden fazla Azure aboneliği genelinde farklı uygulamaların ve Azure hizmetlerinin izlenmesini tümleştiren tek bir izleme çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6698-108">It also provides a single monitoring solution, which can integrate monitoring of different applications and Azure services, across multiple Azure subscriptions.</span></span>

<span data-ttu-id="b6698-109">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="b6698-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b6698-110">Log Analytics’i yükleme ve yapılandırma (OMS)</span><span class="sxs-lookup"><span data-stu-id="b6698-110">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="b6698-111">Günlük analizi toomonitor havuzları ve veritabanları kullanın</span><span class="sxs-lookup"><span data-stu-id="b6698-111">Use Log Analytics toomonitor pools and databases</span></span>

<span data-ttu-id="b6698-112">Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b6698-112">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

* <span data-ttu-id="b6698-113">Merhaba Wingtip SaaS uygulaması dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b6698-113">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="b6698-114">beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="b6698-114">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="b6698-115">Azure PowerShell’in yüklendiğinden.</span><span class="sxs-lookup"><span data-stu-id="b6698-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="b6698-116">Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="b6698-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

<span data-ttu-id="b6698-117">Merhaba bkz [performans izleme ve yönetim öğretici](sql-database-saas-tutorial-performance-monitoring.md) hello SaaS senaryolar ve desenleri ve bir izleme çözümü hello gereksinimleri nasıl etkilediklerini Tartışması için.</span><span class="sxs-lookup"><span data-stu-id="b6698-117">See hello [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md) for a discussion of hello SaaS scenarios and patterns, and how they affect hello requirements on a monitoring solution.</span></span>

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a><span data-ttu-id="b6698-118">Log Analytics (OMS) ile performansı izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="b6698-118">Monitoring and managing performance with Log Analytics (OMS)</span></span>

<span data-ttu-id="b6698-119">SQL Veritabanı için veritabanı ve havuzlarda izleme ve uyarı özellikleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6698-119">For SQL Database, monitoring and alerting is available on databases and pools.</span></span> <span data-ttu-id="b6698-120">Bu yerleşik izleme ve uyarma kaynak özgü ve kaynak küçük sayılar için uygun olmakla birlikte uygun toomonitoring büyük yüklemeleri daha az veya farklı kaynaklar ve abonelikler arasında birleştirilmiş bir görünümünü sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="b6698-120">This built-in monitoring and alerting is resource-specific and convenient for small numbers of resources, but is less well suited toomonitoring large installations or for providing a unified view across different resources and subscriptions.</span></span>

<span data-ttu-id="b6698-121">Yüksek hacimli senaryolar için Log Analytics kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6698-121">For high-volume scenarios Log Analytics can be used.</span></span> <span data-ttu-id="b6698-122">Bu analytics verilmiş tanılama günlüklerini sağlayan ayrı bir Azure hizmeti ve telemetri birçok özellikten toplayabilirsiniz günlük analizi çalışma alanındaki toplanan telemetri Hizmetleri ve kullanılan tooquery olması ve Uyarıları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b6698-122">This is a separate Azure service that provides analytics over emitted diagnostic logs and telemetry gathered in a log analytics workspace, which can collect telemetry from many services and be used tooquery and set alerts.</span></span> <span data-ttu-id="b6698-123">Log Analytics, işlem verilerinin analiz edilmesini ve görselleştirilmesini sağlayan yerleşik bir sorgu dili ve veri görselleştirme araçları sunar.</span><span class="sxs-lookup"><span data-stu-id="b6698-123">Log Analytics provides a built-in query language and data visualization tools allowing operational data analytics and visualization.</span></span> <span data-ttu-id="b6698-124">Hello SQL analiz çözümü çeşitli ön tanımlı esnek havuz ve izleme ve görünümleri ve sorguları uyarı veritabanı sağlar ve kendi geçici sorgular eklemek ve bunları gerektiği gibi kaydetmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b6698-124">hello SQL Analytics solution provides several pre-defined elastic pool and database monitoring and alerting views and queries, and lets you add your own ad-hoc queries and save these as needed.</span></span> <span data-ttu-id="b6698-125">OMS, özel bir görünüm tasarımcısı da sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6698-125">OMS also provides a custom view designer.</span></span>

<span data-ttu-id="b6698-126">Günlük analizi çalışma alanları ve analiz çözümleri hello Azure portalında hem de OMS açılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6698-126">Log Analytics workspaces and analytics solutions can be opened both in hello Azure portal and in OMS.</span></span> <span data-ttu-id="b6698-127">Hello Azure portal hello yeni erişim noktası ancak bazı alanlar hello OMS portalında arkasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6698-127">hello Azure portal is hello newer access point but may be behind hello OMS portal in some areas.</span></span>

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a><span data-ttu-id="b6698-128">Merhaba yük Oluşturucu toocreate veri tooanalyze Başlat</span><span class="sxs-lookup"><span data-stu-id="b6698-128">Start hello load generator toocreate data tooanalyze</span></span>

1. <span data-ttu-id="b6698-129">Açık **Demo PerformanceMonitoringAndManagement.ps1** hello içinde **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="b6698-129">Open **Demo-PerformanceMonitoringAndManagement.ps1** in hello **PowerShell ISE**.</span></span> <span data-ttu-id="b6698-130">Toorun isteyebileceğinizden bu komut dosyası açık hello yük nesil senaryolarından sırasında Bu öğretici tutun.</span><span class="sxs-lookup"><span data-stu-id="b6698-130">Keep this script open as you may want toorun several of hello load generation scenarios during this tutorial.</span></span>
1. <span data-ttu-id="b6698-131">Beşten küçük kiracılar varsa, kiracılar tooprovide daha ilginç bir izleme bağlamı toplu sağlayın:</span><span class="sxs-lookup"><span data-stu-id="b6698-131">If you have less than five tenants, provision a batch of tenants tooprovide a more interesting monitoring context:</span></span>
   1. <span data-ttu-id="b6698-132">**$DemoScenario = 1,** **Kiracı grubu sağlama** değerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b6698-132">Set **$DemoScenario = 1,** **Provision a batch of tenants**</span></span>
   1. <span data-ttu-id="b6698-133">Tuşuna **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b6698-133">Press **F5** toorun hello script.</span></span>

1. <span data-ttu-id="b6698-134">**$DemoScenario** = 2, **Normal yoğunlukta yük (yaklaşık 40 DTU) oluşturma**’yı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b6698-134">Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**.</span></span>
1. <span data-ttu-id="b6698-135">Tuşuna **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b6698-135">Press **F5** toorun hello script.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="b6698-136">Merhaba Wingtip uygulama komut dosyaları alma</span><span class="sxs-lookup"><span data-stu-id="b6698-136">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="b6698-137">Merhaba Wingtip biletleri komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo.</span><span class="sxs-lookup"><span data-stu-id="b6698-137">hello Wingtip Tickets scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="b6698-138">Komut dosyaları hello bulunan [öğrenme modüller klasörüne](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules).</span><span class="sxs-lookup"><span data-stu-id="b6698-138">Script files are located in hello [Learning Modules folder](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules).</span></span> <span data-ttu-id="b6698-139">Merhaba karşıdan **öğrenme modülleri** klasör yapısını koruma klasör tooyour yerel bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="b6698-139">Download hello **Learning Modules** folder tooyour local computer, maintaining its folder structure.</span></span>

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a><span data-ttu-id="b6698-140">Günlük analizi ve hello Azure SQL analiz çözümü yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6698-140">Installing and configuring Log Analytics and hello Azure SQL Analytics solution</span></span>

<span data-ttu-id="b6698-141">Günlük analizi yapılandırılmış toobe gerektiren ayrı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="b6698-141">Log Analytics is a separate service that needs toobe configured.</span></span> <span data-ttu-id="b6698-142">Log Analytics, log analytics çalışma alanında günlük veriler, telemetri ve ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="b6698-142">Log Analytics collects log data and telemetry and metrics in a log analytics workspace.</span></span> <span data-ttu-id="b6698-143">Çalışma alanı, Azure’daki diğer kaynaklara benzer bir kaynaktır ve oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6698-143">A workspace is a resource, just like other resources in Azure, and must be created.</span></span> <span data-ttu-id="b6698-144">Merhaba çalışma hello oluşturulan toobe gerekmez ancak aynı kaynak grubunda izleme hello uygulamaları bu genellikle hello en anlamlı.</span><span class="sxs-lookup"><span data-stu-id="b6698-144">While hello workspace doesn’t need toobe created in hello same resource group as hello application(s) it is monitoring, this often makes hello most sense.</span></span> <span data-ttu-id="b6698-145">Merhaba Wingtip SaaS uygulamasının Hello durumda bu hello kaynak grubunu silerek hello uygulama ile kolayca silinmiş hello çalışma toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6698-145">In hello case of hello Wingtip SaaS app, this enables hello workspace toobe easily deleted with hello application by simply deleting hello resource group.</span></span>

1. <span data-ttu-id="b6698-146">Aç... \\Öğrenme modülleri\\performans izleme ve Yönetim\\günlük analizi\\*Demo LogAnalytics.ps1* hello içinde **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="b6698-146">Open ...\\Learning Modules\\Performance Monitoring and Management\\Log Analytics\\*Demo-LogAnalytics.ps1* in hello **PowerShell ISE**.</span></span>
1. <span data-ttu-id="b6698-147">Tuşuna **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b6698-147">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="b6698-148">Bu noktada mümkün açık günlük analizi hello Azure portal (veya hello OMS portalı) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6698-148">At this point you should be able open Log Analytics in hello Azure portal (or hello OMS portal).</span></span> <span data-ttu-id="b6698-149">Merhaba günlük analizi çalışma alanı ve toobecome görünür toplanan telemetri toobe birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="b6698-149">It will take a few minutes for telemetry toobe collected in hello Log Analytics workspace and toobecome visible.</span></span> <span data-ttu-id="b6698-150">Merhaba veri daha ilginç hello deneyimi hello toplama hello sistem bırakın daha uzun olur.</span><span class="sxs-lookup"><span data-stu-id="b6698-150">hello longer you leave hello system gathering data hello more interesting hello experience will be.</span></span> <span data-ttu-id="b6698-151">Şimdi toograb içecek - yalnızca hello yük Oluşturucu hala çalıştığından emin olun zamanıdır!</span><span class="sxs-lookup"><span data-stu-id="b6698-151">Now's a good time toograb a beverage - just make sure hello load generator is still running!</span></span>


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a><span data-ttu-id="b6698-152">SQL analizi çözüm toomonitor havuzları ve veritabanları Merhaba ve günlük analizi kullanın</span><span class="sxs-lookup"><span data-stu-id="b6698-152">Use Log Analytics and hello SQL Analytics solution toomonitor pools and databases</span></span>


<span data-ttu-id="b6698-153">Bu alıştırmada, günlük analizi ve hello veritabanları ve havuzları için toplanan hello telemetri toolook hello OMS Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="b6698-153">In this exercise, open Log Analytics and hello OMS portal toolook at hello telemetry being gathered for hello databases and pools.</span></span>

1. <span data-ttu-id="b6698-154">Toohello Gözat [Azure portal](https://portal.azure.com) ve daha fazla hizmet tıklayarak günlük analizi açın ve ardından aramak için günlük analizi:</span><span class="sxs-lookup"><span data-stu-id="b6698-154">Browse toohello [Azure portal](https://portal.azure.com) and open Log Analytics by clicking More services, then search for Log Analytics:</span></span>

   ![log analytics’i aç](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. <span data-ttu-id="b6698-156">Adlı hello çalışma alanını seçin *wtploganalytics -&lt;kullanıcı&gt;*.</span><span class="sxs-lookup"><span data-stu-id="b6698-156">Select hello workspace named *wtploganalytics-&lt;USER&gt;*.</span></span>

1. <span data-ttu-id="b6698-157">Seçin **genel bakış** tooopen hello hello Azure portalında günlük analizi çözümde.</span><span class="sxs-lookup"><span data-stu-id="b6698-157">Select **Overview** tooopen hello Log Analytics solution in hello Azure portal.</span></span>
   <span data-ttu-id="b6698-158">![genel bakış-bağlantı](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span><span class="sxs-lookup"><span data-stu-id="b6698-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span></span>

    <span data-ttu-id="b6698-159">**Önemli**: birkaç hello çözüm etkinleştirilmeden önce dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b6698-159">**IMPORTANT**: It may take a couple of minutes before hello solution is active.</span></span> <span data-ttu-id="b6698-160">Sabırlı olun!</span><span class="sxs-lookup"><span data-stu-id="b6698-160">Be patient!</span></span>

1. <span data-ttu-id="b6698-161">Azure SQL analizi döşeme tooopen Hello üzerinde tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b6698-161">Click on hello Azure SQL Analytics tile tooopen it.</span></span>

    ![genel bakış](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![analizler](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. <span data-ttu-id="b6698-164">kendi kaydırma çubuğu hello altındaki (gerekirse yenileme hello dikey) ile Merhaba çözüm dikey kayarken betiklerdeki görünümünde hello.</span><span class="sxs-lookup"><span data-stu-id="b6698-164">hello view in hello solution blade scrolls sideways, with its own scroll bar at hello bottom (refresh hello blade if needed).</span></span>

1. <span data-ttu-id="b6698-165">Burada kullanabileceğiniz hello zaman-kaydırıcı hello ayrıntıya Gezgini, bunları veya kaynakların tooopen tıklatarak çeşitli görünümleri üst sol veya tıklatın hello üzerinde dikey keşfedin üzerinde daha dar bir zaman dilimi içinde toofocus çubuğu.</span><span class="sxs-lookup"><span data-stu-id="b6698-165">Explore hello various views by clicking on them or on individual resources tooopen a drill-down explorer, where you can use hello time-slider in hello top left or click on a vertical bar toofocus in on a narrower time slice.</span></span> <span data-ttu-id="b6698-166">Bu görünüm ile belirli kaynaklar üzerinde tek tek veritabanlarını veya havuzları toofocus seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6698-166">With this view, you can select individual databases or pools toofocus on specific resources:</span></span>

    ![grafik](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. <span data-ttu-id="b6698-168">Geri hello çözüm dikey penceresinde, üzerinde tooopen tıklayın ve Araştır kaydedilmiş bazı sorgular toohello sağ kaydırma görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b6698-168">Back on hello solution blade, if you scroll toohello far right you will see some saved queries that you can click on tooopen and explore.</span></span> <span data-ttu-id="b6698-169">Bunları değiştirmeyi deneyebilir ve oluşturduğunuz ilgi çekici sorguları daha sonra tekrar açıp diğer kaynaklarla kullanmak üzere kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6698-169">You can experiment with modifying these, and save any interesting queries you produce, which you can then re-open and use with other resources.</span></span>

1. <span data-ttu-id="b6698-170">Geri hello günlük analizi çalışma alanı dikey penceresinde, OMS portalı tooopen hello çözümü vardır seçin.</span><span class="sxs-lookup"><span data-stu-id="b6698-170">Back on hello Log Analytics workspace blade, select OMS Portal tooopen hello solution there.</span></span>

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. <span data-ttu-id="b6698-172">Merhaba OMS portalında uyarılar yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6698-172">In hello OMS portal, you can configure alerts.</span></span> <span data-ttu-id="b6698-173">Merhaba uyarı kısmı hello veritabanı DTU görünümünü üzerinde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b6698-173">Click on hello alert portion of hello database DTU view.</span></span>

1. <span data-ttu-id="b6698-174">Merhaba günlük arama görünür görünüm hello ölçümleri temsil ettiği bir çubuk grafik görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b6698-174">In hello Log Search view that appears you will see a bar graph of hello metrics being represented.</span></span>

    ![günlük araması](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. <span data-ttu-id="b6698-176">Merhaba araç çubuğunda uyarıdaki tıklarsanız mümkün toosee hello uyarı yapılandırma olacaktır ve değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6698-176">If you click on Alert in hello toolbar you will be able toosee hello alert configuration and can change it.</span></span>

    ![uyarı kuralı ekle](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

<span data-ttu-id="b6698-178">İzleme ve günlük analizi ve OMS uyarı hello sorgulamaları hello çalışma alanında, kaynak özgü olan her kaynak dikey penceresinde, uyarı hello aksine hello veriler üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="b6698-178">hello monitoring and alerting in Log Analytics and OMS is based on queries over hello data in hello workspace, unlike hello alerting on each resource blade, which is resource-specific.</span></span> <span data-ttu-id="b6698-179">Bu nedenle, veritabanı başına bir uyarı tanımlamak yerine tüm veritabanları için geçerli bir uyarı tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6698-179">Thus, you can define an alert that looks over all databases, say, rather than defining one per database.</span></span> <span data-ttu-id="b6698-180">İsterseniz birden fazla kaynak türü üzerinde birleşik bir sorgu kullanan bir uyarı da yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6698-180">Or write an alert that uses a composite query over multiple resource types.</span></span> <span data-ttu-id="b6698-181">Sorgular yalnızca hello çalışma alanında kullanılabilir hello veri ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b6698-181">Queries are only limited by hello data available in hello workspace.</span></span>

<span data-ttu-id="b6698-182">SQL veritabanı için günlük analizi için hello veri birimi hello çalışma alanında göre ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b6698-182">Log Analytics for SQL Database is charged for based on hello data volume in hello workspace.</span></span> <span data-ttu-id="b6698-183">Bu öğreticide, günde sınırlı too500MB olduğu boş bir çalışma alanı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b6698-183">In this tutorial, you created a Free workspace, which is limited too500MB per day.</span></span> <span data-ttu-id="b6698-184">Bu sınıra ulaşıldığında veri toohello çalışma alanı artık eklenir.</span><span class="sxs-lookup"><span data-stu-id="b6698-184">Once that limit is reached data is no longer added toohello workspace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b6698-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6698-185">Next steps</span></span>

<span data-ttu-id="b6698-186">Bu öğreticide, şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="b6698-186">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b6698-187">Log Analytics’i yükleme ve yapılandırma (OMS)</span><span class="sxs-lookup"><span data-stu-id="b6698-187">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="b6698-188">Günlük analizi toomonitor havuzları ve veritabanları kullanın</span><span class="sxs-lookup"><span data-stu-id="b6698-188">Use Log Analytics toomonitor pools and databases</span></span>

[<span data-ttu-id="b6698-189">Kiracı analizi öğreticisi</span><span class="sxs-lookup"><span data-stu-id="b6698-189">Tenant analytics tutorial</span></span>](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a><span data-ttu-id="b6698-190">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b6698-190">Additional resources</span></span>

* [<span data-ttu-id="b6698-191">Derleme hello ilk Wingtip SaaS uygulama dağıtımı sırasında ek öğreticileri</span><span class="sxs-lookup"><span data-stu-id="b6698-191">Additional tutorials that build upon hello initial Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="b6698-192">Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b6698-192">Azure Log Analytics</span></span>](../log-analytics/log-analytics-azure-sql.md)
* [<span data-ttu-id="b6698-193">OMS</span><span class="sxs-lookup"><span data-stu-id="b6698-193">OMS</span></span>](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
