---
title: "İçeri ve dışarı aktarma Azure Redis önbelleği verilerde | Microsoft Docs"
description: "İçeri aktarma ve blob depolama, premium Azure Redis önbelleği örnekleri ile gelen ve giden verileri dışarı aktarma hakkında bilgi edinin"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: 5e6d731f0a1cecc1a191c74a45e37a9b94fd98ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="75dd2-103">İçeri ve dışarı aktarma veri Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="75dd2-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="75dd2-104">İçeri/dışarı aktarma veri Azure Redis önbelleğine alma veya içeri aktarma ve Redis önbelleği veritabanı'nı (RDB) anlık görüntü premium önbellekten bir Azure blob verme Azure Redis Önbelleği'nden veri verme olanak tanıyan bir Azure Redis önbelleği veri yönetimi, bir işlemdir Depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="75dd2-104">Import/Export is an Azure Redis Cache data management operation, which allows you to import data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="75dd2-105">**Dışarı aktarma** -sayfa blobu için Azure Redis önbelleği RDB anlık görüntü dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75dd2-105">**Export** - you can export your Azure Redis Cache RDB snapshots to a Page Blob.</span></span>
- <span data-ttu-id="75dd2-106">**Alma** -sayfa blobu veya bir blok blobu, Redis önbelleği RDB anlık görüntüleri içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75dd2-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="75dd2-107">İçeri/dışarı aktarma, farklı Azure Redis önbelleği örnekleri arasında geçirmek veya önbellek kullanmadan önce verileri ile doldurmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="75dd2-107">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="75dd2-108">Bu makalede, Azure Redis önbelleği ile veri alma ve verme için bir kılavuz sağlar ve sık sorulan soruların yanıtlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="75dd2-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides the answers to commonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75dd2-109">İçeri/dışarı aktarma Önizleme aşamasındadır ve yalnızca için kullanılabilir [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="75dd2-110">İçeri Aktarma</span><span class="sxs-lookup"><span data-stu-id="75dd2-110">Import</span></span>
<span data-ttu-id="75dd2-111">İçeri aktarma, herhangi bir bulut veya ortamını Linux, Windows ya da herhangi bir bulut sağlayıcısına Amazon Web Hizmetleri ve diğerleri gibi çalışan Redis çalıştıran herhangi bir Redis sunucudan Redis uyumlu RDB dosyaları getirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="75dd2-111">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="75dd2-112">Veri alma, önceden doldurulmuş haldedir verilerle önbellek oluşturmak için kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="75dd2-112">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="75dd2-113">İçeri aktarma işlemi sırasında Azure Redis önbelleği RDB dosyaları Azure Storage'dan belleğe yükler ve ardından anahtarları önbelleğe ekler.</span><span class="sxs-lookup"><span data-stu-id="75dd2-113">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory and then inserts the keys into the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="75dd2-114">İçeri aktarma işlemi başlamadan önce Redis veritabanı (RDB) dosya veya dosyalar sayfası veya blok blobları aynı bölgede ve Azure Redis önbelleği örneğinizi olarak abonelik Azure depolama alanında içine karşıya emin olun.</span><span class="sxs-lookup"><span data-stu-id="75dd2-114">Before beginning the import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in the same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="75dd2-115">Daha fazla bilgi için bkz: [Azure Blob storage ile çalışmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="75dd2-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="75dd2-116">RDB dosyasını kullanarak veriliyorsa [Azure Redis önbelleği dışarı aktarma](#export) özelliği RDB dosyanızın bir sayfa blob'u zaten depolanır ve içeri aktarmak için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-116">If you exported your RDB file using the [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="75dd2-117">Bir veya daha fazla dışa aktarılan önbellek BLOB, içeri aktarmak için [Gözat önbelleğiniz için](cache-configure.md#configure-redis-cache-settings) tıklatın ve Azure Portalı'ndaki **veri içeri aktarma** gelen **kaynak menü**.</span><span class="sxs-lookup"><span data-stu-id="75dd2-117">To import one or more exported cache blobs, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Import data** from the **Resource menu**.</span></span>

    ![Veri içeri aktarma][cache-import-data]
2. <span data-ttu-id="75dd2-119">Tıklatın **seçin Blob(s)** ve içeri aktarmak için verileri içeren depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="75dd2-119">Click **Choose Blob(s)** and select the storage account that contains the data to import.</span></span>

    ![Depolama hesabı seçin][cache-import-choose-storage-account]
3. <span data-ttu-id="75dd2-121">Alınacak verileri içeren kapsayıcı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="75dd2-121">Click the container that contains the data to import.</span></span>

    ![Kapsayıcı seçin][cache-import-choose-container]
4. <span data-ttu-id="75dd2-123">Blob adı solundaki alanda tıklayarak içeri aktarmak için bir veya daha fazla BLOB seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="75dd2-123">Select one or more blobs to import by clicking the area to the left of the blob name, and then click **Select**.</span></span>

    ![BLOB'ları seçin][cache-import-choose-blobs]
5. <span data-ttu-id="75dd2-125">Tıklatın **alma** içeri aktarma işlemini başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="75dd2-125">Click **Import** to begin the import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="75dd2-126">Önbelleğe alma işlemi sırasında önbelleği istemcileri tarafından erişilebilir değil ve önbelleğinde mevcut verileri silinir.</span><span class="sxs-lookup"><span data-stu-id="75dd2-126">The cache is not accessible by cache clients during the import process, and any existing data in the cache is deleted.</span></span>
   >
   >

    ![İçeri Aktarma][cache-import-blobs]

    <span data-ttu-id="75dd2-128">Azure portalından bildirimleri izleyerek veya olayları görüntüleyerek ilerleme durumunu alma işlemini izleyebilirsiniz [denetim günlüğü](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="75dd2-128">You can monitor the progress of the import operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![İçeri aktarma ilerlemesi][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="75dd2-130">Dışarı Aktarma</span><span class="sxs-lookup"><span data-stu-id="75dd2-130">Export</span></span>
<span data-ttu-id="75dd2-131">Dışarı aktarma, Azure Redis uyumlu RDB dosyaları Redis için önbellekte depolanan veriler vermenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="75dd2-131">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB file(s).</span></span> <span data-ttu-id="75dd2-132">Verileri bir Azure Redis önbelleği örneğinden diğerine veya başka bir Redis sunucuya taşımak için bu özelliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="75dd2-132">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="75dd2-133">Dışa aktarma işlemi sırasında geçici bir dosya Azure Redis önbelleği sunucu örneğini barındıran VM oluşturulur ve dosya belirtilen depolama hesabına yüklenir.</span><span class="sxs-lookup"><span data-stu-id="75dd2-133">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="75dd2-134">Ya da durumunu başarı veya hata ile dışarı aktarma işlemi tamamlandıktan sonra geçici dosya silindi.</span><span class="sxs-lookup"><span data-stu-id="75dd2-134">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

1. <span data-ttu-id="75dd2-135">Depolama birimine önbelleğinin geçerli içeriğini dışarı aktarmak için [Gözat önbelleğiniz için](cache-configure.md#configure-redis-cache-settings) tıklatın ve Azure Portalı'ndaki **dışarı veri** gelen **kaynak menü**.</span><span class="sxs-lookup"><span data-stu-id="75dd2-135">To export the current contents of the cache to storage, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Export data** from the **Resource menu**.</span></span>

    ![Depolama kapsayıcısı seçin][cache-export-data-choose-storage-container]
2. <span data-ttu-id="75dd2-137">Tıklatın **depolama kapsayıcısı seçin** ve istenen depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="75dd2-137">Click **Choose Storage Container** and select the desired storage account.</span></span> <span data-ttu-id="75dd2-138">Depolama hesabı aynı abonelikte ve bölgede olarak önbelleğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="75dd2-138">The storage account must be in the same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="75dd2-139">Klasik ve Resource Manager depolama hesapları tarafından desteklenir, ancak tarafından desteklenmeyen sayfa bloblarını çalışır verme [Blob storage hesapları](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) şu anda.</span><span class="sxs-lookup"><span data-stu-id="75dd2-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![Depolama hesabı][cache-export-data-choose-account]
3. <span data-ttu-id="75dd2-141">İstenen blob kapsayıcısı seçin ve tıklatın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="75dd2-141">Choose the desired blob container and click **Select**.</span></span> <span data-ttu-id="75dd2-142">Yeni bir kapsayıcı kullanmak için tıklatın **kapsayıcı ekleme** önce ekleyin ve ardından listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="75dd2-142">To use new a container, click **Add Container** to add it first and then select it from the list.</span></span>

    ![Depolama kapsayıcısı seçin][cache-export-data-container]
4. <span data-ttu-id="75dd2-144">Tür a **Blob adı ön ekini** tıklatıp **verme** dışarı aktarma işlemini başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="75dd2-144">Type a **Blob name prefix** and click **Export** to start the export process.</span></span> <span data-ttu-id="75dd2-145">Blob adı ön eki Bu dışarı aktarma işlemi tarafından oluşturulan dosyaların adlarını öneki için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-145">The blob name prefix is used to prefix the names of files generated by this export operation.</span></span>

    ![Dışarı Aktarma][cache-export-data]

    <span data-ttu-id="75dd2-147">Azure portalından bildirimleri izleyerek veya olayları görüntüleyerek verme işleminin ilerleme durumunu izleyebilirsiniz [denetim günlüğü](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="75dd2-147">You can monitor the progress of the export operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Tam Veri dışarı aktarma][cache-export-data-export-complete]

    <span data-ttu-id="75dd2-149">Önbellekleri dışa aktarma işlemi sırasında kullanılabilir kalır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-149">Caches remain available for use during the export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="75dd2-150">İçeri/dışarı aktarma ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="75dd2-150">Import/Export FAQ</span></span>
<span data-ttu-id="75dd2-151">Bu bölüm içeri/dışarı aktarma özelliği hakkında sık sorulan sorular içerir.</span><span class="sxs-lookup"><span data-stu-id="75dd2-151">This section contains frequently asked questions about the Import/Export feature.</span></span>

* [<span data-ttu-id="75dd2-152">Hangi fiyatlandırma katmanlarını içeri/dışarı aktarma kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75dd2-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="75dd2-153">Herhangi bir Redis sunucudan verileri alabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75dd2-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="75dd2-154">Hangi RDB sürümleri alabilirim?</span><span class="sxs-lookup"><span data-stu-id="75dd2-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="75dd2-155">My önbellek içeri/dışarı aktarma işlemi sırasında var mı?</span><span class="sxs-lookup"><span data-stu-id="75dd2-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="75dd2-156">İçeri/dışarı aktarma ile Redis kümesi kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75dd2-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="75dd2-157">İçeri/dışarı aktarma ayarı için özel bir veritabanlarını nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="75dd2-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="75dd2-158">İçeri/dışarı aktarma Redis kalıcılığı farklı mı?</span><span class="sxs-lookup"><span data-stu-id="75dd2-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="75dd2-159">İçeri/dışarı aktarma PowerShell'i, CLI veya diğer yönetim istemcileri kullanarak otomatik hale getirebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="75dd2-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="75dd2-160">My içeri/dışarı aktarma işlemi sırasında zaman aşımı hatası aldım. Ne anlama geliyor?</span><span class="sxs-lookup"><span data-stu-id="75dd2-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="75dd2-161">Verilerimi Azure Blob depolama alanına dışarı aktarılırken bir hata ile aldım. Ne oldu?</span><span class="sxs-lookup"><span data-stu-id="75dd2-161">I got an error when exporting my data to Azure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="75dd2-162">Hangi fiyatlandırma katmanlarını içeri/dışarı aktarma kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75dd2-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="75dd2-163">İçeri/dışarı aktarma premium fiyatlandırma katmanı yalnızca içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="75dd2-163">Import/Export is available only in the premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="75dd2-164">Herhangi bir Redis sunucudan verileri alabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75dd2-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="75dd2-165">Evet, Azure Redis önbelleği örnekleri üzerinden aktarılan verilerin içe aktarılması yanı sıra Windows, herhangi bir bulut ya da Linux gibi ortam çalıştıran herhangi bir Redis sunucusundan RDB dosyalarını içeri aktarmak veya Amazon Web Hizmetleri gibi sağlayıcıları bulut.</span><span class="sxs-lookup"><span data-stu-id="75dd2-165">Yes, in addition to importing data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="75dd2-166">Bunu yapmak için bir Azure depolama hesabındaki sayfa veya blok blob içine istenen Redis sunucusundan RDB dosyayı karşıya yüklemeyi ve premium Azure Redis önbelleği örneğine içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="75dd2-166">To do this, upload the RDB file from the desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="75dd2-167">Örneğin, üretim önbellekten veri verin ve test etme veya geçiş için hazırlama ortamının bir parçası kullanılan bir önbelleğe almak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75dd2-167">For example, you may want to export the data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75dd2-168">Başarıyla bir sayfa blob'u kullanırken, Azure Redis önbelleği dışında Redis sunucularından dışarı veri almak için sayfa blob boyutu 512 baytlık sınırında hizalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-168">To successfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, the page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="75dd2-169">Tüm gerekli bayt doldurma gerçekleştirmek örnek kod için bkz: [örnek sayfa blog yüklemesi](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span><span class="sxs-lookup"><span data-stu-id="75dd2-169">For sample code to perform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="75dd2-170">Hangi RDB sürümleri alabilirim?</span><span class="sxs-lookup"><span data-stu-id="75dd2-170">What RDB versions can I import?</span></span>

<span data-ttu-id="75dd2-171">Azure Redis önbelleği RDB alma sürüm 7 RDB yukarı destekler.</span><span class="sxs-lookup"><span data-stu-id="75dd2-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="75dd2-172">My önbellek içeri/dışarı aktarma işlemi sırasında var mı?</span><span class="sxs-lookup"><span data-stu-id="75dd2-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="75dd2-173">**Dışarı aktarma** - önbellekleri kullanılabilir olmaya devam eder ve bir dışa aktarma işlemi sırasında önbelleğiniz kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75dd2-173">**Export** - Caches remain available and you can continue to use your cache during an export operation.</span></span>
* <span data-ttu-id="75dd2-174">**Alma** - içe aktarma işlemi başladığında, kullanılamaz hale ve içeri aktarma işlemi tamamlandıktan sonra kullanılabilir hale önbellekleri.</span><span class="sxs-lookup"><span data-stu-id="75dd2-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when the import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="75dd2-175">İçeri/dışarı aktarma ile Redis kümesi kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75dd2-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="75dd2-176">Evet, ve, alma/kümelenmemiş bir önbellek ve kümelenmiş bir önbellek arasında verme.</span><span class="sxs-lookup"><span data-stu-id="75dd2-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="75dd2-177">Redis kümesi itibaren [destekler 0 veritabanı yalnızca](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), herhangi bir veri 0 dışında veritabanlarında içe değil.</span><span class="sxs-lookup"><span data-stu-id="75dd2-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="75dd2-178">Kümelenmiş önbellek verilerini içe aktarıldığında, anahtarları küme parça arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-178">When clustered cache data is imported, the keys are redistributed among the shards of the cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="75dd2-179">İçeri/dışarı aktarma ayarı için özel bir veritabanlarını nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="75dd2-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="75dd2-180">Bazı fiyatlandırma katmanları farklı sahip [veritabanları sınırları](cache-configure.md#databases), böylece bazı noktalar için özel bir değer yapılandırdıysanız alırken `databases` önbellek oluşturma sırasında ayarlama.</span><span class="sxs-lookup"><span data-stu-id="75dd2-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="75dd2-181">Bir fiyatlandırma katmanı ile bir alt içeri aktarırken `databases` içinden dışa aktardığınız katmanı sınırından:</span><span class="sxs-lookup"><span data-stu-id="75dd2-181">When importing to a pricing tier with a lower `databases` limit than the tier from which you exported:</span></span>
  * <span data-ttu-id="75dd2-182">Varsayılan sayısını kullanıyorsanız `databases`, tüm fiyatlandırma katmanlarına 16 olduğu, veri kaybı olmamasına.</span><span class="sxs-lookup"><span data-stu-id="75dd2-182">If you are using the default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="75dd2-183">Özel bir dizi kullanıyorsanız `databases` sınırları içinde bu düştüğünde, içeri aktardığınız, katmanı için hiçbir veriler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="75dd2-183">If you are using a custom number of `databases` that falls within the limits for the tier to which you are importing, no data is lost.</span></span>
  * <span data-ttu-id="75dd2-184">Verilen verilerinizi yeni katmanı sınırlarını aşıyor bir veritabanında veri içeriyorsa, bu daha yüksek veritabanlarındaki verileri içe aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="75dd2-184">If your exported data contained data in a database that exceeds the limits of the new tier, the data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="75dd2-185">İçeri/dışarı aktarma Redis kalıcılığı farklı mı?</span><span class="sxs-lookup"><span data-stu-id="75dd2-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="75dd2-186">Azure Redis önbelleği Kalıcılık Azure depolama birimine Redis depolanan verilere kalıcı olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-186">Azure Redis Cache persistence allows you to persist data stored in Redis to Azure Storage.</span></span> <span data-ttu-id="75dd2-187">Kalıcılık yapılandırıldığında, Azure Redis önbelleği Redis önbelleği Redis ikili biçimde yapılandırılabilir bir yedekleme sıklığına bağlı disk için anlık görüntü devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="75dd2-187">When persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span></span> <span data-ttu-id="75dd2-188">Hem birincil hem de çoğaltma önbelleği devre dışı bırakan geri dönülemez bir olay meydana gelirse, önbellek verilerini otomatik olarak en son anlık görüntü kullanılarak geri yüklendi.</span><span class="sxs-lookup"><span data-stu-id="75dd2-188">If a catastrophic event occurs that disables both the primary and replica cache, the cache data is restored automatically using the most recent snapshot.</span></span> <span data-ttu-id="75dd2-189">Daha fazla bilgi için bkz: [Premium Azure Redis önbelleği için veri kalıcılığını yapılandırma](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="75dd2-189">For more information, see [How to configure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="75dd2-190">Alma / verme verisine Getir veya Azure Redis Önbelleği'nden verme olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-190">Import/ Export allows you to bring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="75dd2-191">Yedekleme yapılandırması yok ve Redis kalıcılığı kullanarak geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75dd2-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="75dd2-192">İçeri/dışarı aktarma PowerShell'i, CLI veya diğer yönetim istemcileri kullanarak otomatik hale getirebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="75dd2-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="75dd2-193">Evet, yönergeler için PowerShell bkz [Redis önbelleği almak için](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) ve [Redis önbelleği dışarı aktarmak için](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="75dd2-193">Yes, for PowerShell instructions see [To import a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [To export a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="75dd2-194">My içeri/dışarı aktarma işlemi sırasında zaman aşımı hatası aldım.</span><span class="sxs-lookup"><span data-stu-id="75dd2-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="75dd2-195">Ne anlama geliyor?</span><span class="sxs-lookup"><span data-stu-id="75dd2-195">What does it mean?</span></span>
<span data-ttu-id="75dd2-196">Üzerinde kalırsa **veri içeri aktarma** veya **dışarı veri** dikey 15'ten daha uzun dakika işlem başlatmadan önce aşağıdaki örneğe benzer bir hata iletisi ile bir hata alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="75dd2-196">If you remain on the **Import data** or **Export data** blade for longer than 15 minutes before initiating the operation, you receive an error with an error message similar to the following example:</span></span>

    The request to import data into cache 'contoso55' failed with status 'error' and error 'One of the SAS URIs provided could not be used for the following reason: The SAS token end time (se) must be at least 1 hour from now and the start time (st), if given, must be at least 15 minutes in the past.

<span data-ttu-id="75dd2-197">Bunu çözmek için içe aktarmayı başlatmak veya dışarı aktarma işlemi 15 dakika önce geçti.</span><span class="sxs-lookup"><span data-stu-id="75dd2-197">To resolve this, initiate the import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened"></a><span data-ttu-id="75dd2-198">Verilerimi Azure Blob depolama alanına dışarı aktarılırken bir hata ile aldım.</span><span class="sxs-lookup"><span data-stu-id="75dd2-198">I got an error when exporting my data to Azure Blob Storage.</span></span> <span data-ttu-id="75dd2-199">Ne oldu?</span><span class="sxs-lookup"><span data-stu-id="75dd2-199">What happened?</span></span>
<span data-ttu-id="75dd2-200">Sayfa blobları depolanan dosyalarla yalnızca RDB verme çalışır.</span><span class="sxs-lookup"><span data-stu-id="75dd2-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="75dd2-201">Diğer blob türleri şu anda, blob storage hesapları sık erişimli ve seyrek katmanları dahil olmak üzere desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="75dd2-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="75dd2-202">Daha fazla bilgi için bkz: [Blob storage hesapları](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="75dd2-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75dd2-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75dd2-203">Next steps</span></span>
<span data-ttu-id="75dd2-204">Daha fazla premium önbellek özelliklerinin nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="75dd2-204">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="75dd2-205">Azure Redis önbelleği Premium katmanına giriş</span><span class="sxs-lookup"><span data-stu-id="75dd2-205">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
