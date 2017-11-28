---
title: "aaa \"Azure Analysis Services Adventure Works Öğreticisi | Microsoft Docs\""
description: "Azure Analysis Services için Hello Adventure Works Öğreticisi sunar"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="84e88-103">Azure Analysis Services - Adventure Works Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="84e88-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="84e88-104">Bu öğretici hakkında dersleri sağlar toocreate hello 1400 uyumluluk düzeyine sahip tablo modeli kullanarak dağıtabilirsiniz [SQL Server veri Araçları (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span><span class="sxs-lookup"><span data-stu-id="84e88-104">This tutorial provides lessons on how toocreate and deploy a tabular model at hello 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="84e88-105">Yeni tooAnalysis Hizmetleri ve tablo modelleme değilseniz, bu öğreticiyi tamamlamak hello hızlı şekilde toolearn nasıl olduğunu toocreate ve temel tablo modeli dağıtın.</span><span class="sxs-lookup"><span data-stu-id="84e88-105">If you're new tooAnalysis Services and tabular modeling, completing this tutorial is hello quickest way toolearn how toocreate and deploy a basic tabular model.</span></span> <span data-ttu-id="84e88-106">Merhaba Önkoşullar olduktan sonra yerinde, iki toothree saatleri toocomplete arasında olması.</span><span class="sxs-lookup"><span data-stu-id="84e88-106">Once you have hello prerequisites in-place, it should take between two toothree hours toocomplete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="84e88-107">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="84e88-107">What you learn</span></span>   
  
-   <span data-ttu-id="84e88-108">Nasıl yeni bir tablolu model toocreate proje hello **1400 uyumluluk düzeyi** ssdt'de.</span><span class="sxs-lookup"><span data-stu-id="84e88-108">How toocreate a new tabular model project at hello **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="84e88-109">Nasıl bir tablo modeli projesine ilişkisel bir veritabanındaki tooimport veri.</span><span class="sxs-lookup"><span data-stu-id="84e88-109">How tooimport data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="84e88-110">Nasıl toocreate ve hello modelindeki tablolar arasında ilişkiler yönetin.</span><span class="sxs-lookup"><span data-stu-id="84e88-110">How toocreate and manage relationships between tables in hello model.</span></span>  
  
-   <span data-ttu-id="84e88-111">Sütunları, ölçüleri ve ana performans göstergelerini'de, kullanıcılar Yardım kritik iş ölçümleri analiz edin toocreate nasıl hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="84e88-111">How toocreate calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="84e88-112">Nasıl toocreate Perspektifler yönetin ve kullanıcıları daha kolay Yardım hiyerarşileri, iş ve uygulamaya özgü görüşlerini sağlayarak model verileri göz atın.</span><span class="sxs-lookup"><span data-stu-id="84e88-112">How toocreate and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="84e88-113">Nasıl toocreate bölümleri, tablo verileri daha küçük diğer bölümlerdeki bağımsız olarak işlenebilen mantıksal parçalara bölmek.</span><span class="sxs-lookup"><span data-stu-id="84e88-113">How toocreate partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="84e88-114">Nasıl toosecure model nesneleri ve veri kullanıcı üyeleriyle rolleri oluşturarak.</span><span class="sxs-lookup"><span data-stu-id="84e88-114">How toosecure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="84e88-115">Nasıl toodeploy tablolu model tooan **Azure Analysis Services** sunucusu veya bir şirket içi SQL Server 2017 Analysis Services sunucusu.</span><span class="sxs-lookup"><span data-stu-id="84e88-115">How toodeploy a tabular model tooan **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="84e88-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="84e88-116">Prerequisites</span></span>  
<span data-ttu-id="84e88-117">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="84e88-117">toocomplete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="84e88-118">Bir Azure Analysis Services veya SQL Server 2017 Analysis Services modelinize toodeploy örneği.</span><span class="sxs-lookup"><span data-stu-id="84e88-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance toodeploy your model to.</span></span> <span data-ttu-id="84e88-119">Ücretsiz [Azure Analysis Services denemesi](https://azure.microsoft.com/services/analysis-services/) için kaydolun ve [bir sunucu oluşturun](../analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="84e88-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="84e88-120">Veya kaydolun ve [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp)’ı indirin.</span><span class="sxs-lookup"><span data-stu-id="84e88-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="84e88-121">Bir SQL Server veri ambarı veya Azure SQL Data Warehouse hello ile [AdventureWorksDW2014 örnek veritabanı](http://go.microsoft.com/fwlink/?LinkID=335807).</span><span class="sxs-lookup"><span data-stu-id="84e88-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with hello [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="84e88-122">Bu örnek veritabanı hello veri gerekli toocomplete Bu öğretici içerir.</span><span class="sxs-lookup"><span data-stu-id="84e88-122">This sample database includes hello data necessary toocomplete this tutorial.</span></span> <span data-ttu-id="84e88-123">[Ücretsiz SQL Server sürümlerini](https://www.microsoft.com/sql-server/sql-server-downloads) indirin.</span><span class="sxs-lookup"><span data-stu-id="84e88-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="84e88-124">Veya ücretsiz bir [Azure SQL Veritabanı denemesi](https://azure.microsoft.com/services/sql-database/) için kaydolun.</span><span class="sxs-lookup"><span data-stu-id="84e88-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="84e88-125">**Önemli:** bir şirket içi SQL sunucusunda hello örnek veritabanını yüklemek ve model tooan Azure Analysis Services sunucusuna dağıtırsanız bir [şirket içi veri ağ geçidi](../analysis-services-gateway.md) gereklidir.</span><span class="sxs-lookup"><span data-stu-id="84e88-125">**Important:** If you install hello sample database on an on-premises SQL Server, and you deploy your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="84e88-126">Merhaba en son sürümünü [SQL Server veri Araçları (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span><span class="sxs-lookup"><span data-stu-id="84e88-126">hello latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="84e88-127">Merhaba en son sürümünü [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="84e88-127">hello latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="84e88-128">[Power BI Desktop](https://powerbi.microsoft.com/desktop/) veya Excel gibi bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="84e88-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="84e88-129">Senaryo</span><span class="sxs-lookup"><span data-stu-id="84e88-129">Scenario</span></span>  
<span data-ttu-id="84e88-130">Bu öğretici, kurgusal bir şirket olan Adventure Works Cycles’ı temel alır.</span><span class="sxs-lookup"><span data-stu-id="84e88-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="84e88-131">Adventure Works üretir ve bisiklet, bölümleri ve Donatılar toocommercial pazarlarda Kuzey Amerika, Avrupa ve Asya dağıtan bir büyük, çokuluslu üretim şirketidir.</span><span class="sxs-lookup"><span data-stu-id="84e88-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories toocommercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="84e88-132">Merhaba şirket 500 çalışanları kullanır.</span><span class="sxs-lookup"><span data-stu-id="84e88-132">hello company employs 500 workers.</span></span> <span data-ttu-id="84e88-133">Ayrıca, Adventure Works pazar ağının tamamında çeşitli bölgesel satış ekipleri görevlendirir.</span><span class="sxs-lookup"><span data-stu-id="84e88-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="84e88-134">Projenize satış ve pazarlama kullanıcıları tooanalyze Internet satış verileri hello AdventureWorksDW veritabanında için tablo modeli toocreate ' dir.</span><span class="sxs-lookup"><span data-stu-id="84e88-134">Your project is toocreate a tabular model for sales and marketing users tooanalyze Internet sales data in hello AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="84e88-135">toocomplete hello öğretici, çeşitli dersleri tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e88-135">toocomplete hello tutorial, you must complete various lessons.</span></span> <span data-ttu-id="84e88-136">Her derste çeşitli görevler vardır.</span><span class="sxs-lookup"><span data-stu-id="84e88-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="84e88-137">Her görev sırasına Tamamlanıyor hello Ders tamamlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="84e88-137">Completing each task in order is necessary for completing hello lesson.</span></span> <span data-ttu-id="84e88-138">Belirli bir dersteyken benzer bir sonucu elde etmek için farklı görevlerle karşılaşabilirsiniz, ancak her görevi tamamlama biçiminiz biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="84e88-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="84e88-139">Bu var olduğunu genellikle yöntemi gösterir birden fazla yollarından toocomplete bir görev ve toochallenge becerileri kullanarak, önceki dersleri ve görevleri öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="84e88-139">This method shows there is often more than one way toocomplete a task, and toochallenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="84e88-140">Merhaba dersleri Hello amacı hello özelliklerinin çoğunu kullanarak temel tablo modeli yazma size SSDT dahil tooguide budur.</span><span class="sxs-lookup"><span data-stu-id="84e88-140">hello purpose of hello lessons is tooguide you through authoring a basic tabular model by using many of hello features included in SSDT.</span></span> <span data-ttu-id="84e88-141">Her ders hello önceki Ders kurulu olduğundan hello dersleri sırayla tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e88-141">Because each lesson builds upon hello previous lesson, you should complete hello lessons in order.</span></span>
  
<span data-ttu-id="84e88-142">Bu öğretici bir sunucu veya veritabanı yönetme SSMS kullanarak veya bir istemci kullanarak Azure portalında bir sunucu yönetmeyle ilgili dersleri uygulama toobrowse model verileri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="84e88-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application toobrowse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="84e88-143">Dersler</span><span class="sxs-lookup"><span data-stu-id="84e88-143">Lessons</span></span>  
<span data-ttu-id="84e88-144">Bu öğretici dersleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="84e88-144">This tutorial includes hello following lessons:</span></span>  
  
|<span data-ttu-id="84e88-145">Ders</span><span class="sxs-lookup"><span data-stu-id="84e88-145">Lesson</span></span>|<span data-ttu-id="84e88-146">Tahmini süre toocomplete</span><span class="sxs-lookup"><span data-stu-id="84e88-146">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="84e88-147">1 - Yeni tablosal model projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="84e88-148">10 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-148">10 minutes</span></span>|  
|[<span data-ttu-id="84e88-149">2 - Veri alma</span><span class="sxs-lookup"><span data-stu-id="84e88-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="84e88-150">10 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-150">10 minutes</span></span>|  
|[<span data-ttu-id="84e88-151">3 - Tarih Tablosu olarak işaretleme</span><span class="sxs-lookup"><span data-stu-id="84e88-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="84e88-152">3 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-152">3 minutes</span></span>|  
|[<span data-ttu-id="84e88-153">4 - İlişki oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="84e88-154">10 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-154">10 minutes</span></span>|  
|[<span data-ttu-id="84e88-155">5 - Hesaplanan sütunlar oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="84e88-156">15 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-156">15 minutes</span></span>|
|[<span data-ttu-id="84e88-157">6 - Ölçü oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="84e88-158">30 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-158">30 minutes</span></span>|  
|[<span data-ttu-id="84e88-159">7 - Ana Performans Göstergeleri (KPI) oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="84e88-160">15 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-160">15 minutes</span></span>|  
|[<span data-ttu-id="84e88-161">8 - Perspektif oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="84e88-162">5 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-162">5 minutes</span></span>|  
|[<span data-ttu-id="84e88-163">9 - Hiyerarşi oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="84e88-164">20 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-164">20 minutes</span></span>|  
|[<span data-ttu-id="84e88-165">10 - Bölüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="84e88-166">15 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-166">15 minutes</span></span>|  
|[<span data-ttu-id="84e88-167">11 - Rol oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e88-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="84e88-168">15 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-168">15 minutes</span></span>|  
|[<span data-ttu-id="84e88-169">12 - Excel’de çözümleme</span><span class="sxs-lookup"><span data-stu-id="84e88-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="84e88-170">5 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-170">5 minutes</span></span>| 
|[<span data-ttu-id="84e88-171">13 - Dağıtma</span><span class="sxs-lookup"><span data-stu-id="84e88-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="84e88-172">5 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="84e88-173">Ek dersler</span><span class="sxs-lookup"><span data-stu-id="84e88-173">Supplemental lessons</span></span>  
<span data-ttu-id="84e88-174">Bu derslerin gerekli toocomplete hello öğretici değildir, ancak yazma özelliklerini daha iyi anlamak Gelişmiş sekmeli modelde yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="84e88-174">These lessons are not required toocomplete hello tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="84e88-175">Ders</span><span class="sxs-lookup"><span data-stu-id="84e88-175">Lesson</span></span>|<span data-ttu-id="84e88-176">Tahmini süre toocomplete</span><span class="sxs-lookup"><span data-stu-id="84e88-176">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="84e88-177">Ayrıntı Satırları</span><span class="sxs-lookup"><span data-stu-id="84e88-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="84e88-178">10 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-178">10 minutes</span></span>|
|[<span data-ttu-id="84e88-179">Dinamik güvenlik</span><span class="sxs-lookup"><span data-stu-id="84e88-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="84e88-180">30 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-180">30 minutes</span></span>|
|[<span data-ttu-id="84e88-181">Düzensiz hiyerarşiler</span><span class="sxs-lookup"><span data-stu-id="84e88-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="84e88-182">20 dakika</span><span class="sxs-lookup"><span data-stu-id="84e88-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="84e88-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84e88-183">Next steps</span></span>  
<span data-ttu-id="84e88-184">başlatıldı, tooget bkz [Ders 1: yeni bir tablolu modeli projesi oluşturmak](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="84e88-184">tooget started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

