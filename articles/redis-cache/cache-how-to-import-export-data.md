---
title: "aaaImport ve Azure Redis önbelleği verileri dışarı aktarma | Microsoft Docs"
description: "Bilgi nasıl tooimport ve dışarı aktarma veri tooand premium Azure Redis önbelleği örnekleri ile blob depolama biriminden"
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
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="f70ca-103">İçeri ve dışarı aktarma veri Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="f70ca-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="f70ca-104">İçeri/dışarı aktarma tooimport veri Azure Redis önbelleği veya Azure Redis önbelleği verme verileri içeri aktarma ve Redis önbelleği veritabanı'nı (RDB) anlık bir Azure premium önbellek tooa blob dışarı aktarma sağlayan bir Azure Redis önbelleği veri yönetimi, bir işlemdir Depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="f70ca-104">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="f70ca-105">**Dışarı aktarma** -Azure Redis önbelleği RDB anlık görüntüleri tooa sayfa blobu dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f70ca-105">**Export** - you can export your Azure Redis Cache RDB snapshots tooa Page Blob.</span></span>
- <span data-ttu-id="f70ca-106">**Alma** -sayfa blobu veya bir blok blobu, Redis önbelleği RDB anlık görüntüleri içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f70ca-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="f70ca-107">İçeri/dışarı aktarma farklı Azure Redis önbelleği örnekleri arasında toomigrate etkinleştirir veya hello önbellek kullanmadan önce verilerle doldurma.</span><span class="sxs-lookup"><span data-stu-id="f70ca-107">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="f70ca-108">Bu makalede, Azure Redis önbelleği ile veri alma ve verme için bir kılavuz sağlar ve hello yanıtlar sağlayan sorular toocommonly.</span><span class="sxs-lookup"><span data-stu-id="f70ca-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides hello answers toocommonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f70ca-109">İçeri/dışarı aktarma Önizleme aşamasındadır ve yalnızca için kullanılabilir [premium katmanı](cache-premium-tier-intro.md) önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="f70ca-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="f70ca-110">İçeri Aktarma</span><span class="sxs-lookup"><span data-stu-id="f70ca-110">Import</span></span>
<span data-ttu-id="f70ca-111">İçeri aktarma kullanılan toobring Redis uyumlu RDB dosyalarından herhangi bir bulut veya ortamını Linux, Windows ya da herhangi bir bulut sağlayıcısına Amazon Web Hizmetleri ve diğerleri gibi çalışan Redis çalıştıran herhangi bir Redis sunucu olabilir.</span><span class="sxs-lookup"><span data-stu-id="f70ca-111">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="f70ca-112">Veri alma kolay bir yolu toocreate önceden doldurulmuş haldedir verilerle bir önbellek olur.</span><span class="sxs-lookup"><span data-stu-id="f70ca-112">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="f70ca-113">Merhaba içeri aktarma işlemi sırasında Azure Redis önbelleği hello RDB dosyaları Azure Storage'dan belleğe yükler ve sonra hello anahtarları hello önbelleğine ekler.</span><span class="sxs-lookup"><span data-stu-id="f70ca-113">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory and then inserts hello keys into hello cache.</span></span>

> [!NOTE]
> <span data-ttu-id="f70ca-114">Merhaba alma işlemi başlamadan önce Redis veritabanı (RDB) dosya veya dosyalar sayfasına yüklenir blok blobları hello de Azure depolama alanında aynı olduğundan emin olun veya bölge ve Azure Redis önbelleği örneğinizi olarak abonelik.</span><span class="sxs-lookup"><span data-stu-id="f70ca-114">Before beginning hello import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in hello same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="f70ca-115">Daha fazla bilgi için bkz: [Azure Blob storage ile çalışmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f70ca-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f70ca-116">RDB dosyanızı hello kullanarak veriliyorsa [Azure Redis önbelleği dışarı aktarma](#export) özelliği RDB dosyanızın bir sayfa blob'u zaten depolanır ve içeri aktarmak için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="f70ca-116">If you exported your RDB file using hello [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="f70ca-117">tooimport bir veya daha fazla önbellek BLOB'ları dışarı [tooyour önbelleği Gözat](cache-configure.md#configure-redis-cache-settings) Azure portal hello ve tıklatın **veri içeri aktarma** hello gelen **kaynak menü**.</span><span class="sxs-lookup"><span data-stu-id="f70ca-117">tooimport one or more exported cache blobs, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Import data** from hello **Resource menu**.</span></span>

    ![Veri içeri aktarma][cache-import-data]
2. <span data-ttu-id="f70ca-119">Tıklatın **seçin Blob(s)** ve hello veri tooimport içeren hello depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="f70ca-119">Click **Choose Blob(s)** and select hello storage account that contains hello data tooimport.</span></span>

    ![Depolama hesabı seçin][cache-import-choose-storage-account]
3. <span data-ttu-id="f70ca-121">Merhaba veri tooimport içeren hello kapsayıcı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f70ca-121">Click hello container that contains hello data tooimport.</span></span>

    ![Kapsayıcı seçin][cache-import-choose-container]
4. <span data-ttu-id="f70ca-123">Bir veya daha fazla BLOB tooimport hello alanı toohello hello blob adı solundaki tıklayarak seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="f70ca-123">Select one or more blobs tooimport by clicking hello area toohello left of hello blob name, and then click **Select**.</span></span>

    ![BLOB'ları seçin][cache-import-choose-blobs]
5. <span data-ttu-id="f70ca-125">Tıklatın **alma** toobegin hello içeri aktarma işlemi.</span><span class="sxs-lookup"><span data-stu-id="f70ca-125">Click **Import** toobegin hello import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f70ca-126">Merhaba önbellek hello içeri aktarma işlemi sırasında önbelleği istemcileri tarafından erişilebilir durumda değil ve hello önbelleğinde mevcut verileri silinir.</span><span class="sxs-lookup"><span data-stu-id="f70ca-126">hello cache is not accessible by cache clients during hello import process, and any existing data in hello cache is deleted.</span></span>
   >
   >

    ![İçeri Aktarma][cache-import-blobs]

    <span data-ttu-id="f70ca-128">Hello Azure portalı aşağıdaki hello bildirimleri tarafından veya hello hello olayları görüntüleyerek hello içeri aktarma işlemi hello ilerlemesini izleyebilirsiniz [denetim günlüğü](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="f70ca-128">You can monitor hello progress of hello import operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![İçeri aktarma ilerlemesi][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="f70ca-130">Dışarı Aktarma</span><span class="sxs-lookup"><span data-stu-id="f70ca-130">Export</span></span>
<span data-ttu-id="f70ca-131">Dışarı aktarma Azure Redis önbelleği tooRedis uyumlu RDB dosyasında depolanan tooexport hello verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f70ca-131">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB file(s).</span></span> <span data-ttu-id="f70ca-132">Bu özellik toomove verilerden bir Azure Redis önbelleği örneği tooanother veya tooanother Redis sunucusu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f70ca-132">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="f70ca-133">Hello dışa aktarma işlemi sırasında Azure Redis önbelleği sunucu örneği konakları hello ve depolama hesabı belirlenmiş karşıya yüklenen toohello hello dosyadır VM hello üzerinde geçici bir dosya oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f70ca-133">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="f70ca-134">Merhaba dışa aktarma işlemi ya da durumunu başarı veya hata ile tamamlandığında hello geçici dosya silindi.</span><span class="sxs-lookup"><span data-stu-id="f70ca-134">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

1. <span data-ttu-id="f70ca-135">tooexport hello geçerli içeriğini hello önbellek toostorage [tooyour önbelleği Gözat](cache-configure.md#configure-redis-cache-settings) Azure portal hello ve tıklatın **dışarı veri** hello gelen **kaynak menü**.</span><span class="sxs-lookup"><span data-stu-id="f70ca-135">tooexport hello current contents of hello cache toostorage, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Export data** from hello **Resource menu**.</span></span>

    ![Depolama kapsayıcısı seçin][cache-export-data-choose-storage-container]
2. <span data-ttu-id="f70ca-137">Tıklatın **depolama kapsayıcısı seçin** ve istenen hello depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="f70ca-137">Click **Choose Storage Container** and select hello desired storage account.</span></span> <span data-ttu-id="f70ca-138">Merhaba depolama hesabı hello olmalıdır aynı abonelikte ve bölgede önbelleğiniz.</span><span class="sxs-lookup"><span data-stu-id="f70ca-138">hello storage account must be in hello same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f70ca-139">Klasik ve Resource Manager depolama hesapları tarafından desteklenir, ancak tarafından desteklenmeyen sayfa bloblarını çalışır verme [Blob storage hesapları](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) şu anda.</span><span class="sxs-lookup"><span data-stu-id="f70ca-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![Depolama hesabı][cache-export-data-choose-account]
3. <span data-ttu-id="f70ca-141">Merhaba istenen blob kapsayıcısı ve tıklatın seçin **seçin**.</span><span class="sxs-lookup"><span data-stu-id="f70ca-141">Choose hello desired blob container and click **Select**.</span></span> <span data-ttu-id="f70ca-142">toouse yeni bir kapsayıcı tıklatın **kapsayıcı ekleme** tooadd ilk ve ardından onu hello listeden.</span><span class="sxs-lookup"><span data-stu-id="f70ca-142">toouse new a container, click **Add Container** tooadd it first and then select it from hello list.</span></span>

    ![Depolama kapsayıcısı seçin][cache-export-data-container]
4. <span data-ttu-id="f70ca-144">Bir **Blob adı ön ekini** tıklatıp **verme** toostart hello dışa aktarma işlemi.</span><span class="sxs-lookup"><span data-stu-id="f70ca-144">Type a **Blob name prefix** and click **Export** toostart hello export process.</span></span> <span data-ttu-id="f70ca-145">Bu dışarı aktarma işlemi tarafından oluşturulan dosyaların kullanılan tooprefix hello adlarını Hello blob adı önekidir.</span><span class="sxs-lookup"><span data-stu-id="f70ca-145">hello blob name prefix is used tooprefix hello names of files generated by this export operation.</span></span>

    ![Dışarı Aktarma][cache-export-data]

    <span data-ttu-id="f70ca-147">Hello Azure portalı aşağıdaki hello bildirimleri tarafından veya hello hello olayları görüntüleyerek hello dışa aktarma işlemi hello ilerlemesini izleyebilirsiniz [denetim günlüğü](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="f70ca-147">You can monitor hello progress of hello export operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Tam Veri dışarı aktarma][cache-export-data-export-complete]

    <span data-ttu-id="f70ca-149">Önbellekleri hello dışa aktarma işlemi sırasında kullanılabilir kalır.</span><span class="sxs-lookup"><span data-stu-id="f70ca-149">Caches remain available for use during hello export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="f70ca-150">İçeri/dışarı aktarma ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="f70ca-150">Import/Export FAQ</span></span>
<span data-ttu-id="f70ca-151">Bu bölümde hello içeri/dışarı aktarma özelliği hakkında sık sorulan sorular bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f70ca-151">This section contains frequently asked questions about hello Import/Export feature.</span></span>

* [<span data-ttu-id="f70ca-152">Hangi fiyatlandırma katmanlarını içeri/dışarı aktarma kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="f70ca-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="f70ca-153">Herhangi bir Redis sunucudan verileri alabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="f70ca-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="f70ca-154">Hangi RDB sürümleri alabilirim?</span><span class="sxs-lookup"><span data-stu-id="f70ca-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="f70ca-155">My önbellek içeri/dışarı aktarma işlemi sırasında var mı?</span><span class="sxs-lookup"><span data-stu-id="f70ca-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="f70ca-156">İçeri/dışarı aktarma ile Redis kümesi kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="f70ca-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="f70ca-157">İçeri/dışarı aktarma ayarı için özel bir veritabanlarını nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="f70ca-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="f70ca-158">İçeri/dışarı aktarma Redis kalıcılığı farklı mı?</span><span class="sxs-lookup"><span data-stu-id="f70ca-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="f70ca-159">İçeri/dışarı aktarma PowerShell'i, CLI veya diğer yönetim istemcileri kullanarak otomatik hale getirebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="f70ca-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="f70ca-160">My içeri/dışarı aktarma işlemi sırasında zaman aşımı hatası aldım. Ne anlama geliyor?</span><span class="sxs-lookup"><span data-stu-id="f70ca-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="f70ca-161">My veri tooAzure Blob Storage dışarı aktarılırken bir hata ile aldım. Ne oldu?</span><span class="sxs-lookup"><span data-stu-id="f70ca-161">I got an error when exporting my data tooAzure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="f70ca-162">Hangi fiyatlandırma katmanlarını içeri/dışarı aktarma kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="f70ca-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="f70ca-163">İçeri/dışarı aktarma premium fiyatlandırma katmanına yalnızca hello içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f70ca-163">Import/Export is available only in hello premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="f70ca-164">Herhangi bir Redis sunucudan verileri alabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="f70ca-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="f70ca-165">Evet, ayrıca Azure Redis önbelleği örneklerden verilen tooimporting verileri RDB dosyaları herhangi bir bulut veya Linux, Windows veya Amazon Web Hizmetleri gibi bulut sağlayıcıları gibi ortam çalıştıran herhangi bir Redis sunucudan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f70ca-165">Yes, in addition tooimporting data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="f70ca-166">toodo bu karşıya yükleme hello RDB dosyanızı istenen hello Redis sunucusundan bir sayfa veya blok blobu bir Azure depolama hesabı ve ardından içeri aktarma, premium Azure Redis önbelleği örneğine.</span><span class="sxs-lookup"><span data-stu-id="f70ca-166">toodo this, upload hello RDB file from hello desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="f70ca-167">Örneğin, üretim önbellekten tooexport hello veri istediğiniz ve test veya geçiş için hazırlama ortamının bir parçası kullanılan bir önbellek içe.</span><span class="sxs-lookup"><span data-stu-id="f70ca-167">For example, you may want tooexport hello data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f70ca-168">toosuccessfully verileri kullanarak bir sayfa blobu, hello sayfa blob boyutu 512 baytlık sınırında hizalanmalıdır aktardığınızda Azure Redis önbelleği dışında Redis sunucularından dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="f70ca-168">toosuccessfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, hello page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="f70ca-169">Bayt doldurma gerekli örnek kodu tooperform için bkz: [örnek sayfa blog yüklemesi](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span><span class="sxs-lookup"><span data-stu-id="f70ca-169">For sample code tooperform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="f70ca-170">Hangi RDB sürümleri alabilirim?</span><span class="sxs-lookup"><span data-stu-id="f70ca-170">What RDB versions can I import?</span></span>

<span data-ttu-id="f70ca-171">Azure Redis önbelleği RDB alma sürüm 7 RDB yukarı destekler.</span><span class="sxs-lookup"><span data-stu-id="f70ca-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="f70ca-172">My önbellek içeri/dışarı aktarma işlemi sırasında var mı?</span><span class="sxs-lookup"><span data-stu-id="f70ca-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="f70ca-173">**Dışarı aktarma** - önbellekleri kullanılabilir olmaya devam eder ve önbelleğiniz toouse dışa aktarma işlemi sırasında devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f70ca-173">**Export** - Caches remain available and you can continue toouse your cache during an export operation.</span></span>
* <span data-ttu-id="f70ca-174">**Alma** - içe aktarma işlemi başladığında, kullanılamaz hale ve hello içeri aktarma işlemi tamamlandıktan sonra kullanılabilir hale önbellekleri.</span><span class="sxs-lookup"><span data-stu-id="f70ca-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when hello import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="f70ca-175">İçeri/dışarı aktarma ile Redis kümesi kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="f70ca-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="f70ca-176">Evet, ve, alma/kümelenmemiş bir önbellek ve kümelenmiş bir önbellek arasında verme.</span><span class="sxs-lookup"><span data-stu-id="f70ca-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="f70ca-177">Redis kümesi itibaren [destekler 0 veritabanı yalnızca](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), herhangi bir veri 0 dışında veritabanlarında içe değil.</span><span class="sxs-lookup"><span data-stu-id="f70ca-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="f70ca-178">Verileri kümelenmiş önbelleğe alındığı sırada hello anahtarları hello küme hello parça arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="f70ca-178">When clustered cache data is imported, hello keys are redistributed among hello shards of hello cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="f70ca-179">İçeri/dışarı aktarma ayarı için özel bir veritabanlarını nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="f70ca-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="f70ca-180">Bazı fiyatlandırma katmanları farklı sahip [veritabanları sınırları](cache-configure.md#databases), böylece bazı noktalar hello için özel bir değer yapılandırdıysanız alırken `databases` önbellek oluşturma sırasında ayarlama.</span><span class="sxs-lookup"><span data-stu-id="f70ca-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="f70ca-181">Fiyatlandırma katmanı ile bir alt tooa alırken `databases` içinden dışa aktardığınız hello katmanı sınırından:</span><span class="sxs-lookup"><span data-stu-id="f70ca-181">When importing tooa pricing tier with a lower `databases` limit than hello tier from which you exported:</span></span>
  * <span data-ttu-id="f70ca-182">Merhaba varsayılan sayısı kullanıyorsanız `databases`, tüm fiyatlandırma katmanlarına 16 olduğu, veri kaybı olmamasına.</span><span class="sxs-lookup"><span data-stu-id="f70ca-182">If you are using hello default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="f70ca-183">Özel bir dizi kullanıyorsanız `databases` hello sınırları içinde düştüğünde hello için içeri aktardığınız toowhich katmanının, veri kaybı olmamasına.</span><span class="sxs-lookup"><span data-stu-id="f70ca-183">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are importing, no data is lost.</span></span>
  * <span data-ttu-id="f70ca-184">Verilen verilerinizi hello yeni katmanının hello sınırlarını aşıyor bir veritabanında veri içeriyorsa, bu daha yüksek veritabanlarındaki hello veriler içe aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="f70ca-184">If your exported data contained data in a database that exceeds hello limits of hello new tier, hello data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="f70ca-185">İçeri/dışarı aktarma Redis kalıcılığı farklı mı?</span><span class="sxs-lookup"><span data-stu-id="f70ca-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="f70ca-186">Azure Redis önbelleği kalıcılığı Redis tooAzure depolama depolanan toopersist verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f70ca-186">Azure Redis Cache persistence allows you toopersist data stored in Redis tooAzure Storage.</span></span> <span data-ttu-id="f70ca-187">Azure Redis önbelleği Kalıcılık yapılandırıldığında, bir anlık görüntüsünü hello Redis Önbelleği'nde yapılandırılabilir bir yedekleme sıklığına bağlı bir Redis ikili biçimi toodisk devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="f70ca-187">When persistence is configured, Azure Redis Cache persists a snapshot of hello Redis cache in a Redis binary format toodisk based on a configurable backup frequency.</span></span> <span data-ttu-id="f70ca-188">Merhaba birincil ve çoğaltma önbelleği devre dışı bırakan geri dönülemez bir olay meydana gelirse, hello önbellek verilerini hello en son anlık görüntü kullanılarak otomatik olarak geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f70ca-188">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache data is restored automatically using hello most recent snapshot.</span></span> <span data-ttu-id="f70ca-189">Daha fazla bilgi için bkz: [nasıl Premium Azure Redis önbelleği için tooconfigure veri kalıcılığını](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="f70ca-189">For more information, see [How tooconfigure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="f70ca-190">Alma / verme verir toobring verisine veya Azure Redis Önbelleği'den dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="f70ca-190">Import/ Export allows you toobring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="f70ca-191">Yedekleme yapılandırması yok ve Redis kalıcılığı kullanarak geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f70ca-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="f70ca-192">İçeri/dışarı aktarma PowerShell'i, CLI veya diğer yönetim istemcileri kullanarak otomatik hale getirebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="f70ca-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="f70ca-193">Evet, yönergeler için PowerShell bkz [tooimport Redis önbelleği](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) ve [tooexport Redis önbelleği](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="f70ca-193">Yes, for PowerShell instructions see [tooimport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [tooexport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="f70ca-194">My içeri/dışarı aktarma işlemi sırasında zaman aşımı hatası aldım.</span><span class="sxs-lookup"><span data-stu-id="f70ca-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="f70ca-195">Ne anlama geliyor?</span><span class="sxs-lookup"><span data-stu-id="f70ca-195">What does it mean?</span></span>
<span data-ttu-id="f70ca-196">Merhaba üzerinde kalırsa **veri içeri aktarma** veya **dışarı veri** aşağıdaki örneğine bir hata iletisi benzer toohello ile bir hata alıyorsunuz dikey penceresinde hello işlemini başlatmadan önce 15 dakikadan daha uzun süre:</span><span class="sxs-lookup"><span data-stu-id="f70ca-196">If you remain on hello **Import data** or **Export data** blade for longer than 15 minutes before initiating hello operation, you receive an error with an error message similar toohello following example:</span></span>

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

<span data-ttu-id="f70ca-197">tooresolve bunu başlatmak hello içeri aktarma veya dışarı aktarma işlemi 15 dakika geçtikten önce.</span><span class="sxs-lookup"><span data-stu-id="f70ca-197">tooresolve this, initiate hello import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a><span data-ttu-id="f70ca-198">My veri tooAzure Blob Storage dışarı aktarılırken bir hata ile aldım.</span><span class="sxs-lookup"><span data-stu-id="f70ca-198">I got an error when exporting my data tooAzure Blob Storage.</span></span> <span data-ttu-id="f70ca-199">Ne oldu?</span><span class="sxs-lookup"><span data-stu-id="f70ca-199">What happened?</span></span>
<span data-ttu-id="f70ca-200">Sayfa blobları depolanan dosyalarla yalnızca RDB verme çalışır.</span><span class="sxs-lookup"><span data-stu-id="f70ca-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="f70ca-201">Diğer blob türleri şu anda, blob storage hesapları sık erişimli ve seyrek katmanları dahil olmak üzere desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f70ca-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="f70ca-202">Daha fazla bilgi için bkz: [Blob storage hesapları](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="f70ca-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f70ca-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f70ca-203">Next steps</span></span>
<span data-ttu-id="f70ca-204">Toouse daha premium özellikleri nasıl önbelleğe alma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="f70ca-204">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="f70ca-205">Giriş toohello Azure Redis önbelleği Premium katmanına</span><span class="sxs-lookup"><span data-stu-id="f70ca-205">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

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
