---
title: "aaaUpgrade toohello son esnek veritabanı istemci kitaplığı | Microsoft Docs"
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
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a><span data-ttu-id="189ad-103">Bir uygulama toouse hello son esnek veritabanı istemci kitaplığı yükseltme</span><span class="sxs-lookup"><span data-stu-id="189ad-103">Upgrade an app toouse hello latest elastic database client library</span></span>
<span data-ttu-id="189ad-104">Merhaba yeni sürümlerini [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md) NuGetand hello NuGetPackage Yöneticisi arabiriminde, Visual Studio aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="189ad-104">New versions of hello [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand hello NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="189ad-105">Yükseltmeler hello istemci kitaplığı yeni özellikler için destek ve hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="189ad-105">Upgrades contain bug fixes and support for new capabilities of hello client library.</span></span>

<span data-ttu-id="189ad-106">**Merhaba en son sürümü için:** çok Git[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="189ad-106">**For hello latest version:** Go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="189ad-107">Uygulamanızı hello yeni kitaplığı ile yeniden gibi Azure SQL veritabanlarını toosupport yeni özellikler depolanan parça eşleme Yöneticisi meta verileriniz varolan değiştirin.</span><span class="sxs-lookup"><span data-stu-id="189ad-107">Rebuild your application with hello new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases toosupport new features.</span></span>

<span data-ttu-id="189ad-108">Adımları sırayla gerçekleştirilmesi meta veri nesnesi güncelleştirildiğinde, hello istemci kitaplığı eski sürümleri artık eski sürümü meta veri nesnelerinin yükseltmeden sonra oluşturulmaz anlamına gelir, ortamınızda mevcut olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="189ad-108">Performing these steps in order ensures that old versions of hello client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="189ad-109">Yükseltme adımları</span><span class="sxs-lookup"><span data-stu-id="189ad-109">Upgrade steps</span></span>
<span data-ttu-id="189ad-110">**1. Uygulamalarınızı yükseltin.**</span><span class="sxs-lookup"><span data-stu-id="189ad-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="189ad-111">Visual Studio, indirme ve başvuru hello son istemci kitaplığı sürümü tüm geliştirme projelerinizi hello kitaplığını kullanın; Daha sonra yeniden oluşturun ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="189ad-111">In Visual Studio, download and reference hello latest client library version into all of your development projects that use hello library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="189ad-112">Visual Studio çözümünüzde seçin **Araçları** --> **NuGet Paket Yöneticisi** -->  **çözüm için NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="189ad-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="189ad-113">(Visual Studio 2013) Merhaba sol panelinde seçin **güncelleştirmeleri**seçip hello **güncelleştirme** hello paket düğmesinde **Azure SQL Database esnek ölçek istemci Kitaplığı** hello görüntülenir penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="189ad-113">(Visual Studio 2013) In hello left panel, select **Updates**, and then select hello **Update** button on hello package **Azure SQL Database Elastic Scale Client Library** that appears in hello window.</span></span>
* <span data-ttu-id="189ad-114">(Visual Studio 2015) Merhaba filtre kutusuna çok ayarlamak**kullanılabilir yükseltme**.</span><span class="sxs-lookup"><span data-stu-id="189ad-114">(Visual Studio 2015) Set hello Filter box too**Upgrade available**.</span></span> <span data-ttu-id="189ad-115">Merhaba paket tooupdate seçin ve hello tıklayın **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="189ad-115">Select hello package tooupdate, and click hello **Update** button.</span></span>
* <span data-ttu-id="189ad-116">(Visual Studio 2017) Merhaba iletişim Hello üstünde seçin **güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="189ad-116">(Visual Studio 2017) At hello top of hello dialog, select **Updates**.</span></span> <span data-ttu-id="189ad-117">Merhaba paket tooupdate seçin ve hello tıklayın **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="189ad-117">Select hello package tooupdate, and click hello **Update** button.</span></span>
* <span data-ttu-id="189ad-118">Derleme ve dağıtma.</span><span class="sxs-lookup"><span data-stu-id="189ad-118">Build and Deploy.</span></span> 

<span data-ttu-id="189ad-119">**2. Komut dosyalarınızı yükseltin.**</span><span class="sxs-lookup"><span data-stu-id="189ad-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="189ad-120">Kullanıyorsanız **PowerShell** toomanage parça komutlar [hello yeni kitaplık sürümü yüklemek](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) ve kendisinden, yürütme komut dosyaları hello dizinine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="189ad-120">If you are using **PowerShell** scripts toomanage shards, [download hello new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into hello directory from which you execute scripts.</span></span> 

<span data-ttu-id="189ad-121">**3. Bölünmüş birleştirme hizmetinizi yükseltin.**</span><span class="sxs-lookup"><span data-stu-id="189ad-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="189ad-122">Merhaba esnek veritabanı bölünmüş Birleştirme aracı tooreorganize parçalı veriler, kullanırsanız [karşıdan yükleyip hello hello aracının en son sürümünü dağıtmak](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span><span class="sxs-lookup"><span data-stu-id="189ad-122">If you use hello elastic database split-merge tool tooreorganize sharded data, [download and deploy hello latest version of hello tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="189ad-123">Ayrıntılı hizmet bulunabilir hello için yükseltme adımları [burada](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="189ad-123">Detailed upgrade steps for hello Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="189ad-124">**4. Parça eşleme Yöneticisi veritabanlarınızı yükseltme**.</span><span class="sxs-lookup"><span data-stu-id="189ad-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="189ad-125">Azure SQL veritabanı'nda, parça eşlemeleri destekleme hello meta verileri yükseltin.</span><span class="sxs-lookup"><span data-stu-id="189ad-125">Upgrade hello metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="189ad-126">Bu, PowerShell veya C# kullanarak gerçekleştirmenin iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="189ad-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="189ad-127">Her iki seçenek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="189ad-127">Both options are shown below.</span></span>

<span data-ttu-id="189ad-128">***Seçenek 1: Meta veri PowerShell kullanarak yükseltme***</span><span class="sxs-lookup"><span data-stu-id="189ad-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="189ad-129">Merhaba son komut satırı yardımcı programı Nuget'ten için karşıdan [burada](http://nuget.org/nuget.exe) ve tooa klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="189ad-129">Download hello latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save tooa folder.</span></span> 
2. <span data-ttu-id="189ad-130">Bir komut istemi açın, toohello gidin aynı klasöre ve sorunu hello komutu:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="189ad-130">Open a Command Prompt, navigate toohello same folder, and issue hello command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="189ad-131">Yalnızca, örneğin yüklediğiniz hello yeni istemci DLL sürümü içeren toohello alt klasöre gidin:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="189ad-131">Navigate toohello subfolder containing hello new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="189ad-132">Hello Hello esnek veritabanı istemci yükseltme Resimli karşıdan [Komut Merkezi](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), ve hello içine Kaydet aynı içeren klasör hello DLL.</span><span class="sxs-lookup"><span data-stu-id="189ad-132">Download hello elastic database client upgrade scriptlet from hello [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into hello same folder containing hello DLL.</span></span>
5. <span data-ttu-id="189ad-133">Bu klasördeki "PowerShell.\upgrade.ps1" Merhaba komut isteminden çalıştırın ve hello istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="189ad-133">From that folder, run “PowerShell .\upgrade.ps1” from hello command prompt and follow hello prompts.</span></span>

<span data-ttu-id="189ad-134">***Seçenek 2: C# kullanarak meta verileri yükseltme***</span><span class="sxs-lookup"><span data-stu-id="189ad-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="189ad-135">Alternatif olarak, hello meta veri yükseltmesi hello yöntemlerini çağırarak gerçekleştirir, ShardMapManager açar ve tüm parça tekrarlanan bir Visual Studio uygulaması oluşturma [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) ve [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) Bu örnekte olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="189ad-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs hello metadata upgrade by calling hello methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="189ad-136">Bu teknikler meta verileri yükseltmeler için birden çok kez zarar uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="189ad-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="189ad-137">Eski bir sürüm zaten güncelleştirdikten sonra yanlışlıkla bir parça oluşturur, örneğin, yükseltme yeniden tüm parça tooensure bu hello çalıştırabilirsiniz, altyapınız son meta veri sürümü varsa.</span><span class="sxs-lookup"><span data-stu-id="189ad-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards tooensure that hello latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="189ad-138">**Not:** hello istemci Kitaplığı'nın yeni sürümleri yayımlanan tarih için Azure SQL DB ve tam tersini hello parça eşleme Yöneticisi meta verilerini önceki sürümleriyle toowork devam edin.</span><span class="sxs-lookup"><span data-stu-id="189ad-138">**Note:**  New versions of hello client library published to-date continue toowork with prior versions of hello Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="189ad-139">Ancak hello son istemcisinde, meta veri hello yeni özelliklerden bazıları tootake avantajlarından toobe yükseltilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="189ad-139">However tootake advantage of some of hello new features in hello latest client, metadata needs toobe upgraded.</span></span>   <span data-ttu-id="189ad-140">Meta veri yükseltme tüm kullanıcı verileri ve uygulamaya özgü verileri, oluşturulan ve hello parça eşleme Yöneticisi tarafından kullanılan nesneler yalnızca etkilemez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="189ad-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by hello Shard Map Manager.</span></span>  <span data-ttu-id="189ad-141">Ve uygulamalar toooperate yukarıda açıklanan hello yükseltme sırası üzerinden devam eder.</span><span class="sxs-lookup"><span data-stu-id="189ad-141">And applications continue toooperate through hello upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="189ad-142">Esnek veritabanı istemci sürüm geçmişi</span><span class="sxs-lookup"><span data-stu-id="189ad-142">Elastic database client version history</span></span>
<span data-ttu-id="189ad-143">Sürüm geçmişi için çok Git[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="189ad-143">For version history, go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

