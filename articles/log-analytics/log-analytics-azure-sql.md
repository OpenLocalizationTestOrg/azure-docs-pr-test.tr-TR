---
title: "Günlük analizi SQL analizi çözümde aaaAzure | Microsoft Docs"
description: "Hello Azure SQL analiz çözümü Azure SQL veritabanlarınızın yönetmenize yardımcı olur."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="96ade-103">Azure SQL veritabanı günlük analizi Azure SQL analizi (Önizleme) kullanarak izleme</span><span class="sxs-lookup"><span data-stu-id="96ade-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Azure SQL analizi simgesi](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="96ade-105">Hello Azure günlük analizi Azure SQL analizi çözümde toplar ve önemli SQL Azure performans ölçümleri visualizes.</span><span class="sxs-lookup"><span data-stu-id="96ade-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="96ade-106">Merhaba çözümüyle topladığınız hello ölçümleri kullanarak özel izleme kurallarını ve uyarıları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96ade-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="96ade-107">Azure SQL veritabanı izleyebilirsiniz ve esnek havuz ölçümler arasında birden çok Azure abonelikleri ve esnek havuzları ve bunları görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="96ade-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="96ade-108">Merhaba çözüm Ayrıca, uygulama yığınının her katmanda tooidentify sorunları yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="96ade-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="96ade-109">Kullandığı [Azure tanılama ölçümleri](log-analytics-azure-storage.md) günlük analizi ile birlikte tüm Azure SQL veritabanları ve esnek havuzlar ilgili toopresent verileri tek bir günlük analizi çalışma alanında görüntüler.</span><span class="sxs-lookup"><span data-stu-id="96ade-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="96ade-110">Şu anda too150, 000 Azure SQL veritabanları ve çalışma alanı başına 5.000 SQL esnek havuzlar yukarı Bu önizleme çözümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="96ade-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="96ade-111">Merhaba günlük analizi için bulunan diğerleri gibi Azure SQL analiz çözümü izlemenize ve Azure kaynaklarınızı hello sistem durumu hakkında bildirim almak yardımcı olur; bu durumda, Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="96ade-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="96ade-112">Microsoft Azure SQL veritabanı hello Azure bulut çalıştıran tanıdık SQL Server gibi özellikleri tooapplications sağlayan ölçeklenebilir ilişkisel veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="96ade-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="96ade-113">Günlük analizi toocollect yardımcı olur, bağıntılı ve yapılandırılmış ve yapılandırılmamış verileri görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="96ade-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="96ade-114">Bağlı kaynaklar</span><span class="sxs-lookup"><span data-stu-id="96ade-114">Connected sources</span></span>

<span data-ttu-id="96ade-115">Hello Azure SQL analiz çözümü aracılarını tooconnect toohello günlük analizi hizmeti kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="96ade-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="96ade-116">Aşağıdaki tablonun hello bu çözümü tarafından desteklenen hello bağlı kaynakları açıklar.</span><span class="sxs-lookup"><span data-stu-id="96ade-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="96ade-117">Bağlı Kaynak</span><span class="sxs-lookup"><span data-stu-id="96ade-117">Connected Source</span></span> | <span data-ttu-id="96ade-118">Destek</span><span class="sxs-lookup"><span data-stu-id="96ade-118">Support</span></span> | <span data-ttu-id="96ade-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96ade-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="96ade-120">Windows aracıları</span><span class="sxs-lookup"><span data-stu-id="96ade-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="96ade-121">Hayır</span><span class="sxs-lookup"><span data-stu-id="96ade-121">No</span></span> | <span data-ttu-id="96ade-122">Doğrudan Windows aracıları hello çözümü tarafından kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="96ade-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="96ade-123">Linux aracıları</span><span class="sxs-lookup"><span data-stu-id="96ade-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="96ade-124">Hayır</span><span class="sxs-lookup"><span data-stu-id="96ade-124">No</span></span> | <span data-ttu-id="96ade-125">Doğrudan Linux aracılarını hello çözümü tarafından kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="96ade-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="96ade-126">SCOM yönetim grubu</span><span class="sxs-lookup"><span data-stu-id="96ade-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="96ade-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="96ade-127">No</span></span> | <span data-ttu-id="96ade-128">Merhaba SCOM Aracısı tooLog Analytics arasında doğrudan bağlantı hello çözümü tarafından kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="96ade-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="96ade-129">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="96ade-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="96ade-130">Hayır</span><span class="sxs-lookup"><span data-stu-id="96ade-130">No</span></span> | <span data-ttu-id="96ade-131">Günlük analizi depolama hesabından hello veri okuyamadı.</span><span class="sxs-lookup"><span data-stu-id="96ade-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="96ade-132">Azure tanılama</span><span class="sxs-lookup"><span data-stu-id="96ade-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="96ade-133">Evet</span><span class="sxs-lookup"><span data-stu-id="96ade-133">Yes</span></span> | <span data-ttu-id="96ade-134">Azure ölçüm verileri tooLog Analytics doğrudan Azure tarafından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="96ade-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="96ade-135">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96ade-135">Prerequisites</span></span>

- <span data-ttu-id="96ade-136">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="96ade-136">An Azure Subscription.</span></span> <span data-ttu-id="96ade-137">Yoksa, için bir tane oluşturabilirsiniz [ücretsiz](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="96ade-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="96ade-138">Günlük analizi çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="96ade-138">A Log Analytics workspace.</span></span> <span data-ttu-id="96ade-139">Mevcut bir kullanabilir veya yapabilecekleriniz [yeni bir tane oluşturun](log-analytics-get-started.md) Bu çözüm kullanmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="96ade-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="96ade-140">Azure SQL veritabanları ve esnek havuzlar için Azure Tanılama'yı etkinleştirmek ve [toosend yapılandırmadan kendi veri tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="96ade-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="96ade-141">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="96ade-141">Configuration</span></span>

<span data-ttu-id="96ade-142">Adımları tooadd hello Azure SQL analizi çözüm tooyour çalışma alanı aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="96ade-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="96ade-143">Hello Azure SQL analizi çözüm tooyour çalışma alanından eklemek [Azure Market](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="96ade-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="96ade-144">Hello Azure portal'ı tıklatın **yeni** (Merhaba + simgesi), kaynak hello listesinde seçin **izleme + Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="96ade-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="96ade-145">![İzleme + Yönetim](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="96ade-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="96ade-146">Merhaba, **izleme + Yönetim** listesine **tümünü görmek**.</span><span class="sxs-lookup"><span data-stu-id="96ade-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="96ade-147">Merhaba, **önerilen** tıklatın **daha fazla** , hello yeni listesinde bulun **Azure SQL analizi (Önizleme)** ve seçin.</span><span class="sxs-lookup"><span data-stu-id="96ade-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="96ade-148">![Azure SQL analiz çözümü](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="96ade-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="96ade-149">Merhaba, **Azure SQL analizi (Önizleme)** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="96ade-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="96ade-150">![Oluşturma](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="96ade-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="96ade-151">Merhaba, **yeni çözüm oluşturmak** dikey penceresinde, tooadd hello çözüm tooand istediğiniz ardından tıklatın select hello çalışma **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="96ade-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="96ade-152">![tooworkspace Ekle](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="96ade-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="96ade-153">tooconfigure birden çok Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="96ade-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="96ade-154">toosupport birden çok abonelik kullanmak hello PowerShell komut dosyasından [PowerShell kullanarak etkinleştirmek Azure kaynak ölçümleri günlük](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="96ade-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="96ade-155">Merhaba çalışma kaynak kimliği hello betik toosend tanılama verilerini bir Azure aboneliği tooa çalışma alanında başka bir Azure aboneliğine kaynaklardan yürütülürken bir parametre olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="96ade-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="96ade-156">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="96ade-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="96ade-157">Merhaba çözümünü kullanarak</span><span class="sxs-lookup"><span data-stu-id="96ade-157">Using hello solution</span></span>

<span data-ttu-id="96ade-158">Merhaba çözüm tooyour çalışma eklediğinizde, Azure SQL analizi döşeme hello tooyour çalışma eklenir ve genel bakış bölümünde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="96ade-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="96ade-159">Hello kutucuğu, Azure SQL veritabanı ve hello çözüm bağlandığı Azure SQL esnek havuzlar hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="96ade-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Azure SQL analizi döşeme](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="96ade-161">Azure SQL analizi verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="96ade-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="96ade-162">Tıklatın hello üzerinde **Azure SQL analizi** döşeme tooopen hello Azure SQL analizi Pano.</span><span class="sxs-lookup"><span data-stu-id="96ade-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="96ade-163">Merhaba Pano hello dikey penceresi aşağıda tanımlanan içerir.</span><span class="sxs-lookup"><span data-stu-id="96ade-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="96ade-164">Her dikey too15 kaynakları (abonelik, sunucu, esnek havuz ve veritabanı) listeler.</span><span class="sxs-lookup"><span data-stu-id="96ade-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="96ade-165">Merhaba kaynakları tooopen hello Pano, belirli bir kaynak için birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="96ade-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="96ade-166">Esnek havuz veya veritabanı seçili kaynak ölçümleri hello grafiklerle içerir.</span><span class="sxs-lookup"><span data-stu-id="96ade-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="96ade-167">Bir grafik tooopen hello günlük arama iletişim kutusu'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="96ade-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="96ade-168">Dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="96ade-168">Blade</span></span> | <span data-ttu-id="96ade-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96ade-169">Description</span></span> |
|---|---|
| <span data-ttu-id="96ade-170">Abonelikler</span><span class="sxs-lookup"><span data-stu-id="96ade-170">Subscriptions</span></span> | <span data-ttu-id="96ade-171">Abonelik sayısını bağlı sunucular, havuzları ve veritabanları ile listesi.</span><span class="sxs-lookup"><span data-stu-id="96ade-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="96ade-172">Sunucular</span><span class="sxs-lookup"><span data-stu-id="96ade-172">Servers</span></span> | <span data-ttu-id="96ade-173">Bağlı havuzları ve veritabanları sayısı ile sunucuları listesi.</span><span class="sxs-lookup"><span data-stu-id="96ade-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="96ade-174">Esnek Havuzlar</span><span class="sxs-lookup"><span data-stu-id="96ade-174">Elastic Pools</span></span> | <span data-ttu-id="96ade-175">En fazla GB ve gözlenen hello eDTU bağlı esnek havuzlar listesi süresi.</span><span class="sxs-lookup"><span data-stu-id="96ade-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="96ade-176">Veritabanları</span><span class="sxs-lookup"><span data-stu-id="96ade-176">Databases</span></span> | <span data-ttu-id="96ade-177">Bağlı veritabanlarında gözlenen hello maksimum GB ve DTU listesi süresi.</span><span class="sxs-lookup"><span data-stu-id="96ade-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="96ade-178">Verileri çözümlemek ve uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="96ade-178">Analyze data and create alerts</span></span>

<span data-ttu-id="96ade-179">Uyarılar, Azure SQL veritabanı kaynaklardan gelen hello verilerle kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96ade-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="96ade-180">İşte birkaç faydalı [günlük arama](log-analytics-log-searches.md) uyarmak için kullanabileceğiniz sorgular:</span><span class="sxs-lookup"><span data-stu-id="96ade-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="96ade-181">*Azure SQL veritabanı yüksek DTU*</span><span class="sxs-lookup"><span data-stu-id="96ade-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="96ade-182">*Azure SQL Database esnek havuzunu üzerinde yüksek DTU*</span><span class="sxs-lookup"><span data-stu-id="96ade-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="96ade-183">Bu uyarı tabanlı sorgular tooalert belirli eşiklere Azure SQL veritabanı ve esnek havuzlar için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96ade-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="96ade-184">OMS çalışma alanınız için bir uyarı tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="96ade-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="96ade-185">tooconfigure çalışma alanınız için bir uyarı</span><span class="sxs-lookup"><span data-stu-id="96ade-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="96ade-186">Toohello Git [OMS portalı](http://mms.microsoft.com/) ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="96ade-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="96ade-187">Merhaba çözüm için yapılandırdığınız hello çalışma alanını açın.</span><span class="sxs-lookup"><span data-stu-id="96ade-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="96ade-188">Merhaba Hello genel bakış sayfasında, tıklatın **Azure SQL analizi (Önizleme)** döşeme.</span><span class="sxs-lookup"><span data-stu-id="96ade-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="96ade-189">Merhaba örnek sorguları birini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96ade-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="96ade-190">Günlük aramada tıklatın **uyarı**.</span><span class="sxs-lookup"><span data-stu-id="96ade-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="96ade-191">![Aramada uyarısı oluştur](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="96ade-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="96ade-192">Merhaba üzerinde **uyarı kuralı Ekle** sayfasında hello uygun özelliklerini yapılandırmak ve istediğiniz ve ardından özel eşikler hello **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="96ade-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="96ade-193">![Uyarı kuralı Ekle](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="96ade-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="96ade-194">Azure SQL analizi verilerde işlem yapmak</span><span class="sxs-lookup"><span data-stu-id="96ade-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="96ade-195">Örnek olarak, gerçekleştirebileceğiniz hello en yararlı sorguları toocompare hello DTU kullanımı tüm Azure SQL esnek havuzlar için tüm Azure abonelikleri biridir.</span><span class="sxs-lookup"><span data-stu-id="96ade-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="96ade-196">Veritabanı işleme birimi (DTU) sağlayan bir şekilde toodescribe hello temel, standart ve Premium veritabanlarını ve havuzları performans düzeyinin göreli kapasitesini.</span><span class="sxs-lookup"><span data-stu-id="96ade-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="96ade-197">Dtu'lar CPU karışık bir ölçüyü temel alır, bellek, okur ve yazar.</span><span class="sxs-lookup"><span data-stu-id="96ade-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="96ade-198">Dtu'lar artırdıkça hello güç sunulan hello performans düzeyi artar.</span><span class="sxs-lookup"><span data-stu-id="96ade-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="96ade-199">Örneğin, 1 DTU performans düzeyiyle beş kez daha fazla güç 5 Dtu'ya sahip bir performans düzeyine sahip.</span><span class="sxs-lookup"><span data-stu-id="96ade-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="96ade-200">Maksimum DTU kota tooeach sunucusu ve esnek havuzu geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="96ade-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="96ade-201">Günlük arama sorgusu aşağıdaki hello çalıştırarak, aşırı veya üzerinde SQL Azure esnek havuzları kullanan, kolayca anlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96ade-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="96ade-202">Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorgu yukarıda hello toohello aşağıdaki değişeceğinden sonra.</span><span class="sxs-lookup"><span data-stu-id="96ade-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="96ade-203">Aşağıdaki örneğine hello bir esnek havuz yüksek kullanımı % 100 yakın olduğunu görebilirsiniz başkalarının çok az kullanım varken DTU.</span><span class="sxs-lookup"><span data-stu-id="96ade-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="96ade-204">Azure etkinlik günlükleri kullanarak, ortamınızda başka tootroubleshoot olası en son değişiklikler araştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96ade-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Günlük arama sonuçları - yüksek kullanım](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="96ade-206">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="96ade-206">See also</span></span>

- <span data-ttu-id="96ade-207">Kullanım [günlük aramaları](log-analytics-log-searches.md) günlük analizi tooview ayrıntılı Azure SQL veri.</span><span class="sxs-lookup"><span data-stu-id="96ade-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="96ade-208">[Kendi panolar oluşturun](log-analytics-dashboards.md) Azure SQL verilerini göstererek.</span><span class="sxs-lookup"><span data-stu-id="96ade-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="96ade-209">[Uyarı oluşturma](log-analytics-alerts.md) belirli Azure SQL olayları olduğunda.</span><span class="sxs-lookup"><span data-stu-id="96ade-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
