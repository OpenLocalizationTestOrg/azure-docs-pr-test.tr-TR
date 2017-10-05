---
title: "En son esnek veritabanı istemci kitaplığına yükseltme | Microsoft Docs"
description: "Uygulamalar ve kitaplıkları Nuget kullanarak yükseltme"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: 7e28d128645e856c0efa6e4f78d8f9f36982a76c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-an-app-to-use-the-latest-elastic-database-client-library"></a><span data-ttu-id="00864-103">En son esnek veritabanı istemci kitaplığı kullanmak için bir uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="00864-103">Upgrade an app to use the latest elastic database client library</span></span>
<span data-ttu-id="00864-104">Yeni sürümlerini [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md) NuGetand Visual Studio NuGetPackage Yöneticisi arabiriminde aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="00864-104">New versions of the [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand the NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="00864-105">Yükseltmeler istemci kitaplığı yeni özellikler için destek ve hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="00864-105">Upgrades contain bug fixes and support for new capabilities of the client library.</span></span>

<span data-ttu-id="00864-106">**En son sürümü için:** Git [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="00864-106">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="00864-107">Uygulamanızı yeni kitaplığı ile yeniden gibi yeni özellikleri desteklemek için Azure SQL veritabanlarının depolanan parça eşleme Yöneticisi meta verileriniz varolan değiştirin.</span><span class="sxs-lookup"><span data-stu-id="00864-107">Rebuild your application with the new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases to support new features.</span></span>

<span data-ttu-id="00864-108">Adımları sırayla gerçekleştirilmesi meta veri nesnesi güncelleştirildiğinde, istemci kitaplığının eski sürümleri artık eski sürümü meta veri nesnelerinin yükseltmeden sonra oluşturulmaz anlamına gelir, ortamınızda mevcut olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="00864-108">Performing these steps in order ensures that old versions of the client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="00864-109">Yükseltme adımları</span><span class="sxs-lookup"><span data-stu-id="00864-109">Upgrade steps</span></span>
<span data-ttu-id="00864-110">**1. Uygulamalarınızı yükseltin.**</span><span class="sxs-lookup"><span data-stu-id="00864-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="00864-111">Visual Studio'da karşıdan yükle ve en son istemci kitaplığı sürümü tüm kitaplığı kullanarak geliştirme projelerinizi başvuru; Daha sonra yeniden oluşturun ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="00864-111">In Visual Studio, download and reference the latest client library version into all of your development projects that use the library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="00864-112">Visual Studio çözümünüzde seçin **Araçları** --> **NuGet Paket Yöneticisi** -->  **çözüm için NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="00864-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="00864-113">(Visual Studio 2013) Sol panelinde seçin **güncelleştirmeleri**ve ardından **güncelleştirme** paket düğmesinde **Azure SQL Database esnek ölçek istemci Kitaplığı** penceresinde görünür.</span><span class="sxs-lookup"><span data-stu-id="00864-113">(Visual Studio 2013) In the left panel, select **Updates**, and then select the **Update** button on the package **Azure SQL Database Elastic Scale Client Library** that appears in the window.</span></span>
* <span data-ttu-id="00864-114">(Visual Studio 2015) Filtre kutusuna kümesine **kullanılabilir yükseltme**.</span><span class="sxs-lookup"><span data-stu-id="00864-114">(Visual Studio 2015) Set the Filter box to **Upgrade available**.</span></span> <span data-ttu-id="00864-115">Güncelleştirme ve tıklatın istediğiniz paketi seçin **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="00864-115">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="00864-116">(Visual Studio 2017) İletişim kutusunun üstündeki seçin **güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="00864-116">(Visual Studio 2017) At the top of the dialog, select **Updates**.</span></span> <span data-ttu-id="00864-117">Güncelleştirme ve tıklatın istediğiniz paketi seçin **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="00864-117">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="00864-118">Derleme ve dağıtma.</span><span class="sxs-lookup"><span data-stu-id="00864-118">Build and Deploy.</span></span> 

<span data-ttu-id="00864-119">**2. Komut dosyalarınızı yükseltin.**</span><span class="sxs-lookup"><span data-stu-id="00864-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="00864-120">Kullanıyorsanız **PowerShell** parça, yönetmek için betikler [yeni kitaplık sürümü yüklemek](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) ve kendisinden, yürütme komut dosyaları dizinine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="00864-120">If you are using **PowerShell** scripts to manage shards, [download the new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into the directory from which you execute scripts.</span></span> 

<span data-ttu-id="00864-121">**3. Bölünmüş birleştirme hizmetinizi yükseltin.**</span><span class="sxs-lookup"><span data-stu-id="00864-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="00864-122">Parçalı veriler yeniden düzenlemek için esnek veritabanı bölünmüş birleştirme aracını kullanırsanız [indirin ve aracının en son sürümünü dağıtmak](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span><span class="sxs-lookup"><span data-stu-id="00864-122">If you use the elastic database split-merge tool to reorganize sharded data, [download and deploy the latest version of the tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="00864-123">Hizmet bulunabilir yükseltme adımlarını ayrıntılı [burada](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="00864-123">Detailed upgrade steps for the Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="00864-124">**4. Parça eşleme Yöneticisi veritabanlarınızı yükseltme**.</span><span class="sxs-lookup"><span data-stu-id="00864-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="00864-125">Azure SQL veritabanı'nda, parça eşlemeleri destekleme meta verileri yükseltin.</span><span class="sxs-lookup"><span data-stu-id="00864-125">Upgrade the metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="00864-126">Bu, PowerShell veya C# kullanarak gerçekleştirmenin iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="00864-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="00864-127">Her iki seçenek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="00864-127">Both options are shown below.</span></span>

<span data-ttu-id="00864-128">***Seçenek 1: Meta veri PowerShell kullanarak yükseltme***</span><span class="sxs-lookup"><span data-stu-id="00864-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="00864-129">Son komut satırı yardımcı programı Nuget'ten için karşıdan [burada](http://nuget.org/nuget.exe) ve bir klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="00864-129">Download the latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save to a folder.</span></span> 
2. <span data-ttu-id="00864-130">Bir komut istemi açın, aynı klasöre gidin ve komutu yürütün:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="00864-130">Open a Command Prompt, navigate to the same folder, and issue the command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="00864-131">Yalnızca, örneğin yüklediğiniz yeni istemci DLL sürümü içeren alt klasöre gidin:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="00864-131">Navigate to the subfolder containing the new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="00864-132">Esnek veritabanı istemci yükseltme Resimli'nden indirin [Komut Merkezi](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9)ve dll dosyasını içeren klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="00864-132">Download the elastic database client upgrade scriptlet from the [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into the same folder containing the DLL.</span></span>
5. <span data-ttu-id="00864-133">Bu klasörü "PowerShell.\upgrade.ps1" komut isteminden çalıştırın ve yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="00864-133">From that folder, run “PowerShell .\upgrade.ps1” from the command prompt and follow the prompts.</span></span>

<span data-ttu-id="00864-134">***Seçenek 2: C# kullanarak meta verileri yükseltme***</span><span class="sxs-lookup"><span data-stu-id="00864-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="00864-135">Alternatif olarak, meta veri yükseltme yöntemlerini çağırarak gerçekleştirir, ShardMapManager açar ve tüm parça tekrarlanan bir Visual Studio uygulaması oluşturma [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) ve [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) Bu örnekte olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="00864-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs the metadata upgrade by calling the methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="00864-136">Bu teknikler meta verileri yükseltmeler için birden çok kez zarar uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="00864-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="00864-137">Örneğin, eski bir sürüm zaten güncelleştirdikten sonra yanlışlıkla bir parça oluşturur, yükseltme son meta veri sürümü, altyapınız mevcut olduğundan emin olmak için tüm parça genelinde yeniden komutunu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00864-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards to ensure that the latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="00864-138">**Not:** istemci Kitaplığı'nın yeni sürümleri yayımlanan tarih için Azure SQL DB ve tam tersini parça eşleme Yöneticisi meta verileri önceki sürümleri ile çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="00864-138">**Note:**  New versions of the client library published to-date continue to work with prior versions of the Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="00864-139">Ancak, en son istemcisinde bazı yeni özelliklerden yararlanmak için meta veri yükseltilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="00864-139">However to take advantage of some of the new features in the latest client, metadata needs to be upgraded.</span></span>   <span data-ttu-id="00864-140">Meta veri yükseltme tüm kullanıcı verileri ve uygulamaya özgü verileri, oluşturulan ve parça eşleme Yöneticisi tarafından kullanılan nesneler yalnızca etkilemez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="00864-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by the Shard Map Manager.</span></span>  <span data-ttu-id="00864-141">Ve uygulamaları aracılığıyla yukarıda açıklanan yükseltme sırası çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="00864-141">And applications continue to operate through the upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="00864-142">Esnek veritabanı istemci sürüm geçmişi</span><span class="sxs-lookup"><span data-stu-id="00864-142">Elastic database client version history</span></span>
<span data-ttu-id="00864-143">Sürüm geçmişi için Git [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="00864-143">For version history, go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

